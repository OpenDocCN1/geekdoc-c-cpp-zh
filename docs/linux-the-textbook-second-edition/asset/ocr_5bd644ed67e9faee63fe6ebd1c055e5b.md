Also, as previously stated, the user must know a valid username/password pair on the remote server system to be able to log in to the remote system!

We show three possible methods that can be used in this dialog. First, if the user has previously already logged into the host successfully from the client before, and the authentication keys have not changed. Second, if the user has never logged into the host successfully before from the client. Third, if the user has logged into the host before, but the authentication key on the host has changed since the last successful login. These are practical situations one might encounter any time you use this remote login method.

# 2.3.3.1 Login and Logout Procedures

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
The authenticity of host '192.168.0.8 (192.168.0.8)' can't be established. ECDSA key fingerprint is SHA256:uZpqi4UGuBN5SOBVFRbqbl5HspmV3eZAw/nUvPBTS5I.
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
```