

Also, as previously stated, the user must know a valid username/password pair on the remote server system to be able to log in to the remote system!

We show three possible methods that can be used in this dialog. First, if the user has previously already logged into the host successfully from the client before, and the authentication keys have not changed. Second, if the user has never logged into the host successfully before from the client. Third, if the user has logged into the host before, but the authentication key on the host has changed since the last successful login. These are practical situations one might encounter any time you use this remote login method.

### 2.3.3.1 Login and Logout Procedures

What the user types in is shown in bold text:

Method 1. Having logged in before successfully:

```
$ ssh 192.168.0.8
bob@192.168.0.8's password: www
Welcome to Linux Mint 18.1 Serena (GNU/Linux 4.4.0-45-generic x86_64)

* Documentation: https://www.linuxmint.com
Last login: Mon Jan  9 07:25:18 2017 from 192.168.0.25
bob@bob-PowerEdge-T110 ~ $ Execute Command Line Linux Commands
bob@bob-PowerEdge-T110 ~ $ logout
Connection to 192.168.0.8 closed.
$
```

Method 2. Having never logged in before:

```
$ ssh 192.168.0.8
The authenticity of host '192.168.0.8 (192.168.0.8)' can't be established.
ECDSA key fingerprint is SHA256:uZpqi4UGuBN5SOBVFRbqbl5HspmV3eZAw/nUvPBTS5I.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.0.8' (ECDSA) to the list of known hosts.
bob@192.168.0.8's password: www
Welcome to Linux Mint 18.1 Serena (GNU/Linux 4.4.0-45-generic x86_64)

* Documentation: https://www.linuxmint.com
Last login: Sat Dec 24 16:54:10 2016 from 192.168.0.6
bob@bob-PowerEdge-T110 ~ $ Execute Command Line Linux Commands
bob@bob-PowerEdge-T110 ~ $ logout
Connection to 192.168.0.8 closed.
$
```

Method 3. Logged in before but host key has changed:

```
$ ssh 192.168.0.8
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
43:e8:cf:33:d5:ed:dd:05:d9:e9:a5:9d:d3:18:1d:2b.
Please contact your system administrator.
Add correct host key in /home/bob/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /usr/home/bob/.ssh/known_hosts:2
ECDSA host key for 192.168.0.8 has changed and you have requested strict checking.
Host key verification failed.
$ cd /home/bob/.ssh
$ rm known_hosts
$ cd
$ ssh 192.168.0.8
The authenticity of host '192.168.0.8 (192.168.0.8)' can't be established.
ECDSA key fingerprint is 43:e8:cf:33:d5:ed:dd:05:d9:e9:a5:9d:d3:18:1d:2b.
No matching host key fingerprint found in DNS.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.0.8' (ECDSA) to the list of known hosts.
bob@192.168.0.8's password: www
Last login: Sat Dec 24 16:54:10 2016 from 192.168.0.6
Output truncated...
bob@bob-PowerEdge-T110 ~ $ Execute Command Line Linux Commands
bob@bob-PowerEdge-T110 ~ $ logout
Connection to 192.168.0.8 closed.
$
```

In all of the three methods, the user is assumed to have an account with the same username, and possibly password, on both client and server systems.

In method 2, the keys are generated on host and client after the user types in yes and presses <Enter>.

In method 3, after the first failed attempt to establish an SSH connection, the error message indicates that the authentication key has changed on the host. A very helpful component of the error message is the instruction:

Add correct host key in /home/bob/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /usr/home/bob/.ssh/known_hosts:2

So a removal of the offending key in the file /home/bob/.ssh/known_hosts on the client machine is done by deleting that file. Then a new key is generated, an exchange can take place, and the login can proceed.

The line in all three methods that reads “Execute Command Line Linux Commands” is where the user types in any of the valid Linux commands we show in this chapter and throughout the rest of this book. Finally, after typing logout, the user cuts the SSH channel connection and is returned to the command line prompt of the local client system.

### In-Chapter Exercises

-   12. Use ssh to log into another machine on your LAN or intranet that can accept ssh logins as a server, and that you have access to with a username and password. Which of the earlier methods in this section did you have to deploy, on first ssh login, and on every subsequent ssh login, to that host?

-   13. Can you log into a system using ssh that is a stand-alone (or dedicated) system, and that you are already logged into? Remember that a stand-alone system can be connected to an intranet, LAN, or the Internet, but as we define it, only one user (out of a population of possibly many users) can be logged into it at any given time. Also, the assumption here is that the ssh client and server software is installed on that system. Why would you want to do this?

It is also interesting that some virtual connections, such as to Docker containers, are not configured to easily do this via a Dynamic Host Configuration Protocol (DHCP) server-assigned IP address on a LAN.

## 2.4 File Maintenance Commands and Help on Linux Command Usage

After your first-time login to a new Linux system using one of the three ways we described in the previous section, one of your first actions will be to construct and organize your workspace environment and the files that will be contained in it. The operation of organizing your files according to some logical scheme is known as file maintenance. A logical scheme used to organize your files might consist of creating bins for storing files according to the subject matter of the contents of the files or according to the dates of their creation. In the following sections, you will type file creation and maintenance commands that produce a structure as shown in Figure 2.3. Complete the operations shown in the following sections in the order they are presented, to get a better overview of what file maintenance really is. Also, it is critical that you review what was presented in Section 2.2 regarding the structure of a Linux command so that when you begin to type commands for file maintenance, you understand how the syntax of what you are typing conforms to the general syntax of any Linux command.

### 2.4.1 File and Directory Structure

When you first log in, you are working in the *home* directory, or folder, of the authorized user associated with the username and password you used to log in. Whatever directory you are presently in is known as the *current working directory*, and there is only one current working directory active at any given time. It is helpful to visualize the structure of your files and directories using a diagram. Figure 2.3 is an example of a home directory and file structure for a user named **bob**. In this figure, directories are represented as parallelograms and plain files (e.g., files that contain text or binary instructions) are represented as rectangles. A *pathname*, or path, is simply a textual way of designating the location of a directory or file in the complete file structure of the Linux system you are working on. For example, the path to the file **myfile2** in Figure 2.3 is **/home/bob/myfile2**. The designation of the path begins at the root (/) of the entire file system, descends to the folder named **home**, and then descends again to the home directory of the user named **bob**.

As shown in Figure 2.3, the files named **myfile**, **myfile2**, and **renamed_file** are stored under or in the directory **bob**. Beneath **bob** is a *subdirectory* named **first**. In the following sections, you will create these files, and the subdirectory structure, in the home directory of the username that you have logged into your Linux system with.

### In-Chapter Exercise

-   14. Type the following two commands on your Linux system:

    ```bash
    $ cd /
    $ ls
    ```

![](img/2a18e06cd9c6395e451f26126ecba1fd_55_0.png)

**FIGURE 2.3** Example directory structure.

