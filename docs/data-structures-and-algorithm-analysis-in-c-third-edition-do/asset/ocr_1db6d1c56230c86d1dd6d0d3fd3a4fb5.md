# 406

# Chap. 11 Graphs

```
// Prim's MST algorithm: priority queue version
void Prim(Graph* G, int S, int s) {
    int i, v;
    // "v" is current vertex
    int V(G->n());
    // V[I] stores I's closest neighbor
    Dijklem E[];
    Dijklem E(G->e());
    // Heap array with lots of space
    temp distance = 0; vertex = s;
    E(0) = temp; // Initialize heap array
    heap-Dijklem, DCComp H(E, 1, G->e()); // Create heap
    for (i=0; i<G->n(); i++) {  // Now build MST
        do {
            if (H.size() == 0) return; // Nothing to remove
            v = H.removefirst();
            while (G->getMark(v) != VISITED); // Skip if visited
            G->setMark(v, VISITED);
            if (v != s) AddEdgeToMST(V[v], v); // Add edge to MST
            if (D[v] == INFINITY) // Unreachable vertex
            for (w=G->next(v,w); w != v; w = G->next(v,w)) {
                if (D[w] > G->weight(v,w)) { // Update D
                    D[w] = G->weight(v,w);
                    V[w] = v; // Update who it came from
                }
            }
            temp.distance = D[v]; vertex = v;
            H.insert(temp); // Insert new instance in heap
        } while (0);
    }
```

**Figure 11.2** An implementation of Prim's algorithm using a priority queue.

be of lower cost than edge eⱼ, because Prim's algorithm did not generate an MST. This situation is illustrated in Figure 11.20. However, Prim's algorithm would have selected the least-cost edge available. It would have selected e', not ej. Thus, it is a contradiction that Prim's would have selected the wrong edge, and Prim's algorithm must be correct.

**Example 11.3** For the graph of Figure 11.20, assume that we begin by marking Vertex A. From A, the least-cost edge leads to Vertex C. Vertex C and edge (A, C) are added to the MST. At this point, our edges connecting the MST (Vertices A and C) with the rest of the graph are... So we add Vertex D to the MST. For the next iteration, our edges are (A, E), (C, B), (C, F), and (D, F). Because edges (C, F) and (D, F) happen to have equal cost, it is an arbitrary decision as to which gets selected. We pick (C, F). The next step marks Vertex E and adds edge (F, E) to the MST. In this manner, Vertex B (through edge (C, B)) is marked. At this point, the algorithm terminates.