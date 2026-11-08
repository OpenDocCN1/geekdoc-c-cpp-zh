This chapter focuses on HSRP and does not discuss VRRP and GLBP other than this brief mention. HSRP, the first of the three FHRP protocols to enter the market, remains a popular option in many networks. The next few pages walk through the concepts of how HSRP works. (Note that Appendix K contains a topic with more depth about GLBP, copied from an earlier edition of the book, if you are interested in reading more.)

# HSRP Concepts

HSRP operates with an active/standby model (also more generally called active/passive). HSRP allows two (or more) routers to cooperate, all being willing to act as the default router. However, at any one time, only one router actively supports the end-user traffic. The packets sent by hosts to their default router flow to that one active router. Then, the other routers, with an HSRP standby state, sit there patiently waiting to take over should the active HSRP router have a problem.

The HSRP active router implements a virtual IP address and matching virtual MAC address. This virtual IP address exists as part of the HSRP configuration, which is an additional configuration item compared to the usual ip address interface subcommand. This virtual IP address is in the same subnet as the interface IP address, but it is a different IP address. The router then automatically creates the virtual MAC address. All the cooperating HSRP routers know these virtual addresses, but only the HSRP active router uses these addresses at any one point in time.

Hosts refer to the virtual IP address as their default router address, instead of any one router’s interface IP address. For instance, in Figure 20-5, R1 and R2 use HSRP. The HSRP virtual IP address is 10.1.1.1, with the virtual MAC address referenced as VMAC1 for simplicity’s sake.

![](bbox=[0.088, 0.561, 0.867, 0.762])

| Host ARP Table |  |
|---|---|
| IP | MAC |
| 10.1.1.1 | VMAC1 |

**Figure 20-5** _All Traffic Goes to .1 (R1, Which Is Active); R2 Is Standby_