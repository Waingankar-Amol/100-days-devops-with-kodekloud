# Day 35
# Task: The Nautilus DevOps team aims to containerize various applications following a recent meeting with the application development team. They intend to conduct testing with the following steps:
- Install docker-ce and docker compose packages on App Server 3.
- Initiate the docker service.
---
**Step 1** - SSH into App Server 3

From the jump host:

`ssh banner@stapp03`

(Use the correct username/password provided by your lab.)

**Step 2** - Install required dependencies

`sudo yum install -y yum-utils device-mapper-persistent-data lvm2`

**Step 3** - Add the Docker CE repository

`sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo`

**Step 4** - Install Docker CE and Docker Compose plugin

`sudo yum install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin`

**Step 5** - Start and enable Docker service

```
sudo systemctl start docker
sudo systemctl enable docker
```
Step 6 - Verify Docker is running

`sudo systemctl status docker --no-pager`

Expected:

```
Active: active (running)
```

Verify Docker version:
```
docker --version
docker compose version
```

---
