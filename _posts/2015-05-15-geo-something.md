---
layout: post
title: "geo"
description: ""
category: "notes"
tags: [geo]
---
{% include JB/setup %}

# geo
Measuring Distance

Geopy can calculate geodesic distance between two points using the Vincenty distance or great-circle distance formulas, with a default of Vincenty available as the class geopy.distance.distance, and the computed distance available as attributes (e.g., miles, meters, etc.).

:
# geopy
Geocoding

To geolocate a query to an address and coordinates:

>>> from geopy.geocoders import Nominatim
>>> geolocator = Nominatim()
>>> location = geolocator.geocode("175 5th Avenue NYC")
>>> print(location.address)
Flatiron Building, 175, 5th Avenue, Flatiron, New York, NYC, New York, ...
>>> print((location.latitude, location.longitude))
(40.7410861, -73.9896297241625)
>>> print(location.raw)
{'place_id': '9167009604', 'type': 'attraction', ...}
To find the address corresponding to a set of coordinates:

>>> from geopy.geocoders import Nominatim
>>> geolocator = Nominatim()
>>> location = geolocator.reverse("52.509669, 13.376294")
>>> print(location.address)
Potsdamer Platz, Mitte, Berlin, 10117, Deutschland, European Union
>>> print((location.latitude, location.longitude))
(52.5094982, 13.3765983)
>>> print(location.raw)
{'place_id': '654513', 'osm_type': 'node', ...}
Measuring Distance

Geopy can calculate geodesic distance between two points using the Vincenty distance or great-circle distance formulas, with a default of Vincenty available as the class geopy.distance.distance, and the computed distance available as attributes (e.g., miles, meters, etc.).

Here's an example usage of Vincenty distance:

>>> from geopy.distance import vincenty
>>> newport_ri = (41.49008, -71.312796)
>>> cleveland_oh = (41.499498, -81.695391)
>>> print(vincenty(newport_ri, cleveland_oh).miles)
538.3904451566326
Using great-circle distance:

>>> from geopy.distance import great_circle
>>> newport_ri = (41.49008, -71.312796)
>>> cleveland_oh = (41.499498, -81.695391)
>>> print(great_circle(newport_ri, cleveland_oh).miles)
537.1485284062816
