
- 3. Initialize n sets, each containing a different element of v
- 4. while(|B| < n - 1) do
   begin
   e = <u,v> the shortest edge not yet considered
   U = Member(u)
   V = Member(v)
   if(U != V)
   {
   Merge(U,V)
   Union(B,u,v)
   }
   end
- 5. T is the minimum spanning tree
- 6. Stop

In step 4 of Algorithm 8.6, when the edge <u,v> with minimum weight is to be added in an existing tree, the function Member() checks for u and v for the connected component they belong to. If they are members of two different connected components, the edge is added as it would not form a cycle. If they belong to the same connected component, then adding the edge forms a cycle.

![](img/a99ec79093c067f0bed8f1086197950e_416_0.png)

Consider the graph as in Fig. 8.27

Let us use Kruskal's algorithm.

- Step 1: The edge with minimum weight is selected edge = <c, d>.
- Weight of the selected edge = 10.
- As the addition of edge to the existing tree does not form a cycle, an edge is added.

![](img/a99ec79093c067f0bed8f1086197950e_416_1.png)

- Step 2: Selected edge <k, l> with weight 10.

![](img/a99ec79093c067f0bed8f1086197950e_416_2.png)

- Step 3: Selected edge <b, f> with weight 10.

![](img/a99ec79093c067f0bed8f1086197950e_417_0.png)

- Step 4: Selected edge <g, k> with weight 20.

![](img/a99ec79093c067f0bed8f1086197950e_417_1.png)

- Step 5: Selected edge <a, b> weight 20.

![](img/a99ec79093c067f0bed8f1086197950e_417_2.png)

- Step 6: Selected edge <f, j> with weight 20.

![](img/a99ec79093c067f0bed8f1086197950e_417_3.png)

- Step 7: Selected edge <c, g> with weight 30.

![](img/a99ec79093c067f0bed8f1086197950e_417_4.png)

- Step 8: Selected edge <j, k> with weight 30.

![](img/a99ec79093c067f0bed8f1086197950e_418_0.png)

- Step 9: Selected edge <g, h> with weight 30.

![](img/a99ec79093c067f0bed8f1086197950e_418_1.png)

- Step 10: Selected edge <i, j> with weight 30.

![](img/a99ec79093c067f0bed8f1086197950e_418_2.png)

Figure 8.28 is a spanning tree with weight 220.

![](img/a99ec79093c067f0bed8f1086197950e_418_3.png)

Fig. 8.28 Spanning tree for graph in Fig. 8.27

### 8.5.4 Biconnected Components

Depth-first search traversal of a graph, one of the most important techniques used for solving a variety of problems is described in Section 8.4.1. DFS can be used to find the connected components of an undirected graph. There are a few non-trivial graph algorithmic problems to be considered.

Consider a graph modelling a communication network problem. We expect the network to be robust under failures of any of the nodes. Even if a node fails, the remaining network should still remain connected. A graph is said to be biconnected if this condition is satisfied.

Often, we need to test whether a given undirected graph is biconnected or not. A biconnected component is a maximal biconnected sub-graph of the graph G = (V, E). Edges and non-separation vertices belong to exactly one component, whereas separation vertices belong to at least two. Biconnected components contain no separation vertices or edges. A separation vertex or edge is one whose removal disconnects G. Between any two vertices, there exists at least two disjoint paths, and G has a simple cycle containing them. Any connected graph can be decomposed into a tree of biconnected components called the block tree of the graph. The blocks are attached to each other at shared vertices called cut vertices or articulation points. Specifically, a cut vertex is any vertex, which, when removed increases the number of connected components. In Fig. 8.29, the separation edge e1 is between A and B, and the separation vertex is E.

![](img/a99ec79093c067f0bed8f1086197950e_419_0.png)

Fig. 8.29 Sample graph with biconnected components

### 8.5.5 Disjoint Set Operations

In minimum spanning tree computation algorithms, we have used two important set operations. Similar to those, there are many algorithms in which a disjoint-set data structure is used. This data structure keeps track of a set of elements partitioned into a number of disjoint subsets. A union–find algorithm is one that performs two useful operations (i.e., find and union) on such a data structure.

**Find** This is a membership check of the element. It determines the set in which a particular element is located and is also useful for determining whether two elements are in the same set or not.

**Union** This operation combines or merges two sets into a single set.

These two operations are supported by a disjoint-set data structure. Hence, it is also called as a union–find data structure or merge–find set.

## 8.6 SHORTEST PATH ALGORITHM

A weighted graph is a graph where the values are assigned to the edges and the length of a path is the sum of the weight of the edges in the path. We let w(i , j) denote the weight of edge (i , j). In a weighted graph, we often need to find the shortest path. The shortest path between two given vertices is the path having minimum length. This problem can be solved by one of the greedy algorithms, by Edsger W. Dijkstra, often called as Dijkstra’s algorithm.

Consider a directed graph G = (A, B). Each edge has a non-negative length. One of the nodes is the source vertex. Suppose we are to determine the shortest path from a to the destination vertex z. Let us use two sets of vertices, visited and unvisited. Let V denote the set of visited vertices that contains the vertices that have already been chosen and the minimal distance from the source is already known for every vertex in V. The set U contains all other vertices whose minimal distance from the source is not yet known.

Let an array Dist hold the length of the shortest distance and the array Path hold the shortest path between the source and each of the vertices. At each step, Dist[i] shows the shortest distance between a and i, and Path[i] shows the shortest path between a and i. The basic idea of the algorithm is to determine the minimum cost from i to one vertex at each of the iterations and call it j, mark j as visited, and recalculate the cost from i to each of the unvisited vertices going through j.

Initially, a is the only vertex in v. At each step we add to v, another vertex, for which the shortest path from a has been determined. The array Dist[] is initialized by setting Dist[i] to the weight of the edge from a to i if it exists and to ∞ if it does not. To determine which vertex to add to v at each step, we apply the criteria of choosing the vertex j with the smallest distance recorded in Dist such that j is not the visited one. When we add j to v (set of visited vertices), we must update the entries of Dist by checking, for each vertex k that is not in v, whether a path through j and then directly to k is shorter than the previously recorded distance of k. That is, we replace Dist[k] by Dist[j] + weight of the edge from j to k if the value of the latter quantity is lesser. Here, j is the currently selected vertex. Let k be a vertex whose distance is updated. If the distance is updated, then path is also updated. Then, path[k] becomes the path of j followed by k.

In brief,

```
if Dist[k] > (Dist[j] + weight<j,k>) then
    Dist[k] = Dist[j] + w<j,k>
and
Path[k] = Path[j] U (k)
```

Algorithm 8.7 is for computing the shortest path from the source vertex to the destination vertex.

- ALGORITHM 8.7
- 1. Let G = (A, B) where A = set of vertices
- 2. Initially, let V = {a} and U = A - {a}
- 3. Let U be the unvisited and V be the visited vertices
- 4. Let Dist[t] = w(a, t) for every vertex t \in A
- 5. Select the vertex in U that has the smallest value Dist[x]. Let x denote this vertex.
- 6. If x is the vertex we wish to reach from a, goto 9. If not, let V = V + (x) and U = U - (x)
- 7. For every vertex t in A, compute Dist[t] with respect to V as,
     Dist[t] = min(Dist[t], Dist[x] + w (x,t))
- 8. Repeat steps 5, 6, and 7
- 9. Stop

Let us consider the graph in Fig. 8.30, and let us compute the shortest path between a and all other vertices using this algorithm.

![](img/a99ec79093c067f0bed8f1086197950e_421_0.png)

Fig. 8.30 Directed weighted graph
