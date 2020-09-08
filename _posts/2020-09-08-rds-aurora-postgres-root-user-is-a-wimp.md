---
layout: post
title: "RDS Aurora Postgres root user is a wimp"
date: 2020-09-08 00:21:00 +0100
categories: tech
tags: postgres rds aurora aws database devops sysadmin
---

One of the better named tickets I've had the pleasure to work with this season, the "RDS Aurora Postgres root user is a wimp" issue turned out to be quite a challenge. Since resources on the topic online seem scarce to say the least I thought I'd note them down for if not others, at least myself should I need to remind myself about this in the future. The original issue was this - doing a routine database maintainenace task some days before I found myself having to delete a few rows in one of the databases created in the AWS Aurora Postgres cluster. As the cluster is shared by many teams and products the provisioning of each database follows a quite traditional pattern. A user notifies the platform/database team who runs a script to setup the database and user, stores the credentials somewhere safe and then notifies the user who ordered it. This script is run as the root user of the cluster, and that user is the only one allowed access across databases. So when assigned the task of deleting a few misplaced rows in one these databases, this was naturally done as the root user. Here's where the problems starts:

```shell
postgres=> \c example
You are now connected to database "example" as user "root".
example=> DELETE FROM sometable WHERE somedata = 'shouldnotbehere';
ERROR:  permission denied for relation sometable
```

OK, so that's unusual. Logging in as the root user would mean "anything goes" in pretty much any system I've worked with, so what's going on here? Turns out that the RDS Aurora clusters have a somewhat different idea on that. Since "anything goes" includes things such as configuring (and possibly breaking) replication - and this is a managed product after all - the root user has been severly limited in what it can do. Checking the available roles with `\du` confirms this:

```shell
                                                                  List of roles
       Role name       |                         Attributes                         |                          Member of
-----------------------+------------------------------------------------------------+-------------------------------------------------------------
 rds_superuser         | Cannot login                                               | {pg_monitor,pg_signal_backend,rds_replication,rds_password}
 rdsadmin              | Superuser, Create role, Create DB, Replication, Bypass RLS+| {}
                       | Password valid until infinity                              |
 root                  | Create role, Create DB                                    +| {rds_superuser}
                       | Password valid until infinity                              |
```
Good news first - at least we can use the `root` role to login! The only attributes assigned to the role however is `Create role` and `Create DB`. Alright, I suppose we can live with that. What doesn't really follow though is how the same root user is unable to modify, or even read, database resources itself created. Looking at the database and user creation script it all looked pretty standard. As the root user something like the below got executed:

```sql
CREATE DATABASE example
CREATE USER someuser WITH ENCRYPTED PASSWORD 'somepassword'
GRANT ALL PRIVILEGES ON DATABASE example TO someuser
```

Surely the root user creating both the user and database here would be granted access to the very same resource? Turns out, well yes _and_ no. The root user has access to the database, and may list tables, etc. It is however **not** allowed acceess to resources later created by the `someuser` user in the `example` database, even if it created both of them. Trying to grant these privileges to the root user, _as_ the root user also turned out to be pointless - the root user would still be denied access. Only by logging in as the user just created, and having _that_ user grant table level privileges to the root account would allow the root user subsequent access to the tables there:

```sql
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO root
ALTER DEFAULT PRIVILEGES FOR USER someuser IN SCHEMA public GRANT ALL ON example TO root
```

The last `ALTER` statement is crucial - granting privileges in postgres only applies to existing resources, not those created at some point in the future. So unless you want to repeat the process every now and then you'll need to ensure that the default privileges are altered as well. Running this procedure for the database in need of maintenance and updating the user and database provisioning scripts means the problem is solved for now and the ticket could be closed. The root (hah!) of the problem however remains - the AWS Aurora Postgres root user is still a wimp!
