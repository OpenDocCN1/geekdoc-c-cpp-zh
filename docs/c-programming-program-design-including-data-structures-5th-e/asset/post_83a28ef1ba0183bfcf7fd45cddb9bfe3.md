
A tree *T* is called a **spanning tree** of graph *G* if *T* is a subgraph of *G* such that *V(T) = V(G)*; that is, all of the vertices of *G* are in *T*.

Suppose *G* denotes the graph of Figure 21–14. Then, the graphs of Figure 21–15 show three spanning trees of *G*. Let us note the following theorem.

**Theorem:** A graph *G* has a spanning tree if and only if *G* is connected.

From this theorem, it follows that in order to determine a spanning tree of a graph, the graph must be connected.

Let *G* be a weighted graph. **A minimal spanning tree** of *G* is a spanning tree with the minimum weight.

Prim’s algorithm and Kruskal’s algorithm are two well-known algorithms that can be used to find the minimal spanning tree of a graph. This section discusses Prim’s algorithm to find a minimal spanning tree. The interested reader can find the Kruskal’s algorithm in the discrete structures book or a data structures book listed in Appendix H.

Prim’s algorithm builds the tree iteratively by adding edges until a minimal spanning tree is obtained. We start with a designated vertex, which we call the source vertex. At each iteration, a new edge that does not complete a cycle is added to the tree.

Let *G* be a weighted graph such that *V(G) = {v₀, v₁, …, vₙ₋₁}*, in which *n* is the number of vertices, is specified. Let *v₀* be the source vertex. Let *T* be the partially built tree. Initially, *V(T)* contains the source vertex, and *E(T)* is empty. At the next iteration, a new vertex that is not in *V(T)* is added to *V(T)*, such that an edge exists from a vertex in *T* to the new vertex so that the corresponding edge has the smallest weight. The corresponding edge is added to *E(T)*.

The general form of Prim’s algorithm is as follows. (Let *n* be the number of vertices in *G*.)

```
1.  Set V(T) = {source}
2.  Set E(T) = empty
3.  for i = 1 to n
    3.1.  minWeight = infinity;
    3.2.  for j = 1 to n
              if vⱼ is in V(T)
                  for k = 1 to n
                      if vₖ is not in T and weight[vⱼ, vₖ] < minWeight
                      {
                          endVertex = vₖ;
                          edge = (vⱼ, vₖ);
                          minWeight = weight[vⱼ, vₖ];
                      }
    3.3.  V(T) = V(T) ∪ {endVertex};
    3.4.  E(T) = E(T) ∪ {edge};
```

Let us illustrate Prim’s algorithm using the graph G of Figure 21-16 (which is same as the graph of Figure 21-14).

![](img/f97f778697507bb6fdd80c5991210cba_1389_0.png)

**FIGURE 21-16** Weighted graph G

Let N denote the set of vertices of G that are not in T. Suppose that the source vertex is 0. After Steps 1 and 2 execute, V(T), E(T), and N are as shown in Figure 21-17.

![](img/f97f778697507bb6fdd80c5991210cba_1389_1.png)

**FIGURE 21-17** Graph G, V(T), E(T), and N after Steps 1 and 2 execute

Step 3.2 checks the following edges:

| Edge | Weight of the Edge |
| --- | --- |
| (0, 1) | 6 |
| (0, 2) | 5 |
| (0, 3) | 2 |

Clearly, the edge (0, 3) has the smallest weight. Therefore, vertex 3 is added to $V(T)$, and the edge (0, 3) is added to $E(T)$. Figure 21-18 shows the resulting graph, $V(T)$, $E(T)$, and $N$. (The dotted line shows the edge in $T$.)

![](img/f97f778697507bb6fdd80c5991210cba_1390_0.png)

**FIGURE 21-18** Graph $G$, $V(T)$, $E(T)$, and $N$ after the first iteration of Step 3

Next, Step 3.2 checks the following edges:

| Edge | Weight of the Edge |
|---|---:|
| (0,1) | 6 |
| (0,2) | 5 |
| (3,4) | 8 |

Clearly, the edge (0, 2) has the smallest weight. Therefore, vertex 2 is added to $V(T)$, and the edge (0, 2) is added to $E(T)$. Figure 21-19 shows the resulting graph, $V(T)$, $E(T)$, and $N$.

![](img/f97f778697507bb6fdd80c5991210cba_1390_1.png)

**FIGURE 21-19** Graph $G$, $V(T)$, $E(T)$, and $N$ after the second iteration of Step 3

At the next iteration, Step 3.2 checks the following edges:

| Edge | Weight of the Edge |
| --- | --- |
| (0, 1) | 6 |
| (2, 5) | 7 |
| (2, 6) | 5 |
| (3, 4) | 8 |

