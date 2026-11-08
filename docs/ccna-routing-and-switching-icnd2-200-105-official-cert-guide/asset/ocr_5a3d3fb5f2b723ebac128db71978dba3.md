```
    The port is in the portfast mode
    Link type is point-to-point by default
    Bpdu guard is enabled
    BPDU: sent 1721, received 0
```

PortFast and BPDU Guard are disabled by default on all interfaces, and to use them, each interface requires interface subcommands like those in Example 3-6. Alternately, for both features, you can enable the feature globally. Then, for interfaces for which the feature should be disabled, you can use another interface subcommand to disable the feature.

The ability to change the global default for these features reduces the number of interface subcommands required. For instance, on an access layer switch with 48 access ports and two uplinks, you probably want to enable both PortFast and BPDU Guard on all 48 access ports. Rather than requiring the interface subcommands on all 48 of those ports, enable the features globally, and then disable them on the uplink ports.

Table 3-3 summarizes the commands to enable and disable both PortFast and BPDU Guard, both globally and per interface. For instance, the global command spanning-tree portfast default changes the default so that all interfaces use PortFast, unless a port also has the spanning-tree portfast disable interface subcommand configured.

**Table 3-3** Enabling and Disabling PortFast and BPDU Guard, Globally and Per Interface

| Action | Globally | One Interface |
| --- | --- | --- |
| Disable PortFast | no spanning-tree portfast default | spanning-tree portfast disable |
| Enable PortFast | spanning-tree portfast default | spanning-tree portfast |
| Disable BPDU Guard | no spanning-tree portfast bpduguard default | spanning-tree bpduguard disable |
| Enable BPDU Guard | spanning-tree portfast bpduguard default | spanning-tree bpduguard enable |

Example 3-8 shows another new command, **show spanning-tree summary**. This command shows the current global settings for several STP parameters, including the PortFast and BPDU Guard features. This output was gathered on a switch that had enabled both PortFast and BPDU Guard globally.

# **Example 3-8** Displaying Status of Global Settings for PortFast and BPDU Guard

```
    SW1# show spanning-tree summary
    Switch is in pvst mode
    Root bridge for: none
    EtherChannel misconfig guard is enabled
    Extended system ID           is enabled
    PortFast Default             is enabled
    PortFast BPDU Guard Default  is enabled
    PortFast BPDU Filter Default is disabled
    Loopguard Default            is disabled
    UplinkFast                   is disabled
    BackboneFast                 is disabled
```