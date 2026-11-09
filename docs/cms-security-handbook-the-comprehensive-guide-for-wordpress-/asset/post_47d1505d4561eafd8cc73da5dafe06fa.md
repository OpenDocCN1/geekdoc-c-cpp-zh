
- **Regular Scan** — This conducts a default Nmap scan
- **Slow comprehensive scan** — This produces the following command:

```
nmap -sS -sU -T4 -A -v -PE -PP -PS21,22,23,25,80,113,31339 -PA80,113,143,10042 -PO --script all
```

> **NOTE** For more information on these options, see http://nmap.org/book/docs/nmap-usage.txt.

## Telnet

Although Telnet should be removed from your server, it’s great as a testing tool and still the norm for connecting to specific types of network gear. Telnet is a very old protocol that allows you to connect to a machine and issue commands. By default, Telnet runs on port 23.

To start using Telnet on a Windows machine, click Start » Accessories » Command Prompt. At the command prompt, type telnet. The TELNET> prompt appears.

To Telnet to another machine, enter the following:

```
machine name port
```

Replace the machine name with the IP or hostname and the port number. Telnet can be used to connect and send e-mail on misconfigured servers. For example, the following command will attempt to connect you to the Mail Services:

```
telnet machine name 25
```

If you are successful in connecting, you can often send unauthorized e-mail through the server. This is also a means to check for open relays in your mail system.

Following is a list of common parameters used with the Windows version of Telnet:

- `c` — Close the connection.
- `d` — Display operating parameters.
- `o` — Connect to hostname (defaults to port 23).
- `q` — Exit (quit) Telnet.
- `set` — Set options (see `set ?` for more information).
- `send` — Send strings (commands) to server.
- `st` — Print status information.
- `-u` — Unset options.
- `-? /h` — Help.

## Netstat

Netstat is a very valuable tool for troubleshooting and observing what is going on with your network. You can use this tool any time to view network connections, routing tables, the statistics of an interface, and more.

Following are common options for Netstat:

- `-a` — Displays all active Transmission Control Protocol (TCP) connections, as well as the TCP and User Datagram Protocol (UDP) ports on which the computer is listening.
- `-e` — Displays Ethernet statistics, such as the number of bytes and packets sent and received. This parameter can be combined with `-s`.
- `-i` — Displays network interfaces and their statistics.
- `-n` — Displays active TCP connections. However, addresses and port numbers are expressed numerically, and no attempt is made to determine names.
- `-o` — Shows which processes are using which sockets.
- `-r` — Displays the contents of the IP routing table.
- `-s` — Displays statistics by protocol. By default, statistics are shown for the TCP, UDP, Internet Control Message Protocol (ICMP), and IP protocols. If the IPv6 protocol for Windows XP is installed, statistics are shown for the TCP over IPv6, UDP over IPv6, ICMPv6, and IPv6 protocols. The `-p` parameter can be used to specify a set of protocols.
- `-v` — Sets verbose mode.
- `-V` (uppercase) — Displays the version information.
- `-h` — Displays help.

## WireShark

WireShark is known as a *sniffer*. It listens in on the network connection and captures each packet. According to the website `www.wireshark.org/about.html`, “Wireshark is the world's foremost network protocol analyzer. It lets you capture and interactively browse the traffic running on a computer network. It is the de facto (and often de jure) standard across many industries and educational institutions.”

You should become familiar with this powerful tool. It is an excellent tool for network and server administrators to use to troubleshoot issues.

> **WARNING** Only use WireShark on a corporate network if you have permission. Never use this tool for any illegal or unethical tasks (such as capturing passwords). Only use it for the proper administrative needs.

Currently, WireShark is available for the following platforms:

- Windows Installer (32-bit)
- Windows Installer (64-bit)
- Windows U3 (32-bit)
- Windows PortableApps (32-bit)
- OS X 10.5 (Leopard) Intel 32-bit .dmg
- OS X 10.6 (Snow Leopard) Intel 64-bit .dmg
- OS X 10.5 (Leopard) PPC 32-bit .dmg

After you download it, follow the installation instructions for your platform. For Windows, you must install WinPcap (included with the installer) or the captures will not work.

