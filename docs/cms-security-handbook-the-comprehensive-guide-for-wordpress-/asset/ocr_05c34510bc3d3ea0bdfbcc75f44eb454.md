# Shadow Password File

A shadow password file stores the encrypted password (technically it's encoded, not encrypted) for users. This file can only be read by the root user, which prevents the dictionary attack from being successful.

The original implementation was built in 1987, after its author experienced a cyber break-in on a SCO XENIX operating system. It was ported over the years to various distributions of UNIX and Linux.

This software is meant to store the passwords and not allow them to be stored in the passwd file. After a password is shadowed, then you'll typically see an x or an * in the password field.

Use the following command to scan your system and ensure that all the passwords themselves are in the shadow file and not in passwd:

```
# awk -F: '($2 != "x") {print}' /etc/passwd
```

When you run this command, it should not return any results. You should take the corrective action of manually removing passwords that appear in this file. The hashes for all user account passwords should be stored in the file /etc/shadow and never in /etc/passwd. The passwd file is readable by all users. If you find a user with a password (hash) showing in the results of this command, then removing and re-creating that user may be best.

For the most part, you should not log in as root. You should log in as a normal user and then elevate your privileges to the root or super user. With that practice in mind, you want to ensure that root (the user) is the only user in the system with root privileges. To do this, issue the following command:

```
# awk -F: '($3 == "0") {print}' /etc/passwd
```

This command should only return one account, as follows:

```
root:x:0:0:root:/root:/bin/bash
```

If you note other users in this output, lower their administrative privileges.

# Expiring Passwords

In terms of managing security for your passwords, changing your passwords on a regular basis is a good practice. The frequency is solely your call, but a good frequency is every 30 to 60 days.

With Linux, you can set passwords to automatically expire. Doing so forces users to change their passwords.

With your information security policy, define the time limit and complexity for passwords. After you do, change them by following a simple process.