# Day 6
##### Task : During the weekly meeting, the Nautilus DevOps team discussed about the automation and configuration management solutions that they want to implement. While considering several options, the team has decided to go with Ansible for now due to its simple setup and minimal pre-requisites. The team wanted to start testing using Ansible, so they have decided to use jump host as an Ansible controller to test different kind of tasks on rest of the servers.

- Install ansible version 4.8.0 on Jump host using pip3 only. Make sure Ansible binary is available globally on this system, i.e all users on this system are able to run Ansible commands.

 **Step 1** — Make sure pip3 is installed

On Jump Host (as thor or root):

`sudo yum install -y python3-pip`

 **Step 2** — Install Ansible 4.8.0 using pip3

The lab requires exact version 4.8.0, so run:

`sudo pip3 install ansible==4.8.0`


This installs Ansible for the system Python, making it available system-wide.

 **Step 3** — Ensure the Ansible binary is globally available

pip3 installs binaries under:

`/usr/local/bin/`


This folder is already part of the global $PATH.

Verify:

`ls -l /usr/local/bin/ansible`

 **Step 4** — Confirm Ansible version

Run:

`ansible --version`