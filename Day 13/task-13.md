# Day 13
##### Task :We have one of our websites up and running on our Nautilus infrastructure in Stratos DC. Our security team has raised a concern that right now Apache’s port i.e 8085 is open for all since there is no firewall installed on these hosts. So we have decided to add some security layer for these hosts and after discussions and recommendations we have come up with the following requirements:

1. Install iptables and all its dependencies on each app host.


2. Block incoming port 8085 on all apps for everyone except for LBR host.


3. Make sure the rules remain, even after system reboot.


Run the below script on each App Server. 

```
#!/bin/bash

sudo yum install -y iptables iptables-services #installing iptables on the server

sudo iptables -F #deleting all rules.

sudo iptables -A INPUT -p tcp -s 172.16.238.14 --dport 3000 -j ACCEPT  # Allowing 3000 port for LBR host. (First enter ACCEPT rule then DROP rule.)

sudo iptables -A INPUT -p tcp --dport 3000 -j DROP # blocking all incoming traffic

sudo service iptables save #Save rules so they persist after reboot

sudo systemctl restart iptables #Restart to validate

sudo iptables -L # List the iptable rules
```

**SSH to LBR Host and Verify**

```
telnet stapp01 3000

telnet stapp02 3000

telnet stapp03 3000
```