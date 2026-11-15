
![](img/6b9226526d7260024653712412f81bfd_8_0.png)

Fig. 3. Algorithms performance versus the number of requests.

important role in the performance improvement, as the slope of arrows keeps close to 1.

Thus, based on the aforementioned analysis the answer on how to prioritize expanding of the caching memory first or the link capacity can be categorized into the following three cases: (1) for the Optimal and GSAC algorithms, both bandwidth and memory expanding lead to better cache-hit ratios. However, raising the link capacity can bring more energy gains, especially when the memory space exceeds 0.5 GB on (P1) or 0.75 GB on (P2); (2) if the Coordinated Caching or Random Caching is utilized then the best network strategy is to prioritize towards bandwidth increase instead of caching to increase energy reduction benefits.

## 6.4. Impact of the network topology

The influence of different network topologies is investigated in Table 4, in which the confidence interval of each simulation scenario is also illustrated. In addition to the normal tree-like network used in the previous simulations which is marked as original, we also employ a strict-tree structure, in which only one path exists between any two nodes on the network, and a full mesh topology that provides the maximum diversity in terms of routes between nodes in the network. It is expected that as the degree of a node in the network increases, both the energy gain and cache-hit ratio of the evaluated algorithms can be further improved since providing more direct connections is equivalent to expanding the available link bandwidth, especially for (P2). It is also clearly illustrated that in the case of a full mesh network topology, even the use of Random Caching can be considered as a suitable method for energy-saving purposes. Observe however that the performance gap between Random Caching and other strategies becomes smaller with the increase of connected links. Coordinated Caching is even under-performing in a fully mesh network topology. The main reason is that one advantage of Optimal, GSAC and Coordinated on saving transmission energy becomes less obvious when every two caching nodes are connected within one hop. As a result, the caching energy dominates the energy gain.

Fig. 4. The trade-off between bandwidth and caching space.

Table 4 Algorithms performance versus network topology.

| | | P1 Tree | P1 Original | P1 Full mesh | P2 Tree | P2 Original | P2 Full mesh |
|---|---|---|---|---|---|---|---|
| # Nodes | | 20 | 20 | 20 | 20 | 20 | 20 |
| # Links | | 29 | 52 | 200 | 29 | 52 | 200 |
| Energy gain | Optimal | 2.48 ±0.04 | 3.19 ±0.04 | 5.93 ±0.05 | 3.02 ±0.03 | 4.07 ±0.06 | 6.94 ±0.05 |
| | GSAC | 2.32 ±0.01 | 3.00 ±0.05 | 5.47 ±0.01 | 2.91 ±0.05 | 3.78 ±0.02 | 6.82 ±0.03 |
| | Coordinated | 2.25 ±0.04 | 2.81 ±0.06 | 3.93 ±0.05 | 2.75 ±0.05 | 3.48 ±0.04 | 4.94 ±0.05 |
| | Random | 1.20 ±0.03 | 1.41 ±0.03 | 4.67 ±0.11 | 1.23 ±0.09 | 1.88 ±0.02 | 6.67 ±0.09 |
| Cache-hit Ratio | Optimal | 0.91 ±0.01 | 1.00 ±0.00 | 1.00 ±0.00 | 0.90 ±0.03 | 0.91 ±0.01 | 1.00 ±0.00 |
| | GSAC | 0.92 ±0.01 | 0.98 ±0.01 | 1.00 ±0.00 | 0.92 ±0.02 | 0.97 ±0.01 | 1.00 ±0.00 |
| | Coordinated | 0.88 ±0.01 | 0.94 ±0.01 | 1.00 ±0.00 | 0.86 ±0.01 | 0.93 ±0.02 | 1.00 ±0.00 |
| | Random | 0.55 ±0.03 | 0.68 ±0.04 | 1.00 ±0.00 | 0.59 ±0.03 | 0.71 ±0.01 | 1.00 ±0.00 |

## 6.5. Impact of the prediction accuracy (\(\rho_{ls}\))

In the previous evaluation, we test the performance of different schemes under the salient assumption of an ideal condition that all users' preference is exactly predicted, i.e. \(\rho_{ls} = 1\). Hereafter, we relax this assumption and perform a wide set of experiments to understand the impact of prediction accuracy by varying it from 100% down to, effectively, 0%. As shown in Figs. 5(a) and 5(c), regarding the Optimal, GSAC, and Coordinated Caching, there is a steep drop on the energy gain from 100% to 80% then, the value decline steadily. By the same token, the performance gap among the Optimal, GSAC, Coordinated, and Random Caching becomes very small when prediction accuracy significantly deteriorates. It is worth noting that for (P1), when the predicted accuracy is less than 30% (For (P2), the threshold is 20%), the energy gain is less than 1. In other words, the proactive caching method cannot save energy but consume more than No-caching, if the user preference prediction is inaccurate, since we pay extra energy for caching contents. This result means that attention should be placed on managing effectively user content prediction in order to fully capitalize on gains stemming from network and storage dimensioning. In Figs. 5(b) and 5(d), the cache-hit ratio reduces as the accuracy is declining. An interesting observation is that even when the prediction accuracy reduces to 0% (for example in the case of very new popular content), the cache-hit ratio is still above 0. The main reason is that inaccurate predicted requests can be redirected to other nodes where the required content is cached, and it is still counted for the cache-hit ratio calculation.

