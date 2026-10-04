# ERROR CORRECTION OF NGS READS FROM VIRAL POPULATIONS

# Algorithm KEC Postprocessing Using Alignment (15)

**Require:** The set of unique reads $\mathcal{R} = \{r_1, \dots, r_n\}$ with multiplicities $m_1, \dots, m_n$.

+   1: Set the iteration counter $nlter \leftarrow 1$

+   2: **repeat**

+   3: Calculate the set of maximal reads $\mathcal{R}_{max} \subseteq \mathcal{R}$, i.e., reads that does not contain other reads as subsequences.

```
$a_{ij} \leftarrow \begin{cases} 1, & \text{if } i=j \text{ or the read } r_j \text{ is a subsequence of the read } r_i; \ 0, & \text{otherwise}; \end{cases}$
```

```
$d_j \leftarrow \sum_{i=1}^n a_{ij}$.
```

+   4: For every read $r_i \in \mathcal{R}$, calculate its frequency $f_i$ as $f_i = m_i / \sum_{k=1}^{|\mathcal{R}|} m_k$. Recalculate frequencies of maximal reads $\mathcal{R}_{max}$ as follows: $f_j - \sum_{k=1}^{|\mathcal{R}|} \frac{R_{jk}}{a_{jk} d_k}$.

+   5: **if** $nlter$ **is odd then**

+   6: Calculate a multiple of the maximal reads $\mathcal{R}_{max}$ and identify homopolymer regions in the alignment. If the position in a homopolymer region contains gaps, calculate the total frequencies of reads with without gap at this position, and if one of them is significantly greater than the other, correct the position accordingly.

+   7: **else**

+   8: Calculate the neighbor joining tree $\mathcal{T}$ of the set $\mathcal{R}_{max}$ using pairwise alignment scores from the previous iteration. Let have a common parent in the tree $\mathcal{T}$. For every pair $(r_i, r_j) \in \mathcal{P}$, calculate a pairwise alignment, identify homopolymer regions containing gaps, and correct those gaps to the more variant if the edit distance between $r_i$ and $r_j$ is 1 or the frequency of one of the reads is significantly greater than the other.

+   9: **end if**

+   10: $\mathcal{R} \leftarrow \mathcal{R}_{max}, nlter \leftarrow nlter + 1$.

+   11: until no corrections are made or the number of iterations $nlter$ does not exceed the maximal allowed value

**Ensure:** haplotypes $\mathcal{R}$ and their frequencies $f_1, \dots, f_{|\mathcal{R}|}$

# 15.3 ALGORITHM COMPARISON

# 15.3.1 Benchmark Data

The data from Reference 15 were used for algorithms comparison.¹ For the data generation, a set of 10 plasmids $C_1-C_{10}$ with sequences a 309 nt segment of the E1/E2 junction of HCV genome was obtained (GenBank accession number AB047639.1) and 24 samples were created, with samples $S_1-S_{14}$ containing a single clone and samples $M_1-M_{10}$ containing mixtures of clones in

> ¹Available at http://alan.cls.edu.gov/NGS/?q=content/pysequencing-error-correction-algorithm