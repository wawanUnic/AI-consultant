# Gotify log storage service

### Web panel - port 8089

Work not as root

Run container
```
sudo docker run -d --restart unless-stopped -it --name gotify -p 8089:80 -e TZ="Europe/Warszawa" -v /var/gotify/data:/app/data gotify/server
```

Default login data
```
admin
admin
```

Next, change the administrator password, create a new user
```
change password
creale user
logout
login
```

Log in as the new user and create a working application, copy the key for the API
```
create application
```
