# ### Example 4-8 Allowed VLAN List and List of Active VLANs

```
```
SW1# show interfaces trunk

Port        Mode             Encapsulation  Status        Native vlan
G10/1       desirable        802.1q         trunking      1

Port        Vlans allowed on trunk
G10/1       1-2,4-4094

Port        Vlans allowed and active in management domain
G10/1       1,4

Port        Vlans in spanning tree forwarding state and not pruned
G10/1       1,4
```
```

The absence of a VLAN in this last part of the command's output does not necessarily mean that a problem has occurred. In fact, a VLAN might be legitimately excluded from a trunk for any of the reasons in the list just before Example 4-8. However, for a given exam question, it can be useful to know why traffic for a VLAN will not be forwarded over a trunk, and the details inside the output identify the specific reasons.

The output of the **show interfaces trunk** command creates three separate lists of VLANs, each under a separate heading. These three lists show a progression of reasons why a VLAN is not forwarded over a trunk. Table 4-2 summarizes the headings that precede each list and the reasons why a switch chooses to include or not include a VLAN in each list.

# ### Table 4-2 VLAN Lists in the show interfaces trunk Command

| List Position | Heading | Reasons |
| --- | --- | --- |
| First | VLANs allowed | VLANs 1–4094, minus those removed by the **switchport trunk allowed** command |
| Second | VLANs allowed and active... | The first list, minus VLANs not defined to the local switch (that is, there is not a **vlan global configuration command** or the switch has not learned of the VLAN with VTP), and also minus those VLANs in shutdown mode |
| Third | VLANs in spanning tree... | The second list, minus VLANs in an STP blocking state for that interface, and minus VLANs VTP pruned from that trunk |

# ### Mismatched Native VLAN on a Trunk

Closing with a brief mention of one other trunking topic, you should also check a trunk's native VLAN configuration at this step. Unfortunately, it is possible to set the native VLAN ID to different VLANs on either end of the trunk, using the **switchport trunk native vlan vlan-id** command. If the native VLANs differ according to the two neighboring switches, the switches will accidentally cause frames to leave one VLAN and enter another.

For example, if switch SW1 sends a frame using native VLAN 1 on an 802.1Q trunk, SW1 does not add a VLAN header, as is normal for the native VLAN. When switch SW2 receives the frame, noticing that no 802.1Q header exists, SW2 assumes that the frame is part of