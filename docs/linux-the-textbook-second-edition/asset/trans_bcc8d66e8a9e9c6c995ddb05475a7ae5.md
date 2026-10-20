

name or IP address of the host on which the server runs as an argument in the command. Some commands also allow port number as an argument. Client software that has such flexibility built in is known as a fully parameterized client. Such clients are important in terms of the flexibility they offer. They also allow testing of updated server software by running it on a port that is not well known and contacting it with the client. A telnet client, discussed in Section 11.8, is a good example of a fully parameterized client.

## 11.8 Application Software

Numerous programs that implement the application-level protocols just discussed are available on networks of Linux hosts. Of the most commonly used applications described here, some are available on Linux and Linux-based systems only, whereas others are available to all the hosts on the Internet.

### 11.8.1 Displaying the Host Name

Network-based applications use the `user@host` address format to identify a user on a network on the Internet. You can use the `hostname` and `uname` commands to display the name of the host you are logged on to. On some systems, the host name is shown in the short, simple name format, and on others it is displayed in the long, FQDN format. If you have to identify the host on the network that you are logged on to, you can use the `hostname -s` command to display the short format, which is simply the name of the host (the leftmost string in the FQDN format). You can use the `uname -n` command to display the host name of the computer that you are logged on to in the FQDN format. The `uname -a` command displays complete information about a host, including the operating system it is running and the name of the CPU. The following are some examples of the `hostname` and `uname` commands.

```
$ hostname
Mint18
$ uname -n
Mint18
$ uname -a
Linux Mint18 4.4.0-21-generic #37-Ubuntu SMP Mon Apr 18 18:33:37 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux
$
```

You can use the `arch` command to print the processor architecture name. This command outputs the same information as does `uname -m`, as can be seen in the following session.

```
$ arch
x86_64
$ uname -m
x86_64
$
```

### Exercise 11.9

Ask your friends and fellow students about the two network services they use most often. Which services are they? Which is the more popular of the two? How many people did you ask?

### 11.8.2 Testing a Network Connection

You can test the status of a network or a particular host on it by using the `ping` command. If the `ping` command does not work on your system, use the `type ping` command to find its location, update your search path, and try the command again. It is normally in the `/bin` directory on a Linux Mint system. You can also use the `whereis ping` command to find the location of the command. The following is a brief description of the command.

| Item | Description |
| --- | --- |
| Syntax | `ping [options] hostname` |
| Purpose | Send IP datagrams to hostname to test whether it is on the network (or Internet); if the host is alive, it simply echoes the received datagram |
| Output | Message(s) indicating whether the machine is alive |
| Commonly used options/features | `-c count`: Send and receive `count` packets<br>`-f`: Send 100 packets per second or as many as can be handled by the network; only the superuser can use this option<br>`-s packetsize`: Send `packetsize`-byte packets; the default is 56 bytes (plus an 8-byte header) |

The following session illustrates the use of the `ping` command on Linux, with and without options. The output of the command is different for some systems, with the command displaying the echoed messages until you press `<Ctrl+C>`. We used the `-c` option in the following session to send and receive three messages. The `-c` and `-s` options are used to send and receive three 32-byte messages plus an 8-byte Internet Control Message Protocol (ICMP) header.

