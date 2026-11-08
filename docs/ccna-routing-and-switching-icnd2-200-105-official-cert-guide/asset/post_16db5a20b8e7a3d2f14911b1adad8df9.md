
### Example 19-13  *Verification Commands Listing Interface Port-Channel12 from Switch SW1*

```
SW1# show interfaces port-channel 12
Port-channel12 is up, line protocol is up (connected)
  Hardware is EtherChannel, address is bcc4.93b8.e543 (bia bcc4.93b8.e543)
  Internet address is 10.1.12.1/24
! lines omitted for brevity

SW1# show interfaces status
! Only ports related to the example are shown.
Port      Name                Status       Vlan       Duplex  Speed Type
Gi1/0/13                      connected    routed     a-full  a-1000 10/100/1000BaseTX
Gi1/0/14                      connected    routed     a-full  a-1000 10/100/1000BaseTX
Po12                          connected    routed     a-full  a-1000

SW1# show ip route
! legend omitted for brevity
      10.0.0.0/8 is variably subnetted, 4 subnets, 2 masks
C     10.1.2.0/24 is directly connected, Vlan2
L     10.1.2.1/32 is directly connected, Vlan2
C     10.1.12.0/24 is directly connected, Port-channel12
L     10.1.12.1/32 is directly connected, Port-channel12
```

For a final bit of verification, you can examine the EtherChannel directly with the show etherchannel summary command as listed in Example 19-14. (Although it has been a while, as a reminder, Chapters 3 and 4 showed examples of this command when used for Layer 2 EtherChannels.) Note in particular that it lists a flag legend for characters that identify key operational states, like whether a port is bundled (included) in the PortChannel (P), and whether it is acting as a routed (R) or switched (S) port.

### Example 19-14  *Verifying the EtherChannel*

```
SW1# show etherchannel 12 summary

Flags:  D - down          P - bundled in port-channel
       I - stand-alone   s - suspended
       H - Hot-standby (LACP only)
       R - Layer3        S - Layer2
       U - in use        f - failed to allocate aggregator

       M - not in use, minimum links not met
       u - unsuitable for bundling
       w - waiting to be aggregated
       d - default port

Number of channel-groups in use: 1
Number of aggregators:          1
```

| Group | Port-channel | Protocol | Ports |
| --- | --- | --- | --- |
| 12 | Po12 (RU) | - | G1/0/13(P) G1/0/14(P) |

### Troubleshooting Layer 3 EtherChannels

When troubleshooting a Layer 3 EtherChannel, there are two main areas to consider. First, you need to look at the configuration of the `channel-group` command, which enables an interface for an EtherChannel. Second, you should check a list of settings that must match on the interfaces for a Layer 3 EtherChannel to work correctly.

As for the `channel-group` interface subcommand, this command can enable EtherChannel statically or dynamically. If dynamic, this command's keywords imply either Port Aggregation Protocol (PAgP) or Link Aggregation Control Protocol (LACP) as the protocol to negotiate between the neighboring switches whether they put the link into the EtherChannel.

If all this sounds vaguely familiar, it is the exact same configuration covered way back in the Chapter 3 section “Configuring Dynamic EtherChannels.” The configuration of the `channel-group` subcommand is exactly the same, with the same requirements, whether configuring Layer 2 or Layer 3 EtherChannels. So, it might be a good time to review those EtherChannel configuration details from Chapter 3. However, regardless of when you review and master those commands, note that the configuration of the EtherChannel (with the `channel-group` subcommand) is the same, whether Layer 2 or Layer 3.

Additionally, you must do more than just configure the `channel-group` command correctly for all the physical ports to be bundled into the EtherChannel. Layer 2 EtherChannels have a longer list of requirements, but Layer 3 EtherChannels do require a few consistency checks between the ports before they can be added to the EtherChannel. The following is the list of requirements for Layer 3 EtherChannels:

- **no switchport:** The PortChannel interface must be configured with the **no switchport** command, and so must the physical interfaces. If a physical interface is not also configured with the **no switchport** command, it will not become operational in the EtherChannel.
- **Speed:** The physical ports in the channel must use the same speed.
- **Duplex:** The physical ports in the channel must use the same duplex.

![](img/79473ea15699e01619d2aa789f5bd43b_596_0.png)

## Chapter Review

One key to doing well on the exams is to perform repetitive spaced review sessions. Review this chapter's material using either the tools in the book, DVD, or interactive tools for the same material found on the book's companion website. Refer to the “Your Study Plan” element for more details. Table 19-2 outlines the key review elements and where you can find them. To better track your study progress, record when you completed these activities in the second column.

