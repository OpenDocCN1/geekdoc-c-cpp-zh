![](bbox=[0.068, 0.121, 0.108, 0.158])

# On physical interfaces and multipoint subinterfaces

+   - They need to use either Inverse ARP or static mapping.
+   - The **show frame-relay map** command should list the remote router’s Frame Relay IP address and the local router’s local DLCI for each PVC associated with the interface or subinterface. The “dynamic” notation means the mapping was learned with InARP.
+   - If you’re using static mapping, the broadcast keyword is needed to support a routing protocol.

For completeness, Example 1-23 shows the output of the **show frame-relay map** command on router R1 from Figure 1-7 with no problems with the mapping. (The earlier problems that were introduced have been fixed.) In this case, interface S0/0/0.2 is a point-to-point subinterface, and S0/0/0.34 is a multipoint with one Inverse ARP-learned mapping and one statically configured mapping.

# **Example 1-23** — show frame-relay map *Command on R1*

```
R1# show frame-relay map
Serial0/0/0.34 (up): ip 10.1.34.4 dlci 104 (0x68,0x1880), static,
        broadcast,
        CISCO, status defined, active

Serial0/0/0.34 (up): ip 10.1.34.3 dlci 103 (0x67,0x1870), dynamic,
        broadcast,, status defined, active

Serial0/0/0.2 (up): point-to-point dlci 102 (0x66,0x1860), broadcast
        status defined, active
```

# End-to-End Encapsulation (Step 5)

The end-to-end encapsulation on a PVC refers to the headers that follow the Frame Relay header, with two options: the Cisco-proprietary header and an IETF standard header. The configuration details were covered earlier in this chapter, in the section “Configuring the Encapsulation and LMI.”

As it turns out, a mismatched encapsulation setting on the routers on opposite ends of the link might cause a problem in one particular case. If one router is a Cisco router using Cisco encapsulation and the other router is a non-Cisco router using IETF encapsulation, pings might fail because of the encapsulation mismatch. However, two Cisco routers can understand both types of encapsulation, so it should not be an issue in networks with only Cisco routers.

# Mismatched Subnet Numbers (Step 6)

At this point, if the problems found in the first five of the six troubleshooting steps have been resolved, all the Frame Relay problems should be resolved. However, if the two routers on either end of the PVC have mistakenly configured IP addresses in different subnets, the routers will not be able to ping one another, and the routing protocols will not become adjacent. So, as a last step, you should confirm the IP addresses on each router and the masks and ensure that they connect to the same subnet. To do so, just see the show ip interface brief and show interfaces commands on the two routers.