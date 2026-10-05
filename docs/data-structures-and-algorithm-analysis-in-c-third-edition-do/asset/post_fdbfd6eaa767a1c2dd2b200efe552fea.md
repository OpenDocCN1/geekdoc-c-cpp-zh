
# 10.8 Projects

**10.6** Under what conditions IS ISAM be more efficient than a B+-tree implementation?

**10.7** Prove that the number of leaf nodes in a 2-3 tree with height $k$ is between $2^k-1$ and $3^k-1$.

**10.8** Show the result of inserting the values 55 and 46 into the 2-3 tree of Figure 10.9.

**10.9** You are given a series of records whose keys are letters. The records in the following order: C, S, D, T, A, M, P, I, B, W, N, G, U, R, K, E, H, O, L. Show the 2-3 tree that results from inserting these records.

**10.10** You are a series of records whose keys are letters. The records are inserted in the following order: C, S, D, T, A, M, P, I, B, W, N, G, U, R, K, E, H, O, L. Show the tree that results from inserting these records when the 2-3 tree is modified to be $2-3^+$; that is, the internal nodes act only as placeholders. Assume the leaf nodes are capable of holding up to two records.

**10.11** Show the result of inserting the value 55 into the B-tree of Figure 10.17.

**10.12** Show the result of inserting values 1, 2, 3, 4, 5, and 6 (in order) into the $B^+$-tree of Figure 10.18.

**10.13** Show the result of deleting the values 18, 19, and 20 (in order) from the $B^+$-tree of Figure 10.24b.

**10.14** You are given a series of records whose keys are letters. The records are inserted in the following order: C, S, D, T, A, M, P, I, B, W, N, G, U, R, K, E, H, O, L. Show the $B^+$-tree of order four that results from inserting these records. Assume the leaf nodes are capable of storing up to three records.

**10.15** Assume that you have a $B^+$-tree whose internal nodes can store up to 100 children and leaf nodes can store up to 15 records. What are the minimum and maximum number of records that can be stored by the $B^+$-tree with heights 1, 2, 3, 4, and 5?

**10.16** Assume that you have a $B^+$-tree whose internal nodes can store up to 50 children and leaf nodes can store up to 50 records. What are the minimum and maximum number of records that can be stored by the $B^+$-tree with heights 1, 2, 3, 4, and 5?

# 10.8 Projects

**10.1** Implement a two-level linear index for variable-length records as illustrated by Figures 10.1 and 10.2. Assume that disk blocks are 1024 bytes in length. Records in the database file should typically range between 20 and 200 bytes, including a 4-byte value. Each record of the index file should store a key value and the byte offset in the database file for the first byte of corresponding record. The top-level index (stored in memory) should be a simple array storing the lowest key value on the corresponding block in the index file.

**10.2** Implement the 2-3+ tree, a 2-3 tree where the internal nodes act only as placeholders. Your 2-3+ should implement the dictionary interface of Section 4.4.

**10.3** Implement the dictionary ADT of Section 4.4 for a large file stored on disk by means of the B+-tree of Section 10.5. Assume that disk blocks are 1024 bytes, and thus both leaf and internal nodes are also 4-byte (int) key value and a 60-byte data field. Internal nodes should store key value/pointer pairs where the "pointer" is actually the block number on disk for the child node. Both internal nodes and leaf nodes will need room to store various information such as a count of the records stored on that node, and a pointer to the next node on that level. Thus, leaf nodes will store 15 records, and internal nodes will have room to store about 120 to 125 children depending on how you implement them. Use a buffer pool (Section 8.3) to manage access to the nodes stored on disk.

# PART IV

# Advanced Data Structures

# 11

# Graphs

Graphs provide the ultimate in data structure flexibility. Graphs can model both real-world systems and abstract problems, so they are used in hundreds of applications. Here is a small sampling of the range of problems that graphs are routinely applied to.

1. Modeling connectivity in computer and communications networks.
2. Representing a map as a set of locations with distances between locations; to compute shortest routes between locations.
3. Modeling flow capacities in transportation networks.
4. Finding a path from a starting condition to a goal condition; for example, in artificial intelligence problem solving.
5. Modeling computer algorithms, showing transitions from one state to another.
6. Finding an acceptable order for finishing subtasks in a complex activity, such as constructing large buildings.
7. Modeling relationships as family trees, business organizations, and scientific taxonomies.

We begin in 11.1 with some basic terminology and define two fundamental representations for graphs, the adjacency matrix and adjacency list. 11.2 presents a graph ADT and simple implementations based on the adjacency matrix and adjacency list. 11.3 presents the most common used traversal algorithms, depth-first and breadth-first, with application to topological sorting. 11.4 presents algorithms for solving some problems related to finding shortest routes in a graph. 11.5 presents algorithms for finding the minimum-cost spanning tree, useful for determining connectivity in a network. Besides being useful and interesting in their own right, these algorithms illustrate the use of some data structures presented in earlier chapters.

![](img/0ae21f56d7253acf0527c86ba21e16_000.png)

** 11..**** of of and terminology. (a) A graph. (b) A directed graph (digraph). (c) A labeled graph with with the edges. In this example, there is a simple path from Vertex 0 to Vertex 3 containing Vertices 0, 1, and 3. Vertices 0, 1, 2, and 4 also form a path, but not a simple path because Vertex 1 appears twice. Vertices 1, 3, 2, and 4 form a simple cycle.

# 11.1 Terminology and Representations

A graph $G = (V, E)$ consists of a set of vertices $V$ and a set of edges $E$, such that each edge $E$ in $E$ is a connection between a pair of vertices in $V$. The number of vertices is written $|V|$, and the number of edges is written $|E|$. A graph can range from zero to a maximum of $|V|^2$. A graph with relatively few edges is called **sparse**, a graph containing all possible edges with many edges is called **dense**.

A graph with edges directed from one vertex to another (as in Figure 11.1(b)) is a *directed graph* or **digraph**. A graph whose edges are not directed is an *undirected graph* (as illustrated in Figure 11.1(a)). A graph with labels associated with its edges (as in Figure 11.1(c)) is a **labeled graph**. Two vertices are **adjacent** if they are joined by an edge. Two vertices are **neighbors** when connecting Vert $U$ and $V$. Such an edge is said to be **incident** on Vert $U$ and $V$. Associated with each edge may be a cost or **weight**. Graphs with weights (as in Figure 11.1(c)) are said to be **weighted**.

A sequence of vertices $v_1, v_2, \dots v_n$ forms a path of length $n-1$ if there exists edges from $v_i$ to $v_{i+1}$ for $1 \le i < n$. A path is **simple** if all the vertices on the path are distinct. The **length** of a path is the number of edges it contains. A **cycle** is a path of length three or more that connects some vertex $v_i$ to itself. A cycle is **simple** if the path is simple, except for the first and last vertices being the same.

> Some graph applications require that a given pair of vertices can have multiple or parallel edges connecting them, or that a vertex can have an edge to itself. However, the applications discussed in this book do not require either of these special cases, for simplicity we assume they cannot occur.

Sec. 11.1 Terminology and Representations

![](img/0ae21f56d7253acf0527c86ba21e16_001.png)

**Figure 11.2** An undirected graph with three connected components. Vertices 0, 1, 2, 3, and 4 form one connected component. Vertices 5 and 6 form a second connected component. Vertex 7 by itself forms a third connected component.

A **subgraph S** is formed from graph **G** by selecting a subset $V_s$ of **G**'s vertices and a subset $E_s$ of **G**'s edges such that for every edge $E$ in $E_s$, both of $E$'s vertices are in $V_s$.

An undirected graph is **connected** if there is at least one path from any vertex to any other. The maximally connected subgraphs of an undirected graph are **connected components**. For example, Figure 11.2 shows an undirected graph with three connected components.

A graph without cycles is **acyclic**. Thus, a directed graph without cycles is a **directed acyclic graph** or DAG.

A **free tree** is a connected, undirected graph with no cycles. An equivalent definition is that a free tree has $|V| - 1$ edges.

There are two commonly used methods for representing graphs. The **adjacency matrix** is illustrated by Figure 11.3(b). The adjacency matrix for a graph is $|V| \times |V|$. Assume that $|V| = n$ and that the vertices are labeled from $v_0$ through $v_{n-1}$. Row $i$ of the adjacency matrix contains entries for Vertex $v_i$. Column $j$ in row $i$ is marked if there is an edge from $v_i$ to $v_j$, and is not marked otherwise. Thus, the adjacency matrix requires one bit at each position. Alternatively, if we wish to associate a number with each edge, as the weight or distance between two vertices, each matrix must contain such number. In this case, the space required for the adjacency matrix are $\Theta(|V|^2)$.

The second common representation for graphs is the **adjacency list**, illustrated by Figure 11.3(c). The adjacency list is an array of linked lists. The array is $|V|$ items long, with position storing a pointer to the list of edges for Vertex $v_i$. This linked list represents the edges by the vertices that are adjacent to Vertex $v_i$. The adjacency list is therefore a generalization of the “list of children” representation for trees described in Section 6.3.1.

**Example 11.1** The tree for Vertex 0 in Figure 11.3(c) stores 1 and 4 because there are two edges in the graph leaving Vertex 0, with one going
