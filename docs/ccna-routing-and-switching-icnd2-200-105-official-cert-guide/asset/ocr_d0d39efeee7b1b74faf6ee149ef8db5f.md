**NOTE** All the troubleshooting examples in the rest of this chapter use the example configuration from Routers R1, R2, R3, and R4, as shown in Figure 24-2.

# EIGRP for IPv6 Interfaces

By enabling EIGRP for IPv6 on an interface, the router attempts to do two things:

+   1. Discover EIGRP for IPv6 neighbors off that interface
+   2. Advertise about the prefix connected to that interface

To make sure that EIGRP for IPv6 works correctly, an engineer should verify that EIGRP for IPv6 is enabled on the right interfaces. Or, from a troubleshooting perspective, one of the most common problems with EIGRP for IPv6 may be that a router did not enable EIGRP for IPv6 on an interface.

As was the case for EIGRP for IPv4, with EIGRP for IPv6, some commands list all interfaces on which EIGRP is enabled (including passive), some list all EIGRP interfaces but note which are passive, and some simply do not list the passive interfaces. Example 24-6 shows a sample that points out these differences, by first making R1’s G0/0 interface passive. It then lists output from the show ipv6 eigrp interfaces command, which omits G0/0, and then the show ipv6 protocols command, which includes G0/0, but noted as a passive interface.

# **Example 24-6**  *Verifying OSPFv3 Interfaces and Related Parameters*

```
R1# configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.

R1(config)# ipv6 router eigrp 1
R1(config-rtr)# passive-interface g0/0
R1(config-rtr)# ^Z

R1#
R1# show ipv6 eigrp interfaces
EIGRP-IPv6 Interfaces for AS(1)

                                      Xmit Queue   Mean   Pacing Time  Multicast  Pending
Interface        Peers   SRTT (ms)  Un/Reliable  SRTT   Un/Reliable Flow Timer  Routes
Se0/0/0             1        0/0       1       0/15       50        0
Se0/0/1             1        0/0       1       0/15       50        0

R1# show ipv6 protocols
IPv6 Routing Protocol is "connected"
IPv6 Routing Protocol is "eigrp 1"
EIGRP-IPv6 Protocol for AS(1)
  Metric weight K1=1, K2=0, K3=1, K4=0, K5=0
  NSF-aware route hold timer is 240
  Router-ID: 1.1.1.1
  Topology: 0 (base)
    Active Timer: 3 min
    Distance: Internal 90 external 170
    Maximum path: 16
```