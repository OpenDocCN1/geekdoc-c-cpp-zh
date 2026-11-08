
Figure J-1 shows the ICMP messages, with IP headers, in an example. In this case, the user at host A opens a command prompt and issues the **ping 172.16.2.101** command, testing connectivity to host B. The command sends one echo request, and waits (Step 1); host B receives the messages, and sends back an echo reply (Step 2).

![](img/79473ea15699e01619d2aa789f5bd43b_1132_0.png)

**Figure J-1** — *Concept Behind ping 172.16.2.101 on Host A*

The ping command is supported on many different devices and many common operating systems. The command has many options: the name or IP address of the destination, how many times the command should send an echo request, how long the command should wait (timeout) for an echo reply, how big to make the packets, and many other options. Example J-1 shows a sample from host A, with the same command that matches the concept in Figure J-1: a ping 172.16.2.101 command on host A.

**Example J-1** — *Sample Output from Host A’s ping 172.16.2.101 Command*

```text
Wendell-Odoms-iMac:~ wendellod$ ping 172.16.2.101
PING 172.16.2.101 (172.16.2.101): 56 data bytes
64 bytes from 172.16.2.101: icmp_seq=0 ttl=64 time=1.112 ms
64 bytes from 172.16.2.101: icmp_seq=1 ttl=64 time=0.673 ms
64 bytes from 172.16.2.101: icmp_seq=2 ttl=64 time=0.631 ms
64 bytes from 172.16.2.101: icmp_seq=3 ttl=64 time=0.674 ms
64 bytes from 172.16.2.101: icmp_seq=4 ttl=64 time=0.642 ms
64 bytes from 172.16.2.101: icmp_seq=5 ttl=64 time=0.656 ms
^C
--- 172.16.2.101 ping statistics ---
6 packets transmitted, 6 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 0.631/0.731/1.112/0.171 ms
```

## Strategies and Results When Testing with the ping Command

Often, the person handling initial calls from users about problems (often called a customer support rep, or CSR) cannot issue ping commands from the user’s device. In some cases, talking users through typing the right commands and making the right clicks on their machines can be a problem. Or, the user just might not be available. As an alternative, using different ping commands from different routers can help isolate the problem.

The problem with using ping commands from routers, instead of from the host that has the problem, is that no single router ping command can exactly replicate a ping command done from the user’s device. However, each different ping command can help isolate a problem further. The rest of this section of ping commands discusses troubleshooting IPv4 routing by using various ping commands from the command-line interface (CLI) of a router.

### Testing Longer Routes from Near the Source of the Problem

Most problems begin with some idea like “host X cannot communicate with host Y.” A great first troubleshooting step is to issue a ping command from X for host Y’s IP address. However, assuming the engineer does not have access to host X, the next best test is to ping host X’s IP address from the router nearest the host that has the problem.

For instance, in Figure J-1, imagine that the user of host A had called IT support with a problem related to sending packets to host B. A ping 172.16.2.101 command on host A would be a great first troubleshooting step, but the CSR cannot access host A or get in touch with the user of host A. So, the CSR telnets to Router R1, and pings host B from there, as shown in Example J-2.

**Example J-2** — *Router R1 Pings Host B (Two Commands)*

```text
R1# ping 172.16.2.101
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 172.16.2.101, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 1/2/4 ms
R1# ping 172.16.2.101
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 172.16.2.101, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/2/4 ms
```

First, take a moment to review the output of the first IOS ping command. By default, the Cisco IOS ping command sends five echo messages, with a timeout of 2 seconds. If the command does not receive an echo reply within 2 seconds, the command considers that message to be a failure, and the command lists a period. If a successful reply is received within 2 seconds, the command displays an exclamation point. So, in this first command, the first echo reply timed out, whereas the other four received a matching echo reply within 2 seconds.

As a quick aside, the example shows a common and normal behavior with ping commands: the first ping command shows one failure to start, but then the rest of the messages work. This usually happens because some device in the end-to-end route is missing an ARP table entry.

