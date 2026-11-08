Done correctly, VTP causes all the switches in the same administrative *VTP domain*—the set of switches with the same domain name and password—to converge to have the exact same configuration of VLAN information. Over time, each time the VLAN configuration is changed on any VTP server, all other switches in the VTP automatically learn of those configuration changes.

VTP does not think of the VLAN configuration as lots of small pieces of information, but rather as one *VLAN configuration database*. The configuration database has a configuration revision number which is incremented by 1 each time a server changes the VLAN configuration. The VTP synchronization process hinges on the idea of making sure each switch uses the VLAN configuration database that has the best (highest) revision number.

Figure 5-3 begins an example that demonstrates how the VLAN configuration database revision numbers work. At the beginning of the example, all the switches have converged to use the VLAN database that uses revision number 3. The example then shows:

+   1. The network engineer defines a new VLAN with the **vlan 10** command on switch SW1.
+   2. SW1, a VTP server, changes the VTP revision number for its own VLAN configuration database from 3 to 4.
+   3. SW1 sends VTP messages over the VLAN trunk to SW2 to begin the process of telling SW2 about the new VTP revision number for the VLAN configuration database.

![](bbox=[0.166, 0.48, 0.84, 0.625])

*Figure 5-3 Adding VLAN 10 at Switch SW1, Starting with All at Revision Number 3*

At this point, only switch SW1 has the best VLAN configuration database with the highest revision number (4). Figure 5-4 shows the next few steps, picking up the process where Figure 5-3 stopped. Upon receiving the VTP messages from SW1, as shown in Step 3 of Figure 5-3, at Step 4 in Figure 5-4, SW2 starts using that new LAN database. Step 5 emphasizes the fact that as a result, SW2 now knows about VLAN 10. SW2 then sends VTP messages over the trunk to the next switch, SW3 (Step 6).

With VTP working correctly on all four switches, all the switches will eventually use the exact same configuration, with VTP revision number 4, as advertised with VTP.

Figure 5-4 also shows a great example of one key similarity between VTP clients and servers: both will learn and update their VLAN database from VTP messages received from another switch. Note that the process shown in Figures 5-3 and 5-4 works the same whether switches SW2, SW3, and SW4 are VTP clients or servers, in any combination. In this scenario, the only switch that must be a VTP server is switch SW1, where the **vlan 10** command was configured; a VTP client would have rejected the command.