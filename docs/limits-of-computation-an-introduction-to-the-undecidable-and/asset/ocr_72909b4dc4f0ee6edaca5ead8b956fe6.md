# More NP-Complete Problems ■ 201

# Problem

+   - Given a graph G, does G have a three-coloring?
- Given a graph G and an integer k, does G have a k-coloring?

# Definition 9.13

The degree of a vertex v in V is the number of edges connected to v. (See the Exercises at the end of the chapter for some problems using vertex degree.)

The proofs that these problems are NP-complete vary from easy to difficult. Also interesting is that some similar problems are not NP-complete. For example, there is a simple polynomial algorithm to determine whether a graph G has a two-coloring.

# 9.6 HAMILTONIAN CIRCUIT (HC)

Hamiltonian circuits (and the related traveling salesman problems) are old and interesting graph problems. Recall that HC asks if one can start at some vertex, visit all the other vertices in the graph, and return to the starting place? For many graphs, the answer is clearly no. There can be no Hamiltonian circuit if there are isolated vertices, or if there are any vertices with only one edge, for example. For small graphs, it is easy to check by inspection whether or is not there a Hamiltonian circuit. For example, in Figure 9.9, the graph on the left is an instance; the graph on the right is no instance.

The HC problem is the decision problem: Given a graph G = (V, E), does G have a Hamiltonian circuit?

![](bbox=[0.238, 0.712, 0.735, 0.873])

FIGURE 9.9 Yes-instance and No-instance of HC.