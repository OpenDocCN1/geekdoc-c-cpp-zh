
**VTP pruning** The VTP feature by which switches dynamically choose interfaces on which to prevent the flooding of frames in certain VLANs, when those frames do not need to go to every switch in the network.

**VTP server mode** One of three sets of operating characteristics (modes) in VTP. Switches in server mode can configure VLANs, tell other switches about the changes, and learn about VLAN changes from other switches.

**VTP synchronization** The process by which switches that use VTP exchange VTP messages and realize that one switch now has an updated VLAN configuration database (one that has a higher revision number), resulting in messages that allow the rest of the switches to learn the contents of that updated configuration database.

**VTP transparent mode** One of three operating characteristics (modes) in VTP. Switches in transparent mode can configure VLANs, but they do not tell other switches about the changes, and they do not learn about VLAN changes from other switches; however, they can pass VTP messages between other switches that use VTP server and client modes.

## W

**WAN edge** The device (typically a router) at enterprise sites that connects to private WAN links, therefore sitting at the edge of the WAN.

**WAN link** Another term for leased line.

**WAN service provider** A company that provides private WAN services to customers; the company may have a heritage as a telco or cable company.

**wildcard mask** The mask used in Cisco IOS ACL commands and OSPF and EIGRP network commands.

**wireless access point (AP)** A wireless LAN device that provides a means for wireless clients to send data to each other and to the rest of a wired network. The wireless access point connects to both the wireless LAN and the wired Ethernet LAN.

**write community** *See read-write community.*

## X

**XML (eXtensible Markup Language)** A popular language used to represent data in a way that is readable both to software and to computers, as defined by the World Wide Web (W3C) consortium.

## Z

**zero subnet** For every classful IPv4 network that is subnetted, the one subnet whose subnet number has all binary 0s in the subnet part of the number. In decimal, the 0 subnet can be easily identified because it is the same number as the classful network number.

![](img/79473ea15699e01619d2aa789f5bd43b_907_0.png)

## Index

### Symbols

- 2-way state (neighbor relationships), 186, 628
- 3G wireless, 393
- 4G wireless, 393
- 802.1D STP, 58, 62
- 802.1Q, 20-21
  - headers, 500-501
  - trunking. *See ROAS*
- 802.1w RSTP
  - defined, 58
  - port roles, 60
  - port states, 62
- 802.11 headers, 501

### A

- aaa authentication login default command, 149
- aaa new-model command, 149
- AAA servers
  - authentication
    - configuration, 148-150
    - login authentication rules, 150
    - login process, 147
    - TACACS+/RADIUS protocols, 148
  - configuring for 802.1x, 145
  - defining, 149
- enabling, 149
- username/passwords, verifying, 145
- aaS (as a Service), 742
- ABR (Area Border Router), 190, 625
  - interface OSPF areas, verifying, 210-211
  - OSPFv2 multiarea configuration, 209-210
  - OSPFv3 multiarea configuration, 625
- access
  - Internet, 389
    - *cable Internet*, 391
    - *DSLs (digital subscriber lines)*, 390-391
    - *fiber*, 393
    - *WANs*, 389
    - *wireless WANs*, 392-393
  - IPv6 restrictions, 685
  - public cloud services
    - *Internet*, 745-746
    - *private WANs*, 746-749
    - *VPNs*, 747
  - securing with IEEE 802.1x, 144-146
    - *AAA servers, configuring*, 145
    - *authentication process*, 145
    - *EAP*, 146
    - *switches as 802.1x authenticators*, 145
    - *username/password combinations, verifying*, 145
- access-class command, 486
- access control lists. *See ACLs*
- Access Control Server (ACS), 147
- access interfaces, 24, 113-114
- access layer switches, 156-157
- access links
  - MetroE, 365
  - MPLS, 378
- access-list command, 445, 457, 463-466, 486
  - building ACLs with, 454
  - examples and logic explanations, 467
  - extended numbered ACL
    - configuration commands, 467
  - keywords
    - *any, 448*
    - *deny, 448-449*
    - *log, 452*
    - *permit, 445, 448-449*
    - *tcp keyword, 464*
    - *udp keyword, 464*
  - reverse engineering from ACL to
    - address range, 454-456
