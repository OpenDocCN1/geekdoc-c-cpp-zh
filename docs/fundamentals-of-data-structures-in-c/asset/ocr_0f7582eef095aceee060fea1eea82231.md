```
Enter the value of 2, 4 element : 1
Enter the value of 2, 5 element : 0
Enter the value of 3, 1 element : 0
Enter the value of 3, 2 element : 0
Enter the value of 3, 4 element : 0
Enter the value of 3, 5 element : 1
Enter the value of 4, 1 element : 0
Enter the value of 4, 2 element : 0
Enter the value of 4, 3 element : 1
Enter the value of 4, 5 element : 1
Enter the value of 5, 1 element : 1
Enter the value of 5, 2 element : 0
Enter the value of 5, 3 element : 0
Enter the value of 5, 4 element : 0
Nodes are visited in this order -> 1 -> 2 -> 3 -> 5 -> 4
```

# ## 4.10.2 Breadth-First Traversal

The breadth-first traversal technique begins at a given vertex and then proceeds to all the vertices connected to that vertex. Visit the first node initially, and then find all the unvisited nodes which is adjacent to the first node. Then unvisited nodes are visited and a breadth first search is initiated from the adjacent node (considering it as the first node). This traversal continues until all nodes have been visited once. The following algorithm describes BFS in a graph.

+   - Step 1: Consider any vertex in the graph. Process the vertex and mark it as visited.
+   - Step 2: Using the adjacency matrix of the graph proceed to the next vertex which has an edge connection wise the vertex considered in Step 1 .
+   - Step 3: Backtrack to the vertex considered in Step 1 descend along an edge towards an unvisited vertex and mark the new vertex as visited.
+   - Step 4: Repeat Step 3 until all vertices adjacent to the node in Step 1 have been marked as visited.
+   - Step 5: Repeat Step 1 to Step 4 starting from vertex visited in Step 2, then start again from vertices visited in Step 3 in the order visited.

The above algorithm executes in a recursive manner, which can also be implemented non-recursively using queues. To understand the traversal clearly, consider the graph shown in Fig. 4.33(c) and its adjacency matrix shown in Fig. 4.37(c). Program 4.7 helps you to understand things better.