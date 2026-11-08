# **Example K-8**  *LSDB Content in Area 4, as Viewed from R4*

```
R4# show ipv6 ospf database

              OSPFv3 Router with ID (4.4.4.4) (Process ID 4)

                         Router Link States (Area 4)

ADV Router       Age        Seq#          Fragment ID  Link count  Bits
  1.1.1.1        258        0x80000072    0            1           B
  4.4.4.4        257        0x80000030    0            1           None

                         Net Link States (Area 4)

ADV Router       Age        Seq#          Link ID       Rtr count
  4.4.4.4        257        0x80000001    4             2

                    Inter Area Prefix Link States (Area 4)

ADV Router       Age        Seq#          Prefix
  1.1.1.1        878        0x80000069    2001:DB8:1:1::/64
  1.1.1.1        878        0x80000068    2001:DB8:1:2::/64
  1.1.1.1        364        0x8000000B    2001:DB8:1:13::/64
  1.1.1.1        364        0x8000000A    2001:DB8:1:23::/64
  1.1.1.1        364        0x8000000A    2001:DB8:1:12::/64
! Lines omitted for brevity
```

> **NOTE** The content under the heading “IPv6 Routing Protocols as Discussed in this Book” has not been previously published in this book, but was written in an early draft for the *Cisco CCNA Routing and Switching ICND2 200-105 Official Cert Guide.*

# IPv6 Routing Protocols as Discussed in This Book

This book discusses the traditional approach to OSPF only; that is, other than this brief introduction, it ignores OSPFv3 address families. In the earlier chapters of this book, all the OSPF examples you have seen for IPv4 are OSPFv2 examples. This section shows examples of OSPFv3, for IPv6 routes only, and specifically OSPFv3 without using the address families feature.

EIGRP (discussed in Chapter 24) has gone through a similar transformation as OSPF through its history of IPv6 support. Cisco calls the traditional EIGRP style either EIGRP *classic* mode or EIGRP *autonomous system* mode. EIGRP supports a newer mode called EIGRP *named* mode; this mode, like OSPFv3's address family mode, uses address families in the configuration. Chapter 24 discusses EIGRP for IPv6 classic mode.

To close the list, Routing Information Protocol (RIP) also supports IPv6, but its history does not track quite as closely. RIP has two versions that support IPv4, with the expected names