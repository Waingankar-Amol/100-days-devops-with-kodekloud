# Day 31
##### Task: The Nautilus application development team was working on a git repository /usr/src/kodekloudrepos/official present on Storage server in Stratos DC. One of the developers stashed some in-progress changes in this repository, but now they want to restore some of the stashed changes. Find below more details to accomplish this task:

- Look for the stashed changes under /usr/src/kodekloudrepos/official git repository, and restore the stash with stash@{1} identifier. Further, commit and push your changes to the origin.

---

**Step - 1** SSH into the Storage Server

From the jump host:

`ssh natasha@ststor01`

**Step 2** - Navigate to the repository

`cd /usr/src/kodekloudrepos/official`

**Step 3** - List available stashes (verification step)

`git stash list`

You should see something similar to:
```
stash@{0}: WIP on master: ...
stash@{1}: WIP on master: ...
```
Confirms that stash@{1} exists.

**Step 4** - Restore the required stash (stash@{1})

Use apply (preferred for labs, because it keeps the stash record):

`git stash apply stash@{1}`

**Step 5** - Verify restored changes

`git status`

You should see modified or newly added files listed.

**Step 6** - Add and commit the restored changes
```
git add .
git commit -m "Restore stashed changes"
```

(Commit message can be anything sensible unless specified; this one is safe.)

Step 7 - Push changes to the origin repository

`git push origin master`

---