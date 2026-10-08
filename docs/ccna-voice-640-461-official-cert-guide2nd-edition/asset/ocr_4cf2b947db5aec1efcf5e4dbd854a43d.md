Note: I'm sure at this point, many of you have a look of concern because of this question: "If the CUCM Publisher has the only writable copy of the database, what happens if it fails? If the Publisher fails, the CUCM cluster goes into a type of "locked configuration" mode. You can no longer make changes to the database (such as adding a new IP phone, changing the route plan, modifying a music on hold selection, and so on). The only exception to this is the user-facing features. These include functions such as forwarding your phone, enabling the message waiting light, pressing the Do Not Disturb button, and many others. The CUCM Subscribers are able to write these changes to their local database, replicate them to the other subscribers in the cluster, and eventually back to the Publisher when you have restored connectivity. By allowing the user-facing features to write to the Subscriber database, the users will never know when a Publisher failure has occurred! This capability emerged in CUCM version 5 and beyond. Before this version, a Publisher failure absolutely impacted the user experience.

Once you understand the database replication piece of CUCM, the call flow is nearly identical to CME, as shown in Figure 2-6.

# CUCM Cluster

![](bbox=[0.144, 0.375, 0.855, 0.814])

Figure 2-6 CUCM Call Processing

As with CME, the primary CUCM server used by the Cisco IP Phone receives the SCCP or SIP off-hook message and responds appropriately in a stimulus/response fashion until the call is placed. One difference is that the IP phones can now use redundant servers (as opposed to the single CME router). Based on your configuration, a phone can use a list of