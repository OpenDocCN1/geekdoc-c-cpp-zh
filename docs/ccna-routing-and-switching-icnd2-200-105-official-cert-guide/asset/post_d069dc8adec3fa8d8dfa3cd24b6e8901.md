
### multilink interface
A virtual interface created by Multilink PPP as the Layer 3 interface used in MLPPP configurations.

### Multilink PPP (MLPPP)
A feature of PPP that manages multiple links between two nodes, load balancing data link frames across those multiple links by fragmenting each frame into pieces (fragments), sending one fragment over each active link. It also presents a single Layer 3 interface to the Layer 3 logic in the endpoint devices.

### multipoint
A topology with more than two devices in it (in contrast to a point-to-point topology, which has exactly two devices). Without any further context, the term *multipoint* does not define whether all devices in the topology can send messages directly to each other (full mesh) or not (partial mesh).

### multipoint GRE
A type of GRE tunnel in which more than two devices can be part of the same tunnel, sending packets directly to each other over the same tunnel, and using one subnet for all devices connected to the tunnel.

### Multiprotocol BGP (MPBGP)
A particular set of BGP extensions that allows BGP to support multiple address families, which when used to create an MPLS VPN service gives the SP the method to advertise the IPv4 routes of many customers while keeping those route advertisements logically separated.

### Multiprotocol Label Switching (MPLS)
A WAN technology used to create an IP-based service for customers, with the service provider’s internal network performing forwarding based on an MPLS label rather than the destination IP address.

### multithreading
In computer architecture, a process of maximizing the use of a processor core by sharing an individual core among multiple programs, taking advantage of the typical idle times for the core while it waits on various other tasks like memory reads and writes.

## N

### named access list
An ACL that identifies the various statements in the ACL based on a name rather than a number.

### National Institute of Standards and Technology (NIST)
A U.S. federal agency that develops national standards, including standards for cloud computing.

### NBI
*See* Northbound API.

### NBMA
*See* nonbroadcast multiaccess.

### neighbor
In routing protocols, another router with which a router decides to exchange routing information.

### Neighbor Advertisement (NA)
A message defined by the IPv6 Neighbor Discovery Protocol (NDP) and used to declare to other neighbors a host’s MAC address. Sometimes sent in response to a previously received NDP Neighbor Solicitation (NS) message.

### Neighbor Discovery Protocol (NDP)
A protocol that is part of the IPv6 protocol suite and is used to discover and exchange information about devices on the same subnet (neighbors). In particular, it replaces IPv4 ARP.

### Neighbor Solicitation (NS)
A message defined by the IPv6 Neighbor Discovery Protocol (NDP) and used to ask a neighbor to reply back with a Neighbor Advertisement, which lists the neighbor's MAC address.

### neighbor table
For OSPF and EIGRP, a list of routers that have reached neighbor status.

### network analyzer
Network management software that captures LAN frames (often frames directed to it by a switch SPAN session) for the purpose of then analyzing the contents of those frames for a network engineer.

### Network Based Application Recognition (NBAR)
A Cisco router feature that looks at message details beyond the Layer 2, 3, and 4 headers to identify over 1000 different classifications of packets from different applications.

### Network Layer Reachability Information (NLRI)
The formal BGP term for a prefix and matching prefix length that defines an address block, which is included in the BGP Update message.

### Network LSA
In OSPF, a type of LSA that a designated router (DR) creates for the network (subnet) for which the DR is helping to distribute LSAs.

### Network Management System (NMS)
Software that manages the network, often using SNMP and other protocols.

### Next Hop Resolution Protocol (NHRP)
A protocol defined by the IETF, used by Cisco's DMVPN feature for the purpose of allowing routers connected to the Internet to discover each other's public IP addresses and inform each other of their private IP addresses as used by DMVPN.

### Nexus 1000V
A Cisco Nexus data center switch that runs as a software-only virtual switch inside one host (one hardware server), to provide switching features to the virtual machines running on that host.

### NHRP client
When using Next Hop Resolution Protocol, a router that registers its public and private IP addresses by informing the NHRP server of the addresses it uses. The NHRP client also asks the NHRP server to inform the client of the public/private address pairs of other routers.

### NHRP server
When using Next Hop Resolution Protocol, a router that collects and distributes the public and private IP address pairs registered to it from NHRP clients.

### NMS
Network Management Station. The device that runs network management software to manage network devices. SNMP is often the network management protocol used between the NMS and the managed device.

### nonbroadcast multiaccess (NBMA)
A characterization of a type of Layer 2 network in which more than two devices connect to the network, but the network does not allow broadcast frames to be sent to all devices on the network.

### Northbound API
In the area of SDN, a reference to the APIs that a controller supports that gives outside programs access to the services of the controller; for instance, to supply information about the network or to program flows into the network. Also called a Northbound Interface.

### Northbound Interface
Another term for Northbound API. *See* Northbound API.

### notification community
An SNMP community (a value that acts as a password), defined on an SNMP manager, which then must be supplied by any SNMP agent that sends the manager any unsolicited SNMP notifications (like SNMP Trap and Notify requests).

### NVRAM
Nonvolatile RAM. A type of random-access memory (RAM) that retains its contents when a unit is powered off.

## O

### ODL
*See* OpenDaylight.

### OID
Object Identifier. Used to uniquely describe a MIB variable in the SNMP database. This is a numeric string that identifies the variable uniquely and also describes where the variable exists in the MIB tree structure.

### on-demand self-service
One of the five key attributes of a cloud computing service as defined by NIST, referring to the fact that the consumer of the service can request the service, with the service being created without any significant delay and without waiting on human intervention.

### one-way delay
The elapsed time from sending the first bit of data at the sending device until the last bit of that data is received on the destination device.

### ONF
*See* Open Networking Foundation.

### Open Networking Foundation
A consortium of SDN users and vendors who work together to foster the adoption of open SDN in the marketplace.

### OpenDaylight
An open source SDN controller, created by an open source effort of the OpenDaylight project under the Linux Foundation, built with the intent to have a common SDN controller code base from which vendors could then take the code and add further features and support to create SDN controller products.

### OpenFlow
The open standard for Software Defined Networking (SDN) as defined by the Open Networking Foundation (ONF), which defines the OpenFlow protocol as well as the concept of an abstracted OpenFlow virtual switch.

### OpFlex
The southbound protocol used by the Cisco ACI controller and the switches it controls.

### OSPF
Open Shortest Path First. A popular link-state IGP that uses a link-state database and the Shortest Path First (SPF) algorithm to calculate the best routes to reach each known subnet.

### OSPF super backbone
Jargon used to refer to how when an MPLS VPN customer uses OSPF, that the MPLS VPN service acts as if it were part of OSPF backbone area 0, with that part of area 0 being called the super backbone.

### OSPF version 2
The version of the OSPF routing protocol that supports IPv4, and not IPv6, and has been commonly used for over 20 years.

### OSPF version 3
The version of the OSPF routing protocol that originally supported only IPv6, and not IPv4, but now supports IPv4 through the use of address family configuration.
