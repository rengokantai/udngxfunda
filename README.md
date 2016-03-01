#### udngxfunda

#####1
######build from source code:
```
wget http://nginx.org/download/nginx-1.9.12.tar.gz
tar zxvf nginx-1.9.12.tar.gz
apt-get install libpcre3 libpcreapp0 libpcre3-dev zlib1g-dev libssl-dev
```
config:
```
./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-debug --with-pcre --with-http_ssl_module
make
make install
```
######update custom.
nginx init scripts.  

```
cd /etc/init.d/
wget https://raw.githubusercontent.com/JasonGiedymin/nginx-init-ubuntu/master/nginx
sudo chmod +x nginx
update-rc.d -f nginx defaults
```
override default setting in init script:
```
echo "NGINX_CONF_FILE=/etc/nginx/nginx.conf" > /etc/default/nginx
echo "DAEMON=/usr/bin/nginx" >> /etc/default/nginx
service nginx start
```
check
```
curl -I google.com
```
If updating,run
```
service nginx reload
```
#####2
######virtual host
```
events{}
http{
include mime.types;     #types{text/html html; text/css css;}
server{
  listen 80;
  server_name 12.23.23.21;
  root /site/root;
  error_log /var/log/nginx/error.log debug;      # or access_log off; error_log off;
  location /param {    # /param  /parammmm   /param/2
    return 200 'string';
  }
  location = /param {    # /param
    return 200 'string';
  }
  location ~ /param[0-9] {    # /param3      /greet is not working.
    return 200 'string';
  }
  location ^~ /param {    # /param  prefix preference
    return 200 'string';
  }
  location /down {
    root /site;
    try_files $uri =404;
  }
}
}
```
######backend comm
```
apt-get install php5-fpm php5 php5-cgi php5-mysql
```
######other useful directives
check no of cpu:
```
nproc
lscpu
ulimit -n  //get connection
```

#####3
######Gzip
```
curl -I -H 'Accept-Encoding:gzip,deflate' http://.......
```

```
gzip on;
gzip_min_length 100;  only gzip file larger than 100 bytes default 20byte.
gzip_comp_level 3;  zip level
gzip_types text/plain text/css text/javascript;

gzip_disable "msie6"
```
######fast_cgi
benchtest
```
ab -n 100 -c 10 http://12.12.12.12/...
```
