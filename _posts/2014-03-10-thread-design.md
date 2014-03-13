---
layout: post
title: "c++中一个简单易用的线程类设计"
description: "c++中一个简单易用的线程类设计,编程语言,工作项目总结"
category: "programming"
tags: [c++,多线程]
---
{% include JB/setup %}

1. 前言
---
现在大家在编写程序时，很少使用单线程的方式，往往会创建多线程。今天我们就针对创建线程来进行讨论。

在java、c#中有Thread类可以调用，提供了丰富的操作线程的接口，可以直接调用，所以这不是我们今天所讲的重点。

今天我们主要讲一讲在c++中如何创建线程(调用系统的接口也可以说是c语言，但是c语言不支持面向对象，所以这里不是重点)。

其实系统都提供了创建线程的接口。Windows中通过**CreateThread**和**\_beginthreadex**，linux中可以调用 **pthread** 接口（支持POSIX标准）来实现线程的创建。但是无论是**\_beginthreadex** 还是 **pthread** 建立线程都不是那么直观，也不像java中的线程那么易于操作。对于深受面向对象思想影响的我们来说，很想将线程操作封装成类，用操作对象的方式来操作线程。

这时你会说开源库**boost**不是已经提供了跨平台的**thread**类了么，为什么还要自己写一个？的确，boost已经提供了我们能想象到的对于线程的操作，为什么我们还要自己重复造轮子呢？

* 由于boost库很大，很多项目无法直接使用boost库，况且单独裁剪boost中thread部分也不是很简单。
* 通过编写一个thread类，可以加强我们面向对象设计能力。

下文中的线程设计仅在Windows下通过了验证，所以并未实现跨平台（虽然原本的初衷是跨平台，但是未在linux/unix下做过尝试）。


2. 需求
---
设计原则：

* 功能简单易用，提供基本的接口，包括如下接口：
    - 开始
    - 停止
    - 获取线程状态
    - 获取线程号
* 满足面向对象程序设计：
	- 可以继承，子类自动获得父类线程类的功能。
	- 允许子类**override**线程处理函数，实现其功能。 

3. 设计与实现
---
如下给出的都是在Windows平台下的实现，对于若要移植到 linux 平台，需要做一些修改。

### 前置定义

为了定义线程状态，我们定义一个枚举来表示，如下：

{% highlight c++ linenos %}
	enum ThreadStatus{T_STOPPED=0,T_STARTING,T_RUNNING,T_STOPPING};
{% endhighlight %}

如上四个值对应的线程状态说明如下：

* **T_STOPPED** ：缺省状态：停止。
* **T_STARTING** :正在开始的状态，表示线程**开始**的接口正在执行，未返回。
* **T_RUNNING** :运行的状态，线程运行中处于这种状态。
* **T_STOPPING** :正在停止的状态，表示线程**停止**的接口正在执行，未返回。




### 数据成员
类需要定义如下成员变量：

* **handle_** : 句柄 / 或线程描述符
* **status_** : 线程状态
* **tid_** : 线程号
* **name_** : 线程名。非必选项。

代码如下：

{% highlight c++ linenos %}
		//预编译宏
	#ifdef _WIN32
		//thread handle
		HANDLE _handle;
	#else
		unsigned int _handle;
	#endif // _WIN32

		//tid
		unsigned int _tid;
		
		//tname
		string _name;

		//Thread status
		ThreadStatus _status;
{% endhighlight %}

### 接口定义
* 公有方法：

{% highlight c++ linenos %}
	//构造函数		
	explicit BaseThread(string tname);

	//析构函数
	virtual ~BaseThread();

	//线程开始，需要返回线程句柄或线程描述符。
	unsigned int Start();
	
	//线程结束，有可能会被阻塞。
	void Stop();
	
	//线程中循环执行的函数，可以被override
	virtual void Run(){};
	
	//获取线程状态
	inline ThreadStatus GetState()	const{	return this->_status;}
	
	//获取线程号
	inline unsigned int GetTid() const {return _tid;}
{% endhighlight %}

* 私有方法：

{% highlight c++ linenos %}
	//拷贝构造函数，设为私有，使该类的对象不可被拷贝 
	BaseThread(const BaseThread&);
	
	//赋值操作符，设为私有，使该类的对象不可被拷贝
	BaseThread& operator=(const BaseThread&);

	//线程函数的入口地址，参数为当前线程类的 this 指针		
	static unsigned __stdcall StartAddress(void* para);
{% endhighlight %}

