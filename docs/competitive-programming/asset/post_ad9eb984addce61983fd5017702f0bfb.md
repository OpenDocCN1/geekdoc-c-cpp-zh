
## Topological Sort (on a Directed Acyclic Graph)

Topological sort or topological ordering of a Directed Acyclic Graph (DAG) is a linear ordering of the vertices in the DAG so that vertex $u$ comes before vertex $v$ if edge $(u \to v)$ exists in the DAG. Every DAG has one or more topological sorts. There are several ways to implement a Topological Sort algorithm. The simplest is to slightly modify the simplest DFS implementation in this section.

```cpp
void topoVisit(int u) {
    dfs_num[u] = DFS_BLACK;
    TRVi (AdjList[u], v)
        if (dfs_num[v->first] == DFS_WHITE)
            topoVisit(v->first);
    topologicalSort.push_back(u); // this is the only change
}

// inside int main()
topologicalSort.clear(); // this global vector stores topological sort in reverse order
memset(dfs_num, DFS_WHITE, sizeof dfs_num);
REP (i, 0, V - 1)
    if (dfs_num[i] == DFS_WHITE)
        topoVisit(i);
reverse(topologicalSort.begin(), topologicalSort.end());
REP (i, 0, topologicalSort.size() - 1)
    printf("%d\n", topologicalSort[i]);
```

In topoVisit(u), we append u to the list of vertices explored only after visiting all subtrees below u. As vector only supports *efficient insertion* from back, we work around this issue by simply reversing the print order in the output phase. This simple algorithm for finding (a valid) topological sort is again due to Tarjan. It again runs in $O(V + E)$ as with DFS.

Exercise: Do you understand why appending `topologicalSort.push_back(u)` in the standard DFS code is enough to help us find topological sort of a DAG? Explain in your own words!

Programming Exercises for Depth First Search (DFS):

- Finding Connected Components / Flood Fill
  1. UVa 260 - Il Gioco dell’X
  2. UVa 352 - Seasonal War (Flood Fill)
  3. UVa 459 - Graph Connectivity (also solvable with Union-Find Disjoint Sets)
  4. UVa 469 - Wetlands of Florida (Flood Fill)
  5. UVa 572 - Oil Deposits (Flood Fill)
  6. UVa 657 - The Die is Cast (Flood Fill)
  7. UVa 782 - Contour Painting (Flood Fill)
  8. UVa 784 - Maze Exploration (Flood Fill)
  9. UVa 785 - Grid Colouring (Flood Fill)
  10. UVa 852 - Deciding victory in Go (Flood Fill)
  11. UVa 10336 - Rank the Languages (Flood Fill)
  12. UVa 10926 - How Many Dependencies?
  13. UVa 10946 - You want what filled? (Flood Fill)
  14. UVa 11110 - Equidivisions (Flood Fill)
  15. UVa 11518 - Dominos 2 (Flood Fill)
  16. UVa 11749 - Poor Trade Advisor (also solvable with Union-Find Disjoint Sets)
- Finding Articulation Points / Bridges
  1. UVa 315 - Network (Articulation Points)
  2. UVa 610 - Street Directions (Bridges)
  3. UVa 796 - Critical Links (Bridges)
  4. UVa 10199 - Tourist Guide (Articulation Points)
- Finding Strongly Connected Components
  1. UVa 10731 - Test
  2. UVa 11504 - Dominos
  3. UVa 11709 - Trust Groups
  4. UVa 11770 - Lighting Away
- Topological Sort (also see shortest/longest paths problems in DAG in Section 4.9.2)
  1. UVa 124 - Following Orders
  2. UVa 200 - Rare Order
  3. UVa 872 - Ordering
  4. UVa 10305 - Ordering Tasks

## 4.3 Breadth First Search

### Basic Form and Application

Breadth First Search - abbreviated as BFS - is another form of graph traversal algorithm. BFS starts with the insertion of initial source vertex *s* into a queue, then processes the queue as follows:

In an unweighted graph, the distance between two neighboring vertices connected with an edge is simply one unit. Thus the layer count of a vertex that we have seen previously is precisely the shortest path length from the source to that vertex. For example in Figure 4.7, the shortest path from the vertex labeled with '35' to the vertex labeled '30', is 3, as '30' is in the third layer in BFS sequence of visitation. Reconstructing the shortest path: 35 → 15 → 10 → 30 is easy if we store the BFS spanning tree, i.e. vertex '30' remembers '10' as its parent, vertex '10' remembers '15', vertex '15' remembers '35' (the source).

