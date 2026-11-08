# ## Autosummarization and Discontiguous Classful Networks

Older routing protocols, namely RIPv1 and IGRP, were classified as classful routing protocols. This term comes from the fact that these classful routing protocols had to pay more attention to details about Class A, B, and C networks, in part because of the simplicity of the routing protocol.

These older classful routing protocols also had to use a more careful and cautious subnet design plan to avoid a problem called a discontiguous classful network. These simpler old routing protocols just got confused when a classful network became discontiguous, because of a required feature of classful routing protocols called autosummarization.

Today, most enterprises use OSPF or EIGRP, or in rare cases, RIPv2. All these protocols are classless routing protocols. As a result, these newer routing protocols can be configured so that the old problem with discontiguous classful networks is not a problem at all.

However, while the more recent IOS versions use good default settings so that this problem can be ignored, EIGRP allows the possibility of enabling the autosummary feature, which then requires the network engineer to be aware of this old discontiguous network problem. So, just in case, these next few pages first discuss the autosummary feature, followed by a discussion of the routing problems that can occur as a result.

> > **NOTE** In real networks, most people simply choose to avoid using autosummary today.

# ## Automatic Summarization at the Boundary of a Classful Network

A routing protocol that uses autosummary automatically creates a summary route under certain conditions. In particular, when a router sits at the boundary between classful networks—that is, with some interfaces in one Class A, B, or C network and other interfaces in another Class A, B, or C network—the router summarizes routes. Routes from one classful network are summarized as one route to the entire Class A, B, or C network. More formally:

![](bbox=[0.074, 0.652, 0.128, 0.699])

Routes related to subnets in network X, when advertised out an interface whose IP address is not in network X, are summarized and advertised as one route. That route is for the entire Class A, B, or C network X.

As usual, an example makes the concept much clearer. Consider Figure 10-9, which shows two networks in use: 10.0.0.0 and 172.16.0.0. R3 has four (connected) routes to subnets of network 10.0.0.0 on the right, and one interface on the left connected to a different classful network, Class B network 172.16.0.0. As a result, R3, with autosummary enabled, will summarize a route for all of Class A network 10.0.0.0.

Let’s follow the steps in the figure:

+   1. R3 has autosummary enabled, with the EIGRP auto-summary router subcommand.
+   2. R3 advertises a route for all of Class A network 10.0.0.0, instead of advertising routes for each subnet inside network 10.0.0.0 because the link to R2 is in another network (172.16.0.0).
+   3. R2 learns one route in network 10.0.0.0: a route to 10.0.0.0/8, which represents all of network 10.0.0.0, with R3 as the next-hop router.