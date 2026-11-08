First, focus on the two commands that should be in every OSPFv3 configuration: the **ipv6 router ospf** *process-id* global command and the **ipv6 ospf** *process-id* **area** *area-id* interface subcommand. The first command creates the OSPFv3 process by number. The second command, one per interface, enables that OSPFv3 process on the interface and assigns the area number. In this case, R2 has a process ID of 2, with both interfaces assigned to area 23.

Next, consider one completely optional feature: OSPFv3 passive interfaces. This feature uses the same concepts and literally the exact same command syntax as OSPFv2. If a router should not form neighbor relationships on an interface, that interface may be made passive. In this case, R2 should find at least one OSPFv3 neighbor on each of its two interfaces, so the configuration does not include the **passive-interface** command at all.

Finally, OSPFv3 follows the *exact* same rules as OSPFv2 when setting the OSPFv3 router ID (RID). The OSPFv3 RID is a 32-bit number, often written in dotted decimal, so it looks like an IPv4 address. The OSPFv3 RID is not a 12-bit number that is then represented to look like an IPv6 address. In this case, R2 sets its RID using the OSPFv3 **router-id** command, but you should be ready to configure all three ways.

Now on to the configuration on R3, which should have a very similar OSPFv3 configuration compared to R2. Both are internal routers in area 23, and both have at least one neighbor off their two interfaces, respectively, so neither can make either of their interfaces passive. Also, just to make the point that OSPFv3 neighbors may use different PID values, R3 uses OSPFv3 PID 3, while R2 uses PID 2. Example 23-2 shows the resulting configuration.

# Example 23-2   IPv6 and OSPFv3 Configuration on R3

```
    ipv6 unicast-routing
    !
    interface GigabitEthernet0/0
     mac-address 0200.0000.0003
     ipv6 address 2001:db8:1:23::3/64
     ipv6 ospf 3 area 23
    !
    interface serial 0/0/0
     ipv6 address 2001:db8:1:13::3/64
     ipv6 ospf 3 area 23
    !
    ipv6 router ospf 3
     router-id 3.3.3.3
```

Moving on to R4, in Example 23-3, the configuration differs slightly from that of the previous two routers. First, R4 can make its G0/1 interface passive because R4 expects to create no OSPFv3 neighbor relationships off that LAN interface. R4 also uses a different OSPFv3 PID.

> > **NOTE**  Although these examples use different OSPFv3 PIDs, to show that such a choice causes no problems, most enterprises would use the same PID value on all routers for consistency.