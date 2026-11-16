forth, just as it would if it were running on-premise. Behind the scenes, the Connectivity Service will step in as needed to broker connection requests, implement secure tunneling, and generally fill in the low-level technical requirements needed to ensure a seamless communication flow.

![](bbox=[0.148, 0.201, 0.942, 0.508])

# Figure 6.29 Understanding the Positioning of the Connectivity Service

Looking closely at Figure 6.29, you can see that calls to on-premise systems are brokered through a separate software component called the SAP HANA Cloud Connector. This software component establishes a secure SSL VPN tunnel between on-premise systems and an SAP HCP instance running in the cloud. Behind the scenes, the Connectivity Service works very closely with the Cloud Connector to establish connections to on-premise systems. From an application perspective, this is all conveniently abstracted behind the aforementioned Connectivity and Destination API.

In the upcoming sections, you'll see how these communication channels are established from a technical perspective. However, before we move on, we thought it might be useful to demonstrate some application scenarios that might call for the use of the Connectivity Service. We've highlighted some of the more common scenarios in Table 6.1. As you browse through this list, we should also point out that the Connectivity Service is not intended to be used as a general-purpose middleware. Instead, it's intended to be used for smaller, ad hoc service