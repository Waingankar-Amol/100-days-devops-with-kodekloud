# Day 12
##### Task :Our monitoring tool has reported an issue in Stratos Datacenter. One of our app servers has an issue, as its Apache service is not reachable on port 8082 (which is the Apache port). The service itself could be down, the firewall could be at fault, or something else could be causing the issue.



- Use tools like telnet, netstat, etc. to find and fix the issue. Also make sure Apache is reachable from the jump host without compromising any security settings.

- Once fixed, you can test the same using command curl http://stapp01:8082 command from jump host.

Note: Please do not try to alter the existing index.html code, as it will lead to task failure.

**Step 1** - SSH into App Server 1

**Step 2** - Check if Apache is running

`sudo systemctl status httpd`

Status was failed. 

**Step 3** - Check listening ports

`sudo netstat -tulnp`

I found one process which running on 8082 port i.e. why apache server was not running. 

**Step 4** - Kill the process running on 8082 Port

I found the process ID in the command `sudo netstat -tulnp`

and then kill the process using below command

`sudo kill -9 <process-id>`

**Step 5** - Start the apache

`sudo systemctl start httpd`

**Step 6** - Check if any firewall is installed or not

I found the installed fireall i.e. iptables. 

Command is `sudo iptables -L`

**Step 7** - Add the firewall rule for 8082 port.

`sudo iptables -I INPUT -p tcp --dport 8082 -j ACCEPT`

**Step 8** - Run the curl command from Jump Host Server.

`curl http://stapp01:8082`