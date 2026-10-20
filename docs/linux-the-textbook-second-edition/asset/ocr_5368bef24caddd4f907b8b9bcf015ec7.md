Debian—As root, use the following command:

```
[root@debian] # apt-get install sudo
```

Then give yourself, or a designated user, sudo privilege, using the following command:

```
[root@debian] # visudo
```

Your default text editor will then open (nano on our Debian 9.1 system), and you will be able to enter the following line into the section entitled “# User privilege specification” of the sudoers file:

```
username            ALL=(ALL:ALL)       ALL
```

where username is the username you want to give blanket sudo privilege to.

Save the file and exit the editor.

Ubuntu—As of the time of the writing of this book, sudo was already installed, and the default user was in the sudoers group. This can be checked with the command id -Gn

Linux Mint—As of the time of the writing of this book, sudo was already installed, and the default user was in the sudoers group. This can be checked with the command id -Gn

For CentOS Installation

As of the time of the writing of this book, sudo was already installed, but as root, you must give yourself (or a designated user) sudo privilege. To give yourself, or a designated user, sudo privilege, use the following command:

```
[root@centos] # visudo
```

Your default text editor will then open, and you will be able to enter the following line into the section titled “# User privilege specification” of the sudoers file:

```
username            ALL=(ALL:ALL)       ALL
```

where username is the username you want to give blanket sudo privilege to.

Save the file, and exit the editor.