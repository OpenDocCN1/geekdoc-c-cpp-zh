
| Key Topic Element | Description | Page Number |
| --- | --- | --- |
| Figure 17-4 | Drawing of the IP header followed by a TCP header | 464 |
| Figure 17-5 | Syntax and notes about matching TCP and UDP ports with extended ACL access-list commands | 465 |
| Figure 17-7 | Logic and syntax to match TCP source ports | 466 |
| List | Guidelines for using extended numbered IP ACLs | 467 |
| List | Differences between named and numbered ACLs when named ACLs introduced | 471 |
| List | Features enabled by IOS 12.3 ACL sequence numbers | 473 |
| List | ACL implementation recommendations | 476 |
| Checklist | ACL troubleshooting checklist | 478 |
| Figure 17-13 | Example of a router bypassing its outbound ACL logic for packets the router generates | 483 |

### Key Terms You Should Know

extended access list, named access list

### Command References

Tables 17-10 and 17-11 list configuration and verification commands used in this chapter. As an easy review exercise, cover the left column in a table, read the right column, and try to recall the command without looking. Then repeat the exercise, covering the right column, and try to recall what the command does.

**Table 17-10 Chapter 17 ACL Configuration Command Reference**

| Command | Description |
| --- | --- |
| *access-list access-list-number* {deny \| permit} *protocol source source-wildcard destination destination-wildcard* [log] | Global command for extended numbered access lists. Use a number between 100 and 199 or 2000 and 2699, inclusive. |
| *access-list access-list-number* {deny \| permit} *tcp source source-wildcard* [operator *port*] *destination destination-wildcard* [operator *port*] [log] | A version of the access-list command with TCP-specific parameters. |
| *access-list access-list-number remark text* | Defines a remark that helps you remember what the ACL is supposed to do. |
| *ip access-group* {number \| name} [in \| out] | Interface subcommand to enable access lists. |
| *access-class number* \| *name* [in \| out] | Line subcommand to enable either standard or extended access lists on vty lines. |
| *ip access-list* {standard \| extended} *name* | Global command to configure a named standard or extended ACL and enter ACL configuration mode. |
| {deny \| permit} *source* [*source wildcard*] [log] | ACL mode subcommand to configure the matching details and action for a standard named ACL. |
| [deny \| permit] protocol source source-wildcard destination destination-wildcard [log] | ACL mode subcommand to configure the matching details and action for an extended named ACL. |
| [deny \| permit] tcp source source-wildcard [operator [port]] destination destination-wildcard [operator [port]] [log] | ACL mode subcommand to configure the matching details and action for a named ACL that matches TCP segments. |
| remark text | ACL mode subcommand to configure a description of a named ACL. |

**Table 17-11 Chapter 17 EXEC Command Reference**

| Command | Description |
| --- | --- |
| show ip interface [type number] | Includes a reference to the access lists enabled on the interface |
| show access-lists [access-list-number \| access-list-name] | Shows details of configured access lists for all protocols |
| show ip access-lists [access-list-number \| access-list-name] | Shows IP access lists |

### Answers to Earlier Practice Problems

Table 17-12 lists the answers to the practice problems listed in Table 17-6. Note that for any question that references a client, you might have chosen to match port numbers greater than 1023. The answers in this table mostly ignore that option, but just to show one sample, the answer to the first problem lists one with a reference to client ports greater than 1023 and one without. The remaining answers simply omit this part of the logic.

**Table 17-12 Building One-Line Extended ACLs: Answers**

| Criteria | Answer |
| --- | --- |
| 1 | access-list 101 permit tcp host 10.1.1.1 10.1.2.0 0.0.0.255 eq www<br>or<br>access-list 101 permit tcp host 10.1.1.1 gt 1023 10.1.2.0 0.0.0.255 eq www |
| 2 | access-list 102 permit tcp 172.16.4.0 0.0.0.127 172.16.3.0 0.0.0.127 eq telnet |
| 3 | access-list 103 permit icmp 192.168.7.192 0.0.0.63 192.168.7.0 0.0.0.7 |
| 4 | access-list 104 permit tcp 10.2.2.0 0.0.1.255 eq www 10.4.4.0 0.0.3.255 |
| 5 | access-list 105 permit tcp 172.20.1.0 0.0.0.255 eq 23 172.20.44.0 0.0.1.255 |
| 6 | access-list 106 permit tcp 192.168.99.96 0.0.0.15 192.168.176.0 0.0.0.15 eq www |
| 7 | access-list 107 permit icmp 10.55.66.0 0.0.0.127 10.66.55.0 0.0.0.63 |
| 8 | access-list 108 permit ip any any |

## Quality of Service (QoS)

**This chapter covers the following exam topics:**

