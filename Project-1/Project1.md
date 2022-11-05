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

Since our Ubuntu server is an EC2 instance, we need to open TCP port 80 in the EC2 Instance




