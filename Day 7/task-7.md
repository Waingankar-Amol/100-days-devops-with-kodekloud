# Day 7
##### Task : The system admins team of xFusionCorp Industries has set up some scripts on jump host that run on regular intervals and perform operations on all app servers in Stratos Datacenter. To make these scripts work properly we need to make sure the thor user on jump host has password-less SSH access to all app servers through their respective sudo users (i.e tony for app server 1). Based on the requirements, perform the following:
- Set up a password-less authentication from user thor on jump host to all app servers through their respective sudo users.

**STEP 1** — Login to jump host as thor

You are already normally logged in as thor in the lab.

**STEP 2** — Generate SSH key on jump host for user thor

Run:

`ssh-keygen -t rsa`

Press Enter for all prompts (no passphrase).

This creates:

```
~/.ssh/id_rsa
~/.ssh/id_rsa.pub
```

**STEP 3** — Copy thor’s public key to each app server’s sudo user
App Server 1 (user: tony)
`ssh-copy-id tony@stapp01`

If you get a fingerprint prompt → type yes.

Enter tony’s password when asked (Stratos DC default):

App Server 2 (user: steve)
`ssh-copy-id steve@stapp02`

App Server 3 (user: banner)
`ssh-copy-id banner@stapp03`


Very Important: Lab expects login via

thor → tony@stapp01

thor → steve@stapp02

thor → banner@stapp03


**STEP 4** — Test password-less login

From jump host (as thor), test each one:
```
ssh tony@stapp01

ssh steve@stapp02

ssh banner@stapp03
```