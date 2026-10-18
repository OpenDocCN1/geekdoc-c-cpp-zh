
# Mobility Management in Cellular Networks

[28] C. Bettsletter and O. Krause, “On border effects in modelling and simulation of wireless ad hoc networks,” Proc. IEEE Intl. Conf. Mobile and Wireless Commun. Network (MWCN), Recife, 2001.

[29] C. Bettsletter, G. Resta and P. Santi, “The node distribution of the random waypoint mobility model for wireless ad hoc networks,” IEEE Trans. Mobile Computing, Vol. 2, pp. 257-269, 2003.

[30] D. Blough, G. Resta and P. Santi, “A statistical analysis of the long-run node spatial distribution in mobile ad hoc networks,” Wireless networks, Vol. 10, pp. 543-554, 2004.

[31] P. Santi and D. Blough, “The critical transmitting range for connectivity in sparse wireless ad hoc networks,” IEEE Trans. Mobile Computing, Vol. 2, pp. 25-39, 2003.

[32] F. Bai, N. Sadagopan and A. Helmy, “Important: A framework to systematically analyze the impact of mobility on performance of routing protocols for ad hoc networks,” Proc. IEEE Infocom, San Francisco, pp. 825-835, 2003.

[33] X. Hong, M. Gerla, G. Pei and C. Chiang, “A group mobility model for ad hoc wireless networks,” Proc. ACM MSWiM, Seattle, pp. 53-60, 1999.

[34] K. Wang and B. Li, “Group mobility and pattern prediction in wireless ad hoc networks,” Proc. IEEE Intl. Conf. Commun., New York, pp. 1017-1021, 2002.

[35] Y. B. Lin, “Determining the user locations for personal communications services networks,” IEEE Trans. Veh. Technol., vol. 43, pp. 466-473, Aug. 1994.

[PAGE 97]

# Chapter 3

# Bandwidth Management in Cellular Networks

| Section | Title | Page |
|---|---|---:|
| 3.1 | Introduction | 78 |
| 3.1.1 | Channel Assignment Problem and Variants | 78 |
| 3.1.2 | Mathematical Formulation of CAP | 81 |
| 3.1.3 | CAP and Generalized Graph Coloring | 83 |
| 3.2 | Benchmark Instances | 84 |
| 3.3 | Lower Bounds on Bandwidth | 89 |
| 3.3.1 | Lower Bounds on Bandwidth for Homogeneous Demand | 91 |
| 3.3.2 | Lower Bounds on Bandwidth for Non-Homogeneous Demand | 101 |
| 3.4 | Genetic Algorithm for Channel Assignment | 108 |
| 3.4.1 | Problem Formulation | 109 |
| 3.4.2 | *Algorithm GA* | 111 |
| 3.4.3 | GA on Special Cases of CAP | 116 |
| 3.4.3.1 | Scheme 1: $s_1=s_2$ | 116 |
| 3.4.3.2 | Scheme 2: For i) $s_2 < s_1 \leq 2s_2$ and ii) $s_1 \geq 2s_2$ | 119 |
| 3.4.3.3 | Scheme 3: For $s_1 \geq s_2$ | 125 |
| 3.4.4 | Overall Bandwidth Requirement | 131 |
| 3.5 | Coalesced CAP | 133 |

[PAGE 98]

+   3.5.1 Construction of Coalesced CAP ..... 133
+   3.5.2 Technique for Solving Original CAP from Coalesced CAP .. 137
+   3.6 Fast Near-Optimal Channel Assignment ..... 147
+   3.6.1 Assignment Algorithm ..... 147
+   3.6.2 Convergence Behavior of Algorithm ..... 159
+   3.6.3 Worst-Case Time Complexity of Assignment Algorithm .... 161
+   3.6.4 Worst-Case Deviation of Bandwidth from Optimality ..... 162
+   3.7 Conclusion ..... 164
+   3.8 Exercises ..... 167
+   Bibliography ..... 169

Mobile computing, particularly over cellular networks, has emerged as an important topic of research because of the need for computing capabilities even when people are on the move. Over the past decade, the number of such cellular network dependent mobile users has increased almost exponentially. However, the available bandwidth for providing services to those users is very limited. Such a limited availability of the radio spectrum, signal distortion, and the interference caused by the environment and other mobile users impose inherent limitations on the capacity of wireless networks. Therefore, developing methods to utilize the scarce radio spectrum efficiently is more critical than ever.

For cellular networks, the available radio spectrum is divided into a number of non-overlapping frequency bands. We assume that the frequency bands are of equal length and numbered 0, 1, 2, ... from the lower end. Each such frequency band is called a channel. The highest numbered channel required in an assignment problem is known as the required bandwidth or span of the assignment. When a mobile cellular network is designed, each cell of the network is assigned a set of channels to provide services to the individual calls. The same frequency channel may be assigned to different cells (reused) if they are at a sufficient distance without causing any interference. However, the assignment of channels to nearby cells should satisfy certain constraints to avoid channel interference. Interference is a function primarily of transmitter power, receiver sensitivity, antenna gains, and channel loss. Channel loss is a function of distance, frequency, and weather, and is quantified by the minimum acceptable signal-to-noise ratio (SNR). Assuming that most of these factors are already determined or beyond the ability to influence, the interference can be defined directly as a function of frequency and distance. Based on that, three types of interference are generally considered: 1) co-channel constraint, due to which the same channel cannot be assigned to certain pairs of cells simultaneously, 2) adjacent channel constraint, for which adjacent channels cannot be assigned to certain pairs of cells simultaneously, and 3) co-site constraint, which implies that any pair of channels assigned to the same cell must be separated by a certain number of channels [20].

The channel assignment problem (CAP) deals with assigning frequency channels to cells to satisfy the frequency separation constraints with a view to avoiding channel interference and using as little bandwidth as possible. This variant of the channel assignment problem is known as the minimum span channel assignment problem.

For another variant of the CAP, consider the channel assignment when the bandwidth B of the system is given, which may even be smaller than the required lower bound on bandwidth for the given problem. Depending on B, it may or may not be possible to satisfy all the channel demands of each cell unless B is sufficiently large.

Thus, a solution to this variant of CAP may cause blocked calls. However, the objective is to minimize call blocking. This class of assignment problem is known as the *fixed bandwidth* channel assignment problem.

There is, however, another class of problem of real-life importance known as the *perturbation-minimizing* frequency assignment problem (PMFAP) [17]. Assume that an assignment has been obtained for a given network to satisfy the required channel demands. After some time, demands of some of the cells may be changed due to either 1) newly generated calls or 2) a handoff situation or 3) completion of some ongoing calls. The objective of this variant of CAP is to accommodate these small changes in demands; but while doing so, the number of changes in the existing assignment should be minimized while meeting the desired QoS. This variant is useful for addressing the short-term demand fluctuations that often arise in real-life scenarios.

Channel assignment schemes can be classified into several categories. In the fixed (or static) channel assignment problem (FCA), the number of calls to each cell is known a priori and a number of nominal channels is permanently allocated to each cell for its exclusive use. In the simple uniform FCA, the same number of nominal channels is allocated to each cell. Since the traffic in cellular systems is mostly nonuniform, uniform allocation may result in poor channel utilization [34]. To achieve better channel utilization, the number of channels allocated to each cell should depend on the expected traffic load of the cell. This technique is called non-uniform channel allocation [35, 36]. Simple FCA schemes are not adaptive to temporal and spatial fluctuations of user demands and to overcome this drawback, dynamic channel assignment (DCA) schemes have been developed [37]. In DCA, all channels are available to every cell and channels are assigned to newly generated calls as and when required, provided they satisfy the interference constraints. Though DCA schemes provide flexibility and traffic adaptability at the cost of higher complexity,
