
During the sabbatical leave, a consultant uses a random proportional rule to decide which cluster to visit next. For a consultant $k$, currently at cluster $V_i$, the probability to choose cluster $V_j$ is given by the following formula:

$$p_{ij}^k = \frac{1/d_{ij}}{\sum_{l \in \mathcal{N}_i^k} (1/d_{il})}$$ (3.24)

where $\mathcal{N}_i^k$ is the feasible neighborhood of person $k$ when at cluster $V_i$ and $d_{il}$ is the virtual distance between clusters $V_i$ and $V_j$.

As mentioned before, the feasible neighborhood $\mathcal{N}_i^k$ contains the set of clusters in the candidate list of cluster $V_i$ that person $k$ has not yet visited. If all clusters in the candidate list have already been visited, the consultant may choose one of the clusters not in the candidate list, by using a random proportional rule similar to the one given by formula (3.24).

Use of virtual distances between clusters as a heuristic during sabbatical leave, leads to reasonably good initial strategies. In general, however, after applying the cluster optimization procedure, a global tour that is optimum with respect to the virtual distances between clusters, does not produce the optimum generalized tour. Therefore, during the solution construction phase, the algorithm does not rely on the distances between clusters, although it still uses candidate lists in order to determine the feasible neighborhood of a cluster.

In each step, a client receives a recommendation for the next cluster to be visited. This recommendation is based on the global tour advertised by the consultant. Let $V_i$ be the cluster visited by client $k$ during a construction step in the current iteration. To decide which cluster to recommend for the next step, the consultant finds the position at which the cluster $V_i$ appears in its advertised global tour and identifies the clusters preceding and succeeding $V_i$ in this tour. If neither of these clusters has already been visited by the client, the consultant randomly recommends one of them. If only one is unvisited, this one is chosen as the recommendation. Finally, if both clusters are already visited, the consultant is not able to make a recommendation for the next step.

The client does not always follow the consultant's recommendation. The rule used for choosing the next cluster $V_j$ to move to, is given by the following formula:

$$V_j = \begin{cases} V_p & \text{if } V_p \neq null \land q \le q_0 \\ \text{random}(\mathcal{N}_i^k) & \text{otherwise.} \end{cases}$$ (3.25)

where:
- $V_p$ is the cluster recommended by the consultant for the next step;
- $q$ is a random variable uniformly distributed in [0,1] and $q_0$ ($0 \le q_0 \le 1$) is a parameter;
- $\mathcal{N}_l^k$ is the feasible neighborhood of person $k$, when at cluster $V_l$;
- random is a function that randomly chooses one element from the set given as its argument.

Again, if all clusters in the candidate list have already been visited, the feasible neighborhood $\mathcal{N}_l^k$ is empty. In this case, a client that ignores the recommendation of his consultant may choose one of the clusters not in the candidate list, by using a random proportional rule similar to the one given by formula (3.24).

The personal preference of a client for a given consultant is computed as the inverse of the cost of the generalized tour that corresponds to the global tour advertised by the consultant. In conjunction with the reputation, personal preference is used by clients in order to compute the probability for choosing a given consultant $k$:

$$p_k = \frac{(\text{reputation}_k \times \text{preference}_k)^2}{\sum_{c \in \mathcal{C}} (\text{reputation}_c \times \text{preference}_c)^2} \quad (3.26)$$

where $\mathcal{C}$ is the set of all available consultants.

At each iteration, the consultant's $k$ reputation fades with a constant rate $r$:

$$\text{reputation}_k \leftarrow \text{reputation}_k(1 - r) \quad (3.27)$$

A consultant enters sabbatical mode when his reputation sinks below a minimum level. In our algorithm, this minimum reputation value is set to 1 and the duration of the sabbatical leave is set to 20 iterations. At the end of the sabbatical leave, a consultant's reputation is reset to a given value, specified by the parameter $initialReputation$.

In addition, the algorithm prevents the reputation of the best consultant from sinking below this initial value. We designate as best consultant the consultant whose strategy has led to the construction of the best-so-far solution.

Each time a client achieves a success, the reputation of his consultant is incremented. Should a client construct a best-so-far solution, the consultant's reputation receives a supplementary $bonus$. The reputation of a consultant cannot exceed the maximum value given by the parameter $maxReputation$.

## An variant of the algorithm, that uses confidence

Here, we propose a variant of our algorithm, based on the approach introduced in [87], which correlates the recommendation of a consultant with a certain level of confidence. Each arc in the global tour, advertised by a consultant, has an associated strength. Strengths are updated each time the consultant adjusts his strategy. If an arc in the newly advertised tour was also present in the old advertised tour, its strength will be incremented. Otherwise, its strength is set to 0. The strength of an arc could be interpreted as the consultant's confidence in recommending this arc to a client. A client is more likely to accept recommendations made with greater confidence.

This idea is expressed in our algorithm by allowing the value of the parameter \( q_0 \) from formula (3.25) to vary in a given range, at each construction step:

