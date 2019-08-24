# This is a project for Udacity FSWD nanodegree.


the project is about deploying a previously submitted Flask web app which you can find [here](https://github.com/Elshafeay/catalog-project-for-udacity) on [Amazon lightsail](https://lightsail.aws.amazon.com).
The linux server runs **ubuntu** and has **512 MB RAM**, **1 vCPU**, **20 GB SSD**


## These are the most important configurations I had to do after cloning the application from git:

### **first::**
#### *Configure and Enable a New Virtual Host*

**1- Create FlaskApp.conf to edit**: ```sudo nano /etc/apache2/sites-available/FlaskApp.conf```

**2- Add the following lines of code to the file to configure the virtual host.**

    <VirtualHost *:80>
    	ServerName http://3.123.76.202/
    	ServerAdmin grader
    	WSGIScriptAlias / /var/www/FlaskApp/flaskapp.wsgi
    	<Directory /var/www/FlaskApp/FlaskApp/>
    		Order allow,deny
    		Allow from all
    	</Directory>
    	Alias /static /var/www/FlaskApp/FlaskApp/static
    	<Directory /var/www/FlaskApp/FlaskApp/static/>
    		Order allow,deny
    		Allow from all
    	</Directory>
    	ErrorLog ${APACHE_LOG_DIR}/error.log
    	LogLevel warn
    	CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>

**3- Enable the virtual host with the following command:** ```sudo a2ensite FlaskApp```

----------------

### **second::**

#### *Create the .wsgi File*

**1- Create the .wsgi File under /var/www/FlaskApp:**

```cd /var/www/FlaskApp```

```sudo nano flaskapp.wsgi```


**2-Add the following lines of code to the flaskapp.wsgi file:**

    #!/usr/bin/python
    import sys
    import logging
    logging.basicConfig(stream=sys.stderr)
    sys.path.insert(0,"/var/www/FlaskApp/")

    from FlaskApp import app as application
    application.secret_key = 'Add your secret key'

----------------

### to connect to the web server via ssh all you have to do is to run this command in your shell:

```ssh grader@3.123.76.202 -p 2200 -i <private key directory>```


### for the normal user you can access the website [here](http://3.123.76.202).

### I wanna also add this [repo](https://github.com/jungleBadger/-nanodegree-linux-server) as a resource as it helped me alot during the process.