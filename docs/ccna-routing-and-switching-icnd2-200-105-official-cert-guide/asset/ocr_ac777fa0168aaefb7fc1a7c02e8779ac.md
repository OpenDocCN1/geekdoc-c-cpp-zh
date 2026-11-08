Example 1-2 shows how a switch can dynamically create a VLAN—the equivalent of the `vlan vlan-id` global config command—when the `switchport access vlan` interface subcommand refers to a currently unconfigured VLAN. This example begins with SW1 not knowing about VLAN 3. When the `switchport access vlan 3` interface subcommand was used, the switch realized that VLAN 3 did not exist, and as noted in the shaded message in the example, the switch created VLAN 3, using a default name (VLAN0003). No other steps are required to create the VLAN. At the end of the process, VLAN 3 exists in the switch, and interfaces Fa0/15 and Fa0/16 are in VLAN 3, as noted in the shaded part of the `show vlan brief` command output.

# VLAN Trunking Protocol

Before showing more configuration examples, you also need to know something about a Cisco protocol and tool called the VLAN Trunking Protocol (VTP). VTP is a Cisco proprietary tool on Cisco switches that advertises each VLAN configured in one switch (with the `vlan number` command) so that all the other switches in the campus learn about that VLAN. However, for various reasons, many enterprises choose not to use VTP.

Each switch can use one of three VTP modes: server, client, or transparent. Switches use either VTP server or client mode when the switch wants to use VTP for its intended purpose of dynamically advertising VLAN configuration information. However, with many Cisco switches and IOS versions, VTP cannot be completely disabled on a Cisco switch; instead, the switch disables VTP by using VTP transparent mode.

Chapter 5, "VLAN Trunking Protocol," discusses how to make use of VTP. Chapters 1 through 4 mostly ignore VTP. To that end, all examples in this book use switches that have been set either to use VTP transparent mode (with the `vtp mode transparent` global command) or to disable it (with the `vtp mode off` global command). Both options allow the administrator to configure both standard- and extended-range VLANs, and the switch lists the `vlan` commands in the running-config file.

Finally, on a practical note, if you happen to do lab exercises with real switches or with simulators, and you see unusual results with VLANs, check the VTP status with the `show vtp status` command. If your switch uses VTP server or client mode, you will find:

+   - The server switches can configure VLANs in the standard range only (1–1005).
+   - The client switches cannot configure VLANs.
+   - Both servers and clients may be learning new VLANs from other switches, and seeing their VLANs deleted by other switches, because of VTP.
+   - The `show running-config` command does not list any `vlan` commands.

If possible in lab, switch to VTP transparent mode and ignore VTP for your switch configuration practice until you are ready to focus on how VTP works when studying for the ICND2 exam topics.

**NOTE** Do not change VTP settings on any switch that also connects to the production network until you know how VTP works as explained in Chapter 5.