$$q_0 = \begin{cases} q_{\min} + s \cdot \frac{q_{\max}-q_{\min}}{s_{\max}} & \text{if } s < s_{\max} \\ q_{\max} & \text{otherwise} \end{cases}, \quad (3.28)$$

where \( s \) is the strength of the recommended arc and \( q_{\min} \), \( q_{\max} \) and \( s_{\max} \) are constant parameters. The use of confidence somehow compensates for the absence of a heuristic during the solution construction phase.

## Local search

The global tours built during the strategy construction and solution construction phases are improved by using a local search procedure of which a generic description is given in Algorithm 3.10.

### Algorithm 3.10 (The local search procedure).

```
procedure applyLocalSearch(H_G)
  H <- clusterOptimization(H_G)
  foreach H'_G \in tourNeighborhood(H_G) do
    if quickCheck(H'_G) then
      H' <- partialClusterOptimization(H'_G, H_G)
      if cost(H') < cost(H) then
        H_G <- H'
        H <- H'
      end if
    end if
  end foreach
end procedure
```

\( H_G \) and \( H'_G \) denote global Hamiltonian tours, that is, tours in the graph of clusters, while \( H \) and \( H' \) denote generalized Hamiltonian tours. Our algorithm can be combined with any local search procedure that conforms to the above algorithmic structure. The working of the \( clusterOptimization \) function (line 2) was explained in Section 3.2.

The \( cost \) function in line 6 computes the cost of a generalized Hamiltonian tour. The other functions referred in Algorithm 3.10 are only specified in generic form and they must be implemented by each concrete instantiation of the local search procedure.

The \( tourNeighborhood \) function (line 3) should return a set of global tours that represent the neighborhood of the global tour \( H_G \) provided as its argument. The \( quickCheck \) function (line 4) is intended to speed up the local search by quickly rejecting a candidate global tour from the partial cluster optimization, if this tour is not likely to lead to an improvement.

The partialClusterOptimization function (line 5) starts with the generalized tour obtained by traversing the nodes of H in accordance with the ordering of clusters in the global tour H'_G. Then, it reallocates some vertices in the resulting generalized tour, and tries to improve its cost. Typically, this function considers only a limited number of vertices for reallocation and it usually has a lower complexity than the clusterOptimization function.

The generalized tour constructed by the function partialClusterOptimization is accepted only if its cost is better than the cost of the current generalized tour (lines 6–9).

We provide two instantiations of the generic local search procedure shown in Algorithm 3.10: one based on a 2-opt local search and one based on a 3-opt local search. We describe here only the 2-opt based variant. Except for the fact that it considers exchanges between 3 arcs, the 3-opt based local search is very similar to the 2-opt based variant.

In the 2-opt based local search, the tourNeighborhood function returns a set of global tours obtained by replacing a pair of arcs (C_a, C_β) and (C_γ, C_δ) in the original global tour with the pair of arcs (C_a, C_γ) and (C_β, C_δ). In order to reduce the number of exchanges that must be taken into consideration, the set returned by our tourNeighborhood function includes only tours for which γ is in the candidate list of α. In other words, a pair of arcs is considered for exchange, only if the center of mass of the cluster γ is close to the center of mass of the cluster α.

The partialClusterOptimization function used in this case is similar to the RP1 procedure introduced in [43]. Let (C_a, C_β) and (C_γ, C_δ) be the two arcs from the original global tour H_G that have been replaced with (C_a, C_γ) and (C_β, C_δ) in the neighboring global tour H'_G, as shown in Figure 3.5:

The vertices in clusters C_α, C_β, C_γ and C_δ can then be reallocated, in order to minimize the cost of the generalized tour. For this purpose, we have to determine the two node pairs (a', w') and (v', z') such that:

$$
\begin{aligned}
d_{a'w'} + d_{w'w} + d_{w'h} &= \min\{d_{ia} + d_{ab} + d_{bh} \mid a \in C_\alpha, b \in C_\gamma\} \\
d_{jv'} + d_{v'z'} + d_{z'k} &= \min\{d_{ja} + d_{ab} + d_{bk} \mid a \in C_\beta, b \in C_\delta\}
\end{aligned}
\quad (3.29)
$$

This computation requires |C_α||C_γ| + |C_β||C_δ| comparisons. In order to speed up the local search, we first perform a quick rejection test. We compute the quantities from formula (3.29), only if the following inequality holds:

$$
d_{\min}(C_\rho, C_\alpha) + d_{\min}(C_\alpha, C_\gamma) + d_{\min}(C_\gamma, C_\alpha) + d_{\min}(C_\alpha, C_\beta) +
d_{\min}(C_\beta, C_\delta) + d_{\min}(C_\delta, C_\tau) < d_{iw} + d_{wv} + d_{vj} + d_{hw} + d_{wz} + d_{zk} \quad (3.30)
$$

where d_{min}(C_α, C_β) is the minimum distance between each pair of vertices from clusters C_α and C_β. These minimum distances are computed only once, when starting the algorithm.
