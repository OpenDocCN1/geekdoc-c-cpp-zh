SPAN configuration actually has quite a few dependencies, with the following list mentioning some of the most important dependencies:

![](bbox=[0.049, 0.14, 0.118, 0.19])

+   - A SPAN destination port can be used with only one SPAN session at a time.
+   - A SPAN destination port cannot also be a SPAN source port.
+   - When configured as a SPAN destination port, the switch no longer treats the port as a normal port. That is, the switch does not learn MAC addresses for received frames, or send frames based on matching the MAC table, for that port.
+   - A SPAN destination port can be unconfigured from one monitor session (`no monitor session number destination interface type number`) and then added to another monitor session.
+   - Multiple SPAN sources can be used in a single SPAN session.
+   - One SPAN session cannot mix interfaces and VLAN sources; that is, the sources must all be interfaces or all be VLANs.
+   - One SPAN session can use any combination of directions (transmit, receive, and both) as applied to different SPAN sources.
+   - EtherChannel interfaces can be used as source ports. Frames for all ports in the EtherChannel will be considered by SPAN.
+   - Trunks can be used as source ports. When used, by default, SPAN includes frames from all VLANs on that trunk, but SPAN VLAN filtering can limit the VLANs included.

The following list details the commands used to configure Local SPAN on a Cisco switch, collected into a checklist for easier review and study. Note that to configure the source port (interface), the command can refer to a single interface, or to the first and last interface numbers in a range. However, the command does not use a range keyword. (Explanations and examples follow the checklist.)

![](bbox=[0.057, 0.584, 0.118, 0.629])

+   1. **Step 1.** Use the `monitor session number source interface type number [ - last-in-range] [rx | tx | both]` command in global configuration mode to identify a SPAN session by number, and define one SPAN source interface. Repeat this command to define all SPAN source ports for this session.
+   2. **Step 2.** Use the `monitor session number source vlan vlan-id [rx | tx | both]` command in global configuration mode to identify a SPAN session by number, and define one SPAN source VLAN. Repeat this command to define all SPAN source VLANs for this session.
+   3. **Step 3.** Use the `monitor session number destination interface type number` global command to define the one SPAN destination port for the monitor session.

For example, Figure 26-20 shows the ideas behind the configuration of two monitor sessions in Example 26-16, numbered 1 and 2. SPAN session 1 uses two source ports, monitoring frames received on those ports. (Session 1 matches the earlier example shown in Figure 26-16.) SPAN session 2 shows the ideas of monitoring VLAN 11, for frames going in both directions on each port in VLAN 11, and sending copies of those frames out destination port G1/0/22. Example 26-16 shows the configuration that matches the figure.