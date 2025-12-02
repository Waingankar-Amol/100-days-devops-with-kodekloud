# Day 15
##### Task : The system admins team of xFusionCorp Industries needs to deploy a new application on App Server 1 in Stratos Datacenter. They have some pre-requites to get ready that server for application deployment. Prepare the server as per requirements shared below:

1. Install and configure nginx on App Server 1.

2. On App Server 1 there is a self signed SSL certificate and key present at location /tmp/nautilus.crt and /tmp/nautilus.key. Move them to some appropriate location and deploy the same in Nginx.

3. Create an index.html file with content Welcome! under Nginx document root.

4. For final testing try to access the App Server 1 link (either hostname or IP) from jump host using curl command. For example curl -Ik https://<app-server-ip>/.
---
**Step 1** - Install Nginx on App Server 1
SSH to App Server 1 from jump host:

`ssh tony@stapp01`

Install nginx:

```
sudo yum install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx
```

**Step 2** - Move SSL certificate and key to correct location (Nginx standard)

Nginx SSL files are usually stored in:

`/etc/nginx/ssl/`


Create directory:

`sudo mkdir -p /etc/nginx/ssl`

Move the certificate and key:

`sudo mv /tmp/nautilus.crt /etc/nginx/ssl/`

`sudo mv /tmp/nautilus.key /etc/nginx/ssl/`


Set proper permissions:

`sudo chmod 600 /etc/nginx/ssl/nautilus.key
sudo chmod 644 /etc/nginx/ssl/nautilus.crt`

**Step 3** - Configure Nginx to use SSL

Edit default SSL config:

`sudo vi /etc/nginx/nginx.conf`


Inside the http { ... } block, add the following server block (or edit the existing one):
```
server {
    listen 443 ssl;
    server_name _;

    ssl_certificate     /etc/nginx/ssl/nautilus.crt;
    ssl_certificate_key /etc/nginx/ssl/nautilus.key;

    root /usr/share/nginx/html;
    index index.html;
}
```


Save and exit.

Test Nginx config:

`sudo nginx -t`

Restart Nginx:

`sudo systemctl restart nginx`

**Step 4** - Create index.html with required content

`echo "Welcome!" | sudo tee /usr/share/nginx/html/index.html`

**Step 5** - Final Test (from Jump Host)

Exit App Server 1:

`exit`


Now from jump host run:

`curl -Ik https://stapp01/`


OR using IP:

`curl -Ik https://<APP-SERVER-1-IP>/`


You should see:

HTTP/1.1 200 OK