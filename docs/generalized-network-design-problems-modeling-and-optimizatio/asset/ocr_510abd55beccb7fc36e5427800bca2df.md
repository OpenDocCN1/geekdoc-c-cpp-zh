# 7.4 Computational results

Hu et al. [82] have tested their VNS variants for solving the GMEBCNP on two types of instances, namely, Euclidean TSPlib instances with geographical center clustering according to [43] and random instances introduced by Ghosh [49], originally in the case of the GMSTP. For more information on these instances, we refer to Section 2.6 or [82].

The experiments were performed on a Pentium 4, 2.6 GHz PC with 1 GB RAM and, in order to compute the average values and standard deviations, Hu et al. performed 30 independent runs for each instance and algorithm variant.

After analyzing the computational results presented in Tables 7.1 and 7.2, we observe that, in the case of TSPlib instances, from among the tested VNS variants SAVNS performs best, whereas for the random instances, the results are ambiguous. For the group Euclidean and non-Euclidean instances SAVNS performs best and in the case of random Euclidean the VNS2 variant performs best.

# 7.5 Notes

The generalized minimum edge-biconnected network problem (GMEBCNP) is an extension of the edge-biconnectivity augmentation problem and consists of finding the minimum cost subgraph containing exactly one node from each cluster and connecting in an edge-biconnected way. The GMEBCNP was introduced by Huygens [84] and arises in the design of backbones in large communication networks.

Within this chapter, we have presented an integer programming model of the problem and an improved Variable Neighborhood Search (VNS) approach, in which several variants were proposed.

The material presented in this chapter is based on the results published by Hu et al. [82].