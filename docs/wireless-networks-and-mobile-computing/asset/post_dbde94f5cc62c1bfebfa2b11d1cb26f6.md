
vided by this approach can be utilized for accommodating small changes in demands dynamically is a topic for further study.

We also described a polynomial time algorithm for near-optimal channel assignment in hexagonal cellular networks with non-homogeneous demands in a two-band buffering system. The CAP for non-homogeneous demands is divided into a number of smaller subproblems, each of which has a homogeneous demand from a subset of the nodes of the original network. A simple assignment scheme gives priority assignment to the higher demand nodes to solve each subproblem. We illustrated this algorithm with the help of the Philadelphia benchmark Problem 6, which is regarded as the most difficult one in the literature. This algorithm yields an assignment which never takes more than 6% of the optimal bandwidth and requires very little execution time (less than 5 milliseconds on a HPxw8400 workstation) for most difficult benchmark problems. Thus, this algorithm is suitable for real-life situations where fast channel assignment is demanded, although a marginal deviation (say, about 6%) from the optimal bandwidth may be tolerated.

## 3.8 Exercises

- 1. Describe the mathematical model of the channel assignment problem in a cellular mobile network.
- 2. Represent the channel assignment problem in a cellular mobile network in terms of the classical vertex coloring problem.
- 3. Derive a lower bound on the bandwidth requirement for assigning channels in a cellular mobile network with a single demand on each of the constituent nodes of the network.

- 4. Derive a lower bound on the bandwidth requirement of a given seven-node hexagonal subgraph (which consists of one central node surrounded by six peripheral nodes at six corners of a hexagon) of a cellular network having non-homogeneous demands from different nodes.

- 5. Describe the frequency exhaustive strategy and the requirement exhaustive strategy for solving the CAP.

- 6. Describe a method by which the CAP with non-homogeneous demand can be partitioned into a sequence of smaller subproblems where each subproblem has a homogeneous demand from a subset of nodes of the network.

- 7. Suppose Algorithm A can solve the CAP with the homogeneous demand of a single channel. Describe an algorithm to solve the CAP with non-homogeneous demands by using Algorithm A.

- 8. Describe a polynomial time algorithm that would solve the channel assignment problem in a cellular mobile network with a β- approximation bandwidth, i.e., the bandwidth required by the assignment algorithm would be within β times the optimal bandwidth for the problem.

- 9. Devise a polynomial time approximation algorithm for assigning channels to meet the non-homogeneous demands of the nodes in a network that will be more efficient than those proposed in this chapter. The worst case execution time of your proposed algorithm for all the benchmark problems needs to be less than that determined by the existing algorithms and the approximation factor by which the required worst case bandwidth will be more than the optimal bandwidth needs to be less than 5/3.

# Bibliography

- [1] A. Sen, T. Roxborough, B. P. Sinha, “On an optimal algorithm for channel assignment in cellular network,” *Proc. of IEEE International Conf. Communications*, Vancouver, Canada, pp. 1147–1151, June 1999.
- [2] A. Sen, T. Roxborough and S. Medidi, “Upper and lower bounds of a class of channel assignment problems in cellular networks,” *Proc. of IEEE INFOCOM ’98*, April 1998.
- [3] W. K. Hale, “Frequency assignment: theory and application,” *Proc. IEEE*, Vol. 68, pp. 1497–1514, 1980.
- [4] M. Duque-Anton, D. Kunz and B. Ruber, “Channel assignment for cellular radio using simulated annealing,” *IEEE Trans. Vehicular Technology*, Vol. 42, No. 1, pp. 14–21, Feb. 1993.
- [5] R. Mathar and J. Mattfeldt, “Channel assignment in cellular radio networks,” *IEEE Trans. Vehicular Technology*, Vol. 42, No. 4, pp. 647–656, Nov. 1993.
- [6] D. Kunz, “Channel assignment for cellular radio using neural networks,” *IEEE Trans. Vehicular Technology*, Vol. 40, No. 1, pp. 188–193, Feb. 1991.
- [7] D. Tcha, Y. Chung and T. Choi, “A new lower bound for the frequency assignment problem,” *IEEE/ACM Trans. Networking*, Vol. 5, No. 1, Feb. 1997.
- [8] K. N. Sivarajan, R. J. McEliece and J. W. Ketchum, “Channel assignment in cellular radio,” *Proc. of 39th IEEE Vehicular Technology Conf.*, pp. 846–850, May 1989.

- [9] W. Wang and C. K. Rushforth, “An adaptive local-search algorithm for the channel assignment problem,” *IEEE Trans. Vehicular Technology*, Vol. 45, No. 3, pp. 459–466, Aug. 1996.

- [10] S. Khanna and K. Kumaran, “On wireless spectrum estimation and generalized graph coloring,” *Proc. of IEEE INFOCOM*, April 1998.

- [11] R. A. Leese, “A unified approach to the assignment of radio channels on a rectangular hexagonal grid,” *IEEE Trans. Vehicular Technology*, Vol. 46, No. 4, pp. 968–980, Nov. 1997.

