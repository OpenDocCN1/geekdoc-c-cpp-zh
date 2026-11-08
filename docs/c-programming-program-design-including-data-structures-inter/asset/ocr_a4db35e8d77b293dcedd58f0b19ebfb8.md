# ### EXAMPLE 20-5

Let G be the graph shown in Figure 20-7.

![](bbox=[0.09, 0.163, 0.9, 0.365])

**FIGURE 20-7** Weighted graph G

Suppose that the source vertex of G is 0. The graph shows the weight of each edge. After Steps 1 and 2 execute, the resulting graph is as shown in Figure 20-8.

![](bbox=[0.09, 0.465, 0.9, 0.806])

| | [0] | [1] | [2] | [3] | [4] |
|---|---|---|---|---|---|
| smallestWeight | 0 | 16 | ∞ | 2 | ∞ |
| weightFound | T | F | F | F | F |

**FIGURE 20-8** Graph after Steps 1 and 2 execute

**Iteration 1 of Steps 3 to 5:** At Step 3, we select a vertex that is closest to the vertex 0 and for which the shortest path has not been found. We do this by finding a vertex in the array smallestWeight that has the smallest weight and a corresponding entry in the array weightFound of false. Therefore, in this iteration, we select the vertex 3. At Step 4, we mark weightFound[3] as true. Next, at Step 5, we consider vertices