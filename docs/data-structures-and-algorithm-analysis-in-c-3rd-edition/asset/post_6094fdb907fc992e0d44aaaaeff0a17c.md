
time. Every time we modify D(X), we could reorder X in the heap by deleting and reinserting it. This is an example of a priority queue with priority update, as described in Section 5.5. To implement true priority updating, we would need to store with each vertex its array index within the heap. A simpler approach is to add the new (smaller) distance value for a given vertex as a new record in the heap. The smallest value for a given vertex currently in the heap will be found first, and greater distance values found later will be ignored because the vertex will already be marked as VISITED. The only disadvantage to repeatedly inserting distance values is that it will raise the number of elements in the heap from Θ(|V|) to Θ(|E|) in the worst case. The time complexity is Θ((|V| + |E|) log |E|), because for each edge we must reorder the heap. Because the objects stored on the heap need to know both their vertex number and their distance, we create a simple class for the purpose called DijkElem, as follows. DijkElem is quite similar to the Edge class used by the adjacency list representation.

```
class DijkElem {
public:
    int vertex, distance;
    DijkElem() { vertex = -1; distance = -1; }
    DijkElem(int v, int d) { vertex = v; distance = d; }
};
```

Figure 11.18 shows an implementation for Dijkstra’s algorithm using the priority queue.

Using MinVertex to scan the vertex list for the minimum value is more efficient when the graph is dense, that is, when |E| approaches |V|². Using a priority queue is more efficient when the graph is sparse because its cost is Θ((|V| + |E|) log |E|). However, when the graph is dense, this cost can become as great as Θ(|V|² log |E|) = Θ(|V|² log |V|).

Figure 11.19 illustrates Dijkstra’s algorithm. The start vertex is A. All vertices except A have an initial value of ∞. After processing Vertex A, its neighbors have their D estimates updated to be the direct distance from A. After processing C (the closest vertex to A), Vertices B and E are updated to reflect the shortest path through C. The remaining vertices are processed in order B, D, and E.

## 11.5 Minimum-Cost Spanning Trees

The minimum-cost spanning tree (MST) problem takes as input a connected, undirected graph G, where each edge has a distance or weight measure attached. The MST is the graph containing the vertices of G along with the subset of G’s edges that (1) has minimum total cost as measured by summing the values for all of the edges in the subset, and (2) keeps the vertices connected. Applications where a solution to this problem is useful include soldering the shortest set of wires needed

```
// Dijkstra’s shortest paths algorithm with priority queue
void Dijkstra(Graph* G, int* D, int s) {
    int i, v, w;                // v is current vertex
    DijkElem temp;
    DijkElem E[G->e()];         // Heap array with lots of space
    temp.distance = 0; temp.vertex = s;
    E[0] = temp;                // Initialize heap array
    heap<DijkElem, DDComp> H(E, 1, G->e()); // Create heap
    for (i=0; i<G->n(); i++) {          // Now, get distances
        do {
            if (H.size() == 0) return; // Nothing to remove
            temp = H.removefirst();
            v = temp.vertex;
        } while (G->getMark(v) == VISITED);
        G->setMark(v, VISITED);
        if (D[v] == INFINITY) return;   // Unreachable vertices
        for (w=G->first(v); w<G->n(); w = G->next(v,w))
            if (D[w] > (D[v] + G->weight(v, w))) { // Update D
                D[w] = D[v] + G->weight(v, w);
                temp.distance = D[w]; temp.vertex = w;
                H.insert(temp);     // Insert new distance in heap
            }
    }
}
```

Figure 11.18 An implementation for Dijkstra’s algorithm using a priority queue.

|  | A | B | C | D | E |
|---|---|---|---|---|---|
| Initial | 0 | ∞ | ∞ | ∞ | ∞ |
| Process A | 0 | 10 | 3 | 20 | ∞ |
| Process C | 0 | 5 | 3 | 20 | 18 |
| Process B | 0 | 5 | 3 | 10 | 18 |
| Process D | 0 | 5 | 3 | 10 | 18 |
| Process E | 0 | 5 | 3 | 10 | 18 |

Figure 11.19 A listing for the progress of Dijkstra’s algorithm operating on the graph of Figure 11.16. The start vertex is A.

to connect a set of terminals on a circuit board, and connecting a set of cities by telephone lines in such a way as to require the least amount of cable.

