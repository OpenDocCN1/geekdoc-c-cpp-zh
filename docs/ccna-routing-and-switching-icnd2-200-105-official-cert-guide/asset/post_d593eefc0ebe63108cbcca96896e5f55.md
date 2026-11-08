
**out-of-band** Traffic that does not share the same network paths with user data traffic. Network management traffic is often sent OOB.

**overlapping subnets** An (incorrect) IP subnet design condition in which one subnet’s range of addresses includes addresses in the range of another subnet.

## P

**packet switching** A WAN service in which each DTE device connects to a telco using a single physical line, with the possibility of being able to forward traffic to all other sites connected to the same service. The telco switch makes the forwarding decision based on an address in the packet header.

**PAgP** Port Aggregation Protocol (PAgP) is a messaging protocol defined by Cisco which enables two neighboring devices to realize that they have multiple parallel links connecting to each other, and then to decide which links can be combined into an EtherChannel.

**PAP** Password Authentication Protocol. A PPP authentication protocol that allows PPP peers to authenticate one another, characterized by the weak authentication it uses by sending the username and password as clear text values.

**partial mesh** A network topology in which more than two devices could physically communicate, but by choice, only a subset of the pairs of devices connected to the network is allowed to communicate directly.

**partial update** With IP routing protocols, the general concept that a routing protocol update lists a subset of all known routes. *See also* full update.

**path attribute** In BGP, one of many types of information that describe a route (path), with the path attributes being used for best path selection and other purposes.

**periodic update** With routing protocols, the concept that the routing protocol advertises routes in a routing update on a regular periodic basis. This is typical of distance vector routing protocols.

**permanent virtual circuit (PVC)** A preconfigured communications path between two Frame Relay DTEs, identified by a local DLCI on each Frame Relay access link, that provides the functional equivalent of a leased circuit but without a physical leased line for each VC.

**permit** An action taken with an ACL that implies that the packet is allowed to proceed through the router and be forwarded.

**ping** Packet Internet Groper. An Internet Control Message Protocol (ICMP) echo message and its reply; ping often is used in IP networks to test the reachability of a network device.

**Platform as a Service (PaaS)** A cloud service intended for software developers as a development platform, with a variety of tools useful to developers already installed, so that the developer can focus on developing software rather than on creating a good development environment.

**point of presence (PoP)** A term used from a service provider’s (SP) perspective to refer to a service provider’s installation that is purposefully located relatively near to customers, with several spread around major cities, so that the distance from each customer site to one of the SP’s PoPs is short.

**point-to-multipoint** *See* hub-and-spoke.

**point-to-point** From a topology perspective, any topology that has two and only two devices that can send messages directly to each other.

**point-to-point edge port** With 802.1w RSTP, a port type in which the switch believes the port is connected to a single other device, specifically one that is not another switch.

**point-to-point port** With 802.1w RSTP, a port type in which the switch believes the port is connected to a single other device, specifically another switch.

**poisoned route** A route advertisement in which the routing protocol assigns the route a maximum metric that represents infinity, as a means to advertise that the route is no longer usable.

**policing** A QoS tool that monitors the bit rate of the messages passing some point in the processing of a networking device, so that if the bit rate exceeds the policing rate for a period of time, the policer can discard excess packets to lower the rate.

**policing rate** The bit rate at which a policer compares the bit rate of packets passing through a policing function, for the purpose of taking a different action against packets that conform (are under) to the rate versus those that exceed (go over) the rate.

**port** (Multiple definitions) 1) In TCP and UDP, a number that is used to uniquely identify the application process that either sent (source port) or should receive (destination port) data. 2) In LAN switching, another term for switch interface.

**PortChannel** One term Cisco switches use to reference a bundle of links that are, in some respects, treated like a single link. Other similar terms include EtherChannel and Channel-group.

**PortFast** A switch STP feature in which a port is placed in an STP forwarding state as soon as the interface comes up, bypassing the listening and learning states. This feature is meant for ports connected to end-user devices.

**PPP over Ethernet (PPPoE)** A specific protocol designed to encapsulate PPP frames inside Ethernet frames, for the purpose of delivering the PPP frames between two devices, effectively creating a point-to-point tunnel between the two devices.

**PPP** Point-to-Point Protocol. A data link protocol that provides router-to-router and host-to-network connections over synchronous and asynchronous circuits.

**PPPoE session** The logical connection between two PPPoE endpoints, used to track the state of the ability of each endpoint to send PPPoE frames to the other endpoint.

**prefix notation** A shorter way to write a subnet mask in which the number of binary 1s in the mask is simply written in decimal. For instance, /24 denotes the subnet mask with 24 binary 1 bits in the subnet mask. The number of bits of value binary 1 in the mask is considered to be the prefix.

**Priority Code Point (PCP)** The formal term for the 3-bit field in the 802.1Q header intended for marking and classifying Ethernet frames for the purposes of applying QoS actions. Another term for Class of Service (CoS).

**priority queue** In Cisco queuing systems, another term for a low latency queue (LLQ).

**private address** Several Class A, B, and C networks that are set aside for use inside private organizations. These addresses, as defined in RFC 1918, are not routable through the Internet.

**private cloud** A cloud computing service in which a company provides its own IT services to internal customers inside the same company but by following the practices defined as cloud computing.

**private IP network** One of several classful IPv4 network numbers that will never be assigned for use in the Internet, meant for use inside a single enterprise.

**private key** A secret value used in public/private key encryption systems. Either encrypts a value that can then be decrypted using the matching public key, or decrypts a value that was previously encrypted with the matching public key.

**problem isolation** The part of the troubleshooting process in which the engineer attempts to rule out possible causes of the problem, narrowing the possible causes until the root cause of the problem can be identified.

**protocol type** A field in the IP header that identifies the type of header that follows the IP header, usually a Layer 4 header, such as TCP or UDP. ACLs can examine the protocol type to match packets with a particular value in this header field.

**provider edge (PE)** A term used by service providers, both generally and also specifically in MPLS VPN networks, to refer to the SP device in a point of presence (PoP) that connects to the customer’s network, and therefore sits at the edge of the SP’s network.

**public cloud** A cloud computing service in which the cloud provider is a different company than the cloud consumer.

**public key** A publicly available value used in public/private key encryption systems. Either encrypts a value that can then be decrypted using the matching private key, or decrypts a value that was previously encrypted with the matching private key.

**PVC** *See* permanent virtual circuit.

**PVST+** An STP option in Cisco switches that creates an STP instance per VLAN while using the STP (802.1D) protocol for those STP instances.

## Q

**Quality of Experience (QoE)** The users’ perception of the quality of their experience in using applications in the network.

**Quality of Service (QoS)** The performance of a message, or the messages sent by an application, in regard to the bandwidth, delay, jitter, or loss characteristics experienced by the message(s).

**queuing** The process by which networking devices hold packets in memory while waiting on some constrained resource; for example, when waiting for the outgoing interface to become available when too many packets arrive in a short period of time.
