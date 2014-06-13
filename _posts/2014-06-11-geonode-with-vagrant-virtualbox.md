---
layout: post
title: "GeoNode Quickstart for Devs with Vagrant"
description: "Walks through the steps to setup Geonode for development in a Vagrant environment"
category: articles
tags: [geonode, boundless, vagrant, virtualbox, postgis, geoserver, pycsw]
comments: false
share: true
---

GeoNode is a sweet little packaging of some heavy-hitting open source software including Geoserver, PyCSW, PostGIS, and OpenLayers all bundled together using some Django middleware apps.  I've been watching the project for a couple of years and I'm a big fan of the building block approach.  I think it's really starting to come together as a spatial CMS-like alternative to the OpenGeo Suite.

Recently I wrote about [a GeoNode project](/articles/collaboration-eastern-caribbean/) that I'm getting started with in the Eastern Caribbean.  So last week I spun up a development environment to try out some of the latest features, particularly Remote Services.  I found the dev install documentation on the Geonode website to be very thorough but unfortunately a bit scattered and hard to follow, even for someone pretty seasoned with all of the Geonode components.  I went ahead and commited some small doc improvements but there's some additional overhaul needed.  So I pieced together an improved workflow here as a first step, and sprinkled in some tips and tricks for good measure.

Enjoy.

#Initialize Your VM With Vagrant

First, install both Virtualbox and Vagrant on your system.  I installed on OSX Mavericks.

{% highlight bash %}
cd ~/src
mkdir geonode
cd geonode
vagrant box add ubuntu/trusty https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box
vagrant init ubuntu/trusty
{% endhighlight %}

This establishes a Ubuntu Trusty 14.04 LTS virtual machine that will be provisioned when you start it up.

Edit the new Vagrantfile file that’s created.  Add 3 new port forward lines below it, 8000 for the django dev server, 8001 for apache, and 8080 for Geoserver

{% highlight bash %}
config.vm.network "forwarded_port", guest: 80, host: 8001   
config.vm.network "forwarded_port", guest: 8000, host: 8000
config.vm.network "forwarded_port", guest: 8080, host: 8080
{% endhighlight %}

Now fire up the VM and log in via SSH

{% highlight bash %} 
vagrant up
vagrant ssh
{% endhighlight %}

# Install Base Libraries

