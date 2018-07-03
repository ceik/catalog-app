# FSND Project 3 - Catalog

Catalog App that implements a category tree, Google OAuth, and user permissions

## Python Dependencies

The project is built with Python2 and uses:
- flask
- sqlalchemy
- requests
- oauth2client
- httplib2

## To Run
- Set up an Apache Webserver with mod_wsgi
- Install dependencies
- Configure the google app and download the google_client_secret.json. The path to this file is currently hardcoded to /var/www/catalog/google_client_secret.json. Change this in all occurences in catalog.py if necessary.
- Create a catalog.wsgi in /var/www/catalog with the content below.
- Change the Apache config located at `/etc/apache2/sites-enabled/000-default.conf` to the content below. Make sure to replace the `xxx` with the proper values and edit the other values if necessary.
- Restart the Apache server with `sudo apache2ctl restart`


## catalog.wsgi
```
import sys
sys.path.append('/var/www/catalog/catalog-app/catalog')

from catalog import app as application
```

## Apache Config
```
<VirtualHost *>
    ServerName xxx

    WSGIDaemonProcess catalog user=xxx group=xxx threads=5
    WSGIScriptAlias / /var/www/catalog/catalog.wsgi

    <Directory /var/www/catalog>
        WSGIProcessGroup catalog
        WSGIApplicationGroup %{GLOBAL}
        Order deny,allow
        Allow from all
    </Directory>
</VirtualHost>
```