
## 5.3.1.3 Mapping Probability Estimation If $p_r$ are assumed to be the same for all read pairs, then the objective (5.1) reduces to maximization of the number of read pairs that agree with the contig orientation $O$. We consider the following factors that reduce the probability $p_r$, that read pair $r$ is aligned correctly:

- 1. *Overlap with Repeats.* As noted earlier, for which both reads map uniquely to the set of contigs for scaffolding. A read that fully or partially overlaps a genomic repeat may be uniquely mapped to the incorrect location in case repeats are collapsed. Preprocess contigs to annotate repeats from known repeat families and by recording the location of remapped reads. An estimate of the repeat-based mapping probability $p_r^{rep}$ is found by taking the percentage of bases $r$ aligned to nonrepetitive parts of the contigs.

- 2. *Contig Dissimilarity.* Although sequencing coverage can have significant departures from uniformity due to biases introduced in library preparation and sequencing, the average coverage of adjacent contigs is expected to be similarly affected by such biases (all read alignments, including randomly allocated nonunique alignments, are used for computing average contig coverage). If the two reads of $r$ map to contigs $i$, respectively $j$, the coverage-based mapping probability of $r$, $p_r^{cov}$, is defined as:

```
$p_r^{cov} = 1 - \frac{|coverage_i - coverage_j|}{coverage_i + coverage_j}$$
```

Note that such repeat content of the sequenced genome and sequencing depth will determine how informative repeat-based and coverage-based mapping probabilities are. Depending on these factors, either $p_r^{rep}$, $p_r^{cov}$, or their product may provide the most accurate estimate for $p_r$. Mismatches and indels in read alignments, which can be caused by sequencing errors or polymorphisms in the sequenced sample, can be incorporated in the estimation of mapping probabilities.

## 5.3.1.4 Integer Linear Program Our integer linear program maximizes the log-likelihood of scaffold orientation using the following Boolean variables:

- a binary variable $S_i$, for each contig $i$, with $S_i = 0$ if the contig orientation remains the same and $S_i = 1$ if the contig orientation is flipped with respect to the default orientation in the final scaffold.
- a binary variable $S_{ij}$ for each edge $(i, j) \in E$, which equals $0$ if neither nor both $i$ and $j$ contigs are flipped and equals $1$ if only one of them is flipped.
- binary variables $A_{ij}$ (respectively, $B_{ij}$, $C_{ij}$, and $D_{ij}$), which are set to $1$ if and only if an edge in state $A$ (respectively, $B$, $C$, or $D$) is used to connect contigs $i$ and $j$ (see Figure 5.2). For any contig pair $i$ and $j$, at most one of these variables can be one.

## SCAFFOLDING ALGORITHMS

Let $A_{ij}^w$ (respectively, $B_{ij}^w$, or $D_{ij}^w$) denote the set of read pairs supporting state A (respectively, B, C, or $D$) between the $i$-th and $j$-th contig. Define the constant $A_{ij}^w$ by

```
$A_{ij}^w = \sum_{r \in A_{ij}^w} \ln \left( \frac{P_r}{1-P_r} \right)$
```

with $B_{ij}^w$, $C_{ij}^w$, and $D_{ij}^w$ defined analogously. now formulate the ILP for maximizing the log-likelihood of a scaffold orientation:

```
$(i,j) \in E \ (A_{ij}^w \cdot A_{ij} + B_{ij}^w \cdot B_{ij} + C_{ij}^w \cdot C_{ij} + D_{ij}^w \cdot D_{ij}) \quad (5.2)
```

where

```
$S_{ij} \le S_i + S_j \quad S_{ij} \le 2 - S_i - S_j \quad (5.3)$
$S_{ij} \ge S_i - S_j \quad S_{ij} \ge S_j - S_i \quad (5.4)$
$A_{ij} + D_{ij} \le 1 - S_{ij} \quad B_{ij} + C_{ij} \le S_{ij}. \quad (5.5)$
```

In this ilp, constraints ((5.3)–(5.5)) enforce agreement between contig variables $S_{ij}'s$ and orientation variables $A_{ij}'s$, $B_{ij}'s$, $C_{ij}'s$, and $D_{ij}'s$.
Since eukaryotic genomes are linear, a valid scaffold orientation should not contain any cycles. The constraints (5.5) allow 2-cycles, 3-cycles are forbidden with the constraints shown in Figure 5.3. Larger cycles generated in the ILP solution are broken heurically because it is infeasible to forbid all of them using explicit constraints.

![](img/46aec008551cecb3bbf3aac2ee69b926_134_0.png)

Figure 5.3 Forbidding 3-cycles in ILP.

## COMPUTATIONAL METHODS FOR DATA ANALYSIS

### 5.3.1. Dynamic Programming For large genomes, the number of variables is too large for dynamic programming. We use dynamic programming (DP) to solve the problem by decomposing the graph into a tree of components. The tree is built using the SPQR-tree. For each node in the tree, we solve the ILP locally. The solutions are then combined to find the global scaffold orientation. This approach is much more efficient than solving the ILP directly.
