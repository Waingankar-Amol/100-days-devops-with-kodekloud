# Day 2
#### Task : Create a user named ravi on App Server 2 in Stratos Datacenter. Set the expiry date to 2024-03-28, ensuring the user is created in lowercase as per standard protocol.


``` sudo useradd -e 2024-03-28 ravi  ```

#### Explanation

- `-e 2024-03-28` → Sets the account expiry date

- `ravi` → Username (lowercase, as required)