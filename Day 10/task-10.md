# Day 10
##### Task :  The production support team of xFusionCorp Industries is working on developing some bash scripts to automate different day to day tasks. One is to create a bash script for taking websites backup. They have a static website running on App Server 2 in Stratos Datacenter, and they need to create a bash script named media_backup.sh which should accomplish the following tasks. (Also remember to place the script under /scripts directory on App Server 2).



a. Create a zip archive named xfusioncorp_media.zip of /var/www/html/media directory.

b. Save the archive in /backup/ on App Server 2. This is a temporary storage, as backups from this location will be clean on weekly basis. Therefore, we also need to save this backup archive on Nautilus Backup Server.

c. Copy the created archive to Nautilus Backup Server server in /backup/ location.

d. Please make sure script won't ask for password while copying the archive file. Additionally, the respective server user (for example, tony in case of App Server 1) must be able to run it.

e. Do not use sudo inside the script.

Note:
The zip package must be installed on given App Server before executing the script. This package is essential for creating the zip archive of the website files. Install it manually outside the script.



**Step 1** - create a script with name `media_backup.sh` under path `/scripts`
```
#!/bin/bash
# media_backup.sh
# Creates /backup/xfusioncorp_media.zip from /var/www/html/media
# Copies the archive to remote backup server. (No sudo used)

set -euo pipefail

# ---------- Configuration (edit these to match your environment) ----------
SRC_DIR="/var/www/html/media"
LOCAL_BACKUP_DIR="/backup"
ARCHIVE_NAME="xfusioncorp_media.zip"           # exact required name
REMOTE_USER="backupuser"                       # <-- replace with actual remote user (eg. 'tony' style user)
REMOTE_HOST="nautilus-backup.example.com"      # <-- replace with actual backup server hostname/IP
REMOTE_DIR="/backup"
# -------------------------------------------------------------------------

# Basic checks
if [ ! -d "$SRC_DIR" ]; then
  echo "ERROR: Source directory $SRC_DIR does not exist." >&2
  exit 2
fi

# Ensure local backup dir exists (no sudo)
mkdir -p -- "$LOCAL_BACKUP_DIR"

# Create archive (create in /tmp first to avoid partial files in /backup)
TMP_ARCHIVE="/tmp/${ARCHIVE_NAME}"
if command -v zip >/dev/null 2>&1; then
  echo "Creating zip archive..."
  # create zip of the media directory - inside /tmp so move later
  ( cd "$(dirname "$SRC_DIR")" && zip -r "$TMP_ARCHIVE" "$(basename "$SRC_DIR")" ) >/dev/null
else
  echo "ERROR: zip command not found. Install 'zip' package before running this script." >&2
  exit 3
fi

# Move to local backup location (overwrite if exists)
mv -f -- "$TMP_ARCHIVE" "${LOCAL_BACKUP_DIR}/${ARCHIVE_NAME}"

# Copy to remote backup server (expects passwordless SSH)
echo "Copying ${LOCAL_BACKUP_DIR}/${ARCHIVE_NAME} to ${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_DIR}/"
scp -q "${LOCAL_BACKUP_DIR}/${ARCHIVE_NAME}" "${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_DIR}/"

echo "Backup completed successfully: ${LOCAL_BACKUP_DIR}/${ARCHIVE_NAME} and copied to ${REMOTE_HOST}:${REMOTE_DIR}/"
exit 0
```
**Step 2** - Now setup password-less authentication between App2 server and Backup Server

On App 2 server run following commands: 

cd /home/steve/
ssh-keygen -t rsa
This creates:

```
~/.ssh/id_rsa
~/.ssh/id_rsa.pub
```

**STEP 3** — Copy steve’s public key to backup server’s user clint.
App Server 1 (user: steve)
`ssh-copy-id clint@stbkp01`

If you get a fingerprint prompt → type yes.

Enter clint’s password when asked (Stratos DC default):

---