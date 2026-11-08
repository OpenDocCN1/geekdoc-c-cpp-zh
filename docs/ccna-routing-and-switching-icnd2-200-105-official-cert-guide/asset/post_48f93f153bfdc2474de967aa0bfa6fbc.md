
Figure 13-21 shows all the specific MLPPP commands in a working example. The example is based on the design in Figures 13-19 and 13-20. Note that for space, Figure 13-21 shows the configuration for only one of the two serial interfaces, but all serial interfaces would have the same subcommands when used for MLPPP.

First, focus on the six configuration commands noted with white highlight boxes in Figure 13-21 as pointed to with arrows. The **interface multilink 1** command on each router creates the multilink interface on that router. The network engineer chooses the interface number, but the number must be the same on both routers, or the link will not work. Additionally, the multilink interfaces and the physical serial interfaces must all have both a **ppp multilink group 1** command, and they must all again refer to that same number (1 in this example). Any number in range could be used, but the number must match with the commands highlighted in the figure.

![](img/79473ea15699e01619d2aa789f5bd43b_405_0.png)

**Figure 13-21** *MLPPP Configuration*

Now look at the **ip address** commands. Note that the configuration shows IPv4 addresses configured on the multilink interfaces, but no IPv4 address at all on the serial interface. In short, the multilink interface has the Layer 3 configuration, and the serial interfaces do not. As a result, the routing and routing protocol logic will work with the multilink interface.

Finally, note that both the multilink and serial interfaces have two additional commands: **encapsulation ppp** (which enables PPP), and **ppp multilink** (which adds multilink support).

> **NOTE** Figure 13-21 shows only one serial interface, but each serial interface in the multi-link group would need the same configuration.

Command lists interfaces on which EIGRP is enabled, listing Mu1 (Multilink 1), and not listing either of the two serial interfaces in the MLPPP bundle. Finally, note that the **show ip interface brief** command does list both the serial interfaces and the multilink interface, but the output confirms that no IP address has been configured on the serial interfaces, as noted with the “unassigned” text under the IP-Address column.

Each multilink interface has a line and protocol status like any other interface, and if that status is up/up, IOS believes the multilink interface is working. By default, that working state implies that at least one of the physical links in the MLPPP group is also working—that is, some of the physical links can fail, and the multilink stays up. You can always directly verify the serial interfaces in the multilink group with the same commands discussed earlier in the chapter (**show controllers**, **show interfaces**). Additionally, the two commands in Example 13-9 give some insight into the specifics of MLPPP operation.

### Example 13-9 Verifying Operational Details of an MLPPP Group

```text
R1# show interfaces multilink 1
Multilink1 is up, line protocol is up
  Hardware is multilink group interface
  Internet address is 192.168.5.1/24
  MTU 1500 bytes, BW 3088 Kbit/sec, DLY 20000 usec,
    reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation PPP, LCP Open, multilink Open
  Open: IPCP, CDPCP, loopback not set
  Keepalive set (10 sec)
! lines omitted for brevity

R1# show ppp multilink

Multilink1
  Bundle name: R2
  Remote Username: R2
  Remote Endpoint Discriminator: [1] R2
  Local Username: R1
  Local Endpoint Discriminator: [1] R1
  Bundle up for 16:50:33, total bandwidth 3088, load 1/255
  Receive buffer limit 24000 bytes, frag timeout 1000 ms
    0/0 fragments/bytes in reassembly list
    0 lost fragments, 96 reordered
    0/0 discarded fragments/bytes, 0 lost received
    0x654D7 received sequence, 0x654D5 sent sequence
  Member links: 2 active, 0 inactive (max 255, min not set)
    Se0/1/1, since 16:50:33
    Se0/0/0, since 16:23:16
No inactive multilink interfaces
```

First, notice that the show interfaces multilink 1 command lists many familiar details and some mentions about multilink. In particular, the output shows the traditional line and protocol status, both in an up state, meaning that the interface is working. On the sixth line, the output mentioned a working multilink state of “Open” in the section about PPP control protocols, confirming that MLPPP is in effect.

