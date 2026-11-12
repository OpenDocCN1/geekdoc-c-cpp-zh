
Question 6 Draw the DFS spanning tree whose root is vertex 0 for the graph in Figure 20-33.

Question 7 Draw the minimum spanning tree whose root is vertex 0 for the graph in Figure 20-33.

Question 8 What are the shortest paths from vertex 0 to each vertex of the graph in Figure 20-24a? (Note the weights of these paths in Figure 20-25.)

### FIGURE 20-32 Graphs for Checkpoint Questions 1, 2, and 3

![](img/288a0c22d14d2450c1e772f228f867b0_657_0.png)

### FIGURE 20-33 A graph for Checkpoint Questions 6 and 7 and for Exercises 1 and 4

![](img/288a0c22d14d2450c1e772f228f867b0_657_1.png)

## SUMMARY

- 1. The two most common implementations of a graph are the adjacency matrix and the adjacency list. Each has its relative advantages and disadvantages. The choice should depend on the needs of the given application.

- 2. Graph searching is an important application of stacks and queues. Depth-first search (DFS) is a graph-traversal algorithm that uses a stack to keep track of the sequence of visited vertices. It goes as deep into the graph as it can before backtracking. Breadth-first search (BFS) uses a queue to keep track of the sequence of visited vertices. It visits all possible adjacent vertices before traversing further into the graph.

- 3. Topological sorting produces a linear order of the vertices in a directed graph without cycles. Vertex x precedes vertex y if there is a directed edge from x to y in the graph.

- 4. Trees are connected undirected graphs without cycles. A spanning tree of a connected undirected graph is a subgraph that contains all of the graph's vertices and enough of its edges to form a tree. DFS and BFS traversals produce DFS and BFS spanning trees.

- 5. A minimum spanning tree for a weighted undirected graph is a spanning tree whose edge-weight sum is minimal. Although a particular graph can have several minimum spanning trees, their edge-weight sums will be the same.

- 6. The shortest path between two vertices in a weighted directed graph is the path that has the smallest sum of its edge weights.

- 7. An Euler circuit in an undirected graph is a cycle that begins at vertex v, passes through every edge in the graph exactly once, and terminates at v.

- 8. A Hamilton circuit in an undirected graph is a cycle that begins at vertex v, passes through every vertex in the graph exactly once, and terminates at v.

## EXERCISES

When given a choice of vertices to visit, the traversals in the following exercises should visit vertices in sorted order.

- 1. Give the adjacency matrix and adjacency list for
  - a. The weighted graph in Figure 20-33
  - b. The directed graph in Figure 20-34

- 2. Show that the adjacency list in Figure 20-8b requires less memory than the adjacency matrix in Figure 20-6b.

- 3. Consider Figure 20-35 and answer the following:
  - a. Will the adjacency matrix be symmetrical?
  - b. Provide the adjacency matrix.
  - c. Provide the adjacency list.

- 4. Use both the depth-first strategy and the breadth-first strategy to traverse the graph in Figure 20-33, beginning with vertex 0, and the graph in Figure 20-36, beginning with vertex a. List the vertices in the order in which each traversal visits them.

- 5. By modifying the DFS traversal algorithm, write pseudocode for an algorithm that determines whether a graph contains a cycle.

- 6. Using the topological sorting algorithm topSort1, as given in this chapter, write the topological order of the vertices for each graph in Figure 20-37.

- 7. Trace the DFS topological sorting algorithm topSort2, and indicate the resulting topological order of the vertices for each graph in Figure 20-37.

- 8. Revise the topological sorting algorithm topSort1 by removing predecessors instead of successors. Trace the new algorithm for each graph in Figure 20-37.

- 9. Trace the DFS and BFS spanning tree algorithms, beginning with vertex a of the graph in Figure 20-11, and show that the spanning trees are the trees in Figures 20-20 and 20-21, respectively.

### FIGURE 20-34 A graph for Exercise 1

![](img/288a0c22d14d2450c1e772f228f867b0_658_0.png)

### FIGURE 20-35 A graph for Exercise 3

![](img/288a0c22d14d2450c1e772f228f867b0_659_0.png)

### FIGURE 20-36 A graph for Exercises 4 and 10

