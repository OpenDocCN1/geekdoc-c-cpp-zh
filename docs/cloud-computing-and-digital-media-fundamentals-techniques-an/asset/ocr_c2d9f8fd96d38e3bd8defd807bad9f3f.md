# Efficient Join Query Processing on the Cloud ■ 213

PROOF: Since $e$ is not considered, it implies that there is a better solution to cover $L_{e'} \setminus L_e$ And this solution can be employed together with $L_{e'} - L_e$, which is more efficient than computing $L_{e'}$; in one step. Therefore, $L_{e'}$ should not be considered.

Note that Lemma 2 is orthogonal to Lemma 1. Since Lemma 1 decides whether an MRJ should be considered a member of $T_{opt}$, if the answer is negative, we can employ Lemma 2 to directly prune more undesired MRJs. By employing the two lemmas proposed earlier, we develop an algorithm to construct $G$ efficiently in an incremental manner, as presented in Algorithm 9.2.

# Algorithm 9.2: Constructing $G\$$

+   **Data:** $G\$$ containing $n$ vertices and $m$ edges, $G\$ = \Delta$$, a sorted list $WL = \varnothing$;
**Result:** $G\$$$
1. for $i = 1 : n$ do
2. for $j > i$ do
3. for $L = 1 : m$ do
4. if there is an L-hop path from $R_i$ to $R_j$ then
5. $e' \\leftarrow$ the L-hop path from $R_i$ to $R_j$
6. if $WL \neq \varnothing$; then
7. scan WL to the first group of edges that cover $e'$
8. apply Lemma 1 to decide whether to report $e'$ to $G\$$$
9. if $e'$ is not reported then
10. break //$Lemma 2 plays the role
11. insert $e'$ into $WL$ that WL maintains a sequence of edges in the ascending order of $w(e')$

Since we do not care about the direction of a path, meaning $e(v_i, v_j) = e(v_j, v_i)$, we compute the pairwise join paths following a fixed order of vertices (relations). In Algorithm 9.2, we employ the linear scan of a sorted list to help decide whether a path should be reported in $G$. One tricky part in the algorithm is line 4. A straightforward way is to employ distributed file systems (DFS) search from a given starting vertex. The time complexity is $O(m+n)$. However, it introduces redundant work for every vertex to perform this task. A better solution is to run Algorithm 9.2. We first traverse $G_v$, once and record the L-hop neighbor of every vertex. It only $O(m+n)$ time complexity. Then, line 4 can be determined in $O(1)$ time. Overall, the worst time complexity of Algorithm 9.2 is $O(n^2m)$. This happens when