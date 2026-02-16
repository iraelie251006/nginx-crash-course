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

