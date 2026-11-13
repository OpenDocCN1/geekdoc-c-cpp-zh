For non-recursive implementation, whenever we reach a node, we shall push it (vertex or node address) onto the stack. We would then pop the vertex, process it, and push all its adjacent vertices onto the stack. Suppose we have a directed graph G where all the vertices are initially marked as unvisited. In a graph, we can reach any vertex more than once through different paths. Hence, to assure that each vertex is visited once, we mark each as visited whenever it is processed. Let us use an array say visited for the same. Initially, all vertices are marked unvisited. Marking visited[i] to 0 indicates that the vertex i is unvisited. Whenever we push the vertex say j onto the stack, we mark it visited by setting its visited[j] to 1.

The recursive algorithm for DFS can be outlined as in Algorithm 8.1. Algorithm 8.1 shows the recursive working of DFS of a graph.

```
ALGORITHM 8.1
1. for v = 1 to n do
   visited[v] = 0 (unvisited)
2. i = 1 (Let us start at vertex 1)
3. DepthFirstSearch(i)
   begin
   visited[i] = 1
   for each vertex j adjacent to i do
   if (visited[j] = 0) then
   DepthFirstSearch(j)
   end
4. stop
```

When we need to show its equivalent non-recursive code, we need to use a stack. Non-recursive DFS can be implemented by using a stack for pushing all unvisited vertices adjacent to the one being visited and popping the stack to find the next unvisited vertex.

Consider the graph in Fig. 8.12(a) and its adjacency list in Fig. 8.12(b).

![](bbox=[0.2, 0.668, 0.85, 0.88])

Fig. 8.12 Sample graph for traversal (a) Graph G (b) Adjacency list representation of G