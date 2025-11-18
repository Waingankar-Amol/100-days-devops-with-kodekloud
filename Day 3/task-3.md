# Day 3
##### Task : Following security audits, the xFusionCorp Industries security team has rolled out new protocols, including the restriction of direct root SSH login. Your task is to disable direct SSH root login on all app servers within the Stratos Datacenter.

To disable direct SSH root login on all App Servers in the Stratos Datacenter, follow the steps below on each App Server (App Server 1, App Server 2, App Server 3).

**Step 1** : Open the SSH Configuration file. 

``` sudo vi /etc/ssh/sshd_config ```

**Step 2** : Find the line

```#PermitRootLogin yes``` or ```PermitRootLogin yes```

**Step 3** : Change it to:

```PermitRootLogin no```

**Step 4** : Restart SSH service

```sudo systemctl restart sshd```