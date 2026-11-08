# ### Gatekeepers

Gatekeepers serve two purposes in H.323 networks. First, they allow entry by endpoints (IP phones) into the network. H.323 gatekeepers use Registration, Admission, and Status (RAS) messages for network admission. Second, gatekeepers perform address translation. For example, the gatekeeper can convert Tom.Carpenter@sysedco.com to 192.168.12.14. Chapter 14 also covers gatekeepers in greater depth.

# ### Call Managers

A call manager is used to initiate a call, manage the call, and terminate that call in a VoIP network. Cisco call managers include the Cisco Unified Communications Manager (CUCM) and Cisco Unified Communications Manager Express (CME). Additionally, the small-office/home-office (SOHO) market product is the Unified Communications 500 (UC500) series, which includes call management capabilities. In Chapters 9, 12, and 13, you will explore these call managers in depth.

# ### VoIP Phones

You may be wondering why VoIP phones are listed in an infrastructure section. The reason is simple: many Cisco VoIP phones act as both a client and an access point to the network. The phone is a client to the network when it acts as a phone. The phone is an access point when it acts as a switch port for a client device. The phone implements a VLAN trunk for the client computers that connect to the phone's switch port. This allows the client computer to exist on one VLAN while the VoIP phone itself exists on another VLAN. A Cisco phone has three ports:

+   - The external Ethernet port for connection to a Cisco switch, which provides the actual infrastructure network connectivity
+   - The external Ethernet port for connection to a PC, which provides networking functionality to the PC in the work area of the VoIP phone
+   - The internal Ethernet port for VoIP traffic, which is a virtual port within the phone allowing for differentiation between the VoIP traffic and the PC traffic

The Cisco VoIP phones support 802.1Q tagging for VLAN identification. They do not support Inter-Switch Link (ISL) encapsulation. Additionally, some Cisco phones do not support a PC Ethernet port. If this feature is important to your implementation, be sure to select a phone model that implements the PC port. The 7940G, 7960G, and 7970G models all support the PC port. They also support inline power for PoE power solutions. The 7910G model does not support the PC