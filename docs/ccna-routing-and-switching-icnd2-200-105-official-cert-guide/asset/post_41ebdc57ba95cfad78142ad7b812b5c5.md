
Another useful marking field exists in the 802.1Q header, in a field originally defined by the IEEE 802.1p standard. This field sits in the third byte of the 4-byte 802.1Q header, as a 3-bit field, supplying eight possible values to mark (see Figure 18-7). It goes by two different names: *Class of Service*, or CoS, and *Priority Code Point*, or PCP.

Ethernet Frame

![](img/79473ea15699e01619d2aa789f5bd43b_1351_0.png)

**Figure 18-7** *Class of Service Field in 802.1Q/p Header*

The solution, LLQ, tells the scheduler to treat one or more queues as special *priority queues*. The LLQ scheduler always takes the next message from one of these special priority queues. Problem solved: very little delay for packets in that queue, resulting in very little jitter as well. Plus the queue never has time to fill up, so there are no drops due to the queue filling up. Figure 18-17 shows the addition of the LLQ logic for the voice queue.

![](img/79473ea15699e01619d2aa789f5bd43b_1354_0.png)

*Figure 18-17  LLQ Always Schedules Voice Packet Next*

This section about queuing introduces several connected ideas, so before leaving the discussion of queuing, think about this strategy for how most enterprises approach queuing in their QoS plans:

1. Use a round robin queuing method like CBWFQ for data classes and for noninteractive voice and video.
2. If faced with too little bandwidth compared to the typical amount of traffic, give data classes that support business-critical applications much more guaranteed bandwidth than is given to less important data classes.
3. Use a priority queue with LLQ scheduling for interactive voice and video, to achieve low delay, jitter, and loss.
4. Put voice in a separate queue from video, so that the policing function applies separately to each.
5. Define enough bandwidth for each priority queue so that the built-in policer should not discard any messages from the priority queues.
6. Use Call Admission Control (CAC) tools to avoid adding too much voice or video to the network, which would trigger the policer function.

Summarizing the key features of policing:

- It measures the traffic rate over time for comparison to the configured policing rate.
- It allows for a burst of data after a period of inactivity.
- It is enabled on an interface, in either direction, but typically at ingress.
- It can discard excess messages, but can also re-mark the message so that it is a candidate for more aggressive discard later in its journey.

Summarizing the key features of shapers:

- Shapers measure the traffic rate over time for comparison to the configured shaping rate.
- Shapers allow for bursting after a period of inactivity.
- Shapers are enabled on an interface for egress (outgoing packets).
- Shapers slow down packets by queuing them, and over time releasing them from the queue at the shaping rate.
- Shapers use queuing tools to create and schedule the shaping queues, which is very important for the same reasons discussed for output queuing.

The configuration and use of the native VLAN on the trunk requires a little extra thought. The native VLAN can be configured on a subinterface, or on the physical interface, or ignored as in Example 19-1. Each 802.1Q trunk has one native VLAN, and if the router needs to route packets for a subnet that exists in the native VLAN, then the router needs some configuration to support that subnet. The two options to define a router interface for the native VLAN are

- Configure the `ip address` command on the physical interface, but without an encapsulation command; the router considers this physical interface to be using the native VLAN.
- Configure the `ip address` command on a subinterface, and use the `encapsulation dot1q vlan-id native` subcommand to tell the router both the VLAN ID and the fact that it is the native VLAN.

First, to check ROAS on the router, you need to start with the intended configuration, and ask questions about the configuration:

1. Is each non-native VLAN configured on the router with an `encapsulation dot1q vlan-id` command on a subinterface?
2. Do those same VLANs exist on the trunk on the neighboring switch (`show interfaces trunk`), and are they in the allowed list, not VTP pruned, and not STP blocked?
3. Does each router ROAS subinterface have an IP address/mask configured per the planned configuration?
4. If using the native VLAN, is it configured correctly on the router either on a subinterface (with an `encapsulation dot1q vlan-id native` command) or implied on the physical interface?
5. Is the same native VLAN configured on the neighboring switch's trunk?
6. Are the router physical or ROAS subinterfaces configured with a `shutdown` command?

The second big area to investigate when troubleshooting SVIs relates to the SVI state, a state that ties to the state of the associated VLANs. Each VLAN interface has a matching VLAN of the same number, and the VLAN interface’s state is tied to the state of the VLAN in certain ways. In particular, for a VLAN interface to be in an up/up state:

1. **Step 1.** The VLAN must be defined on the local switch (either explicitly, or learned with VTP).

2. **Step 2.** The switch must have at least one up/up interface using the VLAN, either/both:
    - **A.** An up/up access interface assigned to that VLAN
    - **B.** A trunk interface for which the VLAN is in the allowed list, is STP forwarding, and is not VTP pruned

3. **Step 3.** The VLAN (not the VLAN interface) must be administratively enabled (that is, not shutdown).

4. **Step 4.** The VLAN interface (not the VLAN) must be administratively enabled (that is, not shutdown).

To see why, consider the design in Figure 19-4, which repeats the same design from Figure 19-3 (used in the SVI examples). In that familiar design, at least two access ports sit in both VLAN 10 and VLAN 20. However, that figure shows a single link from the switch to Router B1. As a result, the switch could configure that link as a routed port.

![](img/79473ea15699e01619d2aa789f5bd43b_1364_0.png)

**Figure 19-4** *Routing on a Routed Interface on a Switch*

> **NOTE** Cisco uses the term *EtherChannel* in concepts discussed in this section, and then uses the term port channel, with command keyword **port-channel**, when verifying and configuring EtherChannels. For the purposes of understanding the technology, you may treat these terms as synonyms. However, it helps to pay close attention to the use of the terms port channel and EtherChannel as you work through the examples in this section, because IOS uses both.

Example 19-12 shows an example of the configuration for a Layer 3 EtherChannel for switch SW1 in Figure 19-7. The EtherChannel defines a port-channel interface 12, and uses subnet 10.1.12.0/24.

![](img/79473ea15699e01619d2aa789f5bd43b_1366_0.png)

**Figure 19-7** Design Used in EtherChannel Configuration Examples

Additionally, you must do more than just configure the `channel-group` command correctly for all the physical ports to be bundled into the EtherChannel. Layer 2 EtherChannels have a longer list of requirements, but Layer 3 EtherChannels do require a few consistency checks between the ports before they can be added to the EtherChannel. The following is the list of requirements for Layer 3 EtherChannels:

- **no switchport:** The port-channel interface must be configured with the **no switchport** command, and so must the physical interfaces. If a physical interface is not also configured with the **no switchport** command, it will not become operational in the EtherChannel.
- **Speed:** The physical ports in the channel must use the same speed.
- **duplex:** The physical ports in the channel must use the same duplex.