![](img/288a0c22d14d2450c1e772f228f867b0_659_1.png)

- 10. Draw the DFS and BFS spanning trees rooted at $a$ for the graph in Figure 20-36. Then draw the minimum spanning tree rooted at $a$ for this graph.

- 11. For the graph in Figure 20-38,
  - a. Draw all the possible spanning trees.
  - b. Draw the minimum spanning tree.

- 12. Write pseudocode for an iterative algorithm that determines a DFS spanning tree for an undirected graph. Base your algorithm on the traversal algorithm dfs.

- 13. Draw the minimum spanning tree for the graph in Figure 20-22 when you start with
  - a. Vertex g
  - b. Vertex c

- *14. Trace the shortest-path algorithm for the graph in Figure 20-39, letting vertex 0 be the origin.

- *15. Implement the shortest-path algorithm in C++. How can you modify this algorithm so that any vertex can be the origin?

### FIGURE 20-37 Graphs for Exercises 6, 7, and 8

![](img/288a0c22d14d2450c1e772f228f867b0_660_0.png)

### FIGURE 20-38 A graph for Exercise 11

![](img/288a0c22d14d2450c1e772f228f867b0_660_1.png)

### FIGURE 20-39 A graph for Exercise 14

![](img/288a0c22d14d2450c1e772f228f867b0_660_2.png)

- *16. Determine an Euler circuit for the graph in Figure 20-40. Why is one possible?

- *17. Prove that a connected undirected graph with n vertices and more than n - 1 edges must contain at least one simple cycle. (See observation 3 in Section 20.4.2.)

- *18. Prove that a graph-traversal algorithm visits every vertex in the graph if and only if the graph is connected, regardless of where the traversal starts.

- *19. Although the DFS traversal algorithm has a simple recursive form, a recursive BFS traversal algorithm is not straightforward.
  - a. Explain why this statement is true.
  - b. Write the pseudocode for a recursive version of the BFS traversal algorithm.

- *20. Prove that the loop invariant of Dijkstra's shortest-path algorithm is true by using a proof by induction on step.

### FIGURE 20-40 A graph for Exercise 16

![](img/288a0c22d14d2450c1e772f228f867b0_661_0.png)

## PROGRAMMING PROBLEMS

- 1. Write a C++ class derived from GraphInterface, as given in Listing 20-1. Use an adjacency matrix to represent the graph.

- 2. Repeat the previous programming problem, but represent the graph using an adjacency list instead of an adjacency matrix.

- 3. Repeat Programming Problems 1 and 2, but allow the graph to be either weighted or unweighted and either directed or undirected.

- 4. Extend Programming Problem 3 by adding ADT operations such as isConnected and hasCycle. Also, include operations that perform a topological sort for a directed graph without cycles, determine the DFS and BFS spanning trees for a connected graph, and determine a minimum spanning tree for a connected undirected graph.

- 5. The HPAir problem was the subject of Programming Problems 11 through 14 of Chapter 6. Revise these problems by implementing the ADT flight map as a derived class of the graph class that you wrote for Programming Problem 3.

*This page intentionally left blank*

## Processing Data in External Storage
Chapter 21

## Contents

- 21.1 A Look at External Storage 638
- 21.2 Sorting Data in an External File 640
- 21.3 External Dictionaries 646
  - 21.3.1 Indexing an External File 648
  - 21.3.2 External Hashing 651
  - 21.3.3 B-Trees 654
  - 21.3.4 Traversals 662
  - 21.3.5 Multiple Indexing 664
- Summary 665
- Exercises 666
- Programming Problems 669

## Prerequisites

- Appendix G Files
- Chapter 11 Sorting algorithms and Their Efficiency
- Chapter 18 Dictionaries and Their Implementations
- Chapter 19 Balanced Search Trees

All of the previous dictionary implementations assume that the data items reside in the computer's internal memory. Many real-world applications, however, require a dictionary so large that it greatly exceeds the amount of available internal memory. In such situations, you must store the dictionary on an external storage device such as a disk and perform dictionary operations there.

This chapter considers the problem of data management in an external environment by using a direct access file as a model of external storage. In particular, this chapter discusses how to sort the data in an external file by modifying the merge sort algorithm and how to search an external file by using generalizations of the hashing and search-tree schemes developed previously.
