### This is a project accompanying Nginx Crash Course

### Commands used in the tutorial

##### start nginx
```nginx
nginx
```

##### get options
```nginx
nginx -h
```

##### restart nginx
```nginx
nginx -s reload
```

##### stop nginx
```nginx
nginx -s stop
```  

##### print logs
**It depends on type of OS you are using**
```nginx
tail -f /usr/local/var/log/nginx/access.log
```

##### restart nginx
```nginx
nginx -s reload
```

##### create folder for nginx certificates
```nginx
mkdir ~/nginx-certs
```
```nginx
cd ~/nginx-certs
```

##### create self-signed certificate
```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout nginx-selfsigned.key -out nginx-selfsigned.crt
```

##### Example nginx config used
```nginx
worker_processes 1;

events {
    worker_connections 1024;
}

http {
    include mime.types;

    upstream backend_cluster {
        least_conn;
        server 127.0.0.1:3001;
        server 127.0.0.1:3002;
        server 127.0.0.1:3003;
    }

    server {
        listen 8080;
        server_name localhost;

        location / {
            proxy_pass http://backend_cluster;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header User-Agent $http_user_agent;
            proxy_set_header Cookie $http_cookie;
        }
    }
}

```

##### Example of how to enable secure communication via https
```nginx
server {
        listen 443 ssl;
        server_name localhost;

        ssl_certificate /Users/mac/nginx-certs/nginx-selfsigned.crt;
        ssl_certificate_key /Users/mac/nginx-certs/nginx-selfsigned.key;

        location / {
            proxy_pass http://backend_cluster;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header User-Agent $http_user_agent;
            proxy_set_header Cookie $http_cookie;
        }
    }
```

##### Example of how to handle redirects
```nginx
server {
        listen 80;
        server_name localhost;

        location / {
            return 301 https://$host$uri;
        }
    }
```
