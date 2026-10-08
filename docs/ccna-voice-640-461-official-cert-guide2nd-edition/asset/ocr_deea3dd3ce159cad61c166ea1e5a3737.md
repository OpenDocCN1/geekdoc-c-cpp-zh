remote (called) phone. The RTP voice streams extend from each phone across the WAN to the other phone. Figure 10-7 illustrates call flow in a distributed deployment.

# Route Pattern

![](bbox=[0.093, 0.146, 0.435, 0.375])

Figure 10-6 WAN Failure to SRST/CFUR

![](bbox=[0.093, 0.433, 0.826, 0.638])

Figure 10-7 Distributed Deployment Call Flow CUCM Call-Routing Components

The signaling protocols available include Inter-Cluster Trunk (ICT), H.323, and Session Initiation Protocol (SIP). CUCM clusters at each site control their local phones using Skinny Client Control Protocol (SCCP) or SIP. The use of gatekeepers (along with a well-designed dial-plan) may allow scalability to thousands of sites, with either a full CUCM for large sites or a CUME for smaller sites (third-party solutions may also be integrated). PSTN backup for WAN failure is achieved through a hierarchical dial-plan, and gatekeeper may be used when bandwidth for calls is not available.

**Note:** Location-based CAC does not work in a distributed deployment because the clusters do not communicate their current bandwidth utilization to other clusters. Instead, Gatekeeper CAC provides a centralized service to track available bandwidth between clusters and trigger AAR when necessary. Gatekeeper is a router IOS feature set that may be configured on one or more gateway routers in the system.