
## Bandwidth Management in Cellular Networks

- [34] I. Katzela and M. Naghshineh, "Channel assignment schemes for cellular mobile telecommunication systems: a comprehensive survey," _IEEE Personal Commun._, vol. 3, pp. 10–31, 1996.
- [35] M. Zhang and T.-S. Yum, "The non-uniform compact pattern allocation algorithm for cellular mobile systems," _IEEE Trans. Vehicular Technology_, vol. 40, no. 2, pp. 387–391, 1991.
- [36] S.-H. Oh and D.-W. Tcha, "Prioritized channel assignment in cellular radio networks," _IEEE Trans. Commun._, vol. 40, pp. 1259–1269, 1992.
- [37] P. Venkata Krishna and N. Ch. S. N. Iyengar, "Optimal channel allocation algorithm with efficient channel reservation in cellular networks," _Int. J. Communication Networks and Distributed Systems_, vol. 1, no. 1, pp. 33–51, 2008.
- [38] G. Vidyarthi, A. Ngom, and I. Stojmenovic, "A hybrid channel assignment approach using an efficient evolutionary strategy in wireless mobile networks," _IEEE Trans. Vehicular Technology_, vol. 54, no. 5, pp. 1887–1895, 2005.
- [39] G. Kendall and M. Mohamad, "Channel assignment optimization using a hyper-heuristic," _Proc. of IEEE Conference on Cybernetics and Intelligent Systems_, Singapore, December 2004.
- [40] A. Boukerche, K. E. Khatib, and T. Huang, "A performance evaluation of distributed dynamic channel allocation protocols for mobile networks," _Wireless Commun. and Mobile Computing_, vol. 7, no. 1, pp. 69–80, 2007.
- [41] M. R. Garey and D. S. Johnson, "The complexity of near-optimal graph coloring," _Journal of the ACM_, vol. 23, pp. 43–49, 1976.
- [42] A. Gamst, "Some lower bounds for a class of frequency assignment problems," _IEEE Trans. Vehicular Technology_, vol. 35, no. 1, pp. 8–14, 1986.
- [43] A. Gamst and W. Rave, "On frequency assignment in mobile automatic telephone systems," _Proceedings of IEEE GLOBECOM_, 1982.
- [44] S. C. Ghosh, B. P. Sinha, and N. Das, "More on lower bounds for channel assignment problem," _Proceedings of 6th International Conference on High Performance Computing in Asia-Pacific Region_, Bangalore, India, vol. II, pp. 522–527, December 2002.
- [45] D. H. Smith, S. Hurley, and S. M. Allen, "A new lower bound for the channel assignment problem," _IEEE Trans. Vehicular Technology_, vol. 49, no. 4, pp. 1265–1272, 2000.
- [46] R. Montemanni, D. Smith, and S. Allen, "Lower bounds for fixed-spectrum frequency assignment," _Annals of Operations Research_, vol. 107, no. 1, pp. 237–250, 2001.
- [47] D. E. Goldberg, _Genetic Algorithms in Search, Optimization, and Machine Learning_, Addison-Wesley, 1989.
- [48] C. A. Murthy and N. Chowdhury, "In search of optimal clusters using genetic algorithms," _Pattern Recognition Letters_, vol. 17, pp. 825–832, 1996.
- [49] D. Bhandari, C. A. Murthy, and S. K. Pal, "Genetic algorithm with elitist model and its convergence," _Int. J. Pattern Recognition and Artificial Intelligence_, vol. 10, pp. 731–747, 1996.
- [50] G. K. Audhya, K. Sinha, K. Mandal, R. Dattagupta, S. C. Ghosh, and B. P. Sinha, "A new approach to fast near-optimal channel assignment in cellular mobile networks," _IEEE Trans. Mobile Computing_, vol. 12, no. 9, pp. 1814–1827, September 2013.
- [51] S. C. Ghosh, B. P. Sinha, and N. Das, "Coalesced CAP: An improved technique for frequency assignment in cellular networks," _IEEE Trans. Vehicular Technology_, vol. 55, no. 2, pp. 640–653, March 2006.
- [52] G. K. Audhya, K. Sinha, S. C. Ghosh, and B. P. Sinha, "A survey on the channel assignment problem in wireless networks," _Wireless Communications and Mobile Computing_, vol. 11, issue 5, pp. 583–609, May 2011.

