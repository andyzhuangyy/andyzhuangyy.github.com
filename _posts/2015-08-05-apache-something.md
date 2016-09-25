---
layout: post
title: "apache"
description: ""
category: "notes"
tags: [apache]
---
{% include JB/setup %}

# osx
directory: /private/etc/apache2
default settings in /etc/apache2/httpd.conf

     DocumentsRoot /Library/WebServer/Documents/
     

    $ sudo apachectl start 
    $ sudo apachectl restart



# virtual host

httpd.conf

    Include /private/etc/apache2/extra/httpd-vhosts.conf

extra/httpd-vhosts.conf

    <VirtualHost *:80>
        DocumentRoot "/Library/WebServer/Documents"
        ServerName localhost
        ErrorLog "/private/var/log/apache2/localhost-error_log"
        CustomLog "/private/var/log/apache2/localhost-access_log" common
    </VirtualHost>


# User home directories

    Include /private/etc/apache2/extra/httpd-userdir.conf

extra/httpd-userdir.conf

    UserDir Sites
    Include /private/etc/apache2/users/*.conf
    <IfModule bonjour_module>
           RegisterUserSite customized-users
    </IfModule>

http://127.0.0.1/~$usrname