Clearly, the edge (2, 6) has the smallest weight. Therefore, vertex 6 is added to V(T), and the edge (2, 6) is added to E(T). Figure 21-20 shows the resulting graph, V(T), E(T), and N. (The dotted lines show the edges in T.)

![](img/f97f778697507bb6fdd80c5991210cba_1391_0.png)

**FIGURE 21-20** Graph G, V(T), E(T), and N after the third iteration of Step 3

At the next iteration, Step 3.2 checks the following edges:

| Edge | Weight of the Edge |
| --- | --- |
| (0, 1) | 6 |
| (2, 5) | 7 |
| (3, 4) | 8 |
| (6, 1) | 4 |

Clearly, the edge (6, 1) has the smallest weight. Therefore, vertex 1 is added to V(T), and the edge (6, 1) is added to E(T). Figure 21-21 shows the resulting graph, V(T), E(T), and N. (The dotted lines show the edges in T.)

![](img/f97f778697507bb6fdd80c5991210cba_1392_0.png)

**FIGURE 21-21**  Graph G, V(T), E(T), and N after the fourth iteration of Step 3

At the next iteration, Step 3.2 checks the following edges:

| Edge | Weight of the Edge |
|---|---:|
| (1, 4) | 2 |
| (2, 5) | 7 |
| (3, 4) | 8 |

Clearly, the edge (1, 4) has the smallest weight. Therefore, vertex 4 is added to V(T), and the edge (1, 4) is added to E(T). Figure 21-22 shows the resulting graph, V(T), E(T), and N. (The dotted lines show the edges in T.)

![](img/f97f778697507bb6fdd80c5991210cba_1392_1.png)

**FIGURE 21-22**  Graph G, V(T), E(T), and N after the fifth iteration of Step 3

At the next iteration, Step 3.2 checks the following edges:

| Edge | Weight of the Edge |
|---|---:|
| (2, 5) | 7 |
| (4, 5) | 10 |

Clearly, the edge (2, 5) has the smallest weight. Therefore, vertex 5 is added to V(T), and the edge (2, 5) is added to E(T). Figure 21-23 shows the resulting graph, V(T), E(T), and N. (The dotted lines show the edges in T.)

![](img/f97f778697507bb6fdd80c5991210cba_1393_0.png)

**FIGURE 21-23** Graph G, V(T), E(T), and N after the sixth iteration of Step 3

The dotted lines show a minimal spanning tree of G of weight 25.

Before we give the definition of the function to implement Prim’s algorithm, let us first define the spanning tree as an ADT.

Let mstV be a bool array such that mstV[j] is true if the vertex v_j is in T, and false otherwise. Let edges be an array such that edges[j] == k if there is an edge connecting vertices v_j and v_k. Suppose that the edge (v_i, v_j) is in the minimal spanning tree. Let edgeWeights be an array such that edgeWeights[j] is the weight of the edge (v_i, v_j).

Using these conventions, the following class defines a spanning tree as an ADT.

```cpp
class msTreeType: public graphType
{
public:
    void createSpanningGraph();
        //Function to create the graph and the weight matrix.
        //Postcondition: The graph using adjacency lists and
        //              its weight matrix is created.

    void minimalSpanning(int sVertex);
        //Function to create a minimal spanning tree with
        //root as sVertex.
        //Postcondition: A minimal spanning tree is created.
        //                The weight of the edges is also
        //                saved in the array edgeWeights.
        //
    void printTreeAndWeight();
        //Function to output the edges of the minimal
        //spanning tree and the weight of the minimal
        //spanning tree.
        //Postcondition: The edges of a minimal spanning tree
        //               and their weights are printed.

    msTreeType(int size = 0);
        //Constructor
        //Postcondition: gSize = 0; maxSize = size;
        //               graph is an array of pointers to linked
        //               lists.
        //               weights is a two-dimensional array to
        //               store the weights of the edges.
        //               edges is an array to store the edges
        //               of a minimal spanning tree.
        //               edgeWeights is an array to store the
        //               weights of the edges of a minimal
        //               spanning tree.

    ~msTreeType();
        //Destructor
        //The storage occupied by the vertices and the arrays
        //weights, edges, and edgeWeights is deallocated.

protected:
    int source;
    double **weights;
    int *edges;
    double *edgeWeights;
};
```

We leave the UML class diagram of the class `msTreeType` and the inheritance hierarchy as an exercise. The definition of the function `createSpanningGraph` is also left as an exercise for you. This function creates the graph and the weight matrix associated with the graph.

The following C++ function, `minimalSpanning`, implements Prim’s algorithm, as described previously.

```cpp
void msTreeType::minimalSpanning(int sVertex)
{
    int startVertex, endVertex;
    double minWeight;

    source = sVertex;

    bool *mstV;
    mstV = new bool[gSize];
```
