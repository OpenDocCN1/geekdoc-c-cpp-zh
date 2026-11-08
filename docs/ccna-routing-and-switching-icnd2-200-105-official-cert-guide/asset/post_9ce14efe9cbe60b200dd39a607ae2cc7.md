
**Top of Rack (ToR) switch** In a traditional data center design with servers in multiple racks, and the racks in multiple rows, a switch placed in the top of the rack for the purpose of providing physical connectivity to the servers (hosts) in that rack.

**topology database** The structured data that describes the network topology to a routing protocol. Link-state and balanced hybrid routing protocols use topology tables, from which they build the entries in the routing table.

**traceroute** A program available on many systems that traces the path that a packet takes to a destination. It is used mostly to debug routing problems between hosts.

**triggered update** A routing protocol feature in which the routing protocol does not wait for the next periodic update when something changes in the network, instead immediately sending a routing update.

**trunk** In campus LANs, an Ethernet segment over which the devices add a VLAN header that identifies the VLAN in which the frame exists.

**trunk interface** A switch interface configured so that it operates using VLAN trunking (either 802.1Q or ISL).

**trunking** Also called VLAN trunking, a method (using either the Cisco ISL protocol or the IEEE 802.1Q protocol) to support multiple VLANs that have members on more than one switch.

**trunking administrative mode** The configured trunking setting on a Cisco switch interface, as configured with the switchport mode command.

**trunking operational mode** The current behavior of a Cisco switch interface for VLAN trunking.

**trust boundary** When thinking about a message as it flows from the source device to the destination device, the trust boundary is the first device the message reaches for which the QoS markings in the message's various headers can be trusted as having an accurate value, allowing the device to apply the correct QoS actions to the message based on the marking.

**trusted port** A switch port configured with DHCP snooping that may receive frames from DHCP servers, so that the DHCP snooping feature should trust all incoming DHCP messages.

**tunnel interface** A virtual interface in a Cisco router used to configure a variety of features, including generic routing encapsulation (GRE), which encapsulates IP packets into other IP packets for the purpose of creating VPNs.

**Type of Service (ToS)** In the original definition of the IP header, a byte reserved for the purpose of QoS functions, including holding the IP Precedence field. The ToS byte was later repurposed to hold the DSCP field.

## U

**unequal-cost load balancing** A concept in EIGRP by which a router adds multiple unequal cost (unequal metric) routes to the routing table, at the same time, allowing equal-metric routes to be used.

**Unified Computing System (UCS)** The Cisco brand name for their server hardware products.

**unique local unicast address** A type of IPv6 unicast address meant as a replacement for IPv4 private addresses.

**untrusted port** A configuration choice for a switch port configured with DHCP snooping and that should never receive frames from DHCP servers. This setting causes the DHCP snooping feature to discard all incoming messages that only a DHCP server would have sent, along with any other DHCP message matching logic that causes the filtering of other incoming DHCP messages.

**update timer** The time interval that regulates how often a routing protocol sends its next periodic routing updates. Distance vector routing protocols send full routing updates every update interval.

**user network interface (UNI)** A term used in a variety of WAN standards, including carrier/Metro Ethernet, that defines the standards for how a customer device communicates with a service provider’s device over an access link.

## V

**variable-length subnet masking (VLSM)** *See* VLSM.

**variance** A value used in routing protocol decisions by EIGRP. EIGRP computes its metric in a way such that for different routes, the calculated metric seldom results in the exact same value. The variance value is multiplied with the lower metric when multiple routes to the same subnet exist. If the product is larger than the metrics for other routes, the routes are considered to have “equal” metric, allowing multiple routes to be added to the routing table.

**virtual-access interface** A virtual interface inside a Cisco router, created by IOS’s PPPoE function to act as the Layer 2 interface, with its Layer 2 PPP parameters being built from the configuration listed on an associated dialer interface.

**virtual CPU (vCPU)** In a virtualized server environment, a CPU (processor) core or thread allocated to a virtual machine (VM) by the hypervisor.

**virtual IP address** For any FHRP protocol, an IP address that the FHRP shares between multiple routers so that they appear as a single default router to hosts on that subnet.

**virtual LAN (VLAN)** A group of devices connected to one or more switches that are grouped into a single broadcast domain through configuration. VLANs allow switch administrators to place the devices connected to the switches in separate VLANs without requiring separate physical switches. This creates design advantages of separating the traffic without the expense of buying additional hardware.

**virtual MAC address (VMAC)** For any FHRP protocol, a MAC address that the FHRP uses to receive frames from hosts.

**virtual machine** An instance of an operating system, running on server hardware that uses a hypervisor to allocate a subset of the server hardware (CPU, RAM, disk, and network) to that VM.

**virtual network function (VNF)** Any function done within a network (for example, router, switch, firewall) that is implemented not as a physical device but as an OS running in a virtualized system (for instance, a VM).

**virtual NIC (vNIC)** In a virtualized server environment, a network interface card (NIC) used by a virtual machine, which then connects to some virtual switch (vSwitch) running on that same host, which in turn connects to a physical NIC on the host.

**virtual private network (VPN)** A set of security protocols that, when implemented by two devices on either side of an insecure network such as the Internet, can allow the devices to send data securely. VPNs provide privacy, device authentication, anti-replay services, and data integrity services.

**Virtual Router Redundancy Protocol (VRRP)** A TCP/IP RFC protocol that allows two (or more) routers to share the duties of being the default router on a subnet, with an active/standby model, with one router acting as the default router and the other sitting by waiting to take over that role if the first router fails.

**virtual switch (vSwitch)** A software-only virtual switch inside one host (one hardware server), to provide switching features to the virtual machines running on that host.

**VLAN** *See* virtual LAN.

**VLAN configuration database** The name of the collective configuration of VLAN IDs and names on a Cisco switch.

**VLAN interface** A configuration concept inside Cisco switches, used as an interface between IOS running on the switch and a VLAN supported inside the switch, so that the switch can assign an IP address and send IP packets into that VLAN.

**VLAN Trunking Protocol (VTP)** A Cisco-proprietary messaging protocol used between Cisco switches to communicate configuration information about the existence of VLANs, including the VLAN ID and VLAN name.

**vlan.dat** The default file used to store a Cisco switch's VLAN configuration database.

**VLSM** Variable-length subnet masking. The ability to specify a different subnet mask for the same Class A, B, or C network number on different subnets. VLSM can help optimize available address space.

**voice VLAN** A VLAN defined for use by IP Phones, with the Cisco switch notifying the phone about the voice VLAN ID so that the phone can use 802.1Q frames to support traffic for the phone and the attached PC (which uses a data VLAN).

**VoIP** Voice over IP. The transport of voice traffic inside IP packets over an IP network.

**VPN** *See* virtual private network.

**VPN client** Software that resides on a PC, often a laptop, so that the host can implement the protocols required to be an endpoint of a VPN.

**VTP** *See* VLAN Trunking Protocol.

**VTP client mode** One of three VTP operational modes for a switch with which switches learn about VLAN numbers and names from other switches, but which does not allow the switch to be directly configured with VLAN information.
