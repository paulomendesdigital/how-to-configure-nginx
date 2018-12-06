# How to configure Nginx

Install the nginx
```
sudo apt-get install nginx
```

Create the vhosts/example folder in /var/www

* The folder **example** is used to the project
```
sudo mkdir -p /var/www/vhosts/example
```

Create the index.html file
```
sudo vi index.html
```

Insert the code below in the index.html
```
My domain........
```

Copy the default file at /etc/nginx/sites-available/default to /etc/nginx/sites-available/example.conf
```
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/example.conf
```

Access the example.conf
```
sudo vi /etc/nginx/sites-available/example.conf
```

Change the lines below
```
listen 80 server_default;
to
listen 80;
```

```
listen [::]:80 server_default;
to
listen [::]:80;
```

```
root /var/www/html;
to
root /var/www/vhosts/example;
```

```
server_name _;
to
server_name www.example.com example.com
```

```
try_files $uri $uri/ =404;
to
try_files $uri $uri/ index.php?$args
```

Create a link symbolic at /etc/nginx/sites-enabled to /etc/nginx/sites-available/example.conf
```
sudo ln -s /etc/nginx/sites-available/example.conf /etc/nginx/sites-enabled
```

Verify the nginx with the code below
```
sudo nginx -t
```

If it`s ok, restart the nginx
```
sudo systemctl restart nginx
```

Access the hosts file in /etc/hosts
```
sudo vi /etc/hosts
```

Inset the line below in the hosts file
```
127.0.0.1 www.example.com example
```
