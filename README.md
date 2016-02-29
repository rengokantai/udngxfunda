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
