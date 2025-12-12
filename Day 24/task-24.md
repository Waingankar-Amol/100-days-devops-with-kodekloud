# Day 24
##### Task: Nautilus developers are actively working on one of the project repositories, /usr/src/kodekloudrepos/apps. Recently, they decided to implement some new features in the application, and they want to maintain those new changes in a separate branch. Below are the requirements that have been shared with the DevOps team:

- On Storage server in Stratos DC create a new branch xfusioncorp_apps from master branch in /usr/src/kodekloudrepos/apps git repo.

- Please do not try to make any changes in the code.

---

**Step 1** - SSH into Storage Server

`ssh natasha@ststor01`

**Step 2** - Navigate to the existing repo

The repo path given is:

`/usr/src/kodekloudrepos/apps`

Go there:

`cd /usr/src/kodekloudrepos/apps`

**Step 3** - Ensure you’re on the master branch

`git branch`

If you are not on master:

`git checkout master`

**Step 4** - Create the new branch from master

Use:

`git checkout -b xfusioncorp_apps`


This creates the branch AND switches to it in one step.

**Step 5** - Confirm the new branch exists

`git branch`


You should see:
```
master
* xfusioncorp_apps
```

---

