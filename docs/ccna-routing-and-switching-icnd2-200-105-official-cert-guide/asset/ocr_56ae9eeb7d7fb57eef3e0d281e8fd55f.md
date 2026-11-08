To show the concept of Layer 3 switching with SVIs, Figure 19-3 shows the design changes and configuration concept for the same branch office used in Figures 19-1 and 19-2. The figure shows the Layer 3 switch function with a router icon inside the switch, to emphasize that the switch routes the packets. The branch still has two user VLANs, so the Layer 3 switch needs one VLAN interface for each VLAN. In addition, the traffic still needs to get to the router to access the WAN, so the switch uses a third VLAN (VLAN 30 in this case) for the link to Router B1. This link would not be a trunk, but would be an access link.

![](bbox=[0.066, 0.229, 0.811, 0.385])

# Figure 19-3 — *Routing on VLAN Interfaces in a Layer 3 Switch*

The following steps show how to configure Layer 3 switching using SVIs. Note that on some switches, like the 2960 and 2960-XR switches used for the examples in this book, the ability to route IPv4 packets must be enabled first, with a reload of the switch required to enable the feature. The rest of the steps after Step 1 would apply to all models of Cisco switches that are capable of doing Layer 3 switching.

+   1. **Step 1.** Enable IP routing on the switch, as needed.
+      - **A.** Use the `sdm prefer lanbase-routing` command (or similar) in global configuration mode to change the switch forwarding ASIC settings to make space for IPv4 routes at the next reload of the switch.
+      - **B.** Use the `reload` EXEC command in enable mode to reload (reboot) the switch to pick up the new sdm prefer command setting.
+      - **C.** Once reloaded, use the `ip routing` command in global configuration mode to enable the IPv4 routing function in IOS software and to enable key commands like `show ip route`.

+   2. **Step 2.** Configure each SVI interface, one per VLAN for which routing should be done by this Layer 3 switch.
+      - **A.** Use the `interface vlan vlan_id` command in global configuration mode to create a VLAN interface, and to give the switch’s routing logic a Layer 3 interface connected into the VLAN of the same number.
+      - **B.** Use the `ip address address mask` command in VLAN interface configuration mode to configure an IP address and mask on the VLAN interface, enabling IPv4 routing on that VLAN interface.
+      - **C.** (As needed) Use the `no shutdown` command in interface configuration mode to enable the VLAN interface (if it is currently in a shutdown state).