The MST contains no cycles. If a proposed MST did have a cycle, a cheaper MST could be had by removing any one of the edges in the cycle. Thus, the MST is a free tree with |V| − 1 edges. The name “minimum-cost spanning tree” comes from the fact that the required set of edges forms a tree, it spans the vertices (i.e., it connects them together), and it has minimum cost. Figure 11.20 shows the MST for an example graph.

![](img/7ea3c39173f146f675b63b146d1535f3_422_0.png)

## Figure 11.20

A graph and its MST. All edges appear in the original graph. Those edges drawn with heavy lines indicate the subset making up the MST. Note that edge (C, F) could be replaced with edge (D, F) to form a different MST with equal cost.

### 11.5.1 Prim’s Algorithm

The first of our two algorithms for finding MSTs is commonly referred to as Prim’s algorithm. Prim’s algorithm is very simple. Start with any Vertex N in the graph, setting the MST to be N initially. Pick the least-cost edge connected to N. This edge connects N to another vertex; call this M. Add Vertex M and Edge (N, M) to the MST. Next, pick the least-cost edge coming from either N or M to any other vertex in the graph. Add this edge and the new vertex it reaches to the MST. This process continues, at each step expanding the MST by selecting the least-cost edge from a vertex currently in the MST to a vertex not currently in the MST.

Prim’s algorithm is quite similar to Dijkstra’s algorithm for finding the single-source shortest paths. The primary difference is that we are seeking not the next closest vertex to the start vertex, but rather the next closest vertex to any vertex currently in the MST. Thus we replace the lines

```
if (D[w] > (D[v] + G->weight(v, w)))
    D[w] = D[v] + G->weight(v, w);
```

in Dijkstra’s algorithm with the lines

```
if (D[w] > G->weight(v, w))
    D[w] = G->weight(v, w);
```

in Prim’s algorithm.

Figure 11.21 shows an implementation for Prim’s algorithm that searches the distance matrix for the next closest vertex. For each vertex I, when I is processed by Prim’s algorithm, an edge going to I is added to the MST that we are building. Array V[I] stores the previously visited vertex that is closest to Vertex I. This information lets us know which edge goes into the MST when Vertex I is processed.

```
void Prim(Graph* G, int* D, int s) { // Prim’s MST algorithm
    int V[G->n()];                 // Store closest vertex
    int i, w;
    for (i=0; i<G->n(); i++) {     // Process the vertices
        int v = minVertex(G, D);
        G->setMark(v, VISITED);
        if (v != s)
            AddEdgetoMST(V[v], v);  // Add edge to MST
        if (D[v] == INFINITY) return; // Unreachable vertices
        for (w=G->first(v); w<G->n(); w = G->next(v,w))
            if (D[w] > G->weight(v,w)) {
                D[w] = G->weight(v,w);  // Update distance
                V[w] = v;               // Where it came from
            }
    }
}
```

## Figure 11.21 An implementation for Prim’s algorithm.

The implementation of Figure 11.21 also contains calls to AddEdgetoMST to indicate which edges are actually added to the MST.

Alternatively, we can implement Prim’s algorithm using a priority queue to find the next closest vertex, as shown in Figure 11.22. As with the priority queue version of Dijkstra’s algorithm, the heap’s Elem type stores a DijkElem object.

Prim’s algorithm is an example of a greedy algorithm. At each step in the for loop, we select the least-cost edge that connects some marked vertex to some unmarked vertex. The algorithm does not otherwise check that the MST really should include this least-cost edge. This leads to an important question: Does Prim’s algorithm work correctly? Clearly it generates a spanning tree (because each pass through the for loop adds one edge and one unmarked vertex to the spanning tree until all vertices have been added), but does this tree have minimum cost?

## Theorem 11.1 Prim’s algorithm produces a minimum-cost spanning tree.

Proof: We will use a proof by contradiction. Let G = (V, E) be a graph for which Prim’s algorithm does not generate an MST. Define an ordering on the vertices according to the order in which they were added by Prim’s algorithm to the MST: v0, v1, ..., vn−1. Let edge ei connect (vx, vi) for some x < i and i ≥ 1. Let ej be the lowest numbered (first) edge added by Prim’s algorithm such that the set of edges selected so far cannot be extended to form an MST for G. In other words, ej is the first edge where Prim’s algorithm “went wrong.” Let T be the “true” MST. Call vp (p < j) the vertex connected by edge ej, that is, ej = (vp, vj).

Because T is a tree, there exists some path in T connecting vp and vj. There must be some edge e′ in this path connecting vertices vu and vw, with u < j and w ≥ j. Because ej is not part of T, adding edge ej to T forms a cycle. Edge e′ must
