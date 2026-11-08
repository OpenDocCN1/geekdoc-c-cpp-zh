
## Review All the Key Topics

**Table 18-5** Key Topics for Chapter 18

| Key Topic Element | Description | Page Number |
|---|---|---:|
| List | Four QoS characteristics | 491 |
| List | Voice call QoS requirements | 494 |
| List | Video QoS requirements | 494 |
| Figure 18-6 | IP Precedence and IP DSCP marking fields | 499 |
| Figure 18-7 | 802.1Q CoS marking fields | 500 |
| Figure 18-10 | Trust boundary with IP Phones | 502 |
| Figure 18-14 | Queuing components | 504 |
| Figure 18-17 | LLQ scheduling logic with a priority queue | 506 |
| List | A strategy for using queuing (congestion management) to prioritize traffic | 507 |
| List | Logic steps for shapers and policers | 508 |
| List | Key features of policers | 510 |
| List | Key features of shapers | 512 |

![](img/79473ea15699e01619d2aa789f5bd43b_570_0.png)

## Key Terms You Should Know

marking, classification, quality of service (QoS), IP Precedence (IPP), Differentiated Services Code Point (DSCP), Class of Service (CoS), bandwidth, delay, jitter, loss, queuing, priority queue, round robin, policing, shaping, Differentiated Services (DiffServ), policing rate, shaping rate

- After you have written every term you can remember into the mind map, review your notes for other terms, or add any terms from this list that you did not happen to add to your mind map:

  application signature, Assured Forwarding (AF), AutoQoS, bandwidth, Class of Service (CoS), Class Selector (CS), classification, delay, Differentiated Services (DiffServ), Differentiated Services Code Point (DSCP), Expedited Forwarding (EF), Integrated Services (IntServ), IP Precedence (IPP), jitter, loss, low latency queue, marking, MPLS Experimental Bits, Network Based Application Recognition (NBAR), one-way delay, policing, policing rate, Priority Code Point (PCP), priority queue, quality of experience (QoE), Quality of Service (QoS), queuing, Real-time Transport Protocol (RTP), round robin, round-trip delay, shaping, shaping rate, tail drop, TCP synchronization, TCP window, time interval (shaper), traffic class, trust boundary, Type of Service (ToS)

Appendix E, “Mind Map Solutions,” lists sample mind map answers. If you choose to use mind map software, rather than paper, you might want to remember where you stored your mind map files. Table P4-2 lists the mind maps for this part review and a place to record those filenames.

**Table P4-2** Configuration Mind Maps for Part IV Review

| Map | Description | Where You Saved It |
| --- | --- | --- |
| 1 | Command Mind Map |  |
| 2 | QoS Terminology Mind Map |  |

## Do Labs

Depending on your chosen lab tool, here are some suggestions for what to do in lab:

- **Pearson Network Simulator:** If you use the full Pearson CCNA simulator, focus more on the configuration scenario and troubleshooting scenario labs associated with the topics in this part of the book. These types of labs include a larger set of topics, and work well as Part Review activities. (See the Introduction for some details about how to find which labs are about topics in this part of the book.)

- **Config Labs:** In your idle moments, review and repeat any of the Config Labs for this book part in the author's blog; launch from http://blog.certskills.com/ccna and navigate to **Hands-On > Config Lab**.

- **Other:** If using other lab tools, here are a few suggestions: When building ACL labs, you can test with Telnet (port 23), SSH (port 22), ping (ICMP), and traceroute (UDP) traffic as generated from an extra router. So, do not just configure the ACL; make an ACL that can match these types of traffic, denying some and permitting others, and then test.

![](img/79473ea15699e01619d2aa789f5bd43b_573_0.png)

Part V completes this book’s many chapters focused on IPv4 routing and related topics. Part II shows how to learn routes with various IPv4 routing protocols. Part III discusses WAN options and how to route IP packets over those WANs. Part IV discusses services over IPv4 networks, both to secure the network with ACLs and to improve the quality of user experience with QoS. Part V wraps up the parts focused on IPv4 routing with a couple of specific topics centered on the edge of the LAN, topping it off with an IPv4 troubleshooting discussion.

This part begins by drilling down into the device and configuration options for routing between LAN-based subnets. Those options include routers and Layer 3 switches, with a variety of configuration variations. This chapter works through all those variations, through to the point of troubleshooting each.

This part’s second chapter (20) looks at a related topic: how to make the default gateway (router) function have redundancy for better availability. So, while Chapter 19 shows the various ways to configure routers to have an address connected to a LAN subnet, Chapter 20 then shows how multiple routers connected to the same subnet can cooperate to provide redundancy and better availability through a protocol: Hot Standby Router Protocol (HSRP).

Every topic related to IPv4 routing in this book has some troubleshooting aspect to learn per the current exam topics. To that end, this part’s final chapter (21) caps this book’s IPv4 routing discussions with a chapter devoted to IPv4 troubleshooting. Many of the earlier chapters in this book already discussed troubleshooting of the content in that same chapter or part. Chapter 21 reviews some of the basics that you may not have thought about since your ICND1 studies, and serves as a great review before moving on to Part VI, which is about IPv6.

## Part V

## IPv4 Routing and Troubleshooting

- **Chapter 19:** IPv4 Routing in the LAN
- **Chapter 20:** Implementing HSRP for First-Hop Routing
- **Chapter 21:** Troubleshooting IPv4 Routing
- **Part V Review**

4. An engineer has successfully configured a Layer 3 switch with SVIs for VLANs 2 and 3. Hosts in the subnets using VLANs 2 and 3 can ping each other with the Layer 3 switch routing the packets. Next week, the network engineer receives a call that those same users can no longer ping each other. If the problem is with the Layer 3 switching function, which of the following could have caused the problem? (Choose two answers.)

   a. Six (or more) out of ten working VLAN 2 access ports failing due to physical problems
   b. A shutdown command issued from interface VLAN 4 configuration mode
   c. VTP on the switch removing VLAN 3 from the switch’s VLAN list
   d. A shutdown command issued from interface VLAN 2 configuration mode

5. A LAN design uses a Layer 3 EtherChannel between two switches SW1 and SW2, with Port-Channel interface 1 used on both switches. SW1 uses ports G0/1, G0/2, and G0/3 in the channel. Which of the following are true about SW1’s configuration to make the channel be able to route IPv4 packets correctly? (Choose two answers.)

   a. The ip address command must be on the port-channel 1 interface.
   b. The ip address command must be on interface G0/1 (lowest numbered port).
   c. The port-channel 1 interface must be configured with the no switchport command.
   d. Interface G0/1 must be configured with the routed port command.

6. A LAN design uses a Layer 3 EtherChannel between two switches SW1 and SW2, with port-channel interface 1 used on both switches. SW1 uses ports G0/1 and G0/2 in the channel. However, only interface G0/1 is bundled into the channel and working. Think about the configuration settings on port G0/2 that could have existed before adding G0/2 to the EtherChannel. Which answers identify a setting that could prevent IOS from adding G0/2 to the Layer 3 EtherChannel? (Choose two answers.)

   a. A different STP cost (spanning-tree cost value)
   b. A different speed (speed value)
   c. A default setting for switchport (switchport)
   d. A different access VLAN (switchport access vlan vlan-id)

## Foundation Topics

### VLAN Routing with Router 802.1Q Trunks

Almost all enterprise networks use VLANs. To route IP packets in and out of those VLANs, some devices (either routers or Layer 3 switches) need to have an IP address in each subnet and have a connected route to each of those subnets. Then the IP addresses on those routers or Layer 3 switches can serve as the default gateways in those subnets.
