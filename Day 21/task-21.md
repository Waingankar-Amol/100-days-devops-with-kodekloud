# Day 21
##### Task : The Nautilus development team has provided requirements to the DevOps team for a new application development project, specifically requesting the establishment of a Git repository. Follow the instructions below to create the Git repository on the Storage server in the Stratos DC:

1. Utilize yum to install the git package on the Storage Server.
2. Create a bare repository named /opt/blog.git (ensure exact name usage).
   
---
**Step 1** - SSH into the Storage server

`ssh natasha@ststor01`

**Step 2** - Install git on Storage Server

`sudo yum install git -y`

**Step 3** - Create bare git repository

`sudo git init --bare /opt/blog.git`

---