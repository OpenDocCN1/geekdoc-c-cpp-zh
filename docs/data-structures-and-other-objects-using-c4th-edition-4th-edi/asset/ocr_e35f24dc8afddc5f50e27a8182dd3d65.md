10. The function need only subtract 1 from the member variable many_vertices.
11. The adjacency matrix could be a two-dimensional array of unsigned integers with a[i][j] storing the number of edges from vertex i to vertex j.
12. This is an open-ended question, but your answer should consider space requirements for each representation, and time requirements for common operations.
13. One solution would call neighbors for each node. Each call to neighbors returns a set, and your function can return the sum of the sizes of all these sets. Another solution could call is_edge for each possible source and target node. The return value from this function returns the number of times that is_edge returns true.
14. At point 1, the label is 42. At point 2, the label is still 42, and the integer variable i is also 42. At point 3, the i has changed to 43, but the label is still 42. (To change the label, the change must be made to g[i] itself).
15. A traversal will loop indefinitely on a graph with a cycle if visited vertices are not marked.
16. Not always. A vertex v in a graph will not be processed by a DFS or BFS if there is no path from the start vertex to v.
17. Traversals sometimes make choices about which vertex to visit next. When we have such a choice, we will visit the vertex that is alphabetically first, giving these two orders: Depth-first: Sydney, Canberra, Adelaide, Melbourne, Hobart, Perth, Black Stump, Darwin, Brisbane. Breadth-first: Sydney, Canberra, Mel-

bourne, Adelaide, Brisbane, Hobart, Perth, Black Stump, Darwin.
18. If n is 1, then the queue needs room for only one vertex. If n is more than 1, then the queue will never have more than n-1 entries. Here is why: The start vertex is only in the queue once (by itself), and then we remove the start vertex from the queue. Each other vertex is placed in the queue at most once, so the largest queue needed would occur if all n-1 vertices are neighbors of the start vertex.
19. A depth-first search
20. The infinity symbol indicates that there is no path between two vertices. An actual algorithm would use some unused number, such as -1, for this infinity. The shortest distances algorithm gradually reduces the values in the distance array, so the largest possible value should be the initial value.
21. From among the unallowed vertices, we select the vertex with the smallest current value in the distance array. This works because the current distance array contains the correct distance values if we are permitting only allowed vertices, and the currently allowed vertices are the n-1 closest vertices. Therefore, the shortest path to the nth closest vertex must pass through only currently allowed vertices, and therefore the distance array contains the correct value for that nth closest vertex.
22. The new final distance array: (0, 2, 10, 0, 7, 4).
23. The new shortest path to vertex 3: vertex 0 to vertex 5, vertex 5 to vertex 4, vertex 4 to vertex 3.

# PROGRAMMING PROJECTS

For more in-depth projects, please see www.cs.colorado.edu/~main/projects/

+   1 Consider our graph objects from Figure 15.2 on page 748. These graphs have a maximum number of vertices, determined by the static constant graph::MAXIMUM. This constant determines the number of rows and columns of the adjacency matrix, and the size of the array for the labels. These two arrays are declared in the highlighted lines of the graph definition: