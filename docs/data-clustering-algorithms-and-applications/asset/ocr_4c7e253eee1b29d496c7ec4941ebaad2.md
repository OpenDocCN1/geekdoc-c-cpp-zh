# Time-Series Data Clustering

Kotsifakos et al. have introduced SMBGT, a subsequence matching method, that allows for gaps in both the query and the target sequences and constrains the maximum match length between the two [26]. In their study, they apply SMBGT to a Query-by-Humming system that given a humming query, retrieves the K most similar sequences in a database. The proposed similarity measure, SMBGT, given a query Q and a target sequence X, finds the subsequence of X that best matches. The experimental evaluation of the proposed similarity measure was performed on two-dimensional time series notes of arbitrary length. Given Q and their subsequences Q[qs,qe] and X[xx,xe] of equal length, SMBGT(Q,X) is defined as follows. Let $G_Q$ and $G_X$ be the indices of $Q[qs,qe]$ and $X[xx,xe]$ in Q and X. If $q_i \approx x_j, \pi_i \in G_Q, \gamma_j \in G_X, \forall i=1,\dots,|G_Q|$, and

```
$\pi_{i+1} - \pi_i - 1 \leq \beta, \gamma_{i+1} - \gamma_i \leq \alpha$ (15.4)
```

then, the pair $(Q[qs,qe], X[xx,xe])$ is a bounded-gapped subsequence of Q and X. The longest subsequence with $xx-xe$ is called SMBGT(Q,X). $\varepsilon$ controls tolerance, and $\alpha$ and $\beta$ allowed gaps in sequences Q and X, respectively, and $r$ controls the maximum alignment length. A graphical example of SMBGT in two dimensions is illustrated in Figure 15.3. In the experimental evaluation shows that the main advantage of SMBGT over compared subsequence matching methods (SPRING, Edit distance, and DTW) is that it can handle high noise levels. In some applications, as the studied Query-by-Humming problem, this is extremely important. Other approaches that perform subsequence matching are described in [20, 5, 7].

# 15.5 Shape-Based Time-Series Clustering Techniques

In this section we review the most and most widely used techniques for shape-based time-series clustering. The two most popular approaches are $k$-means clustering and hierarchical clustering. Most techniques extend or use one of these two clustering methods; thus, we classify the reviewed approaches accordingly.

![](bbox=[0.283, 0.574, 0.712, 0.801])

**FIGURE 15.3 (See color insert): SMBGT distance between a query sequence Q and a database sequence X.