Finally, the output of the `show ppp multilink` command identifies the links configured in each multilink bundle, as well as which ones are active. In this case, on R1, interfaces S0/0/0 and S0/1/1 are active, as highlighted at the bottom of the example. The timer to the side shows that both have been active a little over 16 hours. Seeing these two interfaces in the list confirms not only that the physical interfaces are working, but that the MLPPP configuration includes both of these links in multilink group 1.

## Troubleshooting Serial Links

This final major section discusses how to isolate and find the root cause of problems related to topics covered earlier in this chapter. Also, this section does not attempt to repeat the IP troubleshooting coverage in Part II of this book, but it does point out some of the possible symptoms on a serial link when a Layer 3 subnet mismatch occurs on opposite ends of a serial link, which prevents the routers from routing packets over the serial link.

A simple `ping` command can determine whether a serial link can or cannot forward IP packets. A ping of the other router’s serial IP address—for example, a working `ping 192.168.2.2` command on R1 in Figure 13-11, the figure used for both the HDLC and PPP configuration examples—proves that the link either works or does not.

If the ping does not work, the problem could be related to functions at Layer 1, 2, or 3. The best way to isolate which layer is the most likely cause is to examine the interface status codes described in Table 13-5.

Table 13-5 Interface Status Codes and Typical Meanings When a Ping Does Not Work

| Line Status | Protocol Status | Likely General Reason/Layer |
| --- | --- | --- |
| Administratively down | Down | Interface shutdown |
| Down | Down | Layer 1 |
| Up | Down | Layer 2 |
| Up | Up | Layer 3 |

The serial link verification and troubleshooting process should begin with a simple three-step process:

- **Step 1.** From one router, ping the other router’s serial IP address.
- **Step 2.** If the ping fails, examine the interface status on both routers and investigate problems related to the likely problem areas listed in Table 13-5.
- **Step 3.** If the ping works, also verify that any routing protocols are exchanging routes over the link, as discussed in Chapter 11, “Troubleshooting IPv4 Routing Protocols.”

> **NOTE** The interface status codes can be found using the `show interfaces`, `show ip interface brief`, and `show interfaces description` commands.

The rest of this section explores the specific items to be examined when the ping fails, based on the combinations of interface status codes listed in Table 13-5.

### Troubleshooting Layer 1 Problems

The interface status codes, or interface state, play a key role in isolating the root cause of problems on serial links. In fact, the status on both ends of the link may differ, so it is important to examine the status on both ends of the link to help determine the problem.

For example, a serial link fails when just one of the two routers has administratively disabled its serial interface with the **shutdown** interface subcommand. When one router shuts down its serial interface, the other router sits in a down/down state (line status down, line protocol status down), assuming the second router's interface is not also shut down. The solution is to just configure a **no shutdown** interface configuration command on the interface.

A serial interface with a *down* line status on both ends of the serial link—that is, both ends in a down/down state—usually points to some Layer 1 problem. Figure 13-22 summarizes the most common causes of this state. In the figure, R2's serial interface has no problems at all; the center and left side of the figure show common root causes that then result in R2's serial interface being in a down/down state.

![](img/79473ea15699e01619d2aa789f5bd43b_409_0.png)

*Figure 13-22* Problems That Result in a Down/Down State on Router R2

### Troubleshooting Layer 2 Problems

Data link layer problems on serial links usually result in at least one of the routers having a serial interface status of up/down. In other words, the line status (the first status code) is up, while the second status (the line protocol status) is down. Table 13-6 lists some of these types of problems.

**Table 13-6** Likely Reasons for Data Link Problems on Serial Links

| Line Status | Protocol Status | Likely Reason |
|---|---|---|
| Up | Down on both ends¹ | Mismatched encapsulation commands |
| Up | Down on one end, up on the other | Keepalive disabled on the end in an up state when using HDLC |
| Up | Down on both ends | PAP/CHAP authentication failure |

¹ In this case, the state may flap from up/up, to up/down, to up/up, and so on, while the router keeps trying to make the encapsulation work.