```
$ ping stanford.edu
PING stanford.edu (171.67.215.200) 56(84) bytes of data.
64 bytes from web.stanford.edu (171.67.215.200): icmp_seq=1 ttl=231 time=317 ms
64 bytes from web.stanford.edu (171.67.215.200): icmp_seq=2 ttl=231 time=464 ms
64 bytes from web.stanford.edu (171.67.215.200): icmp_seq=3 ttl=231 time=508 ms
64 bytes from web.stanford.edu (171.67.215.200): icmp_seq=4 ttl=231 time=402 ms
64 bytes from web.stanford.edu (171.67.215.200): icmp_seq=5 ttl=231 time=451 ms
64 bytes from web.stanford.edu (171.67.215.200): icmp_seq=6 ttl=231 time=410 ms
^C
--- stanford.edu ping statistics ---
9 packets transmitted, 8 received, 11% packet loss, time 8002ms
rtt min/avg/max/mdev = 317.866/440.723/531.807/62.377 ms
$ ping -c 3 stanford.edu
PING stanford.edu (171.67.215.200) 56(84) bytes of data.
64 bytes from web.stanford.edu (171.67.215.200): icmp_seq=1 ttl=231 time=406 ms
64 bytes from web.stanford.edu (171.67.215.200): icmp_seq=2 ttl=231 time=493 ms
64 bytes from web.stanford.edu (171.67.215.200): icmp_seq=3 ttl=231 time=470 ms
--- stanford.edu ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2000ms
rtt min/avg/max/mdev = 406.913/457.112/493.781/36.735 ms
$ ping -c 3 -s 32 stanford.edu
PING stanford.edu (171.67.215.200) 32(60) bytes of data.
40 bytes from web.stanford.edu (171.67.215.200): icmp_seq=1 ttl=231 time=568 ms
40 bytes from web.stanford.edu (171.67.215.200): icmp_seq=2 ttl=231 time=547 ms
40 bytes from web.stanford.edu (171.67.215.200): icmp_seq=3 ttl=231 time=317 ms
--- stanford.edu ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2170ms
rtt min/avg/max/mdev = 317.216/477.698/568.159/113.787 ms
$ ping -c 3 -s 128 stanford.edu
PING stanford.edu (171.67.215.200) 128(156) bytes of data.
136 bytes from web.stanford.edu (171.67.215.200): icmp_seq=1 ttl=231 time=340 ms
136 bytes from web.stanford.edu (171.67.215.200): icmp_seq=2 ttl=231 time=476 ms
136 bytes from web.stanford.edu (171.67.215.200): icmp_seq=3 ttl=231 time=325 ms
--- stanford.edu ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 1999ms
rtt min/avg/max/mdev = 325.864/381.032/476.819/67.994 ms
$
```

You can use the IP address of a host in place of its hostname. For example, you can use `ping 171.67.215.200` instead of `ping stanford.edu`, as in

```
$ ping 171.67.215.200
PING 171.67.215.200 (171.67.215.200) 56(84) bytes of data.
64 bytes from 171.67.215.200: icmp_seq=1 ttl=231 time=617 ms
64 bytes from 171.67.215.200: icmp_seq=2 ttl=231 time=312 ms
64 bytes from 171.67.215.200: icmp_seq=3 ttl=231 time=437 ms
64 bytes from 171.67.215.200: icmp_seq=4 ttl=231 time=398 ms
64 bytes from 171.67.215.200: icmp_seq=5 ttl=231 time=438 ms
^C
--- 171.67.215.200 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4000ms
rtt min/avg/max/mdev = 312.828/441.068/617.665/99.423 ms
$
```

### 11.8.3 Displaying Information About Users

You can use the `finger` command to display information about users on a local or remote host. The information displayed is extracted from a user's `~/.plan` and `~/.project` files. By default, the `finger` command is not installed on our Linux Mint system. If your system does not have `finger` available on your Linux system, see Appendix A for instructions to install it on your system. The following is a brief description of the command.

| Item | Description |
| --- | --- |
| Syntax | `finger [options] [user-list]` |
| Purpose | Display information about the users in `user_list`; without a `user_list`, the command displays a short status report about all the users currently logged on to the specified hosts |
| Output | User information extracted from the `~/.project` and `~/.plan` files |
| Commonly used options/features | `-m`: Match `user_list` to login names only<br>`-s`: Display output in a short format |

The following session shows the simplest use of the command in which information about a user, bob, on the host is displayed.

```
$ finger bob
Login: bob                  Name: Robert Koretsky
Directory: /home/bob        Shell: /bin/bash
On since Sun Oct 15 20:21 (PDT) on pts/1 from 103.255.5.99
    1 hour 39 minutes idle
On since Sun Oct 15 21:53 (PDT) on pts/0 from 103.255.5.99
    3 seconds idle
No mail.
No plan.
$
```

You can use the `finger` command with the `-s` option to display the command's output in a short format and the `-m` option to match user-list to login names only. The `finger -m tree` command displays the same information as the `finger tree` command if the login name of the user is `tree` (uppercase and lowercase letters are considered the same by the networking commands). However, if the login name of the user is `btree` and the login name `tree` does not exist in the system, the `finger` command displays the message informing you accordingly.

When run without any argument, the `finger` command returns the status of all the users who are currently logged on to your machine. The amount of information displayed varies somewhat, depending on the Linux system that your host runs. The following command runs on Linux Mint.

