# Day 16
##### Task : Day by day traffic is increasing on one of the websites managed by the Nautilus production support team. Therefore, the team has observed a degradation in website performance. Following discussions about this issue, the team has decided to deploy this application on a high availability stack i.e on Nautilus infra in Stratos DC. They started the migration last month and it is almost done, as only the LBR server configuration is pending. Configure LBR server as per the information given below:

a. Install nginx on LBR (load balancer) server.

b. Configure load-balancing with the an http context making use of all App Servers. Ensure that you update only the main Nginx configuration file located at /etc/nginx/nginx.conf.

c. Make sure you do not update the apache port that is already defined in the apache configuration on all app servers, also make sure apache service is up and running on all app servers.

d. Once done, you can access the website using StaticApp button on the top bar.

---

**Step 1** -  Ensure Apache is running on all App Servers.

SSH to app server and running following commands:

`sudo systemctl status httpd`

**Step 2** - Install Nginx on the LBR and back up nginx.conf

SSH to your LBR host

Install and enable nginx:

`sudo yum install -y nginx`

`sudo systemctl enable --now nginx`

Backup the original main config:

`sudo cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak.$(date +%F_%T)`

**Step 3** - Overwrite only /etc/nginx/nginx.conf with a load-balancer config

Create a configuration that defines an upstream using all three app servers and proxies requests to it. Run this on the LBR:

```
sudo tee /etc/nginx/nginx.conf > /dev/null <<'EOF'
user  nginx;
worker_processes  auto;

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

    # === Upstream backends (App Servers) ===
    upstream backend_appservers {
        # Use the app server hostnames and the app port (do not modify Apache ports on app servers)
        server stapp01:8088;
        server stapp02:8088;
        server stapp03:8088;
        # you can add additional options, e.g. least_conn, max_fails, fail_timeout, if desired:
        # least_conn;
    }

    # === HTTP server block (load-balancer) ===
    server {
        listen       80;
        server_name  _;

        # Proxy all requests to the upstream pool
        location / {
            proxy_pass         http://backend_appservers;
            proxy_set_header   Host $host;
            proxy_set_header   X-Real-IP $remote_addr;
            proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header   X-Forwarded-Proto $scheme;
            proxy_http_version 1.1;
            proxy_set_header   Connection "";
            # optional timeouts
            proxy_connect_timeout  5s;
            proxy_send_timeout     30s;
            proxy_read_timeout     30s;
        }

        # Optional health-check style endpoint mapping (if backends expose one)
        location /health {
            proxy_pass http://backend_appservers/;
            proxy_set_header Host $host;
        }
    }
}
EOF
```

Important: This command edits only `/etc/nginx/nginx.conf` as requested.
**Step 4** - Test and reload Nginx

Test Nginx configuration and reload:

`sudo nginx -t`

`sudo systemctl reload nginx`

**Step 5** - Verify load-balancer from the Jump Host

curl -I http://stlbr01/


---
