# Day 33
##### Task: Sarah and Max were working on writting some stories which they have pushed to the repository. Max has recently added some new changes and is trying to push them to the repository but he is facing some issues. Below you can find more details:
- SSH into storage server using user max and password Max_pass123. Under /home/max you will find the story-blog repository. Try to push the changes to the origin repo and fix the issues. The story-index.txt must have titles for all 4 stories. Additionally, there is a typo in The Lion and the Mooose line where Mooose should be Mouse.
- Click on the Gitea UI button on the top bar. You should be able to access the Gitea page. You can login to Gitea server from UI using username sarah and password Sarah_pass123 or username max and password Max_pass123.
- Note: For these kind of scenarios requiring changes to be done in a web UI, please take screenshots so that you can share it with us for review in case your task is marked incomplete. You may also consider using a screen recording software such as loom.com to record and share your work.
---
**Step 1** - SSH into the Storage Server

From the jump host:

`ssh max@ststor01`

**Step 2** - Navigate to the repository

`cd /home/max/story-blog`

Check status:

`git status`

**Step 3** - Inspect the files

`cat story-index.txt`

**Step 4** - Fix the typo

`vi story-index.txt`

and correct the moose to mouse

**Step 5** - Commit the fixes

`git add story-index.txt`

git commit -m "Fix story index typo"

**Step 6** - Try pushing to origin

`git push origin`

**Step 7** - Resolve the push issue properly

1. Pull remote changes using rebase (IMPORTANT)
   - `git pull --rebase origin master`
2. If conflicts appear (possible but rare)
   -  Check status: `git status`
3. You will see:
```
both added:   story-index.txt
```
4. Open the conflicted file 
   -  `vi story-index.txt`

5. You will see conflict markers like this:
   - Fix story-index.txt correctly
   - Remove ALL conflict markers (<<<<<<<, =======, >>>>>>>)
   - Keep all 4 story titles, correctly spelled.
6. Final content must look like this (order does not matter):
```
The Fox and the Grapes
The Lion and the Mouse
The Tortoise and the Hare
The Crow and the Pitcher
```
7. Mark the conflict as resolved
   - `git add story-index.txt`
   - Continue the rebase
   - `git rebase --continue`
8. You should see something like: 
   -    `Successfully rebased and updated refs/heads/master`.
9. Push the changes (now it will work)
    - `git push origin master`

---
