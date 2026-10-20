
```
local: kernel.txz remote: kernel.txz
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for kernel.txz (32255748 bytes).
226 Transfer complete.
32255748 bytes received in 295.89 secs (106.4592 kB/s)
ftp> ls
kernel.txz
ftp> quit
421 Timeout.
$
```

Once you have established an ftp connection, most sites put you in binary mode so that you can transfer non-ASCII files, such as files containing audio and video clips. You can explicitly put the ftp session into binary mode by using the binary command, which ensures proper file transfer. You can revert to ASCII mode by using the ascii command.

In the following in-chapter exercise, you will use the ftp command to transfer a file from a remote host on the Internet.

## Exercise 11.14

Establish an anonymous ftp session with the host **ftp.FreeBSD.org** and transfer all the files related to the latest release of the software, using the techniques of the earlier command line session. Ftp-transfer them into your system by using the mget command.

## 11.8.5 SSH and Related Commands

The BSD-originated r commands (rsh, rcp, rlogin, r utime, etc. and not available in Linux) operate on *plaintext* (also called *cleartext*) and are insecure, as is telnet. SSH is a modern substitute for them that eliminates the need for the **.rhosts** and **hosts.equiv** files and can authenticate users by cryptographic key. It also increases the security of other TCP/IP-based applications, such as X Windows *forwarding*, which transparently “tunnels” them via SSH-encrypted connections. The program that handles the secure connection protocol is known as the SSH daemon, sshd.

The ssh protocol uses strong cryptography for transmitting data, including commands, command outputs, passwords, and files. Whenever your data is transmitted to your network, ssh automatically encrypts it and automatically decrypts it when the data reaches its intended recipient. The result is *transparent encryption*—that is, the sender and receiver are unaware of the encryption/decryption process.

For these reasons, ssh has become a de facto standard for secure terminal connections within a LAN or the Internet. The encrypted sessions used by ssh, scp, and sftp, for example, prevent anyone from making sense of the ongoing communication while *packet sniffing* it. Also, authentication methods used in ssh prevent any kind of *spoofing*, such as IP address spoofing.

SSH Version 2 is the default protocol. It has three components:

+   1. SSH Transfer Protocol: Handles server identification, encryption algorithm and key encryption, and manages the channel between client and server
+   2. SSH Authentication Protocol: Verifies the validity of the login role of user on the client machine
+   3. SSH Channel Protocol: Handles the encrypted channel and logical connection status for a remote shell session, port forwarding, or X11 forwarding

In Chapter 2, Section 2.3.3, we give details of how to log onto a Linux system using the ssh command, the client side of the SSH protocol. In that section, we also describe some of the possible ways of interacting with an sshd (SSH Daemon) service on a remote system. The following subsections assume that the ssh service is installed and enabled on your host (i.e., the client machine), and the sshd daemon is running on the remote server host machine.

### 11.8.5.1 Remote Login with ssh

Most Linux systems support two commands that allow you to log on to a remote host. They are telnet and ssh, both based on the Internet services for remote login. When you use telnet, commands and data

travel in plaintext on the transmission channel and may be sniffed as it travels. For this reason, telnet is hardly ever used for remote login these days, and we do not discuss it in the book. In case of ssh, commands and data travel through encrypted channels.

The ssh command allows you to basically perform the same tasks that you can perform with the telnet, rlogin, and rsh commands, but in a more secure manner. You are allowed to log in to the remote host or execute a command on it if the ssh server (sshd) is running on the remote machine and your machine is listed in /etc/hosts.equiv or /etc/ssh/shosts.equiv on the server machine, and the user name is the same on the two machines. Alternatively, a user is considered for login if the files ~/.rhosts or ~/.shosts exist in the user’s home directory on the server machine and include a line containing the name of the client machine and the name of the user on that machine. Additional security features are used by ssh, including public-key cryptography, to authenticate a user and its host before allowing the user to log in to the remote machine. Particularly, the server must be able to verify the client’s host key in ~/.ssh/known_hosts before permitting login. This file contains server’s domain name and/or IP address and its public key. You can run the more ~/.ssh/known_hosts command on your client machine to see what this file contains. It is created when you run the ssh user@domain_name or ssh user@IP_address for the first time.

We describe only some of the rather basic features of the ssh command that are needed for remote login, remote execution of commands, and file transfer between your client and the server machines. Here is a brief description of the ssh command:

# Syntax:

