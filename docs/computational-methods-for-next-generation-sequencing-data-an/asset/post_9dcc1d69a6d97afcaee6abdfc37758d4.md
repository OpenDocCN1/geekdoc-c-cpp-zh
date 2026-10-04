
# 118 COMPUTATIONAL METHODS FOR ILP NGS DATA ANALYSIS

The two solutions are combined to solve for component B. The ILP objective for component B should be updated by adding the term of $sol_{00} + (sol_{01} - sol_{00})$. $S_{ij}$ or, equivalently, the value $sol_{00}$ should be added to $A_{ij}^w$ and $D_{ij}^w$ and the value $sol_{01}$ should be added to $B_{ij}^w$ and $C_{ij}^w$. The overall solution is obtained by identifying the common nodes of the components. In the example of Figure 5.4ab, the optimal solution happens when 2-cuts have opposite direction. The corresponding solution of ILP for the component A should be incorporated in the overall solution. When the scaffolding graph has 3-connected components too to handle, 3-cuts could be used for decomposition.

The pseudo-code of the SILP2 NSDP algorithm for processing 3-connected components is given below. SILP2 is different from SILP1 in the else-instead of solving ILP for each of four possible combinations of assignments for $S_i$ and $S_j$ as in SILP1, ILP is solved only two times for combinations $S_i = 0$ & $S_j = 0$ and $\bar{S}_i = 0$ & $\bar{S}_j = 1$.

# Algorithm The Pseudo-Code of the SILP2 NSDP Algorithm for Processing 3-Connected Components.

```
1: STACK ← root of SPQR-tree
2: VISITED ← $\emptyset$
3: while STACK is not empty
4:   p ← STACK.pop(p)
5:   for each q of p
6:     if p not in VISITED
7:       STACK.push(p)
8:     end if
9:   end for
10: if p is root then
11:   $sol_{final}$ = SOLVE(p.skeleton())
12: else
13:   (i,j) ← getcut(p,parent(p))
14:   $sol_{00}$ = SOLVE(p.skeleton()), $S_i = 0, S_j = 0$
15:   $sol_{01}$ = SOLVE(p.skeleton()), $S_i = 0, S_j = 1$
16:   in parent(p), increase weights $A_{ij}^w$ and $D_{ij}^w$ by $sol_{00}$ and weights $B_{ij}^w, C_{ij}^w$ by $sol_{01}$.
17:   end if
18: end while
```

### 5.3.1.6 Thinning Heuristic
Unfortunately the largest tri-connected component may still induce an ILP too large for CPLEX to solve in a reasonable amount of time. In order to address this problem a thinning heuristic is applied to the scaffolding graph. This scenario.

![](img/46aec008551cecb3bbf3aac2ee69b926_138_0.png)

**Figure 5.5** (a) Pairwise ordering obtained from ILP output. (b) The corresponding bipartite graph. (c) The collection of paths and cycles in the bipartite matching. (d) The scaffold represented by a collection of paths obtained by deletion of the lightest edges from cycles.

This scenario can be detected by setting a threshold on the maximum number of contigs allowed in a tri-connected component. When a component exceeds the threshold the number of read pairs necessary to induce an edge is increased by one and decomposition repeated until there is no component above the threshold.

### 5.3.1.7 Contig Ordering via Bipartite Matching
The solution to the ILP does not yield a scaffold, instead gives the pairwise order and orientation of the contigs (see Figure 5.5a). In finding scaffold, we need to remove edges such that remaining graph becomes a collection of paths. Naturally, we want to remove the least probable edges, that is, lightest edges. This problem can be solved efficiently by finding matching in the following bipartite graph $B = (V^1 \cup V^2, E)$ where each vertex in $V^1$ corresponds to the $3'$ end of a contig, each vertex in $V^2$ to the $5'$ end of a contig, and each edge corresponds to an edge from ILP solution connecting the $5'$ of it to the $3'$ end of its end (see Figure 5.5b). Each edge in $B$ has the same weight as the beginning of ILP solution. Obviously, any matching in $B$ corresponds to a collection of paths and simple cycles (see Figure 5.5c). Then from each cycle the lightest (see Figure 5.5d) is deleted and we output the set of paths.