The Windows installation is a fairly simple point-and-click process. Unless you have other reasons to do so, you should choose the defaults.

On a Windows machine, you start WireShark by clicking its corresponding icon. Open the Capture > Interface selection from the toolbar. This will provide a list of installed network interface cards (NICs) on the machine. Your machine may have a wired NIC and a wireless NIC, and each will be listed. Choose the NIC from which you want to collect packets and click Start.

As the collection process starts, you will see the collection window filling up with packets. These listings show the IP source, IP destination, protocol, and other information about the packet. Using this information can enable you to locate all kinds of problems on your network, such as bad NICs and illegal traffic (hackers).

WireShark can capture many protocols that are used for various devices. For example, the most common packet you would see is TCP/IP for your normal Internet traffic. Voice over IP (VoIP) would have a different protocol. Select or deselect the protocols for which you want to capture information.

After you collect enough packets, you can review errors, warnings, and other information WireShark has found. Errors can indicate software or configuration issues. For example, if you're troubleshooting a network storm, the noted errors can be used to track down the offending device. WireShark can also detect problems such as bad patch cables that could be causing network issues such as slow performance.

One very powerful feature is the capability to search for specific information. For example, you could search for all the traffic from a network that was bound to or from `mail.google.com`.

## Backdoor Intruders

Table A-1 shows a list of known (as of this writing) ports and the backdoor viruses and Trojans that try to use these ports. Many of these may be old, but given that virus writers tend to reuse each other’s code, tracking the historical viruses is important. This compiled list from www.sans.org/security-resources/idaq/oddports.php and other sources is one you can cross reference if you believe you have been hacked.

### Table A-1: Common Ports and Backdoor Intruder

| PORT NUMBER | TROJAN NAME |
|---:|---|
| 2 | Death |
| 20 | Senna Spy FTP server |
| 21 | Back Construction, Blade Runner, Doly Trojan, Invisible FTP, Juggernaut 42, Larva, Motly FTP, Net Administrator, Senna Spy FTP server, Traitor 21, WebEx, WinCrash |
| 22 | Shaft |
| 23 | Fire, Hacker, Tiny, Telnet, Server, TTS, Truva, Ati |
| 25 | Ajan, Antigen, Email, Password, Sender, EPS II, Gip, Gris, Happy99, Hpteam, mail, I love you, Kuang2, Magic, Horse, MBT |
| 31 | Agent 31, Hackers, Paradise, MasterParadise |
| 41 | Deep Throat, Foreplay or Reduced Foreplay |
| 48 | DRAT |
| 50 | DRAT |
| 59 | DMSetup |
| 79 | CDK, Firehotcker |
| 80 | AckCmd, BackEnd, CGI, Backdoor, Executor, Hooker, RingZero |
| 81 | RemoConChubo |
| 99 | Hidden Port |
| 110 | ProMail trojan |
| 113 | Identd, Invisible, Deamon, Kazimas |
| 119 | Happy99 |
| 121 | JammerKillah |
| 123 | Net, Controller |
| 133 | Farnaz |
| 142 | NetTaxi |
| 146 | Infector |
| 146 | (UDP) Infector |
| 170 | A-trojan |
| 180 | (TCP/UDP) amanda |
| 334 | Backage |
| 420 | Breach |
| 421 | TCP Wrappers, trojan |
| 456 | Hackers Paradise |
| 513 | Grlogin |
| 514 | RPC Backdoor |
| 531 | Rasmin |
| 559 | (TCP/UDP) teedtap |
| 605 | Secret Service |
| 666 | Attack FTP, Back Construction, Cain & Abel, NokNok, Satans Back Door, SBD, ServU, Shadow Phyre |
| 667 | SniperNet |
| 669 | DP trojan |
| 692 | GayOl |
| 777 | AimSpy, Undetected |
| 808 | WinHole |
| 911 | Dark Shadow |
| 999 | Deep Throat, Foreplay, Reduced Foreplay, WinSatan |
| 1000 | Der Späher / Der Spaether |
| 1001 | Der Späher, Der Spaether, Le |
| 1010 | Doly Trojan |
| 1011 | Doly Trojan |
| 1012 | Doly Trojan |
