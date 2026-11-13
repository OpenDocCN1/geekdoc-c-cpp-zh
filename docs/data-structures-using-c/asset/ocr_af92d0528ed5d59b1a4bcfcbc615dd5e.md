Algorithm 8.4 is an informal statement of the algorithm. Here, G is a graph and T is a spanning tree to be computed.

# ALGORITHM 8.4

```
1. Let G = (V, E) and T = (A, B)
   A = φ and B = φ
2. Let i ∈ V, i is a start vertex
3. A = A ∪ {i}
4. while A ≠ V do
   begin
   find edge <u,v> ∈ E of minimum length
   such that u ∈ A and v ∈ V – A
   A = A ∪ {v} and
   B = B ∪ {<u,v>}
   end
5. stop
```

To obtain a simple implementation in any programming language say C++, suppose that the vertices of G are numbered from 1 to n so that v = {1, 2, ..., n). Let the matrix M give the length of each edge and L[i][j] = ∞ if the edge <i, j> ∉ E, that is, edge <i, j> does not exist. Let us use two arrays—Nearest [i] and Min_Dist [i]. Let T = (A, B) be the minimum spanning tree where initially A and B are empty. For each vertex i ∈ V – A, the array Nearest [i] gives the vertex in A that is nearest to i. Similarly, for each vertex i ∈ V – A, the array Min_Dist [i] gives the distance from i to this nearest vertex. For a vertex i ∈ A, we set Min_Dist [i] = –1. In this way, we can find out whether a vertex is in A or not. The set A arbitrarily initializes to {1}.

Consider the graph in Fig. 8.24.

![](bbox=[0.406, 0.596, 0.7, 0.716])

Fig. 8.24 Sample graph

Using Prim’s algorithm, we get a spanning tree for this graph in the following steps:

+   1. Let f be the start vertex.

Among vertices e, b, g, and j, the vertex b is the nearest one with edge <f, b> and weight 10.

![](bbox=[0.406, 0.856, 0.45, 0.92])

```
w(f, e) = 40
w(f, b) = 10 <- min
w(f, g) = 30
w(f, j) = 20
```