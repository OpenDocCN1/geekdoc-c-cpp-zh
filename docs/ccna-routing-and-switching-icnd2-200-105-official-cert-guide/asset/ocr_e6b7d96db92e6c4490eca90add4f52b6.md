as 1. Setting the value to 1 disables the feature, so that RIP places the first-learned equal-metric route into the routing table.

# ## Understanding Autosummarization and Discontiguous Classful Networks

Older routing protocols, namely RIPv1 and IGRP, were classified as *classful routing protocols*. These older classful routing protocols had to use a more careful and cautious subnet design plan to avoid a problem called a *discontiguous classful network*. These simpler old routing protocols just got confused when a classful network became discontiguous, because of a required feature of classful routing protocols called *autosummarization*.

Today, most enterprises use OSPF or EIGRP, or in a few cases, RIPv2. All these protocols are *classless routing protocols*. These classless routing protocols either do not have a problem with discontiguous classful networks or can be configured so they do not have a problem. In fact, when using RIPv2, if you simply configure the no auto-summary RIP subcommand on every router, you can avoid the problem altogether. But of course, it helps to understand what the problem is as well, so this section looks at both autosummarization and the discontiguous network problem.

A routing protocol that uses autosummarization automatically creates a summary route under certain conditions. That automatic process happens when

+   - That one router connects to subnets of multiple different classful networks
+   - That router uses a routing protocol that uses the autosummary feature. (Note that classful routing protocols had to use this feature and could not disable it.)

To see specifically what that means, consider Figure G-12, which shows one router (R3) that connects to several subnets of network 10.0.0.0 on the right and to a serial link in network 172.16.0.0 on the left. In other words, R3 meets the first criteria in the list. If using a routing protocol with the autosummarization feature, R3, when advertising a route to the left toward R2, would automatically create a summary route; a route for the entire Class A network 10.0.0.0, as shown in the figure.

![](bbox=[0.11, 0.617, 0.85, 0.734])

**Figure G-12** *Autosummarization Example*

Following the steps in the figure:

+   1. R3 has autosummary enabled, with the RIPv2 auto-summary router subcommand.
+   2. R3 advertises a route for all of Class A network 10.0.0.0, instead of advertising routes for each subnet inside network 10.0.0.0, because the link to R2 is a link in another network (172.16.0.0).