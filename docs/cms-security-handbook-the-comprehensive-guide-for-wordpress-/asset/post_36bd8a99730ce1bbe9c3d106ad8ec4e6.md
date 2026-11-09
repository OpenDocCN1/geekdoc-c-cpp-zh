
- An infected machine on the network
- Physical access to a machine by a malicious person
- Network-attached printers that may be used to assault servers either locally or remotely
- Web, database, or network services that are misconfigured or out of date

A breached server will exhibit odd behavior, such as unusually high loads on the machine, excessive bandwidth, many files open, or super users logged in that should not be. Other signs include software that should not be installed, or unexpected reboots. Many more symptoms could exhibit a server breach. In essence, if the machine is acting strangely, when it normally behaves, then you have a problem.

One area to do a quick review on is the date and time stamp of files. Look to see whether any of the files or folders have recently changed. Although not a guarantee of whether a true hack has occurred, the chances are good that if you have been hacked, this area will note it for you.

Data on a server or site that has been compromised is very often modified by the attacker. Check the FTP archives, directories for users, web pages, and so on for changes.

When you are trying to contain an operating system breach, consider the following:

- Using Linux commands on the server
- Updating the server
- Using RKHunter
- Checking for open ports

## Using Linux Commands

The intention of this book is not to teach you how to be a Linux operating system administrator. However, a couple of Linux commands are handy to know when dealing with an operating system breach. These are commonly available on most Linux distributions.

The who command can tell you who is logged on to the machine. In its simplest form, typing the command who will reveal all the users who are logged in.

When dealing with an operating system breach, the first thing you want to find out is who is on the machine. Log in to your server using PuTTY or another SSH client (discussed earlier in this chapter), and then elevate your login to super user. At the # prompt, enter the who command, and you should see something similar to Figure 9-3.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_328_0.png)

**Figure 9-3:** Example using the who command

If you find an unauthorized user logged in, then you can take the necessary steps to log him out. Figure 9-3 shows an example of three different Internet Protocol (IP) addresses logged in as root. If any of those were bad guys, you would be able to take immediate action by terminating their connections and blocking the IP addresses.

What you see here is the *Pseudo Terminal number (or PTY number)*, who they are logged in as, and what username was used. Most importantly, you see the IP address from where the person logged in. To locate your PTY, look at your IP address that you are using, and then you'll know which one to terminate.

To terminate or *kill* a PTY, find the number of the PTY with the command `ps -ef | grep "ssh"`, which will show you all the PIDs logged in using SSH. You'll see something like the following:

```text
[root@host ~]# ps -ef | grep "ssh"
root       26188     1  0 01:08 ?        00:00:00 /usr/sbin/sshd
root       29740 26188  0 14:29 ?        00:00:00 sshd: root@pts/0
```

The number following root is the PID. Issue the command `kill -9 pid`, where pid is the number.

If your distribution of Linux does not support the who command, consult the man pages.

> **WARNING** Be sure you do not log authorized users out, such as your host.

If you find that someone has illegally logged in, you'll want to record that IP address.

You'll also want to review the load on your machine from time to time to keep a basic idea of the average load. If your server is hacked and is serving up IRC chats to the underground community, then you'll see an increase in loads. The top command provides the capability to take a dynamic look at processor activity in real time. This command enables you to see processes, resources, memory consumption, and the user who initiated the activity.

To find out your load, type `top` at the command prompt, as shown in Figure 9-4.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_329_0.png)

**Figure 9-4:** top command showing the processes that are running

In this case, you can see that the total load on the CPU is 0.3 percent, the free memory is 409,720 KB, and the machine has 62 total tasks running. Lastly, you can see that one user is logged in.

If your site is extremely busy, you’ll see much higher loads. Again, this is not necessarily an indicator that your site is or isn’t being hacked, but it’s a data point to look at. Monitor your site’s performance regularly to gain an understanding of your particular traffic pattern.

## Updating Your Server

Updating your server may very well be a task your host has taken care of for you. Hosts such as Rochen.com handle the operating system upgrades for you. Other hosts may handle it differently. If you are tasked with updating your operating system, then the update process is simple in most cases.

At the command prompt type `yum update` (for RedHat/Fedora/CentOS distributions of Linux). This will grab most of the patches necessary to keep your server running optimally and securely.

## Using RKHunter

The next step is to check for the presence of a *rootkit*. RKHunter is a great tool for checking whether the system is compromised.

Installing RKHunter is easy; simply type the following at the # command prompt:

```text
yum install rkhunter
```

If it’s already installed, then you’ll get a message similar to the one shown in Figure 9-5.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_330_0.png)

**Figure 9-5:** RKHunter already installed

With RKHunter installed, start it by entering the following command at the command prompt:

```text
rkhunter -c
```

RKHunter performs a series of diagnostic checks, looking for known rootkit files, directories, malware, back doors, and suspicious processes. It scans your user accounts and looks for accounts that have the equivalent privileges of root or super user.

> **NOTE** If you’re running Windows rather than Linux, you can get equivalent tools to handle those tasks from http://technet.microsoft.com/en-us/sysinternals/bb842062.aspx. Download the Sysinternals suite.

If directories and processes are running that are atypical, RKHunter flags those and immediately lets you know. If RKHunter finds anything wrong, it displays the various checks in red (very noticeable). If you do find something, you may need to enlist the aid of your hosting company to help remove it.

If all these tests are clean, then you’ll be greeted with a message similar to the one shown in Figure 9-6.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_330_1.png)

**Figure 9-6:** RKHunter shows “all clear”

## Checking for Open Ports

Another basic tryout you should perform is to see what ports are open. RKHunter does check for open ports such as 6666 and 6667, which, unless you are running your own IRC (chat) service, should be closed. However, you should look beyond what RKHunter checks and review all the open ports.

Type in the following at the command prompt:

```text
netstat -az | more
```

This command instructs the server to show you all the open ports. The more command enables you to look at the long list of data more easily by providing a portion at a time, as shown in Figure 9-7.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_331_0.png)

This is a basic connection to your machine. The *Local Address* that has been blurred out here is the server's IP address. The *Foreign Address* is the browsing IP address. This, of course, is simply a basic look. What you don't want to see is machines connecting to port 6667 or 6666, which would show up next to the IP address, such as `192.168.1.18:6667`. In that case, the action you would want to take is to close ports 6666 and 6667 (assuming they are open).

An easier method to discovering open ports is to use NMAP to scan your system (with permission from the host or owner of the machine only) and determine what ports are open. Figure 9-8 shows a view of a server's ports from NMAP. In this example, a variety of ports are open, but, in this case, all is well. If you were to see a system with hundreds of ports open, then you have a bigger problem.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_331_1.png)
