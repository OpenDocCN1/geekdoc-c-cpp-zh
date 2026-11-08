
![](img/79473ea15699e01619d2aa789f5bd43b_778_0.png)

**Figure 26-20** *SPAN Monitor Sessions—Some Dependencies*

**Example 26-16** *Configuring SPAN Monitor Sessions 1 and 2*

```text
! Monitor Session 1
monitor session 1 source interface Gi1/0/11 - 12 rx
monitor session 1 destination interface Gi1/0/21

!
! Monitor Session 2 - the default direction is both, so both does not appear in the
! command.
monitor session 2 source vlan 11
monitor session 2 destination interface Gi1/0/22
```

Once configured, all the network engineer would need to do is start using the network analyzer software on the hosts connected to port Gi1/0/21 (for SPAN session 1) or port Gi1/0/22 (for SPAN session 2). The details of how to use the output of the analyzer go beyond the scope of this book. However, when using the analyzer, if the capture does not appear to be working in that no frames are being captured, you can check the SPAN sessions with the **show monitor session all** command, as listed in Example 26-17. This command lists the configuration of each monitor session, including any default settings not listed in the configuration commands.

**Example 26-17** *Configuring a SPAN Monitor Session 1 Per Figure 26-18*

```text
SW1# show monitor session all

Session 1
---------
Type                  : Local Session
Source Ports
    RX Only           : Gi1/0/11-12
Destination Ports     : Gi1/0/21
    Encapsulation     : Native
    Ingress           : Disabled

Session 2
---------
Type                  : Local Session
Source VLANs
    Both              : 11
Destination Ports     : Gi1/0/22
```

## Choosing to Limit SPAN Sources

Good engineers do not just decide to use SPAN on the entire VLAN in both directions without giving any thought to what they really need to capture. Instead, engineers think about what needs to be captured, how to get SPAN to capture that traffic, and *capture as little other traffic as possible*.

For example, if the goal of a capture is to see traffic sent by the switch to all hosts in a VLAN, then create a SPAN session with that VLAN as the source, for the transmit direction. However, if you only really care about 3 of the 12 access ports in that VLAN, take the time to configure the SPAN session just for those ports.

It is also easy to make poor choices regarding the traffic direction—choices that work, but that overload the SPAN destination port. For instance, Figure 26-21 represents the SPAN logic applied to the four ports in the same VLAN (11), with a command like monitor session 1 source VLAN 11 both. Each Tx and Rx bubble represents a location where SPAN is monitoring either transmit or receive traffic. The figure then focuses on one Ethernet frame, sent by PC1 to PC3.

![](img/79473ea15699e01619d2aa789f5bd43b_780_0.png)

**Figure 26-21** *Frame from PC1 to PC3—SPAN Copies Twice*

Enabling SPAN in this VLAN, for both directions, means that SPAN monitors both transmit and receive traffic on each port in that VLAN. The single frame shown in the figure would be seen by SPAN monitoring twice (on the receive function of the port on the left, and the transmit function of the port on the right), so SPAN would send two copies of this single frame to the destination port. Overall, this SPAN session would send twice as many frames as necessary out the SPAN destination port.

A much more efficient choice would be to use either the receive or transmit direction for the SPAN session. Figure 26-22 shows the logic, but now with the Tx bubbles removed, implying that SPAN has been enabled in the receive direction only. As a result, that one example frame sent by PC1 to PC3 is seen only once by SPAN’s monitoring logic, and only one copy of the frame is sent to the destination port.

![](img/79473ea15699e01619d2aa789f5bd43b_780_1.png)

**Figure 26-22** *Frame from PC1 to PC3—SPAN Copies Once*

## Chapter Review

One key to doing well on the exams is to perform repetitive spaced review sessions. Review this chapter’s material using either the tools in the book, DVD, or interactive tools for the same material found on the book’s companion website. Refer to the “Your Study Plan” element for more details. Table 26-3 outlines the key review elements and where you can find them. To better track your study progress, record when you completed these activities in the second column.

**Table 26-3** Chapter Review Tracking

