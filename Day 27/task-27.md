# Day 27
##### Task: The Nautilus application development team was working on a git repository /usr/src/kodekloudrepos/ecommerce present on Storage server in Stratos DC. However, they reported an issue with the recent commits being pushed to this repo. They have asked the DevOps team to revert repo HEAD to last commit. Below are more details about the task:


- In /usr/src/kodekloudrepos/ecommerce git repository, revert the latest commit ( HEAD ) to the previous commit (JFYI the previous commit hash should be with initial commit message ).

- Use revert ecommerce message (please use all small letters for commit message) for the new revert commit.
---
**Step 1** - SSH into the Storage Server

From the jump host:

`ssh natasha@ststor01`

**Step 2** - Navigate to the repository

`cd /usr/src/kodekloudrepos/ecommerce`

**Step 3** - Verify commit history (optional but safe)

This helps confirm what will be reverted:

`git log --oneline -2`


You should see something like:
```
abc1234 Latest commit message
def5678 initial commit
```

Here, abc1234 is HEAD, and def5678 is the previous (initial) commit.

**Step 4** - Revert the latest commit (HEAD)

Run:

`git revert HEAD`

It will open the text editor. and bottom add the comment message as "revert ecommerce" and save the file. 
then revert will be commited. 

---