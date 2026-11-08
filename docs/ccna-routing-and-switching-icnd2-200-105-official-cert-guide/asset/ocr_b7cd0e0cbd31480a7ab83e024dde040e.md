> **NOTE** The section “Mismatched Supported VLAN List on Trunks” in Chapter 4, “LAN Troubleshooting,” discusses the various reasons why a switch trunk does not forward frames in a VLAN, including the allowed VLAN list. That section also briefly references VTP pruning.

Figure 5-6 shows an example of VTP pruning, showing a design that makes VTP pruning feature more obvious. In this figure, two VLANs are used: 10 and 20. However, only switch SW1 has access ports in VLAN 10, and only switches SW2 and SW3 have access ports in VLAN 20. With this design, a frame in VLAN 20 does not need to be flooded to the left to switch SW1, and a frame in VLAN 10 does not need to be flooded to the right to switches SW2 and SW3.

![](bbox=[0.146, 0.319, 0.809, 0.521])

**Figure 5-6**  *VTP Pruning Example*

+   Figure 5-6 shows two steps that result in VTP pruning VLAN 10 from SW2’s G0/2 trunk:
+   
+   **Step 1.** SW1 knows about VLAN 20 from VTP, but switch SW1 does not have access ports in VLAN 20. So SW1 announces to SW2 that SW1 would like to prune VLAN 20, so that SW1 no longer receives data frames in VLAN 20.
+   
+   **Step 2.** VTP on switch SW2 prunes VLAN 20 from its G0/2 trunk. As a result, SW2 will no longer flood VLAN 20 frames out trunk G0/2 to SW1.

VTP pruning increases the available bandwidth by restricting flooded traffic. VTP pruning is one of the two most compelling reasons to use VTP, with the other reason being to make VLAN configuration easier and more consistent.

# Summary of VTP Features

Table 5-2 offers a comparative overview of the three VTP modes.

**Table 5-2 — VTP Features**

| Function | Server | Client | Transparent |
|---|---|---|---|
| Only sends VTP messages out ISL or 802.1Q trunks | Yes | Yes | Yes |
| Allows CLI configuration of VLANs | Yes | No | Yes |
| Can use normal range VLANs (1–1005) | Yes | Yes | Yes |
| Can use extended range VLANs (1006–4095) | No | No | Yes |