### 5.3.2 ScaffMatch
Below we describe ScaffMatch—the problem formulation and algorithmic details are explained in the following scaffolding steps:

- Preprocessing of read pairs including read mapping, handling repeats and gap estimation for each read pair.

![](img/46aec008551cecb3bbf3aac2ee69b26_139_0.png)

**Figure 5.6** Gap estimation $d$ is calculated in conformity with the formula: $d = L_f - (L_A - left(r_1)) - (L_B - right(r_2))$, where $L_f$ is the fragment length, $L_A, L_B$ are lengths of contigs, $left(r_1)$ is the left mapping position of the read $r_1$, $right(r_2)$ is the right mapping position of the read $r_2$.

- Scaffolding graph construction with vertices corresponding to contig strands and edges corresponding to read pairs.
- Matching scaffold finding-maximum weight paths in the scaffolding graph and the corresponding orientation and ordering contigs.
- Insertion of skipped contigs into the matching scaffold.

### 5.3.2 Read Preprocessing
Each contig has two complement strands and each read from a pair is mapped to one of the strands. We discard aligned reads. We first filter read pairs in which least one read has multiple alignments. Then for each contig we compute its read coverage and filter out contigs with coverage greater than threshold. Multiple reads connecting the same pair of contigs are bundled according their gap estimation. Since we want to keep only reads that agree with each other, the reads outside the largest bundle are discarded. This procedure is illustrated in Figure 5.6.

The next step in the construction of the scaffolding graph $G=(V,E)$ is the so-called edge bundling (step 10). Multiple edges that support the same distance, relative ordering and orientation are bundled.

Consider two contigs $A, B \in V(G)$ and let $E_{AB} = \{e_i\}_{i=1}^n$ be the set of edges (paired-reads) supporting the same relative ordering and orientation of $A$ and $B$. The following steps are performed until no edges in $E_{AB}$ remain:

1. Choose $e_k \in E_{AB}$ with the median gap estimation $L_{e_k} = L_{median}(E_{AB})$.
2. Determine edges $e_i \in E_{AB}$ whose gap estimation $L_{e_i}$ is within $3\sigma(L_{median}(E_{AB}))$, bundle them into one single edge $e'$.
3. For the bundled edge $e'$ set the gap estimation and its standard deviation $L_{e'} = a/b$ and $\sigma(e') = \sqrt{b}$, where
$a = \sum_{e_i \in e'} \frac{L_{e_i}}{\sigma(e_i)^2}, b = \sum_{e_i \in e'} \frac{1}{\sigma(e_i)^2},$

4. Set the weight of the bundled edge $W_{e'}$ to $|e'|$.
5. $E_{AB} := E_{AB} \setminus e'$.

![](img/46aec008551cecb3bbf3aac2ee69b926_140_0.png)

**Figure 5.7** Contigs A, B, and C with connecting bundles of read pairs and the corresponding scaffolding graph. Each contig is split into two nodes connected with a dummy edge. Each bundle of read pairs corresponds to an inter-contig edge connecting respective strands with the two strands.

### 5.3.2.2 Scaffolding Graph
ScaffMatch constructs the scaffolding graph in the following way. Each vertex of the scaffolding graph $G = (V, E)$ corresponds to one of the contig strands (SILP2 denotes every contig as a graph node in one of the four states, see Figure 5.2) and *inter-contig* edge corresponds to a bundle of read pairs connecting two strands of different contigs (see Figure 5.7). The weight of an inter-contig edge is equal to the size of the corresponding bundle. Also for each contig we have a dummy edge connecting its two strands.

### 5.3.2.3 Matching Scaffolding
Ideally, we expect that the scaffolding graph would consist of a set of paths each corresponding to a different chromosome (see Figure 5.8a). Unfortunately, repeats introduce noisy edges connecting unrelated contigs from different chromosomes. Additionally, the paths corresponding to chromosomes may skip short contigs (especially contigs which are shorter than the insert length). Therefore, any set of paths passing through dummy edges in the scaffolding graph $G$ corresponds to a plausible scaffold (see Figure 5.8b). The most likely scaffold (see Figure 5.8c) would be supported by the largest number of read pairs.
