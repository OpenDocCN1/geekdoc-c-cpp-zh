The commands passwd and sudo are SUID-capable programs. Even though these commands are ostensibly run with root user privelege, a nonprivileged user can only change their own password with the passwd command, and can only assume root privileges with sudo. That is, if they are given privelege to do so in the /etc/sudoers file.

The find command allows you to search your system to see if there are any hidden or otherwise inappropriate SUID and SGID commands on your system. Here is an example:

```
$ sudo find / -perm /6000 -ls
2104368  4 drwxrwsr-x  2 root  mail  4096 Jun 28  2016 /var/mail
2104383  4 drwxr-sr-x  30 man  root  4096 Dec 25 07:41 /var/cache/man
2235989  4 drwxr-sr-x  2 man  root  4096 Dec 25 07:41 /var/cache/man/tr
2104517  4 drwxr-sr-x  2 man  root  4096 Dec 25 07:41 /var/cache/man/ja
2104518  4 drwxr-sr-x  2 man  root  4096 Dec 25 07:41 /var/cache/man/ko
3300204  4 drwxr-sr-x  2 man  root  4096 Dec 25 07:41 /var/cache/man/ro
2104520  4 drwxr-sr-x  2 man  root  4096 Dec 25 07:41 /var/cache/man/p1
2104519  4 drwxr-sr-x  2 man  root  4096 Dec 25 07:41 /var/cache/man/n1
Output truncated...
```

The find command reveals SetUID and SetGID commands that unprivileged users can run to assume the privileged role.

# Exercise 17.54

Use the find command to list any hidden or inappropriate SUID and SGID commands on your Linux system.

# 17.9.7 Disk Encryption

When the ordinary user is considering disk encryption for security, the critical determination to make is the scope of encryption she wants to implement. For example, she can encrypt the entire system disk she is installing Linux on at the time she installs the system. Or she can do a postinstallation encryption of an entire disk, selected partitions, selected directories, or individual files. What governs the scope of encryption is up to the user, and depends a great deal on the particular use case. It is critical to know why you want to do encryption when considering all of the possible strategies of encrypting your persistent media.

In Chapter W26, Sections 9.7.2, titled “Whole Disk Encryption at Installation,” through 9.7.5, titled “Encrypting a USB Thumb Drive,” at the book website, we detail a large-scope encryption strategy. In those sections, we show how to encrypt the entire system disk at installation of Linux Mint and also an entire single partition on a USB thumb drive. We also cover a smaller-scope encryption strategy of encrypting a directory and a particular important file in your home directory in those sections.

# 17.9.7.1 The Meaning of Encryption

Encryption uses a very developed science, known as cryptography, to implement data hiding.

Cryptography is used on a Linux system to encode data to hide it from unprivileged users, and then decrypt, or decode the data for privileged users. On a Linux system, the following are some of the objects that can be possible targets for encryption:

+   - Individual files
+   - Volumes or individual partitions
+   - Web page connections
+   - Network connections
+   - Backup file objects on additional hard disks or other media
+   - Compressed directories or files