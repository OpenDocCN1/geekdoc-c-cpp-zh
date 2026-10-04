# Algorithm kGEM Error Correction Algorithm (29, 35)

+   1: Find initial generalized haplopes using the following steps. First, iteratively identify reads $s^1, \dots, s^k$ as follows: at each iteration, pick the most frequent read, which have not been picked before and that the minimum Hamming distance to the previously selected reads is maximal. Then define the initial set of generalized haplopes $\mathcal{G}^l = \{G^1, \dots, G^k\}$;
$$G_{e,j}^l \leftarrow \begin{cases} 1-4\epsilon, & \text{if } s_e^j = e; \ \epsilon, & \text{otherwise}. \end{cases}$$
2: Calculate $h_{j,i} = Pr(r|\mathcal{G}^l)$ using (15.9); set the iterations count $t \leftarrow 1; \mathcal{G}^0 = \emptyset$;
3: While $\mathcal{G}^t \neq \mathcal{G}^{t-1}$
4: Estimate frequencies $f_{ij}$ and partitions $p_{1,1}, \dots, p_{k,N}$ as follows. Starting from the initial solution $(p^{(0)}_i \leftarrow j$ for $i=1, \dots, k$, iteratively perform the following steps:
5: While the Euclidean distance between current and previous solution is greater than predefined precision $\mathbf{\delta}$
6: For each read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
$$p_{j,i} \leftarrow \frac{f_{i,j}}{\sum_{u=1}^N h_{u,j}}$$
7: Calculate the expected number of reads emitted by $G^l$ that matches $r_i$;
$$e_{j,i} \leftarrow e_j \cdot p_{j,i}$$
8: Update the multiplicity and frequency of each generalized haplotype $G^l \in \mathcal{G}^t$;
$$m_j \leftarrow \sum_{i=1}^N e_{i,j}, f_j \leftarrow \frac{m_j}{\sum_{u=1}^N m_u}$$
9: end $1-4\epsilon$, if $e = arg$
10: Update the set of generalized haplopes and recalculate probabilities as follows: $\mathcal{G}^{t+1} = \{G^1, \dots, G^k\}$;
$$G_{e,l}^l \leftarrow \begin{cases} \max_{i \in\{1,\dots,N\}; r_i=e} \sum p_{j,i} e'(e \in\{a,c,t,g,d\}); \ \epsilon, \end{cases}$$
11: collapse identical haplotypes and drop haplotypes with a high error probability $p_{err}$ (see (15.13)).
12: $h_{j,i} \leftarrow Pr(r|\mathcal{G}^t); t \leftarrow t+1$;
13: end
14: round the obtained generalized haplopes i.e. find the set of sequences $\mathcal{H} = \{hp^1, \dots, hp^k\}$, where the base at each position $v$ of a haplotype $hp^l$ has the highest frequency in the column $u$ of the generalized haplotype $G^l$;nEnsure: the set of haplotypes $\mathcal{H}$.

+   (3) For every read $r$ find error regions, that is, the positions $[e_i, e_j]$ the k$-mer $s_p$ starting at the position $p$ is weak (or considered as such). If such error region exists, either correct (15, 31, 36, 37) or remove (34) errors.

All heterogeneous viral genomes contain extremely variable regions, which for distinguishing individual inhabitant variants. Consequently, k$-mers derived