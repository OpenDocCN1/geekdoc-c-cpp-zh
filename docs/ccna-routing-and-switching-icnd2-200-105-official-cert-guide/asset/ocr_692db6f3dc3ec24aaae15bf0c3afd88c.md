# Layer 2 Issues on the Access Link (Step 2)

If a router’s physical interface line status is up, but the line protocol status (second status code) is down, the link usually has a Layer 2 problem between the router and the local Frame Relay switch. With Frame Relay interfaces, the problem is often related to either the encapsulation command or the Frame Relay LMI.

The potential problem related to the encapsulation command is simple to check. If a router’s serial interface configuration omits the encapsulation frame-relay interface subcommand but the physical access link is working, the physical interface settles into an up/down state. If the configuration is unavailable, the **show interfaces** command can be used to see the configured encapsulation type, which is listed in the first few lines of command output.

The other potential problem relates to the LMI. LMI status messages flow in both directions between a router (data terminating equipment [DTE]) and Frame Relay switch (data circuit-terminating equipment [DCE]) for two main purposes:

+   - For the DCE to inform the DTE about each VC’s DLCI and its status
+   - To provide a keepalive function so that the DTE and DCE can easily tell when the access link can no longer pass traffic

A router places the physical link in an up/down state when the link physically works, but the router ceases to hear LMI messages from the switch. With the interface not in an up/up state, the router does not attempt to send any IP packets out the interface, so all pings should fail at this point.

A router might cease to receive LMI messages from the switch because of both legitimate reasons and mistakes. The normal legitimate purpose for the LMI keepalive function is that if the link really is having problems, and cannot pass any data, the router can notice the loss of keepalive messages and bring the link down. This allows the router to use an alternative route, assuming that an alternative route exists. However, a router might cease to receive LMI messages and bring down the interface because of the following mistakes:

+   - Disabling LMI on the switch, but leaving it enabled on the router
+   - Configuring different LMI types on the router (with the frame-relay lmi-type *type* physical interface subcommand) and the switch, so that the router and Frame Relay switch do not understand each other’s LMI messages

You can easily check for both encapsulation and LMI using the **show frame-relay lmi** command. This command lists output for interfaces only if the interface has the **encapsulation frame-relay** command configured, so you can quickly confirm whether the encapsulation frame-relay command is configured on the correct serial interfaces. This command also lists the LMI type used by the router, and it shows counters for the number of LMI messages sent and received. Example 1-19 shows an example from router R1 in Figure 1-7.

# Example 1-19  show frame-relay lmi Command on R1

```
R1# show frame-relay lmi

LMI Statistics for interface Serial0/0/0 (Frame Relay DTE) LMI TYPE = ANSI
    Invalid Unnumbered info 0              Invalid Prot Disc 0
    Invalid dummy Call Ref 0               Invalid Msg Type 0
```

![](bbox=[0.069, 0.358, 0.124, 0.394])