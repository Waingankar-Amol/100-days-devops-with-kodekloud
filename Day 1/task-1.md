# Day 1
#### Task : Create a user named james with a non-interactive shell on App Server 1.

``` sudo useradd -s /usr/sbin/nologin james ```

#### Explanation

- `useradd` → Creates the user

- `-s /usr/sbin/nologin` → Assigns a non-interactive shell, preventing login

- `james` → Username