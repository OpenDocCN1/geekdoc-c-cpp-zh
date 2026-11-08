```
```
Configured Pathcost method used is short

Name                 Blocking Listening Learning Forwarding STP Active
-------------------- -------- --------- --------- ---------- ----------
VLAN0001                     3         0         0          2          5
-------------------- -------- --------- --------- ---------- ----------
1 vlan                       3         0         0          2          5
```
```

# Configuring EtherChannel

As introduced back in Chapter 2, two neighboring switches can treat multiple parallel links between each other as a single logical link called an *EtherChannel*. STP operates on the EtherChannel, instead of the individual physical links, so that STP either forwards or blocks on the entire logical EtherChannel for a given VLAN. As a result, a switch in a forwarding state can then load balance traffic over all the physical links in the EtherChannel. Without EtherChannel, only one of the parallel links between two switches would be allowed to forward traffic, with the rest of the links blocked by STP.

> **NOTE**  All references to EtherChannel in this Chapter refer to Layer 2 EtherChannels, and not to Layer 3 EtherChannels (as discussed in Chapter 19, “IPv4 Routing in the LAN”).

EtherChannel may be one of the most challenging switch features to make work. First, the configuration has several options, so you have to remember the details of which options work together. Second, the switches also require a variety of other interface settings to match among all the links in the channel, so you have to know those settings as well.

This section focuses on the correct EtherChannel configuration. Chapter 4’s section “Troubleshooting Layer 2 EtherChannel” looks at many of the potential problems with EtherChannel, including all those other configuration settings that a switch checks before allowing the EtherChannel to work.

# Configuring a Manual EtherChannel

The simplest way to configure an EtherChannel is to add the correct **channel-group** command to each physical interface, on each switch, all with the one keyword. The one keyword tells the switches to place a physical interface into an EtherChannel.

Before getting into the configuration and verification, however, you need to start using three terms as synonyms: *EtherChannel*, *PortChannel*, and *Channel-group*. Oddly, IOS uses the **channel-group** configuration command, but then to display its status, IOS uses the **show etherchannel** command. Then, the output of this show command refers to neither an “EtherChannel” nor a “Channel-group,” instead using the term “PortChannel.” So, pay close attention to these three terms in the example.

To configure an EtherChannel manually, follow these steps:

+   1. **Step 1.** Add the **channel-group number mode** command in interface configuration mode under each physical interface that should be in the channel to add it to the channel.

![](bbox=[0.068, 0.879, 0.126, 0.917])