Which graph traversal algorithm to choose? Table 4.2 can be helpful.

| | O(V + E) DFS | O(V + E) BFS |
|---|---|---|
| Pro | Uses less memory | Can solve SSSP on unweighted graphs |
| Cons | Cannot solve SSSP on unweighted graphs | Uses more memory |
| Code | Slightly easier to code | Slightly longer to code |

Table 4.2: Graph Traversal Algorithm Decision Table

Programming Exercises for Breadth First Search (BFS):

- Single-Source Shortest Paths on Unweighted Graph
  1. UVa 336 - A Node Too Far
  2. UVa 383 - Shipping Routes
  3. UVa 417 - Word Index
  4. UVa 429 - Word Transformation
  5. UVa 439 - Knight Moves
  6. UVa 532 - Dungeon Master (3-D BFS)
  7. UVa 567 - Risk
  8. UVa 627 - The Net (must print the path)
  9. UVa 762 - We Ship Cheap
  10. UVa 924 - Spreading the News
  11. UVa 928 - Eternal Truths
  12. UVa 10009 - All Roads Lead Where?
  13. UVa 10044 - Erdos numbers (parsing part is troublesome)
  14. UVa 10067 - Playing with Wheels (implicit graph in problem statement)
  15. UVa 10102 - The Path in the Colored Field
  16. UVa 10150 - Doublets (BFS state is string!)
  17. UVa 10422 - Knights in FEN
  18. UVa 10610 - Gopher and Hawks
  19. UVa 10653 - Bombs! NO they are Mines!! (BFS implementation must be efficient)
  20. UVa 10959 - The Party, Part I
  21. UVa 11049 - Basic Wall Maze (some restricted moves + print path)
  22. UVa 11352 - Crazy King
  23. UVa 11513 - 9 Puzzle (BFS from goal state + efficient data structure)
  24. UVa 11545 - Avoiding Jungle in the Dark
  25. UVa 11730 - Number Transformation (need prime factoring, see Section 5.3.1)
  26. UVa 11792 - Krochanska is Here! (be careful with the definition of 'important station')
  27. LA 3290 - Invite Your Friends (plus Dijkstra's)
  28. LA 4408 - Unlock the Lock
  29. LA 4637 - Repeated Substitution with Sed
  30. LA 4645 - Infected Land
- **Variants**
  1. UVa 10004 - Bicoloring (Bipartite Graph check)
  2. UVa 11080 - Place the Guards (Bipartite Graph check, some tricky cases)
  3. UVa 11101 - Mall Mania (Multi-Sources BFS from mall1, get min at border of mall2)
  4. UVa 11624 - Fire! (Multi-Sources BFS)

## 4.4 Kruskal’s

### Basic Form and Application

Motivating problem: Given a connected, undirected, and weighted graph $G$ (see the leftmost graph in Figure 4.8), select a subset of edges $E' \subseteq G$ such that the graph $G$ is (still) connected and the total weight of the selected edges $E'$ is minimal.

To satisfy connectivity criteria, edges in $E'$ must form a *tree* that spans (covers) all $V \in G$ — the *spanning tree*! There can be several valid spanning trees in $G$, i.e. see Figure 4.8, middle and right sides. One of them is the required solution that satisfies the minimal weight criteria.

This problem is called the Minimum Spanning Tree (MST) problem and has many practical applications, as we will see later in this section.

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_81_0.png)

Figure 4.8: Example of a Minimum Spanning Tree (MST) Problem (from UVa 908 [17])

This MST problem can be solved with several well-known algorithms, i.e. Prim’s and Kruskal’s, both are greedy algorithms and explained in [4, 21, 14, 23, 16, 1, 13, 5]. For programming contests, we opt for Kruskal’s as its implementation is very easy with the help of 2 data structures.

Joseph Bernard Kruskal Jr.’s algorithm first sorts $E$ edges based on non-decreasing weight in $O(E \log E)$. This can be easily done using `priority_queue` (or alternatively, use `vector` & `sort`). Then, it *greedily* tries to add $O(E)$ edges with minimum costs to the solution as long as such addition does not form a cycle. This cycle check can be done easily using Union-Find Disjoint Sets. The code is short and overall runs in $O(E \log E)$.

```cpp
typedef pair<int, int> ii; // we use ii as a shortcut of integer pair data type

priority_queue<pair<int, ii> > EdgeList; // sort by edge weight O(E log E)
// PQ default: sort descending. To sort ascending, we can use <(negative) weight(i, j), <i, j> >
```
