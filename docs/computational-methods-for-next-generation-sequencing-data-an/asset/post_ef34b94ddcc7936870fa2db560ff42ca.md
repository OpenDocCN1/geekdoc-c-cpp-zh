
# ERROR CORRECTION OF NGS FROM VIRAL HAPLOTYPES

339 is equivalent to maximizing the log-likelihood function.

```
$$\ell(G) = \sum_{i=1}^{N} o_i \log Pr(r_i|G). \quad (15.11)$$
```

kGEM replaces the problem of maximizing 15.11 with the easier problem of maximizing the log-likelihood of the hidden model:

```
$$\ell_{hid}(G) = \sum_{i=1}^{N} \sum_{j=1}^{k} P_{i,j} \log(f_j Pr(r_j|G^)). \quad (15.12)$$
```

where $p_{i,j}$ is the portion of reads matching the $r_j$, which are emitted by the generator-allele haplotype $\mathcal{G}$. It iteratively estimates generalized haplotype $\mathcal{G}$ and the missing data $f_j$ and $p_{i,j}$ using expectation maximization (EM) approach. At each iteration of the algorithm, after EM it estimates the probability $P_{err}$ of errors for each estimated haplotype $\mathcal{G}'$:

```
$$\ell_{err}' = 1 - (1 - \sum_{u=m_j/2}^{m_j} \binom{m_j}{u} \varepsilon^u (1-\varepsilon)^{m_j-u})^L. \quad (15.13)$$
```

Haplotypes with $P_{err} > 0.05$ are discarded. The following is the work flow of kGEM summarized in kGEM error correction algorithm.

## 15.2.2 k-Based Algorithms

k-mer-based algorithms currently available either as separate applications (Reptile (36), EDAR (34), KEC (15)) or as parts of the general genome assembly frameworks (EULER-DB, EASER (31–37), ALLPATH (38)). The main idea behind this family of algorithms is to switch from condition of whole-length reads to substrings of reads of a given length $k$ ($k$-mers). For each $k$-mer, its frequency $k$-count is calculated. Each read of length $l$ contains $l=k+1$ consecutive $k$-mers, distribution of $k$-counts which provides information about possible sequencing errors. $k$-mers with high counts (solid $k$-mers) are usually correct, while $k$-mers with low counts ($k$-mers) more likely contain errors (Figure 15.4a). The basic scheme of $k$-mer-based algorithms can be described as follows:

- 1) Calculate $k$-mers $s$ and their $k$-counts may be inefficient due to large sizes of NGS data sets. This can be resolved by storing $k$-mers in a hash map, where each key is a $k$-mer $s$ and the corresponding value is the array $v(s) = ((r, i) : s$ is a $k$-mer of the read $r$ starting at position $i$) ($15$). $k$-counts can be adjusted based on GC-count (34).
- 2) Determine a threshold-count $t_e$ separating solid and weak $k$-mers.

## Algorithm kGEM Error Correction Algorithm (29, 35)

