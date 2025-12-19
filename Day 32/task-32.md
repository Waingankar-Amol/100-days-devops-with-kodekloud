# Day 32
##### Task: The Nautilus application development team has been working on a project repository `/opt/news.git`. This repo is cloned at `/usr/src/kodekloudrepos` on storage server in Stratos DC. They recently shared the following requirements with DevOps team:

- One of the developers is working on feature branch and their work is still in progress, however there are some changes which have been pushed into the master branch, the developer now wants to rebase the feature branch with the master branch without loosing any data from the feature branch, also they don't want to add any merge commit by simply merging the master branch into the feature branch. Accomplish this task as per requirements mentioned.\
- Also remember to push your changes once done.
---
**Step - 1** SSH into the Storage Server

From the jump host:

`ssh natasha@ststor01`

**Step 2** - Navigate to the repository

`cd /usr/src/kodekloudrepos/news`

**Step 3** - Checkout the feature branch

`git checkout feature`

**Step 4** - Rebase feature branch onto master

`git rebase master`

**Step 5** - Push the rebased feature branch

`git push origin feature --force`

---
