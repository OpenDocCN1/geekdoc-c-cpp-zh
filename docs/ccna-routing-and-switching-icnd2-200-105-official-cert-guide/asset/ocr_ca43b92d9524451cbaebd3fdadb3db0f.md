![](bbox=[0.237, 0.086, 0.734, 0.417])

# Figure 8-2 Sample Network for OSPF Single-Area Configuration

The beginning single-area configuration on R3, as shown in Example 8-2, enables OSPF on all the interfaces shown in Figure 8-2. First, the router ospf 1 global command puts the user in OSPF configuration mode, and sets the OSPF process-id. This number just needs to be unique on the local router, allowing the router to support multiple OSPF processes in a single router by using different process IDs. (The router command uses the process-id to distinguish between the processes.) The process-id does not have to match on each router, and it can be any integer between 1 and 65,535.

# **Example 8-2** OSPF Single-Area Configuration on R3 Using One network Command

```
```
router ospf 1
network 10.0.0.0 0.255.255.255 area 0
```
```

Speaking generally rather than about this example, the OSPF network command tells a router to find its local interfaces that match the first two parameters on the network command. Then, for each matched interface, the router enables OSPF on those interfaces, discovers neighbors, creates neighbor relationships, and assigns the interface to the area listed in the network command. (Note that the area can be configured as either an integer or a dotted-decimal number, but this book makes a habit of configuring the area number as an integer. The integer area numbers range from 0 through 4,294,967,295.)

For the specific command in Example 8-2, any matched interfaces are assigned to area 0. However, the first two parameters—the ip_address and wildcard_mask parameter values of 10.0.0.0 and 0.255.255.255—need some explaining. In this case, the command matches all three interfaces shown for Router R3; the next topic explains why.

# **Matching with the OSPF network Command**

The key to understanding the traditional OSPFv2 configuration shown in this first example is to understand the OSPF network command. The OSPF network command compares the