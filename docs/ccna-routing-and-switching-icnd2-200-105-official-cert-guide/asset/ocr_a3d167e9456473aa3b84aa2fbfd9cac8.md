For example, first, examine the list of neighbors known on Router R3 from the configuration in Examples 8-1, 8-2, and 8-3. R3 should have one neighbor relationship with R1, over the serial link. It also has two neighbor relationships with R4, over the two different VLANs to which both routers connect. Example 8-4 shows all three.

# **Example 8-4** *OSPF Neighbors on Router R3 from Figure 8-2*

```
R3# show ip ospf neighbor

Neighbor ID       Pri   State    Dead Time   Address       Interface
1.1.1.1             0   FULL/-   00:00:33    10.1.13.1     Serial0/0/0
10.1.24.4           1   FULL/DR  00:00:35    10.1.3.130    GigabitEthernet0/0.342
10.1.24.4           1   FULL/DR  00:00:36    10.1.3.4      GigabitEthernet0/0.341
```