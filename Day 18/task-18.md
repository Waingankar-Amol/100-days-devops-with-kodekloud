# Day 18
##### Task: xFusionCorp Industries is planning to host a WordPress website on their infra in Stratos Datacenter. They have already done infrastructure configuration—for example, on the storage server they already have a shared directory /vaw/www/html that is mounted on each app host under /var/www/html directory. Please perform the following steps to accomplish the task:

a. Install httpd, php and its dependencies on all app hosts.

b. Apache should serve on port 8088 within the apps.

c. Install/Configure MariaDB server on DB Server.

d. Create a database named kodekloud_db10 and create a database user named kodekloud_cap identified as password YchZHRcLkL. Further make sure this newly created user is able to perform all operation on the database you created.

e. Finally you should be able to access the website on LBR link, by clicking on the App button on the top bar. You should see a message like App is able to connect to the database using user kodekloud_cap

---

**Step 1** - Install Apache, PHP & dependencies on ALL App Hosts

Perform these steps on:

- stapp01 (user: tony)

- stapp02 (user: steve)

- stapp03 (user: banner)

SSH into each app server
```
sudo yum install -y httpd php php-mysqlnd php-cli php-common php-fpm

sudo systemctl enable httpd

sudo systemctl start httpd
```


Repeat on stapp02 & stapp03 (using correct users).

**Step 2** - Configure Apache to serve on port 8088

Run on each App Server:

Edit Apache config

`sudo vi /etc/httpd/conf/httpd.conf`

Find: `Listen 80` Change to: `Listen 8088`

Save & exit.

Restart Apache:

`sudo systemctl restart httpd`

Verify:

`sudo ss -tulnp | grep httpd`

Expected:

`0.0.0.0:8088   httpd`

**`index.php` file is already added**

**Step 3** - Install & Configure MariaDB on DB Server

SSH into DB Server:

ssh peter@stdb01

Install MariaDB server (if not installed):

```
sudo yum install -y mariadb-server
sudo systemctl enable mariadb
sudo systemctl start mariadb
```

**Step 4** - Create Database + DB User + Permissions

Switch to mysql prompt:

`sudo mysql -u root`

Run:
```
CREATE DATABASE kodekloud_db10;

CREATE USER 'kodekloud_cap'@'%' IDENTIFIED BY 'YchZHRcLkL';

GRANT ALL PRIVILEGES ON kodekloud_db10.* TO 'kodekloud_cap'@'%';

FLUSH PRIVILEGES;

EXIT;
```

Make sure MariaDB listens on all interfaces:

`sudo vi /etc/my.cnf`

Ensure these lines exist or edit them:

```
[mysqld]
bind-address=0.0.0.0
```

Restart MariaDB:

`sudo systemctl restart mariadb`