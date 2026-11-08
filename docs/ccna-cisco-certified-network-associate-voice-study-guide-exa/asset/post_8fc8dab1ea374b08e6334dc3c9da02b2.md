
networks is that they do send broadcasts to all neighboring routers, whether or not anything has changed in the routing tables. This design is not very efficient. Also, both versions are limited to 16 hops in a route. This number limits the size of the network to medium-sized organizations anyway. Those medium-sized organizations would be much better served by OSPF or EIGRP and should avoid RIP.

## VoIP Infrastructure Solutions

Now that you've explored the two core components that make up a network infrastructure, it's time to look at the specific VoIP components you'll need on your network. These components include:

- Gateways
- Gatekeepers
- Call Managers
- VoIP Phones

### Gateways

If you need to provide telephone calls only between internal endpoints, you will have no need for a gateway. Such implementations are rare, however, and it is more common to interface your local VoIP network with another telephony provider. This telephony provider may also use VoIP, or it may use traditional PSTN technology. Either way, the device that allows you to communicate with this other telephony network is a gateway. Gateways provide off-network calling (calls within your VoIP network are considered on-network calls). In the Cisco world, a voice gateway is a router that converts VoIP packets into traditional phone network signals and traditional phone network signals into VoIP packets. Chapter 14 covers gateways in depth.

**exam watch**

Gateways are used to connect your VoIP network to both the PSTN and PBX-based phone networks. If a PBX system is used in your organization, a Cisco router can be configured to act as a gateway between the PBX telephone network and your VoIP network. This is very useful during the transition from traditional PBX systems to new VoIP systems.

### Gatekeepers

Gatekeepers serve two purposes in H.323 networks. First, they allow entry by endpoints (IP phones) into the network. H.323 gatekeepers use Registration, Admission, and Status (RAS) messages for network admission. Second, gatekeepers perform address translation. For example, the gatekeeper can convert Tom.Carpenter@sysedco.com to 192.168.12.14. Chapter 14 also covers gatekeepers in greater depth.

### Call Managers

A call manager is used to initiate a call, manage the call, and terminate that call in a VoIP network. Cisco call managers include the Cisco Unified Communications Manager (CUCM) and Cisco Unified Communications Manager Express (CME). Additionally, the small-office/home-office (SOHO) market product is the Unified Communications 500 (UC500) series, which includes call management capabilities. In Chapters 9, 12, and 13, you will explore these call managers in depth.

### VoIP Phones

You may be wondering why VoIP phones are listed in an infrastructure section. The reason is simple: many Cisco VoIP phones act as both a client and an access point to the network. The phone is a client to the network when it acts as a phone. The phone is an access point when it acts as a switch port for a client device. The phone implements a VLAN trunk for the client computers that connect to the phone's switch port. This allows the client computer to exist on one VLAN while the VoIP phone itself exists on another VLAN. A Cisco phone has three ports:

- The external Ethernet port for connection to a Cisco switch, which provides the actual infrastructure network connectivity
- The external Ethernet port for connection to a PC, which provides networking functionality to the PC in the work area of the VoIP phone
- The internal Ethernet port for VoIP traffic, which is a virtual port within the phone allowing for differentiation between the VoIP traffic and the PC traffic

The Cisco VoIP phones support 802.1Q tagging for VLAN identification. They do not support Inter-Switch Link (ISL) encapsulation. Additionally, some Cisco phones do not support a PC Ethernet port. If this feature is important to your implementation, be sure to select a phone model that implements the PC port. The 7940G, 7960G, and 7970G models all support the PC port. They also support inline power for PoE power solutions. The 7910G model does not support the PC port; however, the 7910G+SW model does, with the +SW signifying a switch is integrated into the model. Additionally, the 7905G model does not support the PC switch port, but the 7912G model does. As you can see, there is a lot of variety in the Cisco phones. Cisco sells and supports both wired and wireless IP phones, which are covered in more detail in Chapter 10.

## CERTIFICATION OBJECTIVE 2.02

### 640-460: Describe the Purpose of VLANs in a VoIP Environment

Cisco switches, as well as most enterprise switches, support VLANs. VLANs are useful in a VoIP environment, and you'll need to understand why for the CCNA Voice and CCVOICE exams. You should understand what a VLAN is, how the VLAN trunking protocol works, and the use of VLANs in VoIP networks.

### VLANs and VoIP

VLANs provide multiple broadcast domains within a single switch or within a switch environment with multiple connected switches. Normally, without VLANs, if a broadcast is sent into a switch port, it is forwarded out on all other switch ports. VLANs allow you to break these ports apart into logical switches. The beauty of this feature is that the VLANs can even span multiple switches using VLAN trunking protocols.

As an example, imagine you have a small 12-port switch. You want six of the ports to be configured with IP addresses from 10.10.10.14 through 10.10.10.19. You want the other six ports to be configured with IP addresses from 10.10.11.14 through 10.10.11.19. While you could statically configure the IP addresses without the requirement of a VLAN, this would not result in separate broadcast domains. The best way to implement this configuration is as follows:

- Create one VLAN for the 10.10.10.x network and another for the 10.10.11.x network.
- Assign the appropriate switch ports to each VLAN.
- Configure the IP addresses appropriately using DHCP or static configurations.

This method results in both separate IP networks and separate broadcast domains. Now, if a broadcast IP message is sent to the switch from the PC at 10.10.10.17, it will only be forwarded to the 10.10.10.14, .15, .16, .18, and .19 addresses. It will not be forwarded to the six ports in the 10.10.11.x network.

In addition to this broadcast domain isolation, which can greatly increase network performance, VLANs can improve manageability and security. The logical grouping of devices based on function rather than location can make for simpler management. This logical group occurs because you are no longer restricted to a single switch acting as a broadcast domain. Instead you can have three ports on one switch, five ports on another, and four ports on another, all participating in the same VLAN.

VLANs can improve security in that they can provide containment or separation within your network. For example, when an insecure client connects, it can be placed on a VLAN with limited access to the rest of the network (via ACLs in routers or simply because of the lack of routing configuration). You can also create "Internet-only" VLANs for guests so they can access the Internet but nothing else.

But how does all this help with VoIP networks? VLANs allow the voice communications to be separated from and treated differently than the standard data communications. In fact, newer Cisco switches support a specific type of VLAN known as a voice VLAN. VLANs work based on VLAN tagging. For the VLANs to work properly, all devices in the path of communications from the initiating VLAN tag point to the drop-off point must use the same tagging protocol such as 802.1Q.

In a Cisco network, the Cisco Discovery Protocol (CDP) is used by the VoIP phones to determine the proper voice VLAN during startup. When the Cisco phone includes an Ethernet switch, it will tag the voice communications with the voice VLAN tag and leave the PC-originating frames untagged. The actual infrastructure switch may still tag these PC frames for normal VLAN operations.

**exam watch**

Remember that the VLAN Trunking Protocol (VTP) is used to keep the VLAN databases up-to-date on all Cisco switches. VTP is not the actual trunking protocol (that's 802.1Q), but it is a Cisco protocol used to maintain the VLAN information across switches.
