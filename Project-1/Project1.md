**STEP 1 — INSTALLING APACHE AND UPDATING THE FIREWALL**

---

The first thing we want to do is to update the list of packages present in Package Manager.

```
#update current packages in package manager
sudo apt update

#run apache2 package installation
sudo apt install apache2
```

Next is to verify that Apache is installed and running by using the command below:

`sudo systemctl status apache2`

We should get the following as output:

![Apache Installed](./images/Apache%20Installed%20and%20running.png)

Since our Ubuntu server is an EC2 instance, we need to open TCP port 80 in the EC2 Instance.

We can confirm by running the below in our ubuntu shell:

`curl http://localhost:80`

or

`curl http://127.0.0.1:80`

Also by typing the public IP address of the EC2 instance on any browser of our choice, we confirm once the default Apache page loads as seen in the output below:

![Can Access Webserver](./images/Web%20Server.png)

**STEP 2 — INSTALLING MYSQL**

---

The  First thing to do is Installing the mysql-server using the code below:

`$ sudo apt install mysql-server`

Once installation is complete, log in to the MySQL console by typing:

`$ sudo mysql`

![mysql login](./images/mysql%20login.png)