- 1: Find initial generalized haplopes using the following steps. First, iteratively identify reads $s^1, \dots, s^k$ as follows: at each iteration, pick the most frequent read, which have not been picked before and that the minimum Hamming distance to the previously selected reads is maximal. Then define the initial set of generalized haplopes $\mathcal{G}^l = \{G^1, \dots, G^k\}$;
$$G_{e,j}^l \leftarrow \begin{cases} 1-4\epsilon, & \text{if } s_e^j = e; \ \epsilon, & \text{otherwise}. \end{cases}$$
- 2: Calculate $h_{j,i} = Pr(r|\mathcal{G}^l)$ using (15.9); set the iterations count $t \leftarrow 1; \mathcal{G}^0 = \emptyset$;
- 3: While $\mathcal{G}^t \neq \mathcal{G}^{t-1}$
- 4: Estimate frequencies $f_{ij}$ and partitions $p_{1,1}, \dots, p_{k,N}$ as follows. Starting from the initial solution $(p^{(0)}_i \leftarrow j$ for $i=1, \dots, k$, iteratively perform the following steps:
- 5: While the Euclidean distance between current and previous solution is greater than predefined precision $\mathbf{\delta}$
- 6: For each read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
$$p_{j,i} \leftarrow \frac{f_{i,j}}{\sum_{u=1}^N h_{u,j}}$$
- 7: Calculate the expected number of reads emitted by $G^l$ that matches $r_i$;
$$e_{j,i} \leftarrow e_j \cdot p_{j,i}$$
- 8: Update the multiplicity and frequency of each generalized haplotype $G^l \in \mathcal{G}^t$;
$$m_j \leftarrow \sum_{i=1}^N e_{i,j}, f_j \leftarrow \frac{m_j}{\sum_{u=1}^N m_u}$$
- 9: end $1-4\epsilon$, if $e = arg$
- 10: Update the set of generalized haplopes and recalculate probabilities as follows: $\mathcal{G}^{t+1} = \{G^1, \dots, G^k\}$;
$$G_{e,l}^l \leftarrow \begin{cases} \max_{i \in\{1,\dots,N\}; r_i=e} \sum p_{j,i} e'(e \in\{a,c,t,g,d\}); \ \epsilon, \end{cases}$$
- 11: collapse identical haplotypes and drop haplotypes with a high error probability $p_{err}$ (see (15.13)).
- 12: $h_{j,i} \leftarrow Pr(r|\mathcal{G}^t); t \leftarrow t+1$;
- 13: end
- 14: round the obtained generalized haplopes i.e. find the set of sequences $\mathcal{H} = \{hp^1, \dots, hp^k\}$, where the base at each position $v$ of a haplotype $hp^l$ has the highest frequency in the column $u$ of the generalized haplotype $G^l$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $E^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 13: end
- 14: round the obtained generalized haplopes i.e. find the set of sequences $\mathcal{H} = \{hp^1, \dots, hp^k\}$, where the base at each position $v$ of a haplotype $hp^l$ has the highest frequency in the column $u$ of the generalized haplotype $G^l$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype calculate p_{j,i};
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 13: end
- 13: end
- 14: round the obtained generalized haplopes i.e. find the set of sequences $\mathcal{H} = \{hp^1, \dots, hp^k\}$, where the base at each position $v$ of a haplotype $hp^l$ has the highest frequency in the column $u$ of the generalized haplotype $G^l$;
- 13 13: end
- 14: round the obtained generalized haplopes i.e. find the set of sequences $\mathcal{H} = \{hp^1, \dots, hp^k\}$, where the base at each position $v$ of a haplotype $hp^l$ has the highest frequency in the column $u$ of the generalized haplotype $G^l$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype--;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype--_{j,i- calculate $p_{j,i;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i}$;
- 3) For every read $r_i$ and generalized haplotype $G^l \in \mathcal{G}^t$ calculate $p_{j,i.
- 3) For every  $r_5$ and   $555555//555.

 (Figure 15.4a)

## 352 COMPUTATIONAL METHODS FOR NGS ANALYSIS

A method for detection and removal of potential sequencing errors implemented in EDAR (34) is based on the following. If $[i_e, j_e]$ is an error region of the read $r$ of length $l$, then all k-mers starting within region probably contains errors, while k-mers starting at positions $i_e - 1$ and $j_e + 1$ are likely to be error-free. In particular, it implies that if $j_e - i_e+1 > k$, then the base at position $i_e + k - 1$ is most probably

## 353 3)

Once errors are localized, different algorithms treat errors differently. EDAR removes potentially erroneous nucleotides and slips, while Reptile (36), KEC (15), and EULER-SR (37) try to correct the errors by finding nucleotide insertions, deletions, or replacements that convert k-mers into strong k-mers. Both approaches have advantages and disadvantages. In particular, correction of errors allows to keep as much genetic variability as possible, thus making the corresponding algorithms especially suitable for detection of minor variants in heterogeneous populations. However, in the process of transforming k-mers, this approach may introduce new artificial errors (31); moreover, it is more time-consuming. Filtering of errors does not introduce new errors, but it is not suitable for amplicon sequencing and presents a risk of loss of rare variants and distortion of frequencies. We will consider some of these approaches in more detail in the following sections.

A method for detection and removal of potential sequencing errors implemented in EDAR (34) is based on the following. If $[i_e, j_e]$ is an error region of the read $r$ of length $l$, then all k-mers starting within region probably contains errors, while k-mers starting at positions $i_e - 1$ and $j_e + 1$ are likely to be error-free. In particular, it implies that if $j_e - i_e+1 > k$, then the base at position $i_e + k - 1$ is most probably

(Figure 15.4a)

**Figure 15.4b**

![](img/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511/460511)

(a) distribution of k-counts

(b) distribution of k-counts

Possible errors in reads are localized in error-prone regions, which can be identified by mean-shift (39, 40) according to k-counts. In particular, KEC (15) estimates errors by:
(i) successfully finding segments $[i_j, j_j]$ such that for every $p \in [i_j, j_j]$, we have $k_p \le l_j$;
(ii) clustering positions;
(iii) extending the obtained segments in both directions by adding consecutive positions $q$ such that $k_q$ belongs to the same cluster; and
(iv) joining the overlapping segments. EDAR (34) first clusters positions, partitions clusters into disjoint segments, and considers the segments with the mean k-counts $l_t$ as error regions.
