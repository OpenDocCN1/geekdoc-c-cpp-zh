The following commands represent typical operations on a Cisco 2950 switch:

```
```text
Switch>enable
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#interface fastethernet 0/4
Switch(config-if)#switchport mode access
Switch(config-if)#

             cdp                 Global CDP configuration subcommands
             channel-group       Etherchannel/port bundling configuration
             channel-protocol    Select the channel protocol (LACP, PAgP)
             description         Interface specific description
             duplex              Configure duplex operation.
             exit                Exit from interface configuration mode
             mac-address         Manually set interface MAC address
             mls                 Mls interface command
             no                  Negate a command or set its defaults
             shutdown            Shutdown the selected interface
             spanning-tree       Spanning Tree Subsystem
             speed               Configure speed operation.
             storm-control      Storm configuration
             switchport          Set switching mode characteristics
             tx-ring-limit       Configure PA level transmit ring limit
Switch(config-if)#cdp enable
Switch(config-if)#mls ?
 qos  qos command keyword
Switch(config-if)#mls qos trust ?
 cos       cos keyword
 device    trusted device class
 dscp      dscp keyword
 <cr>
Switch(config-if)#mls qos trust device cisco-phone
Switch(config-if)#exit
```
```

# Routers

The Cisco routers used for VoIP services are also called integrated services routers (ISRs). Cisco has offered several router series over the years. Older Cisco equipment, including 1700 series, 2600 series, and 3600 series routers, can still be used to implement and test VoIP labs. The newer 800, 1800, 2800, and 3800 series of routers