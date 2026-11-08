
It may be that an enterprise wants to implement a network exactly as shown in Figure 14-4, with two sites and two routers, with MetroE WAN connectivity using an E-Line service. Other variations exist, even other variations using an E-Line.

For example, think of a common enterprise WAN topology with a central site and 100 remote sites. As shown so far, with an E-Line service, the central site router would need 100 Ethernet interfaces to connect to those 100 remote sites. That could be expensive. As an alternative, the enterprise could use the design partially shown in Figure 14-5 (just three remote sites shown). In this case:

- The central site router uses a single 10-Gbps access link.
- The central site connects to 100 E-Lines (only three shown).
- All the E-Lines send and receive frames over the same access link.

![](img/79473ea15699e01619d2aa789f5bd43b_423_0.png)

**Figure 14-5** *Using Multiple E-Lines, One for Each Remote Site*

Note that this chapter does not get into the configuration details for WAN services. However, designs like Figure 14-5, with multiple E-Line services on a single access link, use 802.1Q trunking, with a different VLAN ID for each E-Line service. As a result, the router configuration can use a typical router configuration with trunking and subinterfaces.

Before moving on to the next MetroE service, note that the customer could use switches instead of routers to connect to the WAN. Historically, enterprise engineers place routers at the edge of a WAN, in part because that device connected to both the WAN and the LAN, and the LAN and WAN used different types of physical interfaces and different data link protocols. As a result of how routing works, routers served as the perfect device to sit at the edge between LAN and WAN (called the WAN edge). With MetroE, the LAN and WAN are both Ethernet, so an Ethernet switch becomes an option.

## Ethernet LAN Service (Full Mesh)

Imagine an enterprise needs to connect several sites to a WAN, and the goal is to allow every site to send frames directly to every other site. You could do that with E-Lines, but you would need possibly lots of E-Lines. For instance, to connect three sites with E-Lines so that each site could send frames directly to each other, you would need three E-Lines. But with four, five, and six sites, you would need 6, 10, and 15 E-Lines, respectively. Get up to 20 sites for which all could send frames directly to each other, and you would need 190 E-Lines. (The formula is N(N − 1) / 2.)

The people who created MetroE anticipated the need for designs that allow a full mesh—that is, for each pair of nodes in the service to send frames to each other directly. In fact, allowing all devices to send directly to every other device sounds a lot like an Ethernet LAN, so the MetroE service is called an *Ethernet LAN service*, or E-LAN.

One E-LAN service allows all devices connected to that service to send Ethernet frames directly to every other device, just as if the Ethernet WAN service were one big Ethernet switch. Figure 14-6 shows a representation of a single E-LAN EVC. In this case, the one EVC connects to four customer sites, creating one E-LAN. Routers R1, R2, R3, and R4 can all send frames directly to each other. They would also all be in the same Layer 3 subnet on the WAN.

![](img/79473ea15699e01619d2aa789f5bd43b_424_0.png)

**Figure 14-6** *MetroE Ethernet LAN Service—Any-to-Any Forwarding over the Service*

An E-LAN service connects the sites in a full mesh. The term *full mesh* refers to a design that, for a set of devices, creates a direct communication path for each pair. In contrast, a partial mesh refers to a design in which only some of the pairs can communicate directly. Ethernet Tree services (E-Trees), as discussed in the next topic, create a partial mesh design.

## Ethernet Tree Service (Hub and Spoke)

The Ethernet Tree service (E-Tree) creates a WAN topology in which the central site device can send Ethernet frames directly to each remote (leaf) site, but the remote (leaf) sites can send only to the central site. Figure 14-7 shows the topology, again with a single EVC. In this case, Router R1 is the root site, and can send to all three remote sites. Routers R2, R3, and R4 can send only to R1.

![](img/79473ea15699e01619d2aa789f5bd43b_424_1.png)

**Figure 14-7** *E-Tree Service Creates a Hub-and-Spoke Topology*

With an E-Tree, the central site serves as the root of a tree, and each remote site as one of the leaves. The topology goes by many names: partial mesh, hub-and-spoke, and point-to-multipoint. Regardless of the term you use, an E-Tree service creates a service that works well for designs with a central site plus many remote sites.

