# Day 5
##### Task : Following a security audit, the xFusionCorp Industries security team has opted to enhance application and server security with SELinux. To initiate testing, the following requirements have been established for App server 1 in the Stratos Datacenter:
- Install the required SELinux packages.
- Permanently disable SELinux for the time being; it will be re-enabled after necessary configuration changes.
- No need to reboot the server, as a scheduled maintenance reboot is already planned for tonight.
- Disregard the current status of SELinux via the command line; the final status after the reboot should be disabled.

**Step 1** — Install required SELinux packages

On App Server 1, run:

```sudo yum install -y selinux-policy selinux-policy-targeted```

**Step 2** — Permanently disable SELinux

You must edit the SELinux configuration file.

Open the SELinux config:

```sudo vi /etc/selinux/config```

Set the following value:

```SELINUX=disabled```

Save and exit.