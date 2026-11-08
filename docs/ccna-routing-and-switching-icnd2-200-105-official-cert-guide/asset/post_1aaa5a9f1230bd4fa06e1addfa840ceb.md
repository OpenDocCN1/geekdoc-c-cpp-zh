
EIGRP neighbors. R1, with a single **network 10.0.0.0** EIGRP subcommand, enables EIGRP on all three of its interfaces (per Figure 10-1). The second command lists more detail per interface, including the local router's own Hello Interval and hold time and the split-horizon setting.

Note that neither command lists information about interfaces on which EIGRP is not enabled. For instance, had EIGRP not been enabled on S0/0/0, the **show ip eigrp interfaces detail S0/0/0** command would have simply listed no information under the heading lines. The shorter output of the **show ip eigrp interfaces** command omits interfaces on which EIGRP is not enabled.

Also, note that the **show ip eigrp interfaces...** command does not list information for passive interfaces. Like Open Shortest Path First (OSPF), EIGRP supports the **passive-interface *type number*** subcommand. On passive interfaces, EIGRP does not discover and form neighbor relationships. However, EIGRP still advertises about the subnet connected to the passive interface.

In summary, the **show ip eigrp interfaces** command lists information about interfaces enabled by EIGRP, but it does not list interfaces made passive for EIGRP.

The other two methods to find the EIGRP-enabled interfaces require an examination of the configuration and some thinking about the EIGRP rules. In real life, **show ip eigrp interfaces** is the place to start, but for the exam, you might have just the configuration, or you might not even have that. As an alternative, the **show ip protocols** command lists many details about EIGRP, including a shorthand repeat of the EIGRP **network** configuration commands. Example 10-4 lists these commands as gathered from Router R1.

### Example 10-4 *Using show ip protocols to Derive the List of EIGRP-Enabled Interfaces on R1*

```
R1# show ip protocols
*** IP Routing is NSF aware ***

Routing Protocol is "eigrp 1"
  Outgoing update filter list for all interfaces is not set
  Incoming update filter list for all interfaces is not set
  Default networks flagged in outgoing updates
  Default networks accepted from incoming updates
  EIGRP-IPv4 Protocol for AS(1)
    Metric weight K1=1, K2=0, K3=1, K4=0, K5=0
    NSF-aware route hold timer is 240
    Router-ID: 10.1.5.1
    Topology: 0 (base)
      Active Timer: 3 min
      Distance: internal 90 external 170
      Maximum path: 4
      Maximum hopcount 100
      Maximum metric variance 1

  Automatic Summarization: disabled
Maximum path: 4
Routing for Networks:
  10.0.0.0
  Routing Information Sources:
    Gateway           Distance          Last Update
    10.1.4.3               90            00:22:32
    10.1.5.2               90            00:22:32
  Distance: internal 90 external 170
```

To see the shorthand repeat of the EIGRP configuration, look toward the end of the example, under the heading Routing for Networks. In this case, the next line that lists 10.0.0.0 is a direct reference to the **network 10.0.0.0** configuration command shown in Example 10-1.

For configurations that use the wildcard mask option, the format of the **show ip protocols** command differs a little. Example 10-5 shows an excerpt of the **show ip protocols** command from R3. R3 uses the three **network** commands shown earlier in Example 10-2.

![](img/79473ea15699e01619d2aa789f5bd43b_307_0.png)

### Example 10-5 EIGRP Wildcard Masks Listed with **show ip protocols** on R3

```
R3# show ip protocols
! Lines omitted for brevity

  Automatic Summarization: disabled
  Maximum path: 4
  Routing for Networks:
    10.1.3.0/24
    10.1.4.0/24
    10.1.6.0/24
! Lines omitted for brevity
```

To interpret the meaning of the highlighted portions of this **show ip protocols** command, you have to do a little math. The output lists a number in the format of **/x** (in this case, **/24**). It represents a wildcard mask with x binary 0s, or in this case, 0.0.0.255.

Before moving on from the **show ip protocols** command, take a moment to read some of the other details of this command's output from Example 10-4. For instance, it lists the EIGRP router ID (RID), which for R1 is 10.1.5.1. EIGRP allocates its RID just like OSPF, based on the following:

![](img/79473ea15699e01619d2aa789f5bd43b_307_1.png)

- 1. The value configured with the **eigrp router-id** *number* EIGRP subcommand
- 2. The numerically highest IP address of an up/up loopback interface at the time the EIGRP process comes up
- 3. The numerically highest IP address of a nonloopback interface at the time the EIGRP process comes up

The only difference compared to OSPF is that the EIGRP RID is configured with the **eigrp router-id** *value* router subcommand, whereas OSPF uses the **router-id** *value* subcommand.

## Displaying EIGRP Neighbor Status

Once a router has enabled EIGRP on an interface, the router tries to discover neighboring routers by listening for EIGRP Hello messages. If two neighboring routers hear Hellos from each other and the required parameters match correctly, the routers become neighbors.

The best and most obvious command to list EIGRP neighbors is **show ip eigrp neighbors**. This command lists neighbors based on their interface IP address (and not based on their router ID, which is the convention with OSPF). The output also lists the local router’s interface out of which the neighbor is reachable.

For instance, Example 10-6 shows Router R1’s neighbors, listing a neighbor with IP address 10.1.4.3 (R3). It is reachable from R1’s S0/0/1 interface according to the first highlighted line in the example.

### Example 10-6 *Displaying EIGRP Neighbors from Router R1*

```
R1# show ip eigrp neighbors
EIGRP-IPv4 Neighbors for AS(1)
H   Address                 Interface              Hold Uptime   SRTT   RTO  Q  Seq
                                                   (sec)         (ms)        Cnt Num
1   10.1.4.3                Se0/0/1                13 00:05:49   2   100  0  29
0   10.1.5.2                Se0/0/0                12 00:05:49   2   100  0  39
```

The right side of the output also lists some interesting statistics. The four rightmost columns have to do with RTP, as discussed in Chapter 9, “Understanding EIGRP Concepts.” The uptime lists the elapsed time since the neighbor relationship started. Finally, the hold time should be the current countdown from the Hold Interval (15 seconds in this case) down toward 0. In this case, with a Hello Interval of 5 and a Hold Interval of 15, this counter will vary from 15 down to 10 and then reset to 15 when the next Hello arrives.

Another less-obvious way to list EIGRP neighbors is the **show ip protocols** command. Look back again to Example 10-4, to the end of the **show ip protocols** command output from R1. That output under the heading Routing Information Sources lists the same two neighboring routers’ IP addresses, as does the **show ip eigrp neighbors** command in Example 10-6.

## Displaying the IPv4 Routing Table

Once EIGRP routers become neighbors, they exchange routing information, store it in their topology tables, and then calculate their best IPv4 routes. This section skips past the verification steps for the EIGRP topology table, saving that for the second major topic in the chapter, as an end to itself. However, you should find the IP routing table verification steps somewhat familiar at this point. Example 10-7 shows a couple of examples from R1 in Figure 10-1: the first showing the entire IPv4 routing table, and the second with the **show ip route eigrp** command listing only EIGRP-learned routes.

### Example 10-7 *IP Routing Table on Router R1 from Figure 10-1*

```
R1# show ip route
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
```