![](img/79473ea15699e01619d2aa789f5bd43b_429_0.png)

**Figure 14-12** *Example: 200-Mbps CIR Supported by 1-Gbps Access Links*

The big idea is simple, although the methods to control the data are new. The SP, per the contract with the customer, agrees to not only forward Ethernet frames between the two E-Line sites, but commits to a CIR of 200 Mbps. That is, the carrier commits to pass 200 Mbps worth of Ethernet frames over time.

When a customer asks for a new E-Line with a 200-Mbps CIR, they could send lots more data than 200 Mbps. Remember, the literal transmission rate would be 1 Gbps in this example, because the access links are 1-Gbps links. But over time, if all the customers who had asked for a 200-Mbps CIR E-Line sent lots more than 200 Mbps worth of data, the SP’s network could become too congested. The SP builds its network to support the traffic it has committed to send, plus some extra for expected overuse, and some extra for growth. But it is too expensive to build a network that allows customers that ask for and pay for 200 Mbps to send at 1 Gbps all the time.

## Controlling Overages with Policing and Shaping

To make the idea of fast access links with a slower CIR on the EVCs work, and work well, both the SP and the customer have to cooperate. The tools are two Quality of Service (QoS) tools called policing and shaping.

Historically, in some similar WAN services (like Frame Relay), the SP would actually let you send more data than your CIR, but MetroE networks typically use policing to discard the excess. A policer can watch incoming frames and identify the frames associated with each EVC. It counts the bytes in each frame, and determines a bit rate over time. When the customer has sent more bits than the CIR, the SP discards enough of the currently arriving frames to keep the rate down to the CIR. Figure 14-13 shows the location of policing in the same example shown in Figure 14-12.

![](img/79473ea15699e01619d2aa789f5bd43b_429_1.png)

**Figure 14-13** *SP Polices Incoming Traffic to Discard Excess Beyond CIR*

Recapping this scenario, the customer decides to ask the MetroE SP for an E-Line. The customer’s routers use a 1-Gbps access link that allows the E-Line to support a 200-Mbps CIR. To protect the SP’s network, the SP now uses ingress policing to monitor the bits/sec received over each end of the E-Line’s point-to-point EVC. And the SP discards some incoming frames when the rate gets too high.

![](img/79473ea15699e01619d2aa789f5bd43b_431_0.png)

**Figure 14-14** *Basic IP Routing of IP Packets*

An SP could just build an IP network and connect customers to it. However, MPLS allows the SP to connect to many customers and keep their IP traffic separated in some important ways. For instance, packets sent by one customer will not be forwarded to a second customer, and vice versa. So, rather than just build a generic IP network with routers, SPs use MPLS, which gives them many advantages when creating a Layer 3 service for their customers.

As with all the WAN services, how the SP creates the service is hidden from the customer for the most part. However, just to give you a little insight as to why MPLS is not just an IP network with routers: internally, the devices in an MPLS network use label switching, hence the name MPLS. The routers on the edge of the MPLS network add and remove an MPLS header as packets enter and exit the MPLS network. The devices inside the MPLS network then use the label field inside that MPLS header when forwarding data across the MPLS network.

> **NOTE** While MPLS VPNs provide a Layer 3 service to customers, MPLS itself is sometimes called a Layer 2.5 protocol, because it adds the MPLS header between the data link header (Layer 2) and the IP header (Layer 3).

As usual, the discussion of WAN services in this book ignores as much of the SP’s network as possible. For instance, you do not need to know how MPLS labels work. However, because MPLS VPNs create a Layer 3 service, the customer must be more aware of what the SP does, so you need to know a few facts about how an MPLS network approaches some Layer 3 functions. In particular, the SP’s MPLS network:

**Key Topic**

- Needs to know about the customer’s IP subnets
- Will run IP routing protocols to learn those routes
- Will use routes about the customer’s IP address space to make forwarding decisions

MPLS Virtual Private Networks (MPLS VPNs) is one common offering from SPs, available since the early 2000s, and is one of the most commonly used private WAN services today. Note that MPLS standards can be used to create other services besides Layer 3 MPLS VPNs. However, for the purposes of this chapter, all references to MPLS are specifically about MPLS VPNs.
