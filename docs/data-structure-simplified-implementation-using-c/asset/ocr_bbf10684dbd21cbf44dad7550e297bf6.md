directed graph. Adjacency list of the directed graph as illustrated in the figure 13.2 has been illustrated in the following figure 13.6

![](bbox=[0.2, 0.15, 0.88, 0.44])

Figure 13-6: Adjacency list of figure 13.1

![](bbox=[0.2, 0.45, 0.88, 0.67])

Figure 13-5: Adjacency list for the directed graph of figure 13.2

In the adjacency list, vertex ‘b’ and’d’ does not have any adjacency list consequently, they will point to the NULL.

# 13.3.3 Incidence matrix

Consider the graph ‘G’ with “n” vertices and “ne” edges but does not have any self-loop. Consider the matrix A= (a_ij) with n x ne, where n is the number of vertices and ne is the number of edges as follows.

A_ij=1 if “e_j” is incident to the vertex “v_i”
=0, otherwise

Such a matrix is known as the incidence matrix of a graph. In other terms incidence matrix