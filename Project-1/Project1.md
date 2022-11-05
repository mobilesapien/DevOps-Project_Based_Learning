***STEP 1 — INSTALLING APACHE AND UPDATING THE FIREWALL***

---

The first thing we want to do is to update the list of packages present in Package Manager.

```
#update current packages in package manager
$ sudo apt update
```

Then we proceed to Install Apache2

```
#run apache2 package installation
$ sudo apt install apache2
```

Next is to verify that Apache is installed and running by using the command below:

`$ sudo systemctl status apache2`

We should get the following as output:

![Apache Installed](./images/Apache%20Installed%20and%20running.png)

Since our Ubuntu server is an EC2 instance, we need to open TCP port 80 in the EC2 Instance.

We can confirm by running the below in our ubuntu shell:

`$ curl http://localhost:80`

or

`$ curl http://127.0.0.1:80`

Also by typing the public IP address of the EC2 instance on any browser of our choice, we confirm once the default Apache page loads as seen in the output below:

![Can Access Webserver](./images/Web%20Server.png)

---

***STEP 2 — INSTALLING MYSQL***

---

The  First thing to do is Installing the mysql-server using the code below:

`$ sudo apt install mysql-server`

Once installation is complete, log in to the MySQL console by typing:

`$ sudo mysql`

![mysql login](./images/mysql%20login.png)

It’s recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Before running the script you will set a password for the root user, using mysql_native_password as default authentication method. We’re defining this user’s password as PassWord.1.

`mysql > ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

output:
![rootuser](./images/root%20user%20password.png)

Exit MYSQL Shell with:

`mysql > exit`

Start the interactive script by running:

`sudo mysql_secure_installation`

---

***STEP 3 — INSTALLING PHP***

---

First we will proceed to installing php. libapache2-mod-php and php-mysql

`$ sudo apt install php libapache2-mod-php php-mysql`

Once this is complete, confirm PHP version using:

`$ php -v`

Output should be similar to this:

![PHP Version](./images/PHP%20Version.png)

With these steps, we now have a fully functional LAMP stack.

---

***STEP 4 — CREATING A VIRTUAL HOST FOR WEBSITE USING APACHE***

---

First we need to create directory for domain "projectlamp"using **mkdir** command as follows:

`$ sudo mkdir /var/www/projectlamp`

Then I assigned ownership of the directory with my current system user:

`$ sudo chown -R $USER:$USER /var/www/projectlamp`

Next, i created and opened a new configuration file in APache's sites-available directory using **VI** command line editor.

`$ sudo vi /etc/apache2/sites-available/projectlamp.conf`

I pasted the following configuration into the empty file created:

```
<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

I enabled the new virtual hoste using:

`$ sudo a2ensite projectlamp`

Then proceed to run the below to disable the default website that comes with Apache:

`$ sudo a2dissite 000-default`

And confirmed that the coniguration file does not contain sysntax errors, using:

`$ sudo apache2ctl configtest`

Output:

![Syntax Ok](./images/Syntax%20Ok.png)

Finally, Apache2 was reloaded for the changes to take effect:

`$ sudo systemctl reload apache2`

Since the web root /var/www/projectlamp is still empty, I created an index.html file in that location so that we can test that the virtual host works as expected:

```
sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html
```

Confirm this by checking with curl or browser:

`$ sudo curl http://<Public-IP-Address>:80`


---

***STEP 5 — ENABLE PHP ON THE WEBSITE***

---

First we need to update the directory index, to ensure that index.php takes precedence over index.html:

`$ sudo vim /etc/apache2/mods-enabled/dir.conf`

```
<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```

Then restart Apache for changes to take effect:

`$ sudo systemctl reload apache2`

Next is to create a script to test that php is working successfully:

`$ sudo vim /var/www/projectlamp/index.php`

Enter the following:

```
<?php
phpinfo();
```

Reload your browser to confirm.

Once completed, deleted tthe files created, because it contains sensitive info about php configuration and also ubuntu server.

