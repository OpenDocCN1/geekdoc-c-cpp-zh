![](bbox=[0.168, 0.096, 0.595, 0.282])

**Figure 10-9**  *Autosummarization*

Example 10-16 shows the output of the show ip route command on R2, confirming the effect of the auto-summary setting on R3.

# **Example 10-16**  *R2 with a Single Route in Network 10.0.0.0 for the Entire Network*

```
R2# show ip route eigrp
! lines omitted for brevity

D    10.0.0.0/8 [90/2297856] via 172.16.3.3, 00:12:59, Serial0/0/0
```

Note that auto-summary by itself causes no problems. In the design shown in Figure 10-9, and in the command output in Example 10-16, no problems exist. R2 can forward packets to all subnets of network 10.0.0.0 using the one highlighted summary route, sending those packets to R3 next.

# Discontiguous Classful Networks

Autosummarization does not cause any problems as long as the summarized network is contiguous rather than discontiguous. U.S. residents can appreciate the concept of a discontiguous network based on the common term contiguous 48, referring to the 48 U.S. states besides Alaska and Hawaii. To drive to Alaska from the contiguous 48, for example, you must drive through another country (Canada, for the geographically impaired), so Alaska is not contiguous with the 48 states. In other words, it is discontiguous.

To better understand what the terms contiguous and discontiguous mean in networking, refer to the following two formal definitions when reviewing the example of a discontiguous classful network that follows:

# Key Topic

+   - **Contiguous network:** A classful network in which packets sent between every pair of subnets can pass only through subnets of that same classful network, without having to pass through subnets of any other classful network.
+   - **Discontiguous network:** A classful network in which packets sent between at least one pair of subnets must pass through subnets of a different classful network.

Figure 10-10 creates an expanded version of the internetwork shown in Figure 10-9 to create an example of a discontiguous network 10.0.0.0. In this design, some subnets of network 10.0.0.0 sit off R1 on the left, whereas others still connect to R3 on the right. Packets passing between subnets on the left to subnets on the right must pass through subnets of Class B network 172.16.0.0.