# Day 20
##### Task : The Nautilus application development team is planning to launch a new PHP-based application, which they want to deploy on Nautilus infra in Stratos DC. The development team had a meeting with the production support team and they have shared some requirements regarding the infrastructure. Below are the requirements they shared:

a. Install nginx on app server 2 , configure it to use port 8098 and its document root should be /var/www/html.

b. Install php-fpm version 8.3 on app server 2, it must use the unix socket /var/run/php-fpm/default.sock (create the parent directories if don't exist).

c. Configure php-fpm and nginx to work together.

d. Once configured correctly, you can test the website using curl http://stapp02:8098/index.php command from jump host.

NOTE: We have copied two files, index.php and info.php, under /var/www/html as part of the PHP-based application setup. Please do not modify these files.

---
**Step 1** - Install prerequisites on App Server 2.
```
sudo yum install -y yum-utils epel-release

dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm

dnf install https://rpms.remirepo.net/enterprise/remi-release-9.rpm

dnf module install php:remi-8.3

php -v
```
**Step 2** -  Install nginx and php-fpm 8.3 packages

`sudo yum install -y nginx php-fpm php-cli php-mysqlnd php-xml php-mbstring`

**Step 3** - Create socket directory and set ownership
```
sudo mkdir -p /var/run/php-fpm
sudo chown -R nginx:nginx /var/run/php-fpm
sudo chmod 755 /var/run/php-fpm
```
**Step 4** - Configure a php-fpm pool (create /etc/php-fpm.d/default.conf)

```
sudo tee /etc/php-fpm.d/default.conf > /dev/null <<'EOF'
[default]
user = nginx
group = nginx
listen = /var/run/php-fpm/default.sock
listen.owner = nginx
listen.group = nginx
listen.mode = 0660
pm = dynamic
pm.max_children = 50
pm.start_servers = 5
pm.min_spare_servers = 2
pm.max_spare_servers = 10
chdir = /
clear_env = yes
EOF
```

`sudo mv -f /etc/php-fpm.d/www.conf /etc/php-fpm.d/www.conf.disabled 2>/dev/null || true`

**Step 5** - Enable/start php-fpm
```
sudo systemctl daemon-reload
sudo systemctl enable --now php-fpm
```

**Step 6** - Configure nginx to listen on port 8098 and use the socket
```
sudo tee /etc/nginx/conf.d/php_app.conf > /dev/null <<'NGINXCONF'
server {
    listen 8098;
    server_name _;

    root /var/www/html;
    index index.php index.html index.htm;

    # Serve static files
    location / {
        try_files $uri $uri/ =404;
    }

    # PHP handling
    location ~ \.php$ {
        include fastcgi_params;
        # ensure the SCRIPT_FILENAME is absolute path to the php file
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_pass unix:/var/run/php-fpm/default.sock;
        fastcgi_index index.php;
        # prevent accidental buffering issues
        fastcgi_buffer_size 16k;
        fastcgi_buffers 4 16k;
    }

    # Deny access to hidden files
    location ~ /\. {
        deny all;
    }
}
NGINXCONF
```
7) Ensure docroot ownership (do NOT modify index.php/info.php content)
```
sudo chown -R nginx:nginx /var/www/html
sudo chmod -R 755 /var/www/html
```
**Step 8** - Start nginx
```
sudo systemctl enable --now nginx
sudo systemctl restart php-fpm
sudo systemctl restart nginx
```

**Step 9** - Quick checks:
```
sudo ss -ltnp | grep :8098
sudo ss -xlpn | grep default.sock
```
**Step 10** - From jump host test:
```
curl http://stapp02:8098/index.php
curl http://stapp02:8098/info.php
```
---