### 实现
* **构造函数**。在初始化列表中初始化成员变量，不需要做任何操作。

{% highlight c++ linenos %}
	//构造函数
	BaseThread::BaseThread(string tname):
	_name(tname),_tid(0),_handle(0),_status(T_STOPPED)
	{
	}
{% endhighlight %}

* **Start()** 。使用 **\_beginthreadex** 函数建立线程，并执行，获取**线程号**，设置线程状态，返回线程句柄并保存。如果调用该接口时，线程已经启动，则直接返回线程句柄。
	
{% highlight c++ linenos %}
	//线程开始
	unsigned BaseThread::Start()
	{
		if(0 != _handle)
			return (unsigned)_handle;

		_status = T_STARTING;
		printf("Before begin thread tid=%d State is %d\n",_tid,_status);
		_handle = reinterpret_cast<HANDLE>(_beginthreadex(NULL,0,StartAddress,this,0,&_tid));
		if(0 != _handle)
		{
			printf("Thread %s create succeed. thread tid=%d\n",this->_name.c_str(),this->_tid);
		}
		else
		{
			_status = T_STOPPED;
			printf("Thread create failure.errno=%d\n",errno);
		}
	
		return (unsigned)_handle;
	}
{% endhighlight %}

* **Stop()** 。先将线程状态设置为 **正在停止状态** ，使用 **WaitForSingleObject** 等待线程结束，等待条件为句柄 **\_handle** 无效，线程结束后，将其状态设为 **已经停止状态**。

{% highlight c++ linenos %}
	//线程停止
	void BaseThread::Stop()
	{		
		if(0 != _handle)
		{
			this->_status = T_STOPPING;
			print("Waiting For the thread stopping... tid=%d\n",_tid);
			WaitForSingleObject(_handle,INFINITE);
			CloseHandle(_handle);
			_handle = 0;
		}
		this->_status = T_STOPPED;
	}
{% endhighlight %}

* **StartAddress()**。

{% highlight c++ linenos %}
	//线程入口函数
	unsigned int __stdcall BaseThread::StartAddress(void* para)
	{	
		Sleep(10);
		if(NULL == para)
		{
			printf("Thread \'StartAddress\'  Param is NULL \n");
			return 0;
		}
		BaseThread* pthread = static_cast<BaseThread*>(para);		
		//atomic operation
	#if defined(_MSC_VER) && _MSC_VER>1200
		//vc10
		InterlockedCompareExchange((long*)&pthread->_status,(long)T_RUNNING,(long)T_STARTING);
	#else
		//vc6
		InterlockedCompareExchange((void**)&pthread->_status,(void*)T_RUNNING,(void*)T_STARTING);
	#endif //VC6 == 1200
		while(pthread->_status == T_RUNNING)
		{
			pthread->Run();
		}
		
		return 0;
	}
{% endhighlight %}

注:`InterlockedCompareExchange((long*)&pthread->_status,(long)T_RUNNING,(long)T_STARTING);`，当`pthread->_status` 等于 `T_STARTING`时，其值才被改为`T_RUNNING`；否则其值不变。该操作整体为一个原子操作。

使用`InterlockedCompareExchange`可以解决在连续调用**Start** 和 **Stop** 时对 `pthread->_status` 值的竞争。如果不是原子操作，有一种可能，在判断完`pthread->_status` 等于 `T_STARTING` 与将其改为`T_RUNNING`的间隔，调用 **Stop** 有可能其值会被改为 `T_STOPPING`，随后再被改为`T_RUNNING`，接着线程正常执行循环，但是此时上层用户已经调用过`Stop()`了，所以产生了不一致的矛盾。


* **析构函数** 。调用`Stop()`接口即可，有可能会被阻塞。

{% highlight c++ linenos %}
	//析构函数
	BaseThread::~BaseThread()
	{
		//may block
		this->Stop();
	}
{% endhighlight %} 

4. 使用方法
---
* 继承 `BaseThread`
* override `Run();` 实现自己的功能。

5. TODO
---
此线程类仅实现了最基本的功能。

目前的设计线程自身无法停止自身。可以采用这样的解决方法：添加具有 **“信号”** 含义的数据成员，使`Run()`函数在执行的时候根据条件设置信号的值，从而在线程内部自己停止自己。但是这样会破坏了线程的封装。所以一直没有找到好的解决方法（由于Windows并不支持abort这样的信号来停止一个线程），希望能得到大家多多的指点！

期待和大家的交流！

---
庄永耀 
2014-03-10
