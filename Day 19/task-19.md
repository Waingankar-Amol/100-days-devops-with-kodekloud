# Day 19
##### Task: xFusionCorp Industries is planning to host two static websites on their infra in Stratos Datacenter. The development of these websites is still in-progress, but we want to get the servers ready. Please perform the following steps to accomplish the task:

a. Install httpd package and dependencies on app server 1.

b. Apache should serve on port 6000.

c. There are two website's backups /home/thor/news and /home/thor/cluster on jump_host. Set them up on Apache in a way that news should work on the link http://localhost:6000/news/ and cluster should work on link http://localhost:6000/cluster/ on the mentioned app server.

d. Once configured you should be able to access the website using curl command on the respective app server, i.e curl http://localhost:6000/news/ and curl http://localhost:6000/cluster/

---

**Step 1** - Copy website backups from jump host → App Server 1

`scp -r /home/thor/news /home/thor/cluster tony@stapp01:/home/tony/`

**Step 2** - On App Server 1 — install Apache and configure

`sudo yum install httpd -y`

`sudo vi /etc/httpd/conf/httpd.conf`

Find: `Listen 80` Change to: `Listen 6000`

`sudo systemctl restart httpd`

**Step 3** - Test locally on App Server & Then Jump Host

```
curl -I http://localhost:6000/news/
curl -I http://localhost:6000/cluster/
```
