# 10.2 Use Cases

At this point, you might be asking yourself how you will know in which situations SAP HCI might be applicable or relevant.

Imagine that you have a scenario that requires you to integrate two different applications that have been built on top of SAP HCP. You might be tempted to build direct connections between the different applications using homegrown solutions facilitated by the SAP HCP Connectivity Service. At first sight, this might be an easy and quick solution, especially with fewer applications to connect. However, its disadvantages become visible as the organization’s cloud application landscape becomes more complex and larger. The point-to-point approach forms a spider web of application connections, as shown in Figure 10.2. This connection spaghetti will keep growing exponentially as more systems are introduced into the landscape.

![](bbox=[0.15, 0.42, 0.85, 0.71])

Figure 10.2 Point-to-Point Integration: Cloud Applications Directly Connected to Each Other

When using the point-to-point integration approach, each system is aware of the connection and message details of the system on the other side of the exchange. Every time a particular system changes or needs to be replaced, the impact will be felt by all other systems communicating with it. If a vulnerable security connection is discovered in one of the systems, then all applications currently connecting with it will need to be changed, adapted, and potentially be unavailable for a