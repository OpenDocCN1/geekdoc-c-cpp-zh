# 212 Cloud Computing and Digital Media

+   6. generate (componentID, $T_{R_i}$)
7. for each Reduce task do
8. for any combination of $T_{\ell_{i,j}}$ $\hat{R}_{in}$ do
9. if it is a valid result then
10. Output the result

**Constructing $G$** By applying Algorithm 9.1, we can minimize the time to evaluate a chain theta-join query using MRJ. However, usually a group of MRJs is needed to evaluate multiway theta-joins. Therefore, we now discuss the construction of $G$, which is a subgraph of the path graph $G_{\sigma}$ and sufficient to serve the evaluation of N-join query $Q$. As already discussed in Section 9.3.2, computing is to enumerate all possible no-edge-repeating paths between any pair of vertices. In fact, a subset of the entire edge collection in $G_{\sigma}$ can be further improved in $T_{opt}$. Therefore we propose two pruning conditions to effectively reduce the search space in this section.

The first intuition is the case that many join conditions are covered by multiple MRJs in $T_{opt}$ is not preferred, because each join condition needs to be evaluated only once. However, it does not imply that MRJs in $T_{opt}$ should strictly cover disjoint sets of join conditions. Because sometimes, by including extra join conditions, the output volume of intermediate results can be reduced. Therefore, we exclude M RJJ($e_{\sigma}$) on the only condition that there are other efficient ways to evaluate all the join conditions. Formally, we state the pruning condition in Lemma 1.

> **Lemma 1** $e$ should not be considered if there exists a collection of edges ES, and the following conditions are satisfied: (1) $L(e)$ $	ilde{O} \cup igcup_{\sigma \subseteq ES} L(\sigma)$ (2) $w(e) > M \max_{\sigma \subseteq ES} \{w(\sigma)\}$ and (3) $s(e) \geq \hat{A}_{\sigma \subseteq ES} s(\sigma)$

Lemma 1 is straightforward. If an MRJ can be substituted with some other MRJs that cover at the same number of join conditions and be evaluated more efficiently with less demands on processing units, this MRJ cannot appear in $T_{opt}$. Because $T_{opt}$ is the optimal collection of MRJs to evaluate the query, containing any substitutable MRJ makes $T_{opt}$ sub-optimal. For the second pruning method, we present the lemma that further reduces the search space:

> **Lemma 2**: Given two edges $e$ and $e'$, if $e'$ is not considered and $L(e') \subseteq L(e)$, then $e$ should not be considered either.