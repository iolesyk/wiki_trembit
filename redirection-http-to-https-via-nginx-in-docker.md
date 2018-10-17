. Install Docker
(https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce)

. Install Docker-compose
(https://docs.docker.com/compose/install/#install-compose)

. Create new project folder:
```
mkdir ./nginx
cd ./nginx
```
. Create a file called ``docker-compose.yml`` in your project directory and paste the following:
```
version: '3'
services:
   nginx:
     image: nginx:1.13
     ports:
       - 80:80
     volumes:
       - ./nginx.conf:/etc/nginx/nginx.conf
```
We use image ``nginx:1.13``, port ``80``, and maping local nginx config file ``./nginx.conf`` to container.

. Create a config file for nginx called ``nginx.conf`` in your project directory and paste the following:
```
user  nginx;
worker_processes  1;
error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;
events {
    worker_connections  1024;
}
http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
    access_log  /var/log/nginx/access.log  main;
    sendfile        on;
    keepalive_timeout  65;
server {
    listen       80;
    server_name  localhost;
    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
    return 301 https://$host$request_uri;
}
}
```
This line ``"return 301 https://$host$request_uri;"`` redirection http request to https.

. Build and start 
```
docker-compose up --build
```
Start container in the background
```
docker-compose up -d 
```