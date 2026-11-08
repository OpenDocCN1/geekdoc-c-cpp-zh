5. Two neighboring LAN switches are connected with an operational 802.1Q trunk. Switch SW1 has been configured with the `vtp mode client`, `vtp domain fred`, and `vtp version 2` commands. SW1 has no other VTP configuration commands configured. Which answer lists a possible reason why switch SW2, on the other end of the trunk, is not synchronizing its VLAN database with switch SW1? (Choose two answers.)

+   a. SW2 has a `vtp version 1` command configured.
+   
+   b. SW2 has a `vtp password GoBeeZ` command configured.
+   
+   c. SW2 has a `vtp domain Fred` command configured.
+   
+   d. SW2 has a `vtp mode client` command configured.

6. Switches SW1 and SW2 connect through an operational trunk. The engineer wants to use VTP to communicate VLAN configuration changes. The engineer configures a new VLAN on SW1, VLAN 44, but SW2 does not learn about the new VLAN. Which of the following configuration settings on SW1 and SW2 would be a potential root cause why SW2 does not learn about VLAN 44? (Choose two answers.)

+   a. VTP domain names of larry and LARRY, respectively
+   
+   b. VTP passwords of bob and BOB, respectively
+   
+   c. VTP pruning enabled and disabled, respectively
+   
+   d. VTP modes of server and client, respectively

# Foundation Topics

# VLAN Trunking Protocol (VTP) Concepts

The Cisco-proprietary *VLAN Trunking Protocol* (VTP) provides a means by which Cisco switches can exchange VLAN configuration information. In particular, VTP advertises about the existence of each VLAN based on its VLAN ID and the VLAN name.

This first major section of the chapter discusses the major features of VTP in concept, in preparation for the VTP implementation (second section) and VTP troubleshooting (third section).

# Basic VTP Operation

Think for a moment about what has to happen in a small network of four switches when you need to add two new hosts, and to put those hosts in a new VLAN that did not exist before. Figure 5-1 shows some of the main configuration concepts.

First, remember that for a switch to be able to forward frames in a VLAN, that VLAN must be defined on that switch. In this case, Step 1 shows the independent configuration of VLAN 10 on the four switches: the two distribution switches and the two access layer switches. With the rules discussed in Chapter 1 (which assumed VTP was enabled, by the way), all four switches need to be configured with the `vlan 10` command.

Step 2 shows the additional step to configure each access port to be in VLAN 10 as per the design. That is, in addition to creating the VLAN, the individual ports need to be added to the VLAN, as shown for servers A and B with the `switchport access vlan 10` command.