## Chapter 4: Localization of Nodes in Mobile Networks

| Section | Page |
| --- | --- |
| 4.1 System Model | 178 |
| 4.2 Preliminaries | 179 |
| 4.3 Estimation of Location Error | 183 |
| 4.3.1 Error due to Ambiguity in Node Coordinates | 183 |
| 4.3.2 Contribution by Range Estimation Error | 187 |
| 4.3.3 Combined Error Estimation | 189 |
| 4.4 Beacon Node Selection Algorithm | 192 |
| 4.5 Location Region Identification | 194 |
| 4.5.1 Preliminaries | 195 |
| 4.5.2 Region Estimation Algorithm | 204 |
| 4.5.3 Complexity Analysis | 206 |
| 4.5.4 Simulation Results | 206 |
| 4.6 Exercises | 213 |
| Bibliography | 214 |

In this chapter, we discuss location identification algorithms for computing the location of a node in an ad hoc network. We start with a small percentage of nodes known as reference nodes which are assumed to know their locations with high precision, either through GPS or some other means. Starting from these reference nodes, locations of other nodes are successively computed. A beacon node is a reference node or a node whose location has been computed with the help of location information of its neighbors. We assume errors exist in the advertised locations of all beacon nodes, including the reference nodes. ±ε denotes the maximum possible error in the advertised coordinates of a beacon node along either axis of a two-dimensional coordinate system. ±δ is the maximum possible error along either axis in a measured range between a node and a beacon. We first present an intelligent beacon selection algorithm proposed by [11] such that the error in the computed location of a node is within a bound of ±[3ε(1 + √2) + 2δ] to ±(3ε + 2δ) along one axis and within ±[2δ(1 + √2) + 3ε] to ±(3ε + 2δ) along its orthogonal axis. Authors in [11] also derived a general expression for computing the bounds on an error that can be introduced in the computed location of a node and the conditions that must be met in selecting the beacon nodes to keep the error in the computed location of a node within these bounds.

An ad hoc network is modeled as a graph \( G = (V, E) \) consisting of \( n \) nodes. \( V \) is the set of all nodes, \( |V| = n \) and \( E \) is the set of edges in the graph \( G \). The nodes may be stationary or mobile. All communication links are assumed to be bi-directional. A node \( v \) is said to be a _neighbor_ of \( u \) if they are within each other's hearing zones. The neighborhood \( N(i) \) of a node \( i \) consists of all nodes that are within its transmission range. A small percentage of the nodes are assumed to know their individual locations with high precision, either through GPS or some other means. These nodes serve as the _reference nodes_ (RNs) in the network. Initially, nodes other than the RNs do not possess any knowledge of their locations. A node is defined as a _beacon node_ if it is used in computing the unknown location of another node. A beacon node may be a reference node or a node whose location has been computed with the help of location information of its neighboring beacons.

Considering thermal noise at the receiver, NLOS errors and channel characteristics, the measured range between two nodes *u* and *v* can be expressed as,

$$r_{uv}=d_{uv}+\eta_{uv}+c\tau_{uv}$$

(4.1)

where $d_{uv}$ represents the unknown Euclidean distance between $u$ and $v$. $\eta_{uv}$ completely models the combined additive effects of thermal receiver noise, signal bandwidth and signal-to-noise ratio. $\eta_{uv}$ has been shown to be a zero-mean normal random variable and hence can be measured or pre-computed [1]. $\eta_{uv}$ is assumed to be always additive. $c\tau_{uv}$ represents the NLOS distance error and is the dominant error contributor [2], $c$ being the speed of light in air.

It will be assumed that besides the ranges measured for location computation, the advertised locations of the reference nodes (and beacon nodes in general) are erroneous within certain known bounds. The advertised coordinates of a reference node may have ±ε error along both x-axis and y-axis. The error in a measured range can be erroneous by ±δ along both axes.

### 4.2 Preliminaries

The above model assumes that errors may be present in the advertised coordinates of a beacon node (including reference nodes) and in a measured range between two nodes. We note that a number of existing location sensing technologies mention the accuracy of their location determination processes. This value can be used as the ε error in the advertised coordinates of the reference nodes. For example,
