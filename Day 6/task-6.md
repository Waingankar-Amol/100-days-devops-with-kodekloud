# Day 6
##### Task : The Nautilus system admins team has prepared scripts to automate several day-to-day tasks. They want them to be deployed on all app servers in Stratos DC on a set schedule. Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below:

- Install cronie package on all Nautilus app servers and start crond service.
- Add a cron */5 * * * * echo hello > /tmp/cron_text for root user.

**Step A** — Install cronie and start crond service

Install cronie:

```sudo yum install -y cronie```

Start & enable crond service:

```sudo systemctl start crond```

```sudo systemctl enable crond```

**Step B** — Add the cron job for root

The cron must be added to root’s crontab, and it must be exactly this line:

*/5 * * * * echo hello > /tmp/cron_text

Add to root crontab:

```sudo crontab -e```

Add this line:

```*/5 * * * * echo hello > /tmp/cron_text```

Save & exit.