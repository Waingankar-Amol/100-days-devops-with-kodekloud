# Day 29
##### Task: Max want to push some new changes to one of the repositories but we don't want people to push directly to master branch, since that would be the final version of the code. It should always only have content that has been reviewed and approved. We cannot just allow everyone to directly push to the master branch. So, let's do it the right way as discussed below:


SSH into storage server using user max, password Max_pass123 . There you can find an already cloned repo under Max user's home.


Max has written his story about The 🦊 Fox and Grapes 🍇


Max has already pushed his story to remote git repository hosted on Gitea branch story/fox-and-grapes


Check the contents of the cloned repository. Confirm that you can see Sarah's story and history of commits by running git log and validate author info, commit message etc.


Max has pushed his story, but his story is still not in the master branch. Let's create a Pull Request(PR) to merge Max's story/fox-and-grapes branch into the master branch


Click on the Gitea UI button on the top bar. You should be able to access the Gitea page.


UI login info:

- Username: max

- Password: Max_pass123

PR title : Added fox-and-grapes story

PR pull from branch: story/fox-and-grapes (source)

PR merge into branch: master (destination)


Before we can add our story to the master branch, it has to be reviewed. So, let's ask tom to review our PR by assigning him as a reviewer


Add tom as reviewer through the Git Portal UI

Go to the newly created PR

Click on Reviewers on the right

Add tom as a reviewer to the PR

Now let's review and approve the PR as user Tom


Login to the portal with the user tom


Logout of Git Portal UI if logged in as max


UI login info:

- Username: tom

- Password: Tom_pass123

PR title : Added fox-and-grapes story

Review and merge it.

Great stuff!! The story has been merged! 👏


Note: For these kind of scenarios requiring changes to be done in a web UI, please take screenshots so that you can share it with us for review in case your task is marked incomplete. You may also consider using a screen recording software such as loom.com to record and share your work.

---

### Task Objective

- Verify Max’s local repository and commit history

- Create a Pull Request (PR) from story/fox-and-grapes → master

- Assign tom as reviewer

- Login as tom, review, approve, and merge the PR

---

**Step 1** — SSH into Storage Server as Max

From the jump host:

`ssh max@ststor01`

Password:

`Max_pass123`

**Step 2** — Navigate to the cloned repository

The repository is already cloned under Max’s home directory.
```
cd ~
ls
```

Identify the repo directory, then:

`cd <repo-name>`


(Example: cd story-blog)

**Step 3** — Verify repository contents and commit history

Check files (Sarah’s story should be present):

`ls`

Check commit history and authors:

`git log`

Confirm:

Sarah’s commits exist

Author names and commit messages are visible

Max’s commit exists on branch story/fox-and-grapes

Check current branch:

`git branch`

You should see:
```
* story/fox-and-grapes
  master
```

**Step 4** — Open Gitea UI

Click Gitea UI button from the top bar

This opens the Git Portal in your browser

**Step 5** — Login as Max

Login credentials:

```
Username: max

Password: Max_pass123
```

**Step 6** — Create Pull Request

Open the repository

Click Pull Requests

Click New Pull Request

Fill in details:

PR Title: Added fox-and-grapes story

Pull from (source):

`story/fox-and-grapes`

Merge into (destination):

`master`

Click Create Pull Request

**Step 7** — Assign Tom as Reviewer

Inside the newly created PR:

On the right sidebar, find Reviewers

Click Add

Select tom

Tom added as reviewer

**Step 8** — Logout as Max

Click on Max’s profile → Logout

**Step 9** — Login as Tom

Login credentials:
```
Username: tom

Password: Tom_pass123
```

**Step 10** — Review and Merge the PR

Open Pull Requests

Click PR titled:

`Added fox-and-grapes story`

Review changes

Click Approve

Click Merge Pull Request

Confirm merge

---