# ERROR CORRECTION OF NGS FROM VIRAL HAPLOTYPES

339
is equivalent to maximizing the log-likelihood function
is is equivalent to maximizing the log-likelihood function

```
$$\ell(G) = \sum_{i=1}^{N} o_i \log Pr(r_i|G). \quad (15.11)$
```

kGEM replaces the problem of maximizing 15.11 with the easier problem of maximizing the log-likelihood of the hidden model

```
$$\ell_{hid}(G) = \sum_{i=1}^{N} \sum_{j=1}^{k} P_{i,j} \log(f_j Pr(r_j|G^)). \quad (15.12)$
```

where $p_{i,j}$ is the portion of reads matching the $r_j$, which are emitted by the generator-allele haplotype $\mathcal{G}$. It iteratively estimates generalized haplotype $\mathcal{G}$ and the missing data $f_j$ and $p_{i,j}$ using expectation maximization (EM) approach. At each iteration of the algorithm, after EM it estimates the probability $P_{err}$ of errors for each estimated haplotype $\mathcal{G}'$,

```
$$\ell_{err}' = 1 - (1 - \sum_{u=m_j/2}^{m_j} \binom{m_j}{u} \varepsilon^u (1-\varepsilon)^{m_j-u})^L. \quad (15.13)$
```

Haplotypes with $P_{err} > 0.05$ are discarded. The following is the work flow of kGEM summarized in kGEM error correction algorithm.

# 15.2.2 k-Based Algorithms

k-mer-based algorithms currently available either as separate applications (Reptile (36), EDAR (34), KEC (15)) or as parts of the general genome assembly frameworks (EULER-DB, EASER (31–37), ALLPATH (38)). The main idea behind this family of algorithms is to switch from condition of whole-length reads to substrings of reads of a given length $k$ ($k$-mers). For each $k$-mer, its frequency $k$-count is calculated. Each read of length $l$ contains $l=k+1$ consecutive $k$-mers, distribution of $k$-counts which provides information about possible sequencing errors. $k$-mers with high counts (solid $k$-mers) are usually correct, while $k$-mers with low counts ($k$-mers) more likely contain errors (Figure 15.4a). The basic scheme of $k$-mer-based algorithms can be described as follows:

+   1) Calculate $k$-mers $s$ and their $k$-counts may be inefficient due to large sizes of NGS data sets. This can be resolved by storing $k$-mers in a hash map, where each key is a $k$-mer $s$ and the corresponding value is the array $v(s) = ((r, i) : s$ is a $k$-mer of the read $r$ starting at position $i$) ($15$). $k$-counts can be adjusted based on GC-count (34).

+   2) Determine a threshold-count $t_e$ separating solid and weak $k$-mers.