[http://geonode.readthedocs.org/en/latest/tutorials/devel/install_devmode/index.html#install-devmode]()

{% highlight bash %}
sudo add-apt-repository -y ppa:chris-lea/node.js
sudo apt-get update
sudo apt-get install -y build-essential libxml2-dev libxslt1-dev libjpeg-dev gettext git python-dev python-pip python-pillow python-lxml python-psycopg2 python-django python-bs4 python-multipartposthandler transifex-client python-paver python-nose python-django-nose python-gdal python-django-pagination python-django-jsonfield python-django-extensions python-django-taggit python-httplib2 nodejs apache2 gcc gdal-bin libapache2-mod-wsgi libgeos-dev libpng-dev libpq-dev libproj-dev patch postgresql-9.3 postgresql-9.3-postgis-2.1 python-imaging python-pastescript python-support python-urlgrabber python-virtualenv tomcat7 unzip zip
sudo apt-get install -y --force-yes openjdk-6-jdk ant maven2 --no-install-recommends
sudo npm install -y -g bower grunt-cli
{% endhighlight %}

I skipped the virtualenv steps at this point in the docs since I'm working on a single-purpose VM

# Install Server Apps

[http://geonode.readthedocs.org/en/latest/tutorials/admin/install/custom_install.html#custom-install]()

# Clone and Setup GeoNode

I cloned  the master branch of the GeoNode Github repository and put it in the shared workspace that Vagrant has created at _/vagrant_.  Anything you put in this directory is visible from your host machine in the folder that you did a _vagrant up_ and vice versa.  This allows you to write code from your host operating system with your favorite text editor.

{% highlight bash %}
git clone https://github.com/GeoNode/geonode.git
sudo pip install -e geonode
cd geonode
sudo paver setup
{% endhighlight %}

# Setup PostGIS

The next step was to get Geonode working with PostGIS and install Geoserver to run under the Tomcat web server and startup automatically with the VM.

I also went ahead and setup hosting of the GeoNode Django app using Apache.  I don't use this for active development but its great for making sure that it works well before pushing to staging or production.

{% highlight bash %}
sudo su postgres
createuser -P geonode
{% endhighlight %} 

* Use password geonode also, set as superuser.  Use different password if a public server!

* I was getting a utf8 encoding error when loading the initial data fixture so amended the createdb as follows

{% highlight bash %}
createdb -E 'utf-8' -l en_US.utf8 -O geonode -T template0 geonode
createdb -E 'utf-8' -l en_US.utf8 -O geonode -T template0 geonode-imports
psql -f /usr/share/postgresql/9.3/contrib/postgis-2.1/postgis.sql geonode-imports
psql -f /usr/share/postgresql/9.3/contrib/postgis-2.1/spatial_ref_sys.sql geonode-imports
psql -d geonode-imports -c 'GRANT ALL ON geometry_columns TO PUBLIC;'
psql -d geonode-imports -c 'GRANT ALL ON spatial_ref_sys TO PUBLIC;'
exit
sudo nano /etc/postgresql/9.3/main/pg_hba.conf
# Change the ‘local all all’ from ‘peer’ to ‘trust’
# Save and exit nano
sudo service postgresql restart
cd /vagrant/geonode/geonode/
cp local_settings.py.sample local_settings.py
{% endhighlight %}

Now I opened local_settings.py in my text editor on my host system in the shared folder and did the following:

 * Uncomment line 10
 * Comment out line 11
 * Change line 12 to 'NAME': 'geonode-imports',
 * Add to the bottom of the file for development purposes ALLOWED_HOST = ['*']
 * Comment out the MAP_LAYERS line

Back in the guest VM I then finished up the Django app setup:

{% highlight bash %}
cd /vagrant/geonode
python manage.py syncdb
python manage.py collectstatic
mkdir -p /vagrant/geonode/geonode/uploaded
sudo chown www-data -R /vagrant/geonode/geonode/uploaded
{% endhighlight %}

{% highlight bash %}
cd /vagrant/geonode
paver start_django -b 0.0.0.0:8000
{% endhighlight %}

Browse to [http://localhost:8000]().  You should get the Geonode home page, with no data layers loaded yet.  Let's load up some data layers that come with Geonode using the _setup_data_ command.

{% highlight bash %}
paver setup_data
{% endhighlight %}

For a full list of useful Paver commands for GeoNode, check out [http://geonode.readthedocs.org/en/latest/tutorials/devel/envsetup/paver.html]().  Refresh your GeoNode page to see the new data layers.  You’ll know if the linkage to Geoserver is working properly if you can see the thumbnail images for each layer.

Now we're ready to hack some GeoNode code.  One important note, the _start_django_ paver command by default runs the dev server as a _background process_, sending debug output to the terminal while still allowing you to continue to run commands.  However, if you want to do debugging with Python’s PDB, you will need to run the dev server in the foreground so that it can capture debug commands from you.  To do this you can skip the paver command and just use the Django runserver command directly:

{% highlight bash %}
paver stop_django
python manage.py runserver 0.0.0.0:8000
{% endhighlight %}

GeoNode should work just fine now.  Press Ctrl-C to quit the dev server when you're done.  If you need another terminal to do other things on the server, just open another terminal and vagrant ssh in

# Setup Tomcat

{% highlight bash %}
sudo service tomcat7 stop
sudo cp /vagrant/geonode/downloaded/geoserver.war /var/lib/tomcat7/webapps/
sudo /etc/init.d/tomcat7 start
{% endhighlight %}

## Setup Apache

{% highlight bash %}
sudo a2enmod proxy_http
sudo nano /etc/apache2/sites-available/geonode
{% endhighlight %}

Now let's setup a standard Apache virtual host to serve our Django app using WSGI on Port 80.  We'll also proxy Geoserver through this port as well, a typical configuration for production use.  Note the Pythonpath at the top includes the path to GeoNode and the path to dist-packages where all of the third-party Python modules are.  If you are using a virtual environment, a different version of Python etc. then these paths may be different.

{% highlight apache %}
WSGIDaemonProcess geonode python-path=/vagrant/geonode:/usr/local/lib/python2.7/dist-packages
 user=www-data threads=15 processes=2

<VirtualHost *:80>
    ServerName http://localhost
    ServerAdmin webmaster@localhost
    DocumentRoot /vagrant/geonode/geonode

    ErrorLog /var/log/apache2/error.log
    LogLevel warn
    CustomLog /var/log/apache2/access.log combined

    WSGIProcessGroup geonode
    WSGIPassAuthorization On
    WSGIScriptAlias / /vagrant/geonode/geonode/wsgi.py

    <Directory "/vagrant/geonode/geonode/">
    Order allow,deny
        Options Indexes FollowSymLinks
        Allow from all
        IndexOptions FancyIndexing
    </Directory>

    Alias /static/ /vagrant/geonode/geonode/static_root/
    Alias /uploaded/ /vagrant/geonode/geonode/uploaded/

    <Proxy *>
        Order allow,deny
        Allow from all
    </Proxy>

    ProxyPreserveHost On
    ProxyPass /geoserver http://localhost:8080/geoserver
    ProxyPassReverse /geoserver http://localhost:8080/geoserver
</VirtualHost>
{% endhighlight %}

Next up is enabling the new virtualhost and setting all the proper directory permissions so that the Apache user _www-data_ can read and write files on behalf of our application.

{% highlight bash %}
sudo a2ensite geonode
sudo service apache2 reload
{% endhighlight %}

Now if go to http://localhost:8001/admin on the host machine (8001 is the port on the host that we forwarded port 80 to), the Django admin should load.

{% highlight bash %}
sudo chown www-data:www-data /vagrant/geonode/geonode/static/
sudo chown www-data:www-data /vagrant/geonode/geonode/uploaded/
sudo chown www-data:www-data /vagrant/geonode/geonode/static_root/
{% endhighlight %}

# Final Geoserver test

We setup Geoserver with Tomcat and proxied it through Apache remember?  You should be able to browse to both of these forwarded ports and get the Geoserver home page.

{% highlight html %}
http://localhost:8080/geoserver
http://localhost:8001/geoserver
{% endhighlight %}
