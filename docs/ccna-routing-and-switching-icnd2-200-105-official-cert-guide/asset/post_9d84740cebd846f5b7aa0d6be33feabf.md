
## R

**RADIUS** A security protocol often used for user authentication, including being used as part of the IEEE 802.1x messages between an 802.1x authenticator (typically a LAN switch) and a AAA server.

**RAM** Random-access memory. A type of volatile memory that can be read and written by a microprocessor.

**rapid elasticity** One of the five key attributes of a cloud computing service as defined by NIST, referring to the fact that the cloud service reacts to requests for new services quickly, and it expands (is elastic) to the point of appearing to be a limitless resource.

**Rapid PVST+** An STP option in Cisco switches that creates an STP instance per VLAN while using the **RSTP (802.1w)** protocol for those STP instances.

**Rapid Spanning Tree Protocol (RSTP)** Defined in IEEE 802.1w, it defines an improved version of STP that converges much more quickly and consistently than STP (802.1d).

**reachability** In BGP, a reference to the goal of BGP to advertise about a prefix/length so that other routers know that the prefix is reachable through the router that advertised the prefix.

**read-only community** An SNMP community (a value that acts as a password), defined on an SNMP agent, which then must be supplied by any SNMP manager that sends the agent any messages asking to learn the value of a variable (like SNMP Get and GetNext requests).

**read-write community** An SNMP community (a value that acts as a password), defined on an SNMP agent, which then must be supplied by any SNMP manager that sends the agent any messages asking to set the value of a variable (like SNMP Set requests).

**Real-time Transport Protocol (RTP)** The transport layer protocol used by many voice and video applications, including between Cisco IP Telephone and other Cisco Unified Communications products.

**reference bandwidth** In OSPF, a configurable value for the OSPF routing process, used by OSPF when calculating an interface's default OSPF cost metric, calculated as the interface's bandwidth divided by the reference bandwidth.

**Regional Internet Registry (RIR)** The generic term for one of five current organizations that are responsible for assigning the public, globally unique IPv4 and IPv6 address space.

**registry prefix** In IPv6, the prefix that describes a block of public, globally unique IPv6 addresses assigned to a Regional Internet Registry by ICANN.

**reported distance** From one EIGRP router's perspective, the metric for a subnet as calculated on a neighboring router and reported in a routing update to the first router.

**Representational State Transfer (REST)** A type of API that allows two programs that reside on separate computers to communicate, with the messages used to move requests and data across the network using HTTP messages Get, Post, Put, and Delete.

**resource pooling** One of the five key attributes of a cloud computing service as defined by NIST, referring to the fact that the cloud provider treats its resources as a large group (pool) of resources that its cloud management systems then allocate dynamically based on self-service requests by its customers.

**REST** *See* Representational State Transfer.

**REST API** Any API that uses Representational State Transfer (REST), which means that the two programs, on separate computers, use HTTP messages to request and transfer data.

**RESTful API** A turn of phrase that means that the API uses REST.

**reverse route** From one host's perspective, for packets sent back to the host from another host, the route over which the packet travels.

**RFC** Request For Comments. A document used as the primary means for communicating information about the TCP/IP protocols. Some RFCs are designated by the Internet Architecture Board (IAB) as Internet standards, and others are informational. RFCs are available online from numerous sources, including www.rfc-editor.org.

**RIP** Routing Information Protocol. An interior gateway protocol (IGP) that uses distance vector logic and router hop count as the metric. RIP Version 1 (RIPv1) has become unpopular. RIP Version 2 (RIPv2) provides more features, including support for VLSM.

**root bridge** *See* root switch.

**root cost** The STP cost from a nonroot switch to reach the root switch, as the sum of all STP costs for all ports out which a frame would exit to reach the root.

**root port** In STP, the one port on a nonroot switch in which the least-cost Hello is received. Switches put root ports in a forwarding state.

**root switch** In STP, the switch that wins the election by virtue of having the lowest bridge ID, and, as a result, sends periodic Hello BPDUs (default, 2 seconds).

**round robin** A queue scheduling algorithm in which the scheduling algorithm services one queue, then the next, then the next, and so on, working through the queues in sequence.

**round-trip delay** The elapsed time from sending the first bit of data at the sending device until the last bit of that data is received on the destination device, plus the time waiting for the destination device to form a reply, plus the elapsed time for that reply message to arrive back to the original sender.

**Round Trip Time (RTT)** The time it takes a message to go from the original sender to the receiver, plus the time for the response to that message to be sent back.

**routable protocol** *See* routed protocol.

**route redistribution** A method by which two routing protocol processes running in the same device can exchange routing information, thereby causing a route learned by one routing protocol to then be advertised by another.

**route summarization** The process of combining multiple routes into a single advertised route, for the purpose of reducing the number of entries in routers' IP routing tables.

**routed port** A port on a multilayer Cisco switch, configured with the `no switchport` command, that tells the switch to treat the port as if it were a Layer 3 port, like a router interface.

**routed protocol** A Layer 3 protocol that defines a packet that can be routed, such as IPv4 and IPv6.

**service provider** A company that provides a service to multiple customers. Used most often to refer to providers of private WAN services and Internet services. *See also* Internet service provider.

**session key** With encryption, a secret value that is known to both parties in a communication, used for a period of time, which the endpoints use when encrypting and decrypting data.

**shaping** A QoS tool that monitors the bit rate of the messages exiting a networking device, so that if the bit rate exceeds the shaping rate for a period of time, the shaper can queue the packets, effectively slowing down the sending rate to match the shaping rate.

**shaping rate** The bit rate at which a shaper compares the bit rate of packets passing through the shaping function, so that when the rate is exceeded, the shaper enables the queuing of packets, resulting in slowing the bit rate of the collective packets that pass through the shaper, so the rate of bits getting through the shaper does not exceed the shaping rate.

**shared key** A reference to a security key whose value is known (shared) by both the sender and receiver.

**shared port** With 802.1w RSTP, a port type that is determined by the fact that the port uses half duplex, which could then imply a shared LAN as created by a LAN hub.

**shortest path first (SPF) algorithm** The algorithm used by OSPF to find all possible routes, and then choose the route with the lowest metric for each subnet.

**Simple Network Management Protocol (SNMP)** An Internet-standard protocol for managing devices on IP networks. It is used mostly in network management systems to monitor network-attached devices for conditions that warrant administrative attention.

**single homed** One design of the Internet edge in which the enterprise connects to the ISP with a single link.

**single multihomed** One design of the Internet edge in which the enterprise connects to two or more ISPs, but with a single link to each.

**single point of failure** In a network, a single device or link which, if it fails, causes an outage for a given population of users.

**site prefix** In IPv6, the prefix that describes a public globally unique IPv6 address block that has been assigned to an end-user organization (for example, an enterprise or government agency). The assignment usually is made by an ISP or Internet registry.

**site-to-site VPN** The mechanism that allows all devices at two different sites to communicate securely over some insecure network like the Internet, by having one device at each site perform encryption/decryption and forwarding for all the packets sent between the sites.

**SLSM** Static-length subnet mask. The usage of the same subnet mask for all subnets of a single Class A, B, or C network.

**SNMP** *See* Simple Network Management Protocol.

**SNMP agent** Software that resides on the managed device and processes the SNMP messages sent by the Network Management Station (NMS).
