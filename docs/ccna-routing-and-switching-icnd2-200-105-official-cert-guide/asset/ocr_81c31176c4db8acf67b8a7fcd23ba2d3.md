# (OSPFv2) Link-State Advertisements

Many people tend to get a little intimidated by OSPF LSAs when first learning about them. The output of the **show ip ospf database** command—a command that lists a summary of the output—is pretty long. Commands that look at specific LSAs list a lot more information. The details appear to be in some kind of code, using lots of numbers. It can seem like a bit of a mess.

However, if you examine LSAs while thinking about OSPF areas, and area design, some of the most common LSA types will make a lot more sense. For instance, think about the LSDB in one area. The topology details includes routers and the links between the routers. As it turns out, OSPF defines the first two types of LSAs to define those exact details, as follows:

+   - One *router* LSA for each router in the area
+   - One *network* LSA for each network that has a DR plus one neighbor of the DR

Next, think about the subnets in the other areas. The ABR creates summary information about each subnet in other areas—basically just the subnet IDs and masks—as a third type of LSA:

+   - One *summary* LSA for each subnet ID that exists in a different area

The next few pages discuss these three LSA types in a little more detail; Table K-3 lists some information about all three for easier reference and study.

**Table K-3** The Three OSPFv2 LSA Types Seen with a Multiarea OSPF Design

| Name | Number | Primary Purpose | Contents of LSA |
|---|---:|---|---|
| Router LSA | 1 | Describe a router | RID, interfaces, IP address/mask, current interface state (status) |
| Network | 2 | Describe a network that has a DR | DR and BDR IP addresses, subnet ID, mask |
| Summary | 3 | Describe a subnet in another area | Subnet ID, mask, RID of ABR that advertises the LSA |

> > **NOTE** In some networks, both OSPF and other routing protocols are used. In that case, one or more routers run both OSPF and the other routing protocol, with those routers acting as an OSPF Autonomous System Border Router, or ASBR, redistributing routing information between OSPF and the other protocol. In such a case, the ASBR creates a Type 4 LSA, which describes the ASBR itself, and Type 5 LSAs for each external route learned from the other routing protocol and then advertised into OSPF.

# Router LSAs Build Most of the Intra-Area Topology

OSPF needs very detailed topology information inside each area. The routers inside area X need to know all the details about the topology inside area X. And the mechanism to give routers all these details is for the routers to create and flood router (Type 1) and network (Type 2) LSAs about the routers and links in the area.