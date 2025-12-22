# Day 34
##### Task: The Nautilus application development team was working on a git repository /opt/media.git which is cloned under /usr/src/kodekloudrepos directory present on Storage server in Stratos DC. The team want to setup a hook on this repository, please find below more details:

- Merge the feature branch into the master branch, but before pushing your changes complete below point.
- Create a post-update hook in this git repository so that whenever any changes are pushed to the master branch, it creates a release tag with name release-2023-06-15, where 2023-06-15 is supposed to be the current date. For example if today is 20th June, 2023 then the release tag must be release-2023-06-20. Make sure you test the hook at least once and create a release tag for today's release.
- Finally remember to push your changes.
Note: Perform this task using the natasha user, and ensure the repository or existing directory permissions are not altered.

---
**Step - 1** SSH into the Storage Server

From the jump host:

`ssh natasha@ststor01`

**Step 2** - Navigate to the repository

`cd /usr/src/kodekloudrepos/media`

**Step 3** - Merge feature branch into master

Ensure master is up to date:
```
git checkout master
git pull origin master
```

Merge feature branch:

`git merge feature`

**Step 4** - Create the post-update hook in the bare repo

```
cd /opt/media.git/hooks
printf '%s\n' '#!/usr/bin/env bash
set -euo pipefail

DATE=$(date +%F)
TAG="release-$DATE"

# Only when master was updated
for ref in "$@"; do
  if [ "$ref" = "refs/heads/master" ]; then
    NEWREV=$(git rev-parse refs/heads/master)
    if git rev-parse -q --verify "refs/tags/$TAG" >/dev/null; then
      echo "Tag $TAG already exists; skipping."
    else
      git tag "$TAG" "$NEWREV"
      echo "Created tag: $TAG at $NEWREV"
    fi
  fi
done

# Keep server info updated
exec git update-server-info
' | tee post-update >/dev/null

chmod +x post-update
```

**Step 5** - Test the hook (MANDATORY)

Make a small test commit on master:
```
cd /usr/src/kodekloudrepos/media
git checkout master
echo "release test" >> test.txt
git add test.txt
git commit -m "Test release hook"
```

Push to master:

`git push origin master`

**Step 6** - Verify the tag exists in the bare repo (origin)

On the working clone :  

`git ls-remote --tags origin | grep "release-$(date +%F)" || echo "Tag not found yet"`

Or inspect directly in the bare repo : 
```
cd /opt/news.git
git tag | grep "release-$(date +%F)"
git show "release-$(date +%F)" --no-patch --pretty=oneline
```

---