### Table 19-4  Chapter 19 Configuration Command Reference

| Command | Description |
|---|---|
| interface type number.subint | Router global command to create a subinterface and to enter configuration mode for that subinterface |
| encapsulation dot1q vlan-id [native] | Router subinterface subcommand that tells the router to use 802.1Q trunking, for a particular VLAN, and with the native keyword, to not encapsulate in a trunking header |
| [no] ip routing | Global command that enables (ip routing) or disables (no ip routing) the routing of IPv4 packets on a router or Layer 3 switch |
| interface vlan vlan-id | A switch global command on a Layer 3 switch to create a VLAN interface and to enter configuration mode for that VLAN interface |
| sdm prefer lanbase-routing | Command on some Cisco switches that reallocates forwarding chip memory to allow for an IPv4 routing table |
| [no] switchport | Layer 3 switch subcommand that makes the port act as a Layer 2 port (switchport) or Layer 3 routed port (no switchport) |
| interface port-channel channel-number | A switch command to enter PortChannel configuration mode, and also to create the PortChannel if not already created |
| channel-group channel-number mode {auto &#124; desirable &#124; active &#124; passive &#124; on} | Interface subcommand that enables EtherChannel on the interface |

### Table 19-5  Chapter 19 EXEC Command Reference

| Command | Description |
|---|---|
| show ip route | Lists the router's entire routing table |
| show ip route [connected] | Lists a subset of the IP routing table |
| show vlans | Lists VLAN configuration and statistics for VLAN trunks configured on routers |
| show interfaces [interface type number] | Lists detailed status and statistical information, including IP address and mask, about all interfaces (or the listed interface only) |
| show interfaces [interface type number] status | Among other facts, for switch ports, lists the access VLAN or the fact that the interface is a trunk; or, for routed ports, lists "routed" |
| show interfaces interface-id switchport | For switch ports, lists information about any interface regarding administrative settings and operational state; for routed ports, the output simply confirms the port is a routed (not switched) port |
| show interfaces vlan number | Lists the interface status, the switch's IPv4 address and mask, and much more |
| show etherchannel [channel-group-number] summary | Lists information about the state of EtherChannels on this switch, including whether the channel is a Layer 2 or Layer 3 EtherChannel |

**4.** The following text lists output taken from Router R3, which is using HSRP. Subnet 10.1.12.0 uses mask 255.255.255.0. Based on the output of this command, which of the following answers is true?

```
R3# show standby brief
Interface  Grp  Pri  P State  Active  Standby  Virtual IP
Gi0/0      1    105  Active   local   10.1.12.1  10.1.12.2
```

- a. Hosts with a default router setting of 10.1.12.1 are sending their packets to Router R3.
- b. Hosts with a default router setting of 10.1.12.2 are sending their packets to Router R3.
- c. Router R3 has an ip address 10.1.12.2 255.255.255.0 command configured on its G0/0 interface.
- d. Router R3 has an ip address 10.1.12.1 255.255.255.0 command configured on its G0/0 interface.

**5.** Two routers, R1 and R2, are configured to be part of an HSRP group. R1’s configuration includes the **standby 1 priority 1** command, and R2’s configuration includes the **standby 1 priority 2** command. R1 powers up. An hour later, R2 powers up. Which of the following answers is true about which router is now the HSRP active router?

- a. R2 is active regardless of other configuration settings.
- b. R1 is active regardless of other configuration settings.
- c. R2 is active only if R2 is also configured with **standby 1 preempt**.
- d. R1 is active only if R1 is also configured with no **standby 1 preempt**.

**6.** Another engineer has configured HSRP on two routers that connect to the same LAN. You connect to the console of one of the routers, and see this log message:

```
*Mar  12 17:18:19.123: %IP-4-DUPADDR: Duplicate address 10.2.2.2 on GigabitEthernet0/0, sourced by 0000.0c9f.f002
```

Which of the answers list an HSRP configuration mistake that would cause the router to list this message? (Choose two answers.)

- a. The two HSRP routers are configured with different HSRP group numbers.
- b. The local router is filtering all incoming HSRP messages.
- c. The two HSRP routers are configured with different HSRP version numbers.
- d. The two HSRP routers have configured different virtual IP addresses.

## Foundation Topics

### FHRP and HSRP Concepts

When networks use a design that includes redundant routers, switches, LAN links, and WAN links, in some cases other protocols are required to both take advantage of that redundancy and to prevent problems caused by it.