- ACI (Application Centric Infrastructure), 773-774
- ACLs (access control lists), 586
  - ACL Analysis tool, 777-778
  - classification, 497
  - comparison of ACL types, 442-443
  - extended numbered ACLs
    - *configuration, 467-470*
    - *matching protocol, source IP, and destination IP, 463-464*
    - *matching TCP and UDP port numbers, 464-467*
    - *overview, 462*
- GRE tunnel issues, 409-410
- implementation considerations, 476-477
- IPv4, 666-667
- IPv6, 664-666
  - *access-list commands, building, 678-679*
  - *access restrictions, 685*
  - *blocking, 683*
  - *capabilities, 669*
  - *extended, 674-678*
  - *filtering ICMPv6 NDP messages, 679-683*
  - *filtering policies, 668*
  - *ICMPv6 message filtering, 668-669*
  - *implicit filtering ICMPv6 NDP messages, 683-684*
  - *IPv4 ACL compared, 666-667*
  - *limitations, 669-670*
  - *logging, 670*
  - *management control, 685*
  - *prefix lengths, 670*
  - *problems, 612*
  - *router originated packets, 670*
  - *standard, configuring, 671-674*
  - *testing, 677*
  - *tunneled traffic matching, 670*
- location and direction, 440-441
- matching packets, 441-442
- named ACLs
  - *configuration, 472*
  - *editing, 473-475*
  - *overview, 471-472*
- numbered ACLs, 475-476
- overview, 440
- QoS tools, compared, 496
- SNMP security, 698
- standard numbered ACLs
  - *access-list command, 454*
  - *command syntax, 445*
  - *configuration examples, 448-452*
  - *list logic, 444-445*
  - *matching any/all addresses, 448*
  - *matching exact IP address, 445-446*
  - *matching subset of address, 446-447*
  - *overview, 443*
  - *reverse engineering from ACL to address range, 454-456*
  - *troubleshooting, 452-453*
  - *verification, 452-453*
  - *wildcard masks, 446-448*
- troubleshooting, 477
  - *ACL behavior in network, 477-479*
  - *ACL interactions with router-generated packets, 483-485*
  - *commands, 479-480*
  - *common syntax mistakes, 481*
  - *inbound ACL filters routing protocol packets, 481-482*
  - *reversed source/destination IP address, 480-481*
- ACL Analysis tool, 777-778
- ACS (Access Control Server), 147
- active HSRP routers, 558
- address blocks. See prefixes
- addresses
  - *families, 619*
  - *global unicast, 593*
  - *IPv4, 197*
  - *IPv6*
    - *assigning to hosts, 595-597*
    - *connectivity, verifying, 600-603*
- *multicast, 682*
  - *router configuration, 598-599*
  - *static route configuration, 599*
  - *unicast, 593-595*
- link, 311-312
- link-local, 595
- MAC, 49
- public cloud assignment services, 756-757
- source/destination, 406
- unique local unicast, 593
- adjacent neighbors, 186, 633
- administrative distance, 177-178
- administratively shutdown interfaces, 49
- ADSL (asymmetric DSL), 391
- advertising
  - *BGP routes, 303-304*
  - *eBGP enterprise public prefixes, 307-308*
  - *subnets to ISPs, 318*
- AF (Assured Forwarding), 502-503
- agents (SNMP), 695
  - *Get/Set messages, 696*
  - *MIB, 697*
  - *NMS polling, 696*
  - *notifications, 696-697*
- algorithms
  - *Dijkstra SPF, 180*
  - *DUAL (Diffusing Update Algorithm), 242-243, 646*
  - *IGP routing protocol algorithm, 175*
  - *SPF (Shortest Path First), 180, 186-188*
  - *STA (spanning-tree algorithm), 48*
- all IP addresses, matching, 448
- alternate ports, 60-61, 91-92
- Amazon Web Services (AWS), 742