```
ssh [-option(s)] [-option argument(s)] [user@]hostname [command]
```

Purpose: ssh (SSH client) is a program for logging into a remote machine and for executing commands on a remote machine. It is intended to replace rlogin and rsh, and provide secure encrypted communications between two untrusted hosts over an insecure network

Output: A remote connection over a secure channel to a host on a network or the Internet

# Commonly used options/features:

+   -D [bind_address:]port
+   Specify a local “dynamic” application-level port forwarding. This works by allocating a socket to listen to the port on the local side, optionally bound to the specified bind_address.
+   -L [bind_address:]port:host:hostport
+   Specify that the given port on the local (client) host is to be forwarded to the given host and port on the remote side.
+   -C
+   Request on all data. The compression algorithm is the same as used by the gzip command.
+   -l login_name
+   Specify the user to log in as on the remote machine. This also may be specified on a per-host basis in the configuration file.
+   -o option
+   Specify options for which there is no explicit option/flag, using the format given in the configuration file.
+   -p port
+   Specify the ports to connect to if the sshd is not running on the well-known port (22).

In the following session, we start an ssh session on a remote host running the SSH server named 192.168.0.12, using the default username (which in this case is the same username you have on the local client machine), execute shell commands, and log out of the remote host. The remote machine happens to be an OpenIndiana UNIX machine that has never had an ssh connection made to it from this client, i.e., your host.

```
$ ssh 192.168.0.12
The authenticity of host '192.168.0.12 (192.168.0.12)' can't be established.
RSA key fingerprint is 37:a2:db:ce:97:17:ce:37:26:bf:58:9d:a2:ed:1c:0f.
No matching host key fingerprint found in DNS.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.0.12' (RSA) to the list of known hosts.
Password: xxxxxx
Last login: Tue Sep 23 08:51:38 2014
OpenIndiana (powered by illumos)    SunOS 5.11    oi_151a9    November 2013
$
...
[ Execute command line commands ]
...
$ <Ctrl+D>
Connection to 192.168.0.12 closed.
$
```

Notice that since this session is the first ssh connection from the local client to the remote server host, an exchange of authentication keys is necessary. On every subsequent connection, the key exchange is not necessary if the keys have not been changed.

Using the following command, you log in to a host 202.147.169.195 (an ssh server running Linux Mint18 4.4.0) with username sarwar, use the uname -a command to display the machine information of the server-side machine (which is running Linux Mint18 4.4.0), log out, and use the uname -a command on the client machine (which is running Darwin 10.8.0) to display information of the client-side machine. Note that there is no exchange of authentication keys in this particular session, because this is not the first ssh connection between the client and server machines.

```
$ ssh -l sarwar 202.147.169.195
sarwar@202.147.169.195's password: xxxxxxx
Welcome to Linux Mint 18 Sarah (GNU/Linux 4.4.0-21-generic x86_64)

* Documentation: https://www.linuxmint.com
Last login: Fri Oct 27 13:56:47 2017 from 119.160.96.60
$ uname -a
Linux Mint18 4.4.0-21-generic #37-Ubuntu SMP Mon Apr 18 18:33:37 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux
$
...
[ Your use of the remote Linux machine using the command line interface ]
...
$ <Ctrl+D>
Connection to 202.147.169.195 closed.
$ uname -a
Darwin Sarwars-MacBook-Pro.local 10.8.0 Darwin Kernel Version 10.8.0: Tue Jun 7 16:32:41 PDT 2011; root:xnu-1504.15.3~1/RELEASE_X86_64 x86_64
$
```

Following is a somewhat atypical, but nonetheless important and very instructive ssh log-in session, ended by a graceful logout and termination of the ssh channel. It is done between a Linux Mint client (192.168.0.13) and a Linux Mint host (192.168.0.8), where sshd has already been installed on the host system. This example illustrates the use of known hosts concept of ssh. Known hosts are established so that the client and server authenticate each other to make a secure connection between the two. When you connect to any host for the first time, a public counterpart of the host key is stored on the client. The known host concept prevents what is known as man-in-the-middle attacks.

After the first failed attempt to establish an ssh connection, an error message indicates that the authentication key has changed on the host. This could have happened for any number of reasons, including something you yourself did, rather than some attacker. Therefore, in our scenario that follows, a removal of the offending key in the file /home/bob/.ssh/known_hosts on the client machine is done by deleting that file. Then a new key is generated when you make another attempt to ssh into the host from the client, an exchange can
