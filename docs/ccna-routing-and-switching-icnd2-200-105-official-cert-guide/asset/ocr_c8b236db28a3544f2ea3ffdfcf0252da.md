# Choosing to Limit SPAN Sources

Good engineers do not just decide to use SPAN on the entire VLAN in both directions without giving any thought to what they really need to capture. Instead, engineers think about what needs to be captured, how to get SPAN to capture that traffic, and *capture as little other traffic as possible*.

For example, if the goal of a capture is to see traffic sent by the switch to all hosts in a VLAN, then create a SPAN session with that VLAN as the source, for the transmit direction. However, if you only really care about 3 of the 12 access ports in that VLAN, take the time to configure the SPAN session just for those ports.

It is also easy to make poor choices regarding the traffic direction—choices that work, but that overload the SPAN destination port. For instance, Figure 26-21 represents the SPAN logic applied to the four ports in the same VLAN (11), with a command like monitor session 1 source VLAN 11 both. Each Tx and Rx bubble represents a location where SPAN is monitoring either transmit or receive traffic. The figure then focuses on one Ethernet frame, sent by PC1 to PC3.

![](bbox=[0.158, 0.397, 0.764, 0.535])

**Figure 26-21**  *Frame from PC1 to PC3—SPAN Copies Twice*

Enabling SPAN in this VLAN, for both directions, means that SPAN monitors both transmit and receive traffic on each port in that VLAN. The single frame shown in the figure would be seen by SPAN monitoring twice (on the receive function of the port on the left, and the transmit function of the port on the right), so SPAN would send two copies of this single frame to the destination port. Overall, this SPAN session would send twice as many frames as necessary out the SPAN destination port.

A much more efficient choice would be to use either the receive or transmit direction for the SPAN session. Figure 26-22 shows the logic, but now with the Tx bubbles removed, implying that SPAN has been enabled in the receive direction only. As a result, that one example frame sent by PC1 to PC3 is seen only once by SPAN’s monitoring logic, and only one copy of the frame is sent to the destination port.

![](bbox=[0.158, 0.785, 0.764, 0.91])

**Figure 26-22**  *Frame from PC1 to PC3—SPAN Copies Once*