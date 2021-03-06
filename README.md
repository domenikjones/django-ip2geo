django-ip2geo
=============

  * [Description](#description)
  * [Configuration](#configuration)


Description
=============

Simple Django pluggable that uses MaxMind (http://www.maxmind.com/) to get country/region/city from the IP address

Configuration
=============

  * settings.py

```
# path to dat file
# Download this file in http://www.maxmind.com/app/geolitecity
GEOIP_DATA = '/path/to/GeoLiteCity.dat'
    
# You can choose the following fields that will be stored in the session: 
GEOIP_SESSION_FIELDS = ['country_name', 'country_code', 'country_code3', 'region_name', 'city', 'latitude', 'longitude', 'postal_code']
    
# You do not have to select all of them, for example:
GEOIP_SESSION_FIELDS = ['country_name', 'region_name', 'city',]
    
# PS1: The data is responsability of MaxMind database.
# PS2: The documentation of each field you can find in MaxMind reference.
# PS3: The field 'geoip' is set to True in session to identify that the data was loaded
  
# Need SessionMiddleware. If you do not want to use session you will have to edit the plugin.
MIDDLEWARE_CLASSES = (
    ...
    'django.contrib.sessions.middleware.SessionMiddleware',
    'ip2geo.middleware.CityMiddleware',
    ...
)

# If you want to use session variable in templates
TEMPLATE_CONTEXT_PROCESSORS = (
  ...
    'ip2geo.context_processors.add_session',
    ...
)

# Need SessionMiddleware. If you do not want to use session you will have to edit the plugin.
INSTALLED_APPS = (
	...
    'django.contrib.sessions',
    'ip2geo',
    ...
)
```
  

  * views.py (just for example of usage)

```
print(request.session['country_name'])
print(request.session['country_code'])
print(request.session['country_code3'])
print(request.session['region_name'])
print(request.session['city'])
print(request.session['latitude'])
print(request.session['longitude'])
print(request.session['postal_code'])
```

  * Templates

If you are using 'ip2geo.context_processors.add_session', you can do:

```
{{ session.city }}
{{ session.country_name }}
...
```

and all variables that you set in GEOIP_SESSION_FIELDS

    
MaxMind
==========

More information about Python and MaxMind

  * http://code.google.com/p/pygeoip/
  * http://www.maxmind.com/app/geolitecity
  * http://www.maxmind.com/app/python
  * http://www.maxmind.com/app/api
  * http://www.maxmind.com/app/installation?city=1

  