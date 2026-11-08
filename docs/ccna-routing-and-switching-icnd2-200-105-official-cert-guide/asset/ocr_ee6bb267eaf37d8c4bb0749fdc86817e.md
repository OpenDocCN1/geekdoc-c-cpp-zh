```
```
69 packets, 20914 bytes input
147 packets, 11841 bytes output

Virtual LAN ID: 10 (IEEE 802.1Q Encapsulation)

   VLAN Trunk Interface:    GigabitEthernet0/0.10

This is configured as native Vlan for the following interface(s) :
GigabitEthernet0/0        Native-vlan Tx-type: Untagged

   Protocols Configured:   Address:              Received:       Transmitted:
            IP             10.1.10.1                    2               3
         Other                                          0               1

   3 packets, 722 bytes input
   4 packets, 264 bytes output

Virtual LAN ID: 20 (IEEE 802.1Q Encapsulation)

   VLAN Trunk Interface:    GigabitEthernet0/0.20

   Protocols Configured:   Address:              Received:       Transmitted:
            IP             10.1.20.1                    0             134
         Other                                          0               1

   0 packets, 0 bytes input
 135 packets, 10498 bytes output
```
```

# Troubleshooting ROAS

The biggest challenge when troubleshooting ROAS has to do with the fact that if you misconfigure only the router, or misconfigure only the switch, the other device on the trunk has no way to know that the other side is misconfigured. That is, if you check the `show ip route` and `show vlans` commands on a router, and the output looks like it matches the intended configuration, and the connected routes for the correct subinterfaces show up, routing may still fail because of problems on the attached switch. So troubleshooting ROAS often begins with checking the configuration on both the router and switch, because there is no status output on either device that tells you where the problem might be.

First, to check ROAS on the router, you need to start with the intended configuration, and ask questions about the configuration:

![](bbox=[0.07, 0.874, 0.134, 0.92])

+   1. Is each non-native VLAN configured on the router with an encapsulation `dot1q vlan-id` command on a subinterface?
+   2. Do those same VLANs exist on the trunk on the neighboring switch (`show interfaces trunk`), and are they in the allowed list, not VTP pruned, and not STP blocked?