- 4.0 Infrastructure Services
- 4.3 Describe Basic QoS concepts
    - 4.3.a Marking
    - 4.3.b Device trust
    - 4.3.c Prioritization
        - 4.3.c.(i) Voice
        - 4.3.c.(ii) Video
        - 4.3.c.(iii) Data
    - 4.3.d Shaping
    - 4.3.e Policing
    - 4.3.f Congestion Management

Quality of Service (QoS) refers to tools that network devices can use to manage several related characteristics of what happens to a packet while it flows through a network. Specifically, these tools manage the bandwidth made available to that type of packet, the delay the packet experiences, the jitter (variation in delay) between successive packets in the same flow, and the percentage of packet loss for packets of each class. These tools balance the tradeoffs of which types of traffic receive network resources, and when, giving more preference to some traffic, and less preference to others.

In the entire history of CCNA R&S, the exam topics have not focused on QoS beyond the barest small mention—until this latest version of the ICND2 (200-105) and CCNA (200-125) exams, Cisco adds one major topic, “Describe Basic QoS concepts,” with a list of subitems that list specific QoS tools. As listed in the exam topics, this new QoS material is concepts only—not configuration and verification—and basic.

This chapter works through the QoS tools listed in the exam topics, with an emphasis on the problems they solve and how each tool manages bandwidth, delay, jitter, and loss.

### “Do I Know This Already?” Quiz

Take the quiz (either here, or use the PCPT software) if you want to use the score to help you decide how much time to spend on this chapter. The answers are at the bottom of the page following the quiz, and the explanations are in DVD Appendix C and in the PCPT software.

**Table 18-1** “Do I Know This Already?” Foundation Topics Section-to-Question Mapping

| Foundation Topics Section | Questions |
| --- | --- |
| Introduction to QoS | 1 |
| Classification and Marking | 2, 3 |
| Congestion Management (Queuing) | 4 |
| Shaping and Policing | 5 |
| Congestion Avoidance | 6 |

1. Which of the following attributes do QoS tools manage? (Choose three answers.)
    a. Bandwidth
    b. Delay
    c. Load
    d. MTU
    e. Loss

2. Which of the following QoS marking fields could remain with a packet while being sent through four different routers, over different LAN and WAN links? (Choose two answers.)
    a. CoS
    b. IPP
    c. DSCP
    d. MPLS EXP

3. Which of the following are available methods of classifying packets in DiffServ on Cisco routers? (Choose three answers.)
    a. Matching the IP DSCP field
    b. Matching the 802.1p CoS field
    c. Matching fields with an extended IP ACL
    d. Matching the SNMP Location variable

4. Which of the following behaviors is applied to a low latency queue in a Cisco router or switch?
    a. Congestion management
    b. Shaping
    c. Policing
    d. Priority scheduling
    e. Round robin scheduling

5. Think about a policing function that is currently working, and also think about a shaping function that is also currently working. That is, the current bit rate of traffic exceeds the respective policing and shaping rates. Which statements are true about these features? (Choose two answers.)
    a. The policer may or may not be discarding packets.
    b. The policer is definitely discarding packets.
    c. The shaper may or may not be queuing packets to slow down the sending rate.
    d. The shaper is definitely queuing packets to slow down the sending rate.

6. A queuing system has three queues serviced with round robin scheduling and one low latency queue that holds all voice traffic. Round robin queue 1 holds predominantly UDP traffic, while round robin queues 2 and 3 hold predominantly TCP traffic. The packets in each queue happen to have a variety of DSCP markings per the QoS design. In which queues would it make sense to use a congestion avoidance (drop management) tool? (Choose two answers.)
    a. The LLQ
    b. Queue 1
    c. Queue 2
    d. Queue 3

### Foundation Topics

#### Introduction to QoS

Routers typically sit at the WAN edge, with both WAN interfaces and LAN interfaces. Those LAN interfaces typically run at much faster speeds, while the WAN interfaces run at slower speeds. While that slower WAN interface is busy sending the packets waiting in the router, hundreds or even thousands more IP packets could arrive in the LAN interfaces, all needing to be forwarded out that same WAN interface. What should the router do? Send them all, in the same order in which they arrived? Prioritize the packets, to send some earlier than others, preferring one type of traffic over another? Discard some of the packets when the number of packets waiting to exit the router gets too large?

That first paragraph described some of the many classic Quality of Service (QoS) questions in networking. QoS refers to the tools that networking devices use to apply some different treatment to packets in the network as they pass through the device. For instance, the WAN edge router would queue packets waiting for the WAN interface to be available. The router could also use a queue scheduling algorithm to determine which packets should be sent next, using some other order than the arrival order—giving some packets better service, and some worse service.
