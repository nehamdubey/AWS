### Frontend 

Expense App Frontend or UI is developed by  by using a web-server `Nginx`


#### Who decides the type of Web-Server to be used ?
```
    In our case, we selected to use nginx and it's also the suggested entity from Developer.
    Nginx is also one of the highly used Web-Server 

```

Nginx will have the webframe for the web application. 

Our application servers static content and we need a web server to perform the same:

#### Install Nginx On The Top Of The Server-01 as Frondend

To run the command we need to always use SUDO.... as a root user

```
Ex... sudo dnf install nginx -y to install Nginx on frontend server
    # dnf install nginx -y  

    [ Hint : dnf is the package manager on RHEL9 ]
```

#### Start & Enable Nginx service 

```
    # sudo systemctl enable nginx       [ Enabling the service will keep the service to be started automatically when server goes for a boot ]
    # sudo systemctl start nginx 
```
Note:- You need to make sure your security group for the EC2 server (Frontend,mysql and backend) check for Inbound rule to allow IP's from ALL tracfic.


!!! Try to access the service once over the browser and ensure you get some default content.

```
    1) Open your browser 
    2) IP Address 
    3) You should be able to see some default content and thus proves your nginx is working 
```

#### Remove the default content as we have our content developed and shared to us by the frontend developer 

```
You can do this two way...
either first go to /usr/share/nginx/html via CD /usr/share/nginx/html and then run
# Sudo rm -rf *
OR
    # sudo rm -rf /usr/share/nginx/html/*          [ Nginx path where web content is stored ]

```


#### Download the web-content for frontend
This is provided by developer
```
    # curl -o /tmp/frontend.zip https://expense-web-app.s3.amazonaws.com/frontend.zip
```

#### Extract the frontend content.

```
    # sudo cd /usr/share/nginx/html 
    # sudo unzip /tmp/frontend.zip
```

!!! Try to access the nginx service once more over the browser via server IP or DNS name and ensure you get expense content.


#### Create Nginx Reverse Proxy Configuration.
edit the file via VIM editor
```
    # sudo vim /etc/nginx/default.d/expense.conf   ( empty the file if any and add the below content )
--------------------------------------------------
Copy this and add the ip of backedn server instead of localhost...
To add below content on VIM editor press i (for insert) and pase below
proxy_http_version 1.1;

location /api/ { proxy_pass http://localhost:8080/; }

location /health {
stub_status on;
access_log off;
}
```
To save and exit editor use ESC key from keyboard
Above reverse proxy config plays a critical role and you'll get this more when detailing with backend.

!!! NOTE : Replace the localhost with the private ip address of your backend server. Word localhost is just used to avoid the failures on the Nginx Server.

**Load the service.**
    # sudo systemctl daemon-reload

### Restart Nginx Service to load the changes of the configuration.

```
    # sudo systemctl restart nginx 
    # sudo systemctl status nginx           ( service should show up as running, if not, you'd have made some mistakes above )
```


proceed with `002-mysql` for database install.
