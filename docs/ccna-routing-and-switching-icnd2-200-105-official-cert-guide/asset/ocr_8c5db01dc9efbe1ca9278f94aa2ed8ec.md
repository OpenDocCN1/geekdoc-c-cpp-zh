# # Miscellaneous LAN Topics

**This chapter covers the following exam topics:**

+   1.0 LAN Switching Technologies
+   
+   1.6 Describe the benefits of switch stacking and chassis aggregation
+   
+   1.7 Describe common access layer threat mitigation techniques
+   
+   - 1.7.a 802.1x
+   - 1.7.b DHCP snooping
+   
+   5.0 Infrastructure Maintenance
+   
+   5.4 Describe device management using AAA with TACACS+ and RADIUS

Between this book and the ICND1 100-105 Cert Guide, 14 chapters have been devoted to topics specific to LANs. This chapter is the last of those chapters. This chapter completes the LAN-specific discussion with a few small topics that just do not fit neatly in the other chapters.

The chapter begins with three security topics. The first section addresses IEEE 802.1x, which defines a mechanism to ensure user access to a LAN by requiring the user to supply a username and password before a switch allows the device’s sent frames into the LAN. This tool helps secure the network against attackers gaining access to the network. The second section, “AAA Authentication,” discusses network device security, protecting router and switch CLI access by requiring username/password login with an external authentication server. The third section, “DHCP Snooping,” explores how switches can prevent security attacks that take advantage of DHCP messages and functions. By watching DHCP messages, noticing when they are used in abnormal ways not normally done with DHCP, DHCP can prevent attacks by simply filtering certain DHCP messages.

The final of the four major sections in this chapter looks at two similar design tools that make multiple switches act like one switch: switch stacking and chassis aggregation. Switch stacking allows a set of similar switches that sit near to each other (in the same wiring closet, typically in the same part of the same rack) to be cabled together and then act like a single switch. Using a switch stack greatly reduces the amount of work to manage the switch, and it reduces the overhead of control and management protocols used in the network. Switch chassis aggregation has many of the same benefits, but is supported more often as a distribution or core switch feature, with switching acting as a more typical access layer switch feature.

All four sections of this chapter have a matching exam topic that uses the verb “describe,” so this chapter touches on the basic descriptions of a tool, rather than deep configuration. A few of the topics will show some configuration as a means to describe the topic, but the chapter is meant to help you come away with an understanding of the fundamentals, rather than an ability to configure the features.