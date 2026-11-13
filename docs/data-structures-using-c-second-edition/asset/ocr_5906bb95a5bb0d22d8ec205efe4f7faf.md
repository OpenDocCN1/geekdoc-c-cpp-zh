```
front=0;
 queue[++rear] = node ;
}
}
int delete_queue()
{
 int del_node;
 if (front == -1 || front > rear)
 {
 printf("\n UNDERFLOW ");
 return ;
 }
 else
 {
 del_node = queue[front++];
 return del_node;
 }
}
int find_indegree(int node)
{
 int i,in_deg = 0;
 for(I = 1; I <= n; I++)
 {
 if( adj[I][node] == 1 )
 in_deg++;
 }
 return in_deg;
}
```

Output
Enter number of vertices: 7
Enter edge 1(0 to quit): 1 2
Enter edge 2(0 to quit): 2 3
Enter edge 3(0 to quit): 2 5
Enter edge 4(0 to quit): 2 4
Enter edge 5(0 to quit): 3 5
Enter edge 6(0 to quit): 4 5
Enter edge 7(0 to quit): 5 6
Enter edge 8(0 to quit): 7 4
The topological sorting can be given as:
1 7 2 3 4 5 6

# 13.8 SHORTEST PATH ALGORITHMS

In this section, we will discuss three different algorithms to calculate the shortest path between the vertices of a graph 6. These algorithms include:

+   - Minimum spanning tree
+   - Dijkstra's algorithm
+   - Warshall's algorithm

While the first two use an adjacency list to find the shortest path, Warshall's algorithm uses an adjacency matrix to do the same.

# 13.8.1 Minimum Spanning Trees

A spanning tree of a connected, undirected graph G is a sub-graph of G which is a tree that connects all the vertices together. A graph G can have many different spanning trees. We can assign weights to each edge (which is a number that represents how unfavourable the edge is), and use it to assign a weight to a spanning tree by calculating the sum of the weights of the edges in that spanning