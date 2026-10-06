0 1 0 0 1 0
1 0 1 1 0 0
0 1 0 1 1 0
0 1 1 0 1 0
1 0 0 0 1 1
0 0 0 1 1 0

2. An adjacency list: Each vertex $v_i$ has an attached list of all vertices connected to it. In an undirected graph, each edge $e_{i,j}$ will have $v_j$ appear in $v_i$'s list and $v_i$ appear in $v_j$'s list. This is a duplication of information, but eliminating the duplication would make algorithms more complicated and would only halve the length of the representation of $|G|$. As elsewhere in the book, two encodings (or two algorithms) whose length only differs by a constant factor will be considered essentially the same size.

Size of encoding: $|V| + 2|E|$ (each edge appears twice, but only one end is in the list at each appearance).

Example: $G_1$ stored as adjacency lists:

+   1: 2, 6
2: 1, 3, 4
3: 2, 5
4: 2, 5
5: 3, 4, 6, 7
6: 1, 5, 7
7: 5, 6

3. A count of the vertices ($n$) followed by a list of the edges. Here, n would not be necessary if every vertex was connected to something, but that is not necessarily the case. In this representation:

Size of encoding: $|G| = 1 + 2|E|$ (each edge appears once, but with two vertices).

Example: See the edge list for $G_1$ in Figure 9.2.