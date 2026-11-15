# Fig. 4. The trade-off between bandwidth and caching space.

# Table 4 Algorithms performance versus network topology.

| Topology | | P1 | | | P2 | | |
|---|---|---|---|---|---|---|---|
| | | Tree | Original | Full mesh | Tree | Original | Full mesh |
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

Coordinated, and Random Caching becomes very small when prediction accuracy significantly deteriorates. It is worth noting that for (P1), when the predicted accuracy is less than 30% (For (P2), the threshold is 20%), the energy gain is less than 1. In other words, the proactive caching method cannot save energy but consume more than No-caching, if the user preference prediction is inaccurate, since we

pay extra energy for caching contents. This result means that attention should be placed on managing effectively user content prediction in order to fully capitalize on gains stemming from network and storage dimensioning. In Figs. 5-(b) and 5-(d), the cache-hit ratio reduces as the accuracy is declining. An interesting observation is that even when the prediction accuracy reduces to 0% (for example in the case of very new