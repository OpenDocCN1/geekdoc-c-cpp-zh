
## L

**LACP**  Link Aggregation Control Protocol is a messaging protocol defined by the IEEE 802.3ad standard which enables two neighboring devices to realize that they have multiple parallel links connecting to each other, and then to decide which links can be combined into an EtherChannel.

**LAN broadcast**  An Ethernet frame sent to destination address FFFF.FFFF.FFFF, meaning that the frame should be delivered to all hosts on that LAN.

**LAPF**  Link Access Procedure Frame Bearer Services. Defines the basic Frame Relay header and trailer. The header includes DLCI, FECN, BECN, and DE bits.

**Layer 2 EtherChannel (L2 EtherChannel)**  An EtherChannel that acts as a switched port (that is, not a routed port), and as such, is used by a switch’s Layer 2 forwarding logic. As a result, the Layer 2 switch lists the Layer 2 EtherChannel in switch MAC address tables, and when forwarding a frame based on one of these MAC table entries, the switch balances traffic across the various ports in the Layer 2 EtherChannel.

**Layer 3 EtherChannel (L3 EtherChannel)**  An EtherChannel that acts as a routed port (that is, not a switched port), and as such, is used by a switch’s Layer 3 forwarding logic. As a result, the Layer 3 switch lists the Layer 3 EtherChannel in various routes in the switch’s IP routing table, with the switch balancing traffic across the various ports in the Layer 3 EtherChannel.

**Layer 3 switch**  A LAN switch that can also perform Layer 3 routing functions. The name comes from the fact that this device makes forwarding decisions based on logic from multiple OSI layers (Layers 2 and 3).

**learn**  Describes how switches discover MAC addresses by examining the source MAC addresses of frames they receive. They add each new MAC address, along with the port number of the port on which it learned of the MAC address, to an address table.

**learning state**  In STP, a temporary port state in which the interface does not forward frames, but it can begin to learn MAC addresses from frames received on the interface.

**leased line**  A transmission line reserved by a communications carrier for a customer’s private use. A leased line is a type of dedicated line.

**Link Control Protocol**  A control protocol defined as part of PPP for the purpose of initializing and maintaining a PPP link.

**link state**  A classification of the underlying algorithm used in some routing protocols. Link-state protocols build a detailed database that lists links (subnets) and their state (up, down), from which the best routes can then be calculated.

**link-local address**  A type of unicast IPv6 address that represents an interface on a single data link. Packets sent to a link-local address cross only that particular link and are never forwarded to other subnets by a router. Used for communications that do not need to leave the local link, such as neighbor discovery.

**link-state advertisement (LSA)**  In OSPF, the name of the data structure that resides inside the LSDB and describes in detail the various components in a network, including routers and links (subnets).

**link-state database (LSDB)**  In OSPF, the data structure in RAM of a router that holds the various LSAs, with the collective LSAs representing the entire topology of the network.

**Link-State Request**  An OSPF packet used to ask a neighboring router to send a particular LSA.

**Link-State Update**  An OSPF packet used to send an LSA to a neighboring router.

**listening state**  A temporary STP port state that occurs immediately when a blocking interface must be moved to a forwarding state. The switch times out MAC table entries during this state. It also ignores frames received on the interface and doesn’t forward any frames out the interface.

**local loop**  A line from the premises of a telephone subscriber to the telephone company CO.

**local SPAN**  A SPAN monitor session in which the monitored frames and the SPAN destination port are in the same switch.

**local username**  A username (with matching password), configured on a router or switch. It is considered local because it exists on the router or switch, and not on a remote server.

**logical switch**  In a switch stack, the term *logical switch* refers to the behavior of the switch stack as a whole in that the entire stack together acts as one switch.

**loss**  A reference to packets in a network that are sent but do not reach the destination host.

**low latency queue**  In Cisco queuing systems, a queue from which the queue scheduling algorithm always takes packets next if the queue holds any packets. This scheduling choice means that packets in this queue spend little time in the queue, achieving low delay (latency) as well as low jitter.

**Low Latency Queuing (LLQ)**  The name of a queuing system that can be enabled on Cisco routers and switches by which messages sensitive to latency and jitter are placed in a queue that is always serviced first, resulting in low latency and jitter for those messages.

**LSA**  *See* link-state advertisement.

**LTE**  Literally, Long Term Evolution, but is used as a word itself to represent the type of wireless 4G technology that allows faster speeds than the original 4G specifications.

## M

**Management Information Base (MIB)**  The data structures defined by SNMP to define a hierarchy (tree) structure with variables at the leaves of the tree, so that SNMP messages can reference the variables.

**management plane**  Functions in networking devices and controllers that control the devices themselves, but that do not impact the forwarding behavior of the devices like control plane protocols do.

**man-in-the-middle attack**  Any type of attack in which the attacker gains control of some device or process between a user and some server, for the purpose of then capturing the messages sent between the user and the server.

**marking**  The process of changing one of a small set of fields in various network protocol headers, including the IP header's DSCP field, for the purpose of later classifying a message based on that marked value.

**match/action logic**  The basic logic done by a networking element: to receive incoming messages, to match fields in the message, to then use logic based on those matches to take action against the message, and to then forward the message.

**MaxAge**  In STP, a timer that states how long a switch should wait when it no longer receives Hellos from the root switch before acting to reconverge the STP topology. Also called the MaxAge timer.

**maximum paths**  In Cisco IOS, a reference to the number of equal cost routes (paths) to reach a single subnet that IOS will add to the IP routing table at the same time.

**metric**  A numeric measurement used by a routing protocol to determine how good a route is as compared to other alternate routes to reach the same subnet.

**Metro Ethernet**  The original term used for WAN service that used Ethernet links as the access link between the customer and the service provider.

**metropolitan-area network (MAN)**  A service provided by a service provider to connect customer sites, with the customer sites existing in the same city; it takes its name from the metropolitan area of cities.

**MIB**  *See* Management Information Base.

**MIB view**  A concept in SNMPv3 that identifies a subset of an SNMP agent's MIB for the purpose of limiting access to some parts of the MIB to certain SNMP managers.

**modem**  Modulator-demodulator. A device that converts between digital and analog signals so that a computer may send data to another computer using analog telephone lines. At the source, a modem converts digital signals to a form suitable for transmission over analog communication facilities. At the destination, the analog signals are returned to their digital form.

**MPLS**  *See* Multiprotocol Label Switching.

**MPLS Experimental Bits**  A 3-bit field in the MPLS label used for QoS marking.

**MPLS VPN**  A WAN service that uses MPLS technology, with many customers connecting to the same MPLS network, but with the VPN features keeping each customer's traffic separate from others.

**MTU**  Maximum transmission unit. The maximum packet size, in bytes, that a particular interface can handle.

**multiarea**  In OSPFv2 and OSPFv3, a design that uses multiple areas.

**Multichassis EtherChannel (MEC)**  A Cisco technology that allows switches in a switch stack to be one endpoint of an EtherChannel, with links in the EtherChannel connecting to different switches in the switch stack.

**multilayer switch**  A LAN switch that can also perform Layer 3 routing functions. The name comes from the fact that this device makes forwarding decisions based on logic from multiple OSI layers (Layers 2 and 3).
