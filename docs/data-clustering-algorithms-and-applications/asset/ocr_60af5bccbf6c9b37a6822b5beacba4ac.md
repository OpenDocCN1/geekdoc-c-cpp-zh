# Cluster Ensembles: Theory and Applications

consensus $\tilde{\lambda}$, by

```
$$\Phi(\Lambda, \tilde{\lambda}) = \frac{1}{r} \sum_{q=1}^r \ell(\lambda^{(q)}, \tilde{\lambda}) \quad (22.2)$
```

This serves as the objective function in cluster ensemble formulations, where the goal is to find the combined clustering $\tilde{\lambda}$ with $\hat{k}$ clusters such that $\Phi(\Lambda, \tilde{\lambda})$ is maximized. It turns out that this objective is intractable, so heuristic approaches have resorted to.

# 22.3 Measuring Similarity Between Clustering Solutions

Since no ground truth is available for clustering problems, cluster ensemble algorithms aim to maximize similarity between the consensus clustering and each of the base clustering solutions. Two of the most desirable properties of such similarity measures are

+   • The index should be normalized for easy interpretation and comparison across solutions with varying numbers of clusters.

+   • The expected value of the index between independent clusterings should be constant (preferably zero indicating no similarity). The utility of such a property will be clarified later in this section.

Below, we present different indices and show how these are modified to achieve zero expected value of the same. The general rule for any "adjustment for chance" is as follows:

```
$adjusted\ index = \frac{index - Expected-index}{Max - Expected-index} \quad (22.3)$
```

where Expected-index is calculated using a permutation model [40]. In such a model, cluster labels are assumed to be generated randomly to the constraints of a fixed number of clusters and a fixed number of points in cluster. Max-index is the maximum value the index can take.

Now us discuss two key approaches for measuring the similarity of two clustering solutions [50]. The first is based on counting the number of pairs in agreement or disagreement in two clustering solutions. The second approach uses information from theory.

**1. Pair-Counting Base Measures:** These of type are based on counting the number of pairs on which two candidate solutions agree or disagree. More formally, suppose we have two clusterings $\lambda^{(a)} = \{C_h^{(a)}\}_{h=1,2,...,k^{(a)}}$ and $\lambda^{(b)} = \{C_l^{(b)}\}_{l=2,..,k^{(b)}}$. Let $n_h^{(a)}$ be the number of objects in cluster $C_h^{(a)}$ and $n_l^{(b)}$ be the number of objects in cluster $C_l^{(b)}$. Table 22.1 is a contingency table that shows the overlap between different clusters of these clusterings, $n_{hl} = |C_h^{(a)} \cap C_l^{(b)}|$. The most well-known index of this is the Rand Index (RI), which is a normalized measure of number of agreements between two candidate solutions and is

```
$$\phi^{(RI)}(\lambda^{(a)}, \lambda^{(b)}) = \sum_{hl} \left( \frac{n_{hl}}{2} \right) \frac{1}{2}(S_a + S_b) \quad (22.4)$
```

Expected value of RI, however, is not constant. This led Hubert and Arabie [32] to propose