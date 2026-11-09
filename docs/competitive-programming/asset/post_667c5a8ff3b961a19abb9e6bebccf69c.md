
### 3.5 Chapter Notes

- DP with non-trivial states
  1. LA 4106 - ACORN (Singapore07) (DP with dimension reduction)
  2. LA 4143 - Free Parentheses (Jakarta08) (Problem set by Felix Halim)
  3. LA 4146 - ICPC Team Strategy (Jakarta08) (DP with 3 states)
  4. LA 4336 - Palindromic paths (Amritapuri08)
  5. LA 4337 - Pile it down (Amritapuri08)
  6. LA 4525 - Clues (Hsinchu09)
  7. LA 4526 - Inventory (Hsinchu09)
  8. LA 4643 - Twenty Questions (Tokyo09)

- DP on Tree
  1. UVa 10243 - Fire! Fire!! Fire!!! (Min Vertex Cover ≈ Max Independent Set on Tree)
  2. UVa 11307 - Alternative Arborescence (Min Chromatic Sum, 6 colors are sufficient)
  3. LA 3685 - Perfect Service (Kaohsiung06)
  4. LA 3794 - Party at Hali-Bula (Tehran06)
  5. LA 3797 - Bribing FIPA (Tehran06)
  6. LA 3902 - Network (Seoul07)
  7. LA 4141 - Disjoint Paths (Jakarta08)

The main source of the ‘Complete Search’ material in this chapter is the USACO training gateway [18].

We adopt the name ‘Complete Search’ rather than ‘Brute-Force’ as we believe that some Complete Search solutions can be clever and fast enough, although it is complete, e.g. **Branch & Bound** and **A* Search** (both are not discussed yet in this book). We believe the term ‘clever Brute-Force’ is a bit self-contradicting.

Divide and Conquer paradigm is usually used in the form of its popular algorithms: binary search (bisection method), merge/quick/heap sort, and data structures: binary search tree, heap, segment tree, etc. We will see more Divide and Conquer later in Computational Geometry (Section 7.5).

*Basic* Greedy and Dynamic Programming (DP) techniques are always included in popular algorithm textbooks, e.g. Introduction to Algorithms [4], Algorithm Design [13], Algorithms [5], Programming Challenges [23], The Art of Algorithms and Programming Contests [16], Art of Programming Contest [1]. However, to keep pace with the growing difficulties and creativity of these techniques, especially the DP techniques, we include more references from the Internet: TopCoder algorithm tutorial [25] and recent programming contests, e.g. ACM ICPC Regional Kaohsiung 2006, Singapore 2007, Jakarta 2008, Central European Olympiad in Informatics 2009, etc.

However, for some real-life problems, especially those that are classified as NP-Complete [4], many of the approaches discussed so far will not work. For example, 0-1 Knapsack Problem, which has $O(NW)$ DP complexity, is too slow if $W$ is big. For this, people use heuristics or local search: Beam Search, Tabu Search [10], Genetic Algorithm, Ants Colony Optimization, etc.

There are approximately **109 programming exercises** discussed in this chapter.

## Chapter 4: Graph

*Many real-life problems can be classified as graph problems. Some have efficient solutions. Some do not have them yet. In this chapter, we learn various graph problems with known efficient solutions, ranging from basic traversal, minimum spanning trees, shortest paths, and network flow algorithms.*

### 4.1 Overview and Motivation

In this chapter, we discuss graph problems that commonly appear in programming contests, the algorithms to solve them, and the practical implementations of these algorithms. The issue on how to store graph information has been discussed earlier in Section 2.3.1.

We assume that the readers are familiar with the following terminologies: Vertices/Nodes, Edges, Un/Weighted, Un/Directed, In/Out Degree, Self-Loop/Multiple Edges (Multigraph) versus Simple Graph, Sparse/Dense, Path, Cycle, Isolated versus Reachable Vertices, (Strongly) Connected Component, Sub-Graph, Tree/Forest, Complete Graph, Directed Acyclic Graph, Bipartite Graph, Euler/Hamiltonian Path/Cycle. If you encounter any unknown terms, please go to Wikipedia [46] and search for that particular term.

Table 4.1 summarizes our research so far on graph problems in recent ACM ICPC Asia regional contests and its ICPC Live Archive [11] IDs. Although there are so many graph problems (many are discussed in this chapter), they only appear either once or twice in a problem set. The question is: “Which ones do we have to learn?” If you want to do well in contests, you have no choice but to study all these materials.

### 4.2 Depth First Search

#### Basic Form and Application

Depth First Search - abbreviated as DFS - is a simple algorithm to traverse a graph. With the help of a global array `int dfs_num[V]` which is initially set to ‘unvisited’ (a constant value `DFS_WHITE = 0`), DFS starts from a starting vertex, visits the deepest possible vertex from the start vertex before attempting other branches. Note that this sequence of visitation depends very much on the way we order neighbors of a vertex, i.e. the sequence 0 → 1 → 3 → 2 (backtrack to 3) → 4 is also a possible visitation sequence. Also notice that one call of `dfs(u)` will only visit all vertices that are *connected* to vertex `u`. That is why vertices 5, 6, and 7 in Figure 4.1 are currently unvisited by calling `dfs(0)`.

