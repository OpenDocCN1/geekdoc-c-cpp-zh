**global unicast address** A type of unicast IPv6 address that has been allocated from a range of public globally unique IP addresses as registered through IANA/ICANN, its member agencies, and other registries or ISPs.

**GRE tunnel** A site-to-site VPN idea, in which the endpoints act as if a point-to-point link (the tunnel) exists between the sites, while actually encapsulating packets using GRE standards.

# # H

**HDLC** High-level Data Link Control. A bit-oriented synchronous data link layer protocol developed by the International Organization for Standardization (ISO). Derived from synchronous data link control (SDLC), HDLC specifies a data encapsulation method on synchronous serial links using frame characters and checksums.

**Hello** (Multiple definitions) 1) A protocol used by OSPF routers to discover, establish, and maintain neighbor relationships. 2) A protocol used by EIGRP routers to discover, establish, and maintain neighbor relationships. 3) In STP, refers to the name of the periodic message sourced by the root bridge in a spanning tree.

**Hello BPDU** The STP and RSTP message used for the majority of STP communications, listing the root's bridge ID, the sending device's bridge ID, and the sending device's cost with which to reach the root.

**Hello Interval** With OSPF and EIGRP, an interface timer that dictates how often the router should send Hello messages.

**Hello timer** In STP, the time interval at which the root switch should send Hello BPDUs.

**host** In a virtualized server environment, the term used to refer to one physical server that is running a hypervisor to create multiple virtual machines.

**Hot Standby Router Protocol (HSRP)** A Cisco-proprietary protocol that allows two (or more) routers to share the duties of being the default router on a subnet, with an active/standby model, with one router acting as the default router and the other sitting by waiting to take over that role if the first router fails.

**HSRP active** A Hot Standby Router Protocol (HSRP) state in which the router actively supports the forwarding of off-subnet packets for hosts in that subnet.

**HSRP standby** A Hot Standby Router Protocol (HSRP) state in which the router does not currently support the forwarding of off-subnet packets for hosts in that subnet, instead waiting for the currently active router to fail before taking over that role.

**hub-and-spoke** From a topology perspective, any topology that has a device that can send messages to all other devices (the hub), with one or more spoke devices that can send messages only to the hub. Also called point-to-multipoint.

**Hyperthreading** The name of Intel's multithreading technology.

**hypervisor** Software that runs on server hardware to create the foundations of a virtualized server environment primarily by allocating server hardware components like CPU core/threads, RAM, disk, and network to the VMs running on the server.