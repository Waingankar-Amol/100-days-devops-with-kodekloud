# Day 14
##### Task : The production support team of xFusionCorp Industries has deployed some of the latest monitoring tools to keep an eye on every service, application, etc. running on the systems. One of the monitoring systems reported about Apache service unavailability on one of the app servers in Stratos DC. 
- Identify the faulty app host and fix the issue. Make sure Apache service is up and running on all app hosts. They might not have hosted any code yet on these servers, so you don’t need to worry if Apache isn’t serving any pages. Just make sure the service is up and running. Also, make sure Apache is running on port 8088 on all app servers.
---

**Step 1** - Check Apache Service Status on all APP Server
Run below command on APP server: 

`sudo systemctl status httpd`

**Step 2** - Troubleshoot the Apache Server

If Apache service status is failed then run the below command to check running ports.

`sudo netstat -tunlp`
with this command you'll get port number and process running on it.  

Now we'll kill the process using process id using below command: 

`sudo kill -9 <process-id>`

**Step 3** - Restart the Apache Server

`sudo systemctl start httpd`


**Step 4** - Do Final Verification from Jump Host

```
curl http://stapp01:8088
curl http://stapp02:8088
curl http://stapp03:8088
```

---
