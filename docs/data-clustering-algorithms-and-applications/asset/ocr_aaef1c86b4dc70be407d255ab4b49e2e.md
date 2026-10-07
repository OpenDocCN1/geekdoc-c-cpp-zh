# Algorithm 23 GRIDCLUS Algorithm

```
Algorithm 23 GRIDCLUS Algorithm
1: Set u := 0, W := {}. C := {initialization};\n2: Create the grid structure and calculate the block densities;
3: Generate a sorted block sequence B1, B2, ..., Bp; mark all blocks "not active" and "not clustered";
4: while a "not active" block exist
5: u := u + 1;
6: mark first B1, B2, ..., Bp with equal density index "active";
7: for each "not active" block Bp := B1, B2, ..., Bp
8: Create a new set C[u];
9: W[u] ⊄ W[u] + 1.C[u, W[u]] ⊄ Bp;
10: Mark block Bp clustered;
11: NEIGHBOR_SEARCH(Bp, W[u]);
12: end for
13: for each "not active" block B
14: W[u] ⊄ W[u] + 1.C[u, W[u]] ⊄ B;
15: end for
16: Mark all blocks "not clustered";
17: end while
```

# Algorithm 24 Procedure NEIGHBOR_SEARCH(B,C)

```
Algorithm 24 Procedure NEIGHBOR_SEARCH(B,C)
1: for each "active" and "not clustered" neighbor B' of B
2: C ← B';
3: Mark block B "clustered";
4: NEIGHBOR_SEARCH(B',C);
5: end for
```

discriminatory density thresholds, the pathological case of step 7 could also apply and the complexity would be O(n²). (Granted average case complexity for several distributions may be significantly better (i.e., O(n)) and that may be a better analysis to consider).

The BANG algorithm introduced by Shikuta and Erhart [26] is an extension of the GRIDCLUS algorithm. It addresses some of the inefficiencies of the GRIDCLUS algorithm in terms of grid structure, searching, and managing blocks by their density. BANG also places data points in blocks and uses variants of the grid directory called BANG to maintain blocks. Neighborhood search and processing the blocks in decreasing order of density are determined by the maximum dimensions shared by a common between blocks. A binary tree is used to store the grid structure; that neighbor searching can be done more efficiently. From this the dendrogram is calculated. Centers of clusters are still the most highly blocks in the clustering phase. The BANG algorithm is summarized in Algorithm 25 [10]. While both GRIDCLUS and BANG discern nested clusters efficiently, BANG has been shown to be more efficient than GRIDCLUS on data sets because of significantly reduced growth of grid structure [26].

# 6.2.2 STING and STING+: The Statistical Information Grid Approach

Wang et al. [28] proposed a STAtistical InformationGrid-based clustering method (STING) to cluster spatial databases and facilitate region-oriented queries. STING divides the spatial area into rectangular cells and stores the cells in a hierarchical grid tree. Each cell (except leaves in