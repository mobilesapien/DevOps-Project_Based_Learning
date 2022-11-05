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
**STEP 2 — INSTALLING MYSQL**

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

**STEP 3 — INSTALLING PHP**

---

First we will proceed to installing php. libapache2-mod-php and php-mysql

`$ sudo apt install php libapache2-mod-php php-mysql`

Once this is complete, confirm PHP version using:

`$ php -v`

Output should be similar to this:

![PHP Version](./images/PHP%20Version.png)

With these steps, we now have a fully functional LAMP stack.