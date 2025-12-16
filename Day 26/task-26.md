# Day 26
##### Task: The xFusionCorp development team added updates to the project that is maintained under /opt/blog.git repo and cloned under /usr/src/kodekloudrepos/blog. Recently some changes were made on Git server that is hosted on Storage server in Stratos DC. The DevOps team added some new Git remotes, so we need to update remote on /usr/src/kodekloudrepos/blog repository as per details mentioned below:

a. In /usr/src/kodekloudrepos/blog repo add a new remote dev_blog and point it to /opt/xfusioncorp_blog.git repository.

b. There is a file /tmp/index.html on same server; copy this file to the repo and add/commit to master branch.

c. Finally push master branch to this new remote origin.

---

**Step 1** - SSH into the Storage Server

From the jump host:

`ssh natasha@ststor01`


**Step 2** - Navigate to the cloned repository

The repository is already cloned at:

`/usr/src/kodekloudrepos/blog`

Run:

`cd /usr/src/kodekloudrepos/blog`

**Step 3** - Add the new Git remote

You must add a remote named `dev_blog` pointing to:

`/opt/xfusioncorp_blog.git`

Run:

`git remote add dev_blog /opt/xfusioncorp_blog.git`

Verify:

`git remote -v`


You should see something like:

```
dev_blog  /opt/xfusioncorp_blog.git (fetch)
dev_blog  /opt/xfusioncorp_blog.git (push)
origin    <existing-origin> (fetch)
origin    <existing-origin> (push)
```

**Step 4** - Ensure you are on the master branch

`git checkout master`

**Step 5** - Copy /tmp/index.html into the repo

`cp /tmp/index.html .`


Verify the file exists:

`ls -l index.html`

**Step 6** - Add and commit the file to master

`git add index.html`

`git commit -m "Add index.html as per xFusionCorp update"`

**Step 7** - Push master branch to the new remote

The task says:

“Finally push master branch to this new remote origin”

That refers to the new remote you just added (dev_blog).

Run:

`git push dev_blog master`

---