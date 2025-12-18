# Day 30
##### Task : The Nautilus application development team was working on a git repository /usr/src/kodekloudrepos/news present on Storage server in Stratos DC. This was just a test repository and one of the developers just pushed a couple of changes for testing, but now they want to clean this repository along with the commit history/work tree, so they want to point back the HEAD and the branch itself to a commit with message add data.txt file. Find below more details:

- In /usr/src/kodekloudrepos/news git repository, reset the git commit history so that there are only two commits in the commit history i.e initial commit and add data.txt file.
- Also make sure to push your changes.
---

**Step 1** - SSH into the Storage Server

`ssh natasha@ststor01`

**Step 2** - Navigate to the repository

`cd /usr/src/kodekloudrepos/news`

**Step 3** - Identify the commit hash to reset to

List commits with messages:

`git log --oneline`


You will see something similar to:
```
c3d9f10 some test commit
b8a7c22 another test commit
9f2a4e1 add data.txt file
1a2b3c4 initial commit
```

Note the commit hash for:

`add data.txt file`

Example hash used below: 9f2a4e1
(Use the actual hash from your output.)

**Step 4** - Reset branch and HEAD to that commit

This removes all commits after add data.txt file:

`git reset --hard 9f2a4e1`

Now the repository history contains only:
```
initial commit
add data.txt file
```
**Step 5** - Verify commit history

`git log --oneline`

Expected output:
```
9f2a4e1 add data.txt file
1a2b3c4 initial commit
```

**Step 6** - Push the rewritten history to remote

Since history was rewritten, force push is required:

`git push origin master --force`

---
