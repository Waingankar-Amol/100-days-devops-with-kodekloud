# Day 6
##### Task : There is a critical issue going on with the Nautilus application in Stratos DC. The production support team identified that the application is unable to connect to the database. After digging into the issue, the team found that mariadb service is down on the database server.
- Look into the issue and fix the same.

MariaDB Service Failure – Root Cause & Permanent Fix
Task	Solution
MariaDB fails to start because it cannot create its PID directory under /run (a tmpfs). A persistent tmpfiles rule, correct ownership, and proper SELinux context are required to ensure MariaDB starts and remains enabled.	Detailed root cause analysis, permanent fix script, application steps, and verification procedures are provided below.

**Step 1** - Root Cause Analysis

The directory /run (or /var/run) resides on tmpfs, meaning it is wiped clean on every reboot.

MariaDB requires the directory /run/mariadb — owned by mysql:mysql — to store its PID file.

If the directory is missing, incorrectly owned, or has the wrong SELinux context, MariaDB cannot create its PID file.

As a result, mariadb.service fails immediately upon startup.

**Step 2** - Permanent Fix Script

Save the following script as fix_mariadb.sh and execute it with elevated privileges:

```
#!/bin/bash
# Permanent fix for MariaDB PID directory issues
# Compatible with RHEL, CentOS, Fedora and similar distributions

set -e

echo "=== Step 1: Create /run/mariadb directory ==="
sudo mkdir -p /run/mariadb
sudo chown mysql:mysql /run/mariadb
sudo chmod 0755 /run/mariadb

echo "=== Step 2: Fix SELinux context (if enabled) ==="
if command -v getenforce &>/dev/null && [ "$(getenforce)" != "Disabled" ]; then
    if ! command -v semanage &>/dev/null; then
        echo "Installing semanage tool..."
        sudo dnf install -y policycoreutils-python-utils || sudo yum install -y policycoreutils-python
    fi
    sudo semanage fcontext -a -t mysqld_var_run_t "/run/mariadb(/.*)?"
    sudo restorecon -Rv /run/mariadb
fi

echo "=== Step 3: Create systemd-tmpfiles rule for persistence ==="
sudo bash -c 'cat > /etc/tmpfiles.d/mariadb.conf <<EOF
d /run/mariadb 0755 mysql mysql -
EOF'
sudo systemd-tmpfiles --create /etc/tmpfiles.d/mariadb.conf

echo "=== Step 4: Reload systemd and enable MariaDB ==="
sudo systemctl daemon-reexec
sudo systemctl enable --now mariadb

echo "=== Step 5: Verify MariaDB service status ==="
sudo systemctl status mariadb --no-pager
```
**Step 3** - How to Apply the Fix

Create, save, and execute the script

`vi fix_mariadb.sh`      # Paste the script

`chmod +x fix_mariadb.sh`

`./fix_mariadb.sh`


**Step 4** - What the Script Does

Creates the /run/mariadb directory with correct ownership and permissions.

Applies SELinux context (mysqld_var_run_t) if SELinux is enabled.

Adds a systemd-tmpfiles rule so the directory is automatically recreated on every reboot.

Reloads systemd, enables MariaDB, and starts the service immediately.

Verifies that MariaDB is running successfully.