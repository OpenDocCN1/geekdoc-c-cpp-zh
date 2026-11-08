to some IPv6 routing problem, check the routers, count the EIGRP neighbor relationships, and make sure all the neighbor relationships exist. If any are missing, start troubleshooting EIGRP for IPv6 neighbor relationships based on Table 24-3.

To examine the neighbors, use the **show ipv6 eigrp neighbors** command. Because of the length of IPv6 addresses, this command lists two lines per neighbor rather than one line (as is the case with the EIGRP for IPv4 version of this command). The output in Example 24-8 shows this command's output from Router R2, with highlights in two lines for a single neighbor (R3).

# **Example 24-8** *R2's EIGRP for IPv6 Neighbors*

```
R2# show ipv6 eigrp neighbors
EIGRP-IPv6 Neighbors for AS(1)
H   Address                 Interface       Hold Uptime   SRTT   RTO  Q  Seq
                                             (sec)         (ms)       Cnt Num
2   Link-local address:     Se0/1/0        10 06:37:34   104   624  0  13
    FE80::D6C8:B5FF:FE69:DB48
1   Link-local address:     Se0/0/0        11 06:37:54     1   100  0  38
    FE80::FF:FE00:3
0   Link-local address:     Se0/0/1        11 06:46:11     1   100  0  30
    FE80::FF:FE00:1
```

Take a moment to focus on the IPv6 address and interface listed in the highlighted two lines. The output, taken from Router R2, lists R3's link-local address that sits on the other end of R2's S0/0/0 interface. The listed S0/0/0 interface is R2's interface. In summary, the details list the local router's interface and the neighbor's link-local address. So, to identify the EIGRP for IPv6 neighbor, you have to use that neighbor's link-local address (and not their EIGRP for IPv6 RID).

# ## EIGRP for IPv6 Topology Database

If you keep the discussions to topics within the scope of this book, once EIGRP for IPv6 routers become neighbors, they should exchange all appropriate topology data. Outside the scope of this book, other router features can filter the topology data sent between routers. But for now, if the neighbor comes up, you can assume they exchange the topology data.

However, you should be ready to interpret the meaning of some of the topology data described by EIGRP for IPv6. Thankfully, the EIGRP for IPv6 topology data works just like it does for EIGRP for IPv4, other than one obvious difference: It lists IPv6 prefixes. The following list points out the concepts that remain identical between the two:

+   - The metric components (bandwidth, delay, reliability, load)
+   - The metric calculation
+   - The idea of a successor route (the best route)
+   - The idea of FS routes
+   - The feasibility condition, in which the reported distance (the composite metric reported by the neighbor) is lower (better) than the local router's metric