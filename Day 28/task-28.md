# Day 28
##### Task: The Nautilus application development team has been working on a project repository /opt/blog.git. This repo is cloned at /usr/src/kodekloudrepos on storage server in Stratos DC. They recently shared the following requirements with the DevOps team:

There are two branches in this repository, master and feature. One of the developers is working on the feature branch and their work is still in progress, however they want to merge one of the commits from the feature branch to the master branch, the message for the commit that needs to be merged into master is Update info.txt. Accomplish this task for them, also remember to push your changes eventually.


---

**Step 1** - SSH into the Storage Server

From the jump host:

`ssh natasha@ststor01`

**Step 2** - Go to the cloned repository

`cd /usr/src/kodekloudrepos/blog`

**Step 3** - Find the commit hash on feature branch

Switch to feature branch and locate the commit:

`git checkout feature`

`git log --oneline`

Look for the commit with message: Update info.txt


Example output:
```
a1b2c3d Update info.txt
e4f5g6h Some other work
```

Note the commit hash (example: a1b2c3d).

**Step 4** - Switch back to master branch

`git checkout master`

**Step 5** - Cherry-pick the required commit into master

Use the commit hash you noted:

`git cherry-pick a1b2c3d`

**Step 6** - Verify the commit is now in master

`git log --oneline`

You should see:

`a1b2c3d Update info.txt`

listed in the master branch history.

**Step 7** - Push the updated master branch to remote

`git push origin master`

---