The DFS code shown here is very similar to the recursive backtracking code shown earlier in Section 3.1. If we compare the pseudocode of a typical backtracking code (replicated below) with the DFS code shown above, we can see that the main difference is just whether we flag visited vertices. DFS does. Backtracking does not. By not revisiting vertices, DFS runs in $O(V + E)$, but the time complexity of backtracking goes up exponentially.

```c
void backtracking(state) {
    if (hit end state or invalid state) // invalid state includes states that cause cycling
        return; // we need terminating/pruning condition
    for each neighbor of this state // regardless it has been visited or not
        backtracking(neighbor);
}
```

#### Other Applications

DFS is not only useful for traversing a graph. It can be used to solve many other graph problems.

##### Finding Connected Components in Undirected Graph

The fact that one single call of `dfs(u)` will only visit vertices that are actually connected to `u` can be utilized to find (and to count) the connected components of an undirected graph (see further below for a similar problem on directed graph). We can simply use the following code to restart DFS from one of the remaining unvisited vertices to find the next connected component (until all are visited):

```c
// all sample codes involving REP use this macro
#define REP(i, a, b) \
  for (int i = int(a); i <= int(b); i++)

// inside int main()
numComponent = 0;
memset(dfs_num, DFS_WHITE, sizeof dfs_num);
REP (i, 0, V - 1)
    if (dfs_num[i] == DFS_WHITE) {
        printf("Component %d, visit: ", ++numComponent);
        dfs(i);
        printf("\n");
    }
printf("There are %d connected components\n", numComponent);

// For the sample graph, the output is like this:
// Component 1, visit: 0 1 2 3 4
// Component 2, visit: 5
// Component 3, visit: 6 7
```

**Exercise:** We can also use Union-Find Disjoint Sets to solve this graph problem. How?

##### Flood Fill - Labeling the Connected Components

DFS can be used for other purposes than just finding (and counting) the connected components. Here, we show how a simple tweak of `dfs(u)` can be used to *label* the components. Typically, we ‘label’ (or ‘color’) the component by using its component number. This variant is more famously known as ‘flood fill’.

```c
void floodfill(int u, int color) {
    dfs_num[u] = color; // not just a generic DFS_BLACK
    TRvii(AdjList[u], v) // try all neighbors v of vertex u, note that we use our TRvii macro again
        if (dfs_num[v->first] == DFS_WHITE) // avoid cycle
            floodfill(v->first, color); // v is an (neighbor, weight) pair
}

// inside int main()
numComponent = 0;
memset(dfs_num, DFS_WHITE, sizeof dfs_num);
REP (i, 0, V - 1) // for each vertex u in [0..V-1], note that we use our REP macro again
    if (dfs_num[i] == DFS_WHITE) // if not visited
        floodfill(i, ++numComponent);
REP (i, 0, V - 1)
    printf("Vertex %d has color %d\n", i, dfs_num[i]);

// For the sample graph, the output is like this:
// Vertex 0 1 2 3 4 have color 1
// Vertex 5 has color 2
// Vertex 6 7 has color 3
```

**Exercise:** Flood Fill is more commonly performed on 2-D grid (implicit graph). Try to solve UVa 352, 469, 572, etc.

##### Graph Edges Property Check via DFS Spanning Tree

Running DFS on a connected component of a graph will form a DFS *spanning tree* (or *spanning forest* if the graph has more than one component and DFS is run on each component). With one more vertex state: `DFS_GRAY = 2` (visited but not yet completed) on top of `DFS_WHITE` (unvisited) and `DFS_BLACK` (visited and completed), we can use this DFS spanning tree (or forest) to classify graph edges into four types:

1. **Tree edges:** those traversed by DFS, i.e. from vertex with `DFS_GRAY` to vertex with `DFS_WHITE`.
2. **Back edges:** part of cycle, i.e. from vertex with `DFS_GRAY` to vertex with `DFS_GRAY` too. Note that usually we do not count bi-directional edges as having ‘cycle’ (We need to remember `dfs_parent` to distinguish this, see the code below).
3. **Forward/Cross edges:** from vertex with `DFS_GRAY` to vertex with `DFS_BLACK`. These two types of edges are not typically used in programming contest problems.

Figure 4.2 shows an animation (from top left to bottom right) of calling `dfs(0)`, then `dfs(5)`, and finally `dfs(6)` on the sample graph in Figure 4.1. We can see that 1 → 2 → 3 → 1 is a (true) cycle and we classify edge (3 → 1) as a back edge, whereas 0 → 1 → 0 is not a cycle but edge (1 → 0) is just a bi-directional edge. The code for this DFS variant is shown below.
