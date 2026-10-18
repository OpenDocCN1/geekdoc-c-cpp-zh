![](bbox=[0.297, 0.095, 0.701, 0.313])

tal energy expenditure on the nodes, and average message communication time, if the network has a so-called *leader* that will take control of message routing with a view to optimizing those parameters. Again, referring to Figure 1.5 with seven nodes in the ad hoc network, the node 4 is elected as a leader and after this election, node 4 broadcasts a message to all other nodes informing them of its election as the leader.

Often it is advisable to cluster the network so that the nodes within a cluster are geographically near each other, requiring very little communication power of the transceivers; and a cluster head or leader of a cluster is chosen based on some criterion (for example, the smallest average distance from all the nodes in the cluster, maximum remaining energy, etc.). This is illustrated by the example in Figure 1.6. Communication between a node *u* in, say, cluster 1 and a node *v* in, say, cluster 2, may then be effected through the leaders of clusters 1 and 2.

In Chapter 5 of the book, we will discuss the different communication protocols used in ad hoc networks.

# 1.4.2  Location Identification

Most location estimation systems in cellular mobile and ad hoc networks utilize the fundamental method of using *trilateration* or *triangulation* of received sig-