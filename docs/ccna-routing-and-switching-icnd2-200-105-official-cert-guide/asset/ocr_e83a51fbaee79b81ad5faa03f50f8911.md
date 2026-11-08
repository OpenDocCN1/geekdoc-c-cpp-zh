# Key Topic

# Table 3-2  STP Defaults and Configuration Options

| Setting | Default | Command(s) to Change Default |
|---|---|---|
| BID priority | Base: 32,768 | `spanning-tree vlan vlan-id root [primary \| secondary]`<br>`spanning-tree vlan vlan-id priority priority` |
| Interface cost | 100 for 10 Mbps<br>19 for 100 Mbps<br>4 for 1 Gbps<br>2 for 10 Gbps | `spanning-tree vlan vlan-id cost cost` |
| PortFast | Not enabled | `spanning-tree portfast` |
| BPDU Guard | Not enabled | `spanning-tree bpduguard enable` |

Next, the configuration section shows how to examine the operation of STP in a simple network, along with how to change these optional settings.

# Verifying STP Operation

Before taking a look at how to change the configuration, first consider a few STP verification commands. Looking at these commands first will help reinforce the default STP settings. In particular, the examples in this section use the network shown in Figure 3-4.

![](bbox=[0.176, 0.487, 0.741, 0.787])

**Figure 3-4**  *Sample LAN for STP Configuration and Verification Examples*

Example 3-1 begins the discussion with a useful command for STP: the `show spanning-tree vlan 10` command. This command identifies the root switch and lists its settings on the local switch. Example 3-1 lists the output of this command on both SW1 and SW2, as explained following the example.