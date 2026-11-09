A  Adjacency Matrix, usually in form of 2-D array.

In contest problems involving graph, usually $V$ is known, thus we can build a ‘connectivity table’ by setting up a 2-D, $O(V^2)$ static array: `int AdjMat[V][V]`. For an unweighted graph, we set `AdjMat[i][j] = 1` if there is an edge between vertex $i$-$j$ and set 0 otherwise. For a weighted graph, we set `AdjMat[i][j] = weight(i, j)` if there is an edge between vertex $i$-$j$ with weight $(i, j)$ and set 0 otherwise.

Adjacency Matrix is good if the connectivity between two vertices in a *small dense graph* is frequently asked, but it is not good for *large sparse graph* as there will be too many cells in the 2-D array that are blank (contain zeroes). An adjacency Matrix requires exactly $O(V)$ to enumerate the list of neighbors of a vertex $v$ – an operation commonly used in many graph algorithms – even if vertex $v$ only has a handful of neighbors. A more compact and efficient form of graph representation is Adjacency List.

B  Adjacency List, usually in form of C++ STL `vector<vii> AdjList`, with vii defined as:

```
typedef pair<int, int> ii; typedef vector<vii> vii; // our data type shortcuts
```

In Adjacency List, we have a *vector* of $V$ vertices and for each vertex $v$, we store another vector that contains pairs of (neighboring vertex and it’s edge weight) that have connection to $v$. If the graph is unweighted, simply store weight = 0 or drop this second attribute.

With Adjacency List, we can enumerate the list of neighbors of a vertex $v$ efficiently. If there are $k$ neighbors of $v$, this enumeration is $O(k)$. As this is one of the most common operations in most graph algorithms, it is advisable to stick with Adjacency List as your default choice.

C  Edge List, usually in form of C++ STL `priority_queue<pair<int, ii> > EdgeList`.

In Edge List, we store the list of edges, usually in some order. This structure is very useful for Kruskal’s algorithm for MST (Section 4.4) where the collection of edges are sorted by their length from shortest to longest.

D  Parent-Child Tree Structure, usually in form of `int parent` & C++ STL `vector<int> child`.

If the graph is a tree (connected graph with no cycle and $E = V - 1$), like a directory/folder structure, then there exists another form of data structure. For each vertex, we only store two attributes: the parent (NULL for root vertex) and the list of children (NULL for leaves).

Exercise: Show the Adjacency Matrix, Adjacency List, and Edge List of the graph in Figure 4.1.

# 2.3.2  Union-Find Disjoint Sets

Union-Find Disjoint Sets is a data structure to model a collection of disjoint sets which has abilities to efficiently<sup>4</sup> 1). ‘find’ which set an item belongs to (or to test whether two items belong to the same set) and 2). ‘union’ two disjoint sets into one bigger set. These two operations are useful for algorithms like Kruskal’s (Section 4.4) or problems that involve ‘partitioning’, like keeping track of connected components of an undirected graph (see Section 4.2).

These seemingly simple operations are not *efficiently* supported by C++ STL `<set>` which only deals with a single set. Having a *vector* of sets and looping through each one to find which set