- [12] L. Narayanan and S. Shende, “Static frequency assignment in cellular networks,” *Proc. of 4th International Colloquium on Structural Information and Communication Complexity*, 1997.

- [13] A. Sen, T. Roxborough and S. Medidi, “Upper and lower bounds of a class of channel assignment problems in cellular networks,” *Proc. of IEEE INFOCOM*, April 1998.

- [14] S. Kim and S. Kim, “A two-phase algorithm for frequency assignment in cellular mobile systems,” *IEEE Trans. Vehicular Technology*, Vol. 43, No. 3, pp. 542–548, Aug. 1994.

- [15] D. Beckmann and U. Killat, “A new strategy for the application of genetic algorithms to the channel assignment problem,” *IEEE Trans. Vehicular Technology*, Vol. 48, No. 4, pp. 1261–1269, July 1999.

- [16] C. Y. Ngo and V. O. K. Li, “Fixed channel assignment in cellular radio networks using a modified genetic algorithm,” *IEEE Trans. Vehicular Technology*, Vol. 47, No. 1, pp. 163–172, Feb. 1998.

# Bandwidth Management in Cellular Networks

- [17] D.-W. Tcha, J.-H. Kwon, T.-J. Choi, and S.-H. Oh, “Perturbation-minimizing frequency assignment in a changing TDMA/FDMA cellular environment,” _IEEE Trans. Vehicular Technology_. Vol. 49, No. 2, pp. 390–396, March 2000.
- [18] W. K. Lio and G. G. Coghill, “Channel assignment through evolutionary optimization,” _IEEE Trans. Vehicular Technology_, Vol. 45, No. 1, pp. 91–96, Feb. 1996.
- [19] J. S. Kim, S. H. Park, P. W. Dowd, and N. M. Nasrabadi, “Cellular radio channel assignment using a modified Hopfield network,” _IEEE Trans. Vehicular Technology_. Vol. 46, pp. 957–967, Nov. 1997.
- [20] C. W. Sung, and W. S. Wong, “Sequential packing algorithm for channel assignment under co-channel and adjacent-channel interference constraint,” _IEEE Trans. Vehicular Technology_. Vol. 46, pp. 676–686, Aug. 1997.
- [21] J. S. Kim, S. H. Park, P. W. Dowd, and N. M. Nasrabadi, “Channel assignment in cellular radio using genetic algorithm,” _Wireless Personal Commun._, Vol. 3, No. 3, pp. 273–286, Aug. 1996.
- [22] T.-M. Ko, “A frequency selective insertion strategy for fixed channel assignment,” _in Proc. of 5th IEEE Int. Symp., Personal, Indoor and Mobile Radio Commun._, pp. 311–314, Sept. 1994.
- [23] N. Funabiki and Y. Takefuji, “A neural network parallel algorithm for channel assignment in cellular radio network,” _IEEE Trans. Vehicular Technology_. Vol. 41, pp. 430–437, Nov. 1992.
- [24] R. Battiti, A. Bertossi, and D. Cavallaro, “A randomized saturation degree heuristic for channel assignment in cellular radio networks,” _IEEE Trans. Vehicular Technology_, Vol. 50, No. 2, pp. 364–374, Mar. 2001.

Wireless Networks and Mobile Computing

- [25] K. Smith and M. Palaniswami, “Static and dynamic channel assignment using neural network,” _IEEE J. Select. Areas Commun._, Vol. 15, pp. 238–249, Feb. 1997.

- [26] G. Chakraborty, “An efficient heuristic algorithm for channel assignment problem in cellular radio networks,” _IEEE Trans. Vehicular Technology_, Vol. 50, No. 6, pp. 1528–1539, Nov. 2001.

- [27] http://www.specbench.org/osg/cpu95/results/cint95(cfp95).html

- [28] S. C. Ghosh, B. P. Sinha and N. Das, “A new approach to efficient channel assignment for hexagonal cellular networks,” _Int. J. Foundations Computer Sci._, Vol. 14, No. 3, pp. 439–463, June 2003.

- [29] S. C. Ghosh, B. P. Sinha and N. Das, “Channel assignment using genetic algorithm based on geometric symmetry,” _IEEE Trans. Vehicular Technology_, Vol. 52, No. 4, pp. 860–875, July 2003.

- [30] A. Gamst, “A new lower bound for the channel assignment problem,” _IEEE Trans. Vehicular Technology_, Vol. 49, No. 4, pp. 1265–1272, July. 2000.

- [31] R. Montemanni, J. N. J. Moon, and D. H. Smith, “An improved tabu search algorithm for the fixed-spectrum frequency assignment problem,” _IEEE Trans. Vehicular Technology_, Vol. 52, No. 3, pp. 891–901, May 2003.

- [32] D. Kunz, “Channel assignment for cellular radio using neural networks,” _IEEE Trans. Vehicular Technology_, Vol. 40, No. 1, pp. 188–193, Feb. 1991.

- [33] W. Wang and C. K. Rushforth, “Local search for channel assignment in cellular mobile networks,” in _DIMACS Series in Discrete Mathematics and Theoretical Computer Science_, Vol. 35, pp. 689–709, 1997.
