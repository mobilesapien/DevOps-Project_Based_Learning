## WEB STACK IMPLEMENTATION (LEMP STACK)

### STEP ! - INSTALLING THE NGINX WEB SERVER

#### Steps

* Start by updating the server package followed by Installing the Nginx.

```
    sudo apt update
    sudo apt install
```

* Next confirm Nginx is properly configured by running.

```
sudo systemctl status nginx
```

* The Green indicator shows that the server was successfully installed and is running.
![Nginx Status](./images/1%20-%20Nginx%20Status.png "Nginx installed Correctly")

* Next we can test connection to our servers in two ways; either locally or through the browser.

```
curl http://localhost:80
or
curl http://127.0.0.1:80
```

![Status check via browser](./images/2-%20Nginx_Status_check.png "Nginx is online")


### STEP 2 - INSTALLING MYSQL

#### Steps

* Use the following command to install MYSQL:
```
sudo apt install mysql-server
``` 
* If prompted, type Y and hit the enter key to continue installation.

* Next, log into MySQL using:
``` 
sudo mysql
```
![MySQL](./images/3%20-%20Connecting_to_Mysql.png "MySQL Console")

* It’s recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Before running the script you will set a password for the root user, using mysql_native_password as default authentication method. We’re defining this user’s password as PassWord.1.
![Security Script](./images/4%20-%20Security_Script.png "Securing the sql database")
* Exit SQL interactive shell by typing ```quit```.
* Start interactive scripting to configure the validate password pluggin. Run: sudo mysql_secure_installation and answer Y to all the prompts. At the point you can change the password of your root user and also decide the level of password validation.
![My SQL Console](./images/5%20-%20MySQL_Console.png "mysql console")
* When done, test to know if login to the console is possible. type: ```sudo mysql -p```
* This would prompt you to enter root user password. Enter the choosen password
* Type exit to exit MySQL console.

### STEP 3 - INSTALLING PHP
#### Steps