| Review Element | Review Date(s) | Resource Used |
|---|---|---|
| Review key topics |  | Book, DVD/website |
| Review key terms |  | Book, DVD/website |
| Answer DIKTA questions |  | Book, PCPT |
| Do labs |  | Blog |
| Review memory tables |  | Book, DVD/website |
| Review config checklists |  | Book, DVD/website |
| Review command tables |  | Book |

### Review All the Key Topics

![](img/79473ea15699e01619d2aa789f5bd43b_781_0.png)

**Table 26-4** Key Topics for Chapter 26

| Key Topic Element | Description | Page Number |
|---|---|---|
| Figure 26-2 | The SNMP Get Request and Get Response message flow | 696 |
| Figure 26-3 | SNMP notification with SNMP Trap messages | 697 |
| Figure 26-5 | The use of SNMP RO and RW communities with SNMP Get and Set | 699 |
| List | SNMPv3 security features | 699 |
| Figure 26-7 | SNMPv3 snmp-server group command syntax and meaning | 705 |
| Table 26-2 | SNMPv3 security levels and the actions taken for each | 705 |
| Figure 26-9 | Linkage and requirements between the snmp-server group and snmp-server user commands | 707 |
| Figure 26-10 | Linkage between SNMPv3 Trap host definition, user, and group | 710 |
| Figure 26-12 | IP SLA ICMP-Echo operation concepts | 714 |
| Example 26-14 | Output that shows counters of success/failure of IP SLA operations | 716 |
| Example 26-15 | Output of IP SLA history for an ICMP-Echo operation | 717 |
| Figure 26-16 | SPAN copying frames to a destination port | 720 |
| Figure 26-17 | SPAN monitoring in Transmit direction, concepts | 720 |
| List | SPAN exceptions and dependencies | 722 |

### Key Terms You Should Know

Simple Network Management Protocol, SNMP community, read-only community, read-write community, notification community, SNMP Get, SNMP Set, SNMP Trap, SNMP Inform, Management Information Base (MIB), SNMPv2c, SNMPv3, Network Management System (NMS), SNMP manager, SNMP agent, MIB view, service level agreement (SLA), IP Service Level Agreement (IP SLA), IP SLA operation, ICMP-Echo operation, IP SLA source, IP SLA responder, Round Trip Time (RTT), Switched Port Analyzer (SPAN), SPAN source port, SPAN source VLAN, SPAN destination port, network analyzer, Local SPAN, SPAN monitor session (SPAN session)

### Command References

Tables 26-5 and 26-6 list configuration and verification commands used in this chapter. As an easy review exercise, cover the left column in a table, read the right column, and try to recall the command without looking. Then repeat the exercise, covering the right column, and try to recall what the command does.

**Table 26-5** Chapter 26 Configuration Command Reference

| Command | Description |
|---|---|
| SNMP Configuration Commands | |
| snmp-server community communitystring RO [ipv6 acl-name] [acl-name] | Configures an SNMPv1 or SNMPv2c community string that allows reads (Get and related messages), and also enables the SNMP agent if not yet enabled by another snmp-server command. Optionally enables ACL filtering of the incoming SNMP messages that use this community string. |
| snmp-server community communitystring RW [ipv6 acl-name] [acl-name] | Configures an SNMPv1 or SNMPv2c community string that allows both write and read (Get and Set messages), and also enables the SNMP agent if not yet enabled by another snmp-server command. Optionally enables ACL filtering of the incoming SNMP messages that use this community string. |
| snmp-server location text-describing-location | Defines the text setting of an SNMP variable meant to identify the location of the device. |
| snmp-server contact contact-name | Defines the text setting of an SNMP variable meant to identify the person to contact for questions about the device. |
| snmp-server host hostname \| ip-address version 2c community-string | Identifies one SNMP manager (NMS) to which to send SNMPv2 Trap messages, using the listed notification community. |
| snmp-server host hostname \| ip-address informs version 2c community-string | Identifies one SNMP manager (NMS) to which to send SNMPv2 Inform messages, using the listed notification community. |
| snmp-server enable traps | Enables the SNMP agent to send all supported Traps/Inform messages to any NMS hosts defined with the snmp-server host command. |