Now think about troubleshooting and what a working ping command tells us about the current behavior of this internetwork. First, focus on the big picture for a moment:

- R1 can send ICMP echo request messages to host B (172.16.2.101).
- R1 sends these messages from its outgoing interface’s IP address (by default), 172.16.4.1 in this case.
- Host B can send ICMP echo reply messages to R1’s 172.16.4.1 IP address (hosts send echo reply messages to the IP address from which the echo request was received).

Figure J-2 shows the packet flow.

![](img/79473ea15699e01619d2aa789f5bd43b_1134_0.png)

**Figure J-2** — *Standard ping 172.16.2.101 Command Using the Source Interface IP Address*

Next, think about IPv4 routing. In the forward direction, R1 must have a route that matches host B’s address (172.16.2.101); this route will be either a static route or one learned with a routing protocol. R2 also needs a route for host B’s address, in this case a connected route to B’s subnet (172.16.2.0/24), as shown in the top arrow lines in Figure J-3.

![](img/79473ea15699e01619d2aa789f5bd43b_1134_1.png)

**Figure J-3** — *Layer 3 Routes Needed for R1’s Ping 172.16.2.101 to Work*

The arrow lines on the bottom of Figure J-3 show the routes needed to forward the ICMP echo reply message back to Router R1’s 172.16.4.1 interface. First, host B must have a valid default router setting because 172.16.4.1 is in a different subnet than host B. R2 must also have a route that matches destination 172.16.4.1 (in this case, likely to be a connected route).

The working ping commands in Example J-2 also require the data link and physical layer details to be working. The serial link must be working: The router interfaces must be up/up, which typically indicates that the link can pass data. On the LAN, R2’s LAN interface must be in an up/up state. In addition, everything discussed about Ethernet LANs must be working because the ping confirmed that the packets went all the way from R1 to host B and back. In particular:

- The switch interfaces in use are in a connected (up/up) state.
- Port security does not filter frames sent by R2 or host B.
- STP has placed the right ports into a forwarding state.

> **NOTE** The ICND2 book discusses STP in depth, but the need to consider STP port state is mentioned here for completeness for those planning to achieve CCNA R&S certification.

![](img/79473ea15699e01619d2aa789f5bd43b_1138_0.png)

**Figure J-7** — *Standard ping Command Confirms That the LAN Works*

If the ping works, it confirms the following, which rules out some potential issues:

- The host with address 172.16.1.51 replied.
- The LAN can pass unicast frames from R1 to host 172.16.1.51 and vice versa.
- You can reasonably assume that the switches learned the MAC addresses of the router and the host, adding those to the MAC address tables.
- Host A and Router R1 completed the ARP process and list each other in their respective Address Resolution Protocol (ARP) tables.

The failure of a ping, even with two devices on the same subnet, can point to a variety of problems, like those mentioned in this list. For instance, if the ping 172.16.1.51 on R1 fails (Figure J-7), that result points to this list of potential root causes:

- **IP addressing problem:** Host A could be statically configured with the wrong IP address.
- **DHCP problems:** If you are using Dynamic Host Configuration Protocol (DHCP), many problems could exist: Host A could be using a different IP address than 172.16.1.51, the DHCP configuration could be wrong, the routers may be missing the DHCP relay configuration and so host A never got its IPv4 address lease, and so on.
- **VLAN trunking problems:** The router could be configured for 802.1Q trunking, when the switch is not (or vice versa).
- **LAN problems:** Any LAN problem discussed in Parts II and III of the ICND1 book, and Part I of the ICND2 book.

So, whether the ping works or fails, simply pinging a LAN host from a router can help further isolate the problem.

### Testing LAN Neighbors with Extended Ping

A standard ping of a LAN host from a router does not test that host’s default router setting. However, an extended ping can test the host’s default router setting. Both tests can be useful, especially for problem isolation, because:

- If a standard ping of a local LAN host works…
- But an extended ping of the same LAN host fails…
- The problem likely relates somehow to the host’s default router setting.
