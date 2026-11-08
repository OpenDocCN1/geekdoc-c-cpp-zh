# **Example 4-4**  *Examining SW1 and SW2 Dynamic MAC Address Table Entries*

```
SW1# show mac address-table dynamic
              Mac Address Table

-------------------------------------------

Vlan    Mac Address       Type       Ports
----    -----------       --------   -----
 1      0200.AAAA.AAAA    DYNAMIC    Gi0/2
 2      0200.BBBB.BBBB    DYNAMIC    Gi0/1

SW2# show mac address-table dynamic
              Mac Address Table

-------------------------------------------

Vlan    Mac Address       Type       Ports
----    -----------       --------   -----
 1      0200.AAAA.AAAA    DYNAMIC    Gi0/2
 2      0200.BBBB.BBBB    DYNAMIC    Gi0/1
```

# Predicting EtherChannel Impact on MAC Tables

Most designs use multiple links between switches, with those links configured to be part of an EtherChannel. What does that do to the MAC forwarding logic? In short, the switch uses the PortChannel interfaces, and not the physical interfaces bundled into the EtherChannel, in the MAC address table. Specifically:

**MAC learning:** Frames received in a physical interface that is part of a PortChannel are considered to arrive on the PortChannel interface. So, MAC learning adds the PortChannel interface rather than the physical interface to the MAC address table.

**MAC forwarding:** The forwarding process will find a PortChannel port as an outgoing interface when matching the MAC address table. Then the switch must take the additional step to choose the outgoing physical interface, based on the load-balancing preferences configured for that PortChannel.

For example, consider Figure 4-5, which updates previous Figure 4-4 with two-link PortChannels between each pair of switches. With VLAN 1 blocking again on switch SW3, but this time on SW3’s PortChannel3 interface, what MAC table entries would you expect to see in each switch? Similarly, what MAC table entries would you expect to see for VLAN 2, with SW3 blocking on its PortChannel2 interface?

The logic of which entries exist on which ports mirrors the logic with the earlier example surrounding Figure 4-4. In this case, the interfaces just happen to be PortChannel interfaces. Example 4-5 shows the same command from the same two switches as Example 4-4: **show mac address-table dynamic** from both SW1 and SW2. (Note that to save length, the MAC table output shows only the entries for the two servers in Figure 4-5.)