![](img/6b9226526d7260024653712412f81bfd_10_0.png)

## 7. Conclusions

To meet the significant growth of popular on-demand content whilst empowering a network energy saving operation, we jointly consider the problem of anchoring popular content at network nodes with caching capabilities and deciding delivery routing paths. The proposed integer linear programming model amalgamates energy consumption, the constraints of caching memory, link bandwidth, multipath routing, and different delivery modes, i.e. multicast and unicast. In addition, a greedy simulated annealing caching algorithm is presented and the effectiveness of the proposed scheme is evaluated by a wide set of numerical investigations. For instance, we test the performance of evaluated algorithms under different network resources, topologies, mobility patterns, user preferences, and cache sizes. The results suggest that the proposed algorithms have the potential to reduce the energy consumption to up to 75% compared with other caching schemes. Furthermore, expanding link bandwidth, enriching path diversity, and increasing the preference prediction accuracy can have beneficial effects on energy saving. Furthering this work, we plan to consider ML/AI-driven algorithms amalgamated with the proposed framework to augment the model with deep learning capabilities so that the optimal allocation patterns can be learnt autonomously. In that case a number of open ended questions arises such as the resource usage history to be used in machine-learning-based decision making actions has to be made some appropriate algorithms should also be taking into account to provide theoretical performance guarantees. Those aspects open up new research avenues that may expand our contributions in future work.

## CRediT authorship contribution statement

Yantong Wang: Conceptualization, Methodology, Software, Investigation, Data curation, Writing – original draft. Vasilis Friderikos: Validation, Writing – review & editing, Supervision.

## Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

## Data availability

Data will be made available on request.

## References

- [1] P. Cornwall, J. Johnston, S. Carson, Ericsson Mobility Report, White Paper, Ericsson, 2021. (Online): https://www.ericsson.com/4ad256/assets/local/mobility-report/documents/2021/ericsson-mobility-report.pdf
- [2] G. Xylomenos, C. Ververidis, V.A. Siris, N. Fotiou, C. Tsilopoulos, V. Vasilakos, K.V. Katsaros, G.C. Polyzos, A survey of information-centric networking research, IEEE Commun. Surv. Tutor. 16 (2) (2014) 1024–1049.
- [3] Y. Wang, V. Friderikos, A survey of deep learning for data caching in edge computing and information, Vol. 7, Multidisciplinary Digital Publishing Institute, 2020, p. 43.
- [4] C. Fang, H. Yao, Z. Wang, W. Wu, X. Jin, F.R. Yu, A survey of mobile information-centric networking: Research issues and challenges, IEEE Commun. Surv. Tutorials 18 (2016) 2337–2362.
- [5] S. Buzzi, I. Chih-Lin, T.E. Klein, H.V. Poor, C. Yang, A. Zappone, A survey of energy-efficient techniques for 5G networks and challenges ahead, IEEE J. Sel. Areas Commun. 34 (4) (2016) 697–709.
- [6] Area 5.1: Knowledge sharing and dissemination, beyond 5G network with the advent of 6G: Architecture and emerging technologies, IEEE Access 9 (2020) 67512–67547.
- [7] M. Matalo, K. Leppänen, F. Clazzer, A. Munari, Key Drivers and Research Challenges for 5G Ubiquitous Wireless Intelligence, White Paper, 5G PPP, 5G Infrastructure Public Private Partnership, 2019. (Online): http://5g-ppp.eu/wp-content/uploads/2014/02/5G-PPP-White-Paper-on-AI.pdf
- [8] N. Choi, K. Guan, D.C. Kilper, G. Atkinson, In-network caching effect on optimal energy consumption in content-centric networking, in: Proc. of IEEE International Conference on Communications (ICC), Ottawa, ON, Canada, IEEE, 2012, pp. 2689–2694.
- [9] J. Llorca, A.M. Tulino, K. Guan, J. Esteban, M. Varvello, N. Choi, D.C. Kilper, Dynamic in-network caching for energy efficient content delivery, in: Proc. of IEEE International Conference on Computer Communications (INFOCOM), Turin, Italy, 2013, pp. 245–249.
- [10] C. Fang, F.R. Yu, T. Huang, J. Liu, Y. Liu, An energy-efficient distributed in-network caching scheme for green content-centric networks, Comput. Netw. 78 (2015) 119–134.
- [11] E. Yaacoub, M. Alouini, Key6G: energy-delay aware cache management using quantized Huffman, J. Netw. Syst. Manage. (2018) 1–21.
- [12] J. Li, B. Liu, H. Wu, Energy-efficient in-network caching for content-centric networking, IEEE Commun. Lett. 17 (1) (2013) 797–800.
- [13] D. Liu, B. Chen, C. Yang, T. Abdelzaher, Caching at the edge: A survey of architecture, challenges, and future directions, IEEE Commun. Mag. 54 (9) (2016) 22–28.
- [14] Y. Xu, Y. Li, Z. Wang, T. Liu, G. Zhang, S. Ci, Coordinated caching model for minimizing energy consumption in radio access network, in: Proc. of IEEE International Conference on Communications (ICC), Sydney, Australia, IEEE, 2014, pp. 2406–2411.
- [15] J. Xu, K. Ota, M. Dong, Energy efficient hybrid edge caching scheme for tactile internet in 5G, IEEE Trans. Green Commun. Netw. 3 (2) (2019) 483–493.
