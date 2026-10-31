![](bbox=[0.08, 0.12, 0.92, 0.42])

Figure 17-4: Processing Unit Modularization Example

design are driven by technical constraints. A processing unit that hosts a cache agent, for example, cannot host more than one cache agent and may not host any other type of agent.

Further partitioning of agents into processing units is generally driven by performance considerations. While there is a lot of tuning capability in each agent, there is a practical limitation as to how much can be done in a processing unit, which is just a JVM.

Figure 17-4 shows the processing unit modularization for the Claim Tracker example. Note that each processing unit contains exactly one agent. In keeping with the earlier demand analysis, there must be seventeen Cache PU and fourteen Monitor Claim Processing PU processing units to support the anticipated volume of activity.

# Clusters

Clusters are the highest level of organization for TIBCO BusinessEvents. To some extent your choice of which agents to use will determine the minimum number of clusters needed. For example, if you decide to use both process agents and inference agents, you have no choice other than to use at least two clusters since the two cannot be mixed in the same cluster (see Chapter 8).

More commonly, however, your decision to use multiple clusters will be driven by performance considerations. By default, communications between cache agents and other agents within a cluster occur via the multicast address that defines the cluster. If your solution involves cache objects that are unrelated to one another and share no logic, there is a performance advantage to using a different cluster for each group of cache objects and their related logic. Channels can then be used for communications between the clusters. This is the rationale for