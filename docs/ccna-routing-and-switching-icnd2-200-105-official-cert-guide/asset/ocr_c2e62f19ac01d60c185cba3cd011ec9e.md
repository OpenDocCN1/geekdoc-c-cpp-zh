Just to give you a sense of the scale of the IP routing tables used in the Internet core routers, check out the website http://bgp.potaroo.net, a site by Geoff Huston, who has been publishing statistics about the Internet for several decades. A check of this website while writing this chapter showed that the size of the BGP table in the Internet—which indicates the number of IPv4 routes expected to be in those routers—is at just over 600,000 entries. BGP has a big job to do.

# Advertising Routes with BGP

BGP exchanges routing information by using the same general process used by IGPs, but with some differences of course. To begin the BGP process, one router must have knowledge of some IPv4 prefix. It then uses a BGP protocol message (a BGP update message) to exchange the routing information with another router, as shown in Figure 12-1. With BGP, the other router is called a BGP neighbor or BGP peer.

![](bbox=[0.163, 0.348, 0.847, 0.473])

**Figure 12-1** *Using BGP Between Autonomous Systems*

One big difference with BGP compared to IGPs is that BGP advertises the routes to other routers in other companies, shown in the figure as other ISPs. IGPs, by definition, advertise routes to other routers inside the same company.

> **NOTE**  While IGPs advertise blocks of addresses that we generally refer to as *subnets*, with BGP, we refer to the blocks of addresses as either *prefixes*, *address blocks*, or even the formal BGP name, *Network Layer Reachability Information (NLRI)*. The reason for not using the word *subnet* is that, in practice, BGP seldom advertises address blocks as small as an individual subnet.

BGP differs from IGPs in its purpose, including the fact that, for an enterprise, BGP can be used to advertise the enterprise’s public IPv4 prefix to its local ISP. In Figure 12-1, the enterprise sits on the far left, with a BGP peering relationship to the enterprise’s ISP (ISP1 in this case). The enterprise then advertises its public prefix, Class C network 192.0.2.0/24, into ISP1. To create the global Internet, ISPs connect to each other, so ISP1 then advertises this prefix (192.0.2.0/24) to the other ISPs as shown, so that all parts of the Internet know how to forward packets to addresses in 192.0.2.0/24.