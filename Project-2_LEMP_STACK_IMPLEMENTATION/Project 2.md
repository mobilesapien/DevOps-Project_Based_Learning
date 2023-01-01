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

![Status check via browser](./images/2-%20Nginx_Status_check.png "Nginx is online").

