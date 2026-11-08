Mount Pilot needs to configure a frame-relay map command with the ietf keyword for its VC to Raleigh, just like Mayberry. This change is not shown in the examples.

# ## Frame Relay Address Mapping

Figure I-1 does not even bother listing the DLCIs used for the VCs. The earlier configurations work as stated, and, frankly, if you never knew the DLCIs, this network would work! However, for the exams, and for real networking jobs, engineers need to know the DLCIs, and the process of Frame Relay mapping.

Frame Relay mapping matches a next-hop IP address that sits on the Frame Relay network with the right DLCI used to send frames to that next-hop device, with the same goal as ARP on a LAN. Figure I-2 shows the same network, this time with local DLCI values shown.

Frame Relay “mapping” creates a correlation between a Layer 3 address and its corresponding Layer 2 address. The concept is similar to the ARP cache for LAN interfaces. For example, the IP Address Resolution Protocol (ARP) cache used on LANs is an example of Layer 3-to-Layer 2 address mapping. With IP ARP, you know the IP address of another device on the same LAN, but not the MAC address; when the ARP completes, you know another device’s LAN (Layer 2) address. Similarly, routers that use Frame Relay need a mapping between a router’s Layer 3 address and the DLCI used to reach that other router.

![](bbox=[0.178, 0.451, 0.834, 0.686])

**Figure I-2** *Full Mesh with Local DLCIs Shown*

This section discusses the basics of why mapping is needed for LAN connections and Frame Relay, with a focus on Frame Relay. Here’s a more general definition of mapping:

The information that correlates to the next-hop router’s Layer 3 address and the Layer 2 address used to reach it is called mapping. Mapping is needed on multiaccess networks.

Thinking about routing helps make the need for mapping more apparent. For example, consider a packet that enters Mayberry’s LAN interface destined for network 199.1.11.0/24, the Class C network off Mount Pilot’s LAN interface. As shown in Figure I-3, the route goes through normal routing steps, removing the packet from between the Ethernet header and trailer, choosing to route the packet out Mayberry’s S0/1 interface to Mount Pilot next, and so on. But what DLCI should Mayberry put into the new Frame Relay header?