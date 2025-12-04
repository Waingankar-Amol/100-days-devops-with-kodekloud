# Day 17
##### Task: The Nautilus application development team has shared that they are planning to deploy one newly developed application on Nautilus infra in Stratos DC. The application uses PostgreSQL database, so as a pre-requisite we need to set up PostgreSQL database server as per requirements shared below:

PostgreSQL database server is already installed on the Nautilus database server.


a. Create a database user kodekloud_sam and set its password to GyQkFRVNr3.


b. Create a database kodekloud_db7 and grant full permissions to user kodekloud_sam on this database.


Note: Please do not try to restart PostgreSQL server service.

---
 **Step 1** — SSH into the Database Server

From the jump host:

`ssh peter@stdb01`

**Step 2** — Switch to the postgres system user

PostgreSQL administrative commands must be executed as the postgres Linux user:

`sudo su - postgres`

 **Step 3** — Create the PostgreSQL user

Use PostgreSQL CLI (psql) to create the user:

`psql -c "CREATE USER kodekloud_sam WITH PASSWORD 'GyQkFRVNr3';"`

**Step 4** — Create the database

`psql -c "CREATE DATABASE kodekloud_db7;"`

**Step 5** — Grant full permissions to user

`psql -c "GRANT ALL PRIVILEGES ON DATABASE kodekloud_db7 TO kodekloud_sam;"`

**Done** — No restart required