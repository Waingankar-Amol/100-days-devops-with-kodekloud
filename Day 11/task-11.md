# Day 11
##### Task :The Nautilus application development team recently finished the beta version of one of their Java-based applications, which they are planning to deploy on one of the app servers in Stratos DC. After an internal team meeting, they have decided to use the tomcat application server. Based on the requirements mentioned below complete the task:



a. Install tomcat server on App Server 3.

b. Configure it to run on port 8083.

c. There is a ROOT.war file on Jump host at location /tmp.


Deploy it on this tomcat server and make sure the webpage works directly on base URL i.e curl http://stapp03:8083


**Step 1** - Install Tomcat on App Server 3
On App Server 3:

Install tomcat

`sudo yum install -y tomcat`

**Step 2** - Change Tomcat HTTP port from 8080 to 8083

`sudo cp /etc/tomcat/server.xml /etc/tomcat/server.xml.bak`

**Step 3** -  Update the below line in server.xml
`<Connector port="8083" protocol="HTTP/1.1"connectionTimeout="20000"redirectPort="8443" />`

**Step 4** - Start and enable tomcat
   
`sudo systemctl daemon-reload
sudo systemctl enable --now tomcat`

**Step 5** - Ensure webapps dir exists and owned by tomcat
   
`sudo mkdir -p /var/lib/tomcat/webapps
sudo chown -R tomcat:tomcat /var/lib/tomcat/webapps`

**Step 6** - From the Jump Host — copy ROOT.war to stapp03
scp /tmp/ROOT.war banner@stapp03:/tmp/

**Step 7** - On App Server 3 — deploy the WAR and finalize

`sudo mv -f /tmp/ROOT.war /var/lib/tomcat/webapps/ROOT.war
sudo chown tomcat:tomcat /var/lib/tomcat/webapps/ROOT.war`

`sudo systemctl restart tomcat`

**Step 8** - Verify from Jump Host
Verify the port is running or not using below command On App Server 3:

`sudo ss -tulnp | grep 8083`

And then run the command from Jumo Host
`curl -I http://stapp03:8083`

