# Day 25
##### Task: The Nautilus application development team has been working on a project repository /opt/beta.git. This repo is cloned at /usr/src/kodekloudrepos on storage server in Stratos DC. They recently shared the following requirements with DevOps team:

- Create a new branch xfusion in `/usr/src/kodekloudrepos/beta` repo from master and copy the `/tmp/index.html` file (present on storage server itself) into the repo. Further, add/commit this file in the new branch and merge back that branch into master branch. Finally, push the changes to the origin for both of the branches.

---
**Step 1** - SSH to the Storage Server

From the jump host:

ssh natasha@ststor01

**Step 2** - Go to the cloned repository

The repo is cloned under:

`/usr/src/kodekloudrepos/beta`

Run:

`cd /usr/src/kodekloudrepos/beta`

**Step 3** - Make sure you are on master branch
   
`git checkout master`

`git pull`


This ensures you start from the latest master.

**Step 4** - Create the new branch xfusion from master

`git checkout -b xfusion`

This creates and switches to the new branch.

Confirm:

`git branch`

Expected:

```
master
* xfusion
```

**Step 5** - Copy /tmp/index.html into the repo

`cp /tmp/index.html .`


Or if they want it specifically inside repo root, this is correct.

Verify:

`ls -l index.html`

**Step 6** - Add and commit the file to the new branch

`git add index.html`

`git commit -m "Add index.html as per requirements"`

**Step 7** - Switch back to master

`git checkout master`

**Step 8** - Merge the xfusion branch into master

`git merge xfusion`

If no conflicts, merge completes.

**Step 9** - Push both branches to the origin

First push the new branch:

`git push origin xfusion`

Then push updated master:

`git push origin master`

- Verification (optional but safe)

`git branch -a`

`git log --oneline --decorate --graph`


You should see the commit from xfusion also appearing in master.

---
