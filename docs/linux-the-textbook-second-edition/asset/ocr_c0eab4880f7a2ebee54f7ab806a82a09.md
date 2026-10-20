The examples in this section illustrate

+   - simple cases of text-based user account creation and configuration,
+   - text-based group creation and configuration, and
+   - text-based deletion of a user account and a group.

# Exercise 17.5

Make a table or chart of what users and groups need to be added to your system, and what their default account parameters and group memberships should be. What command can you use to identify all existing groups on the system?

# 17.3.1 Adding a User and Group in a Text-Based Interface on Linux

The commands adduser and addgroup, by default, add a “normal” (non-system level) user or group to the system using command line options and option arguments. They take default configuration information from /etc/adduser.conf. They are a more developed front-end for the older, low-level commands, such as useradd, groupadd, and usermod. adduser utilizes patented user ID (UID) and group ID (GID) values for creation of new accounts and groups, and by default creates a home directory from a skeletal configuration file, etc.

adduser itself is a script file that interfaces to the following commands and their functionality:

```
useradd, groupadd, passwd, gpasswd, usermod, chfn, chage, edquota.
```

An abbreviated listing of the syntax of the adduser and addgroup commands is as follows:

**adduser, addgroup** - add a user or group to the system

```
Syntax:
adduser [options] [--home DIR] [--shell SHELL] [--no-create-home] [--uid ID] [--firstuid ID] [--lastuid ID] [--ingroup GROUP | --gid ID] [--disabled-password] [--disabled-login] [--gecos GECOS] [--add_extra_groups] [--encrypt-home] user

adduser --system [options] [--home DIR] [--shell SHELL] [--no-create-home] [--uid ID] [--group | --ingroup GROUP | --gid ID] [--disabled-password] [--disabled-login] [--gecos GECOS] user

addgroup [options] [--gid ID] group

addgroup --system [options] [--gid ID] group

adduser [options] user group
```

**Purpose:** adduser and addgroup add users and groups to the system according to command line options and configuration information in /etc/adduser.conf. They are friendlier front ends to the low-level tools like useradd, groupadd, and usermod programs, by default choosing Debian policy conformant UID and GID values, creating a home directory with skeletal configuration, running a custom script, and other features. adduser and addgroup can be run in one of five modes

**Output:** New or modified user accounts or groups

# **Commonly used options/features:**

+   [--quiet]
+   [--debug]
+   [--force-badname]
+   [--help|-h]
+   [--version]
+   [--conf FILE]