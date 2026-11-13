
Consider node 1 as the root node, it has two incident edges with 4 and 6 as their costs. The edge with minimum cost 4 is selected and used to connect 1 with 2. Node 2 has only one edge with cost 8; this is used to connect nodes 2 and 3. Node 3 also has only one edge with cost 3 and is used to connect nodes 3 and 4. Node 4 has two incident edges with 4 and 2 as their cost. Edge with cost 2 is selected to connect node 7 with 4. Node 7 has two incident edges with costs 1 and 16, the edge with cost 1 is used to connect node 5 with 7. Node 5 has only one edge with cost 3 to proceed to an unvisited node 6. So, it is used to connect 6 with 5. Now, all the nodes are connected using minimum possible edge costs resulting in a minimum cost spanning tree T of graph G_s, such that T \subseteq G is a subgraph where G=(V, E) and T=(V', E') (Figure 10.31). The time complexity of Prim's algorithm is O(n^2).

## 10.7 GRAPH ADT

- `is_empty (G)` Check whether graph G is empty
- `INSERT (G,V)` Insert vertex V into graph G
- `INSERT (G,U,V)` Insert an edge connecting vertices U and V
- `DELETE(G,V)` Delete vertex V from graph G and all the edges belonging to V
- `DELETE(G,U,V)` Delete an edge from the graph G connecting vertices u and v
- `ADD-DATA(G,V,ITEM)` Add ITEM into vertex V of graph G
- `RETRIEVE (G,V,ITEM)` Retrieve data of a vertex V in the graph G and store it in ITEM
- `BREADTH-FIRST(G)` Implements breadth first traversal of a graph G
- `DEPTH-FIRST(G)` Implement depth first traversal of a graph G

## SUMMARY

- A graph G=(V,E) consists of a set of vertices V and a set of edges E.
- A graph in which every edge is directed is called a directed graph or simply a digraph.
- A graph in which every edge has no direction (undirected) is called an undirected graph.
- Two graphs G and G_1 are said to be isomorphic, if there is a one-to-one correspondence between their vertices and between their edges.
- A circuit is called an Eulerian circuit if every edge of Graph G appears exactly once.
- Hamiltonian path in a connected graph is defined as a path that traverses each vertex of the graph exactly once.
- Hamiltonian circuit is a circuit that passes through all the vertices in a graph exactly once except the starting vertex.
- Graphs can be represented using adjacency matrix representation and incidence matrix representation.
- The primitive operations of a graph are Create a Graph, Insertion of a Vertex, Deletion of a Vertex, Insertion of an Edge, Deletion of an Edge, Search for a Vertex, Traversal of a Graph and deletion or destruction of a graph.
- Insert vertex operation is used to add a vertex to a graph.
- Delete vertex operation is used to remove a vertex from a graph.
- Insert edge operation is used to add an edge that connects a vertex to a destination vertex.
- Delete edge operation is used to remove an edge from a graph. To delete an edge the two vertices source and destination must be identified.
- Graphs can be traversed in two ways. They are Breadth first traversal and Depth first traversal.
- The applications of graphs are minimum cost spanning tree, single-source shortest path, union-find problem and connectivity of components.

## EXERCISES

### FILL IN THE BLANKS

- 1. A graph in which every edge is directed is called________.
- 2. ________ is a path that traverses each vertex of the graph exactly once.
- 3. Graphs can be represented sequentially using ________ and ________.
- 4. Linked representation is also called ________.
- 5. ________ and ________ are the traversal of graphs.

### MULTIPLE-CHOICE QUESTIONS

- 1. ________ passes through all the vertices in a graph exactly once except the starting vertex.
  - a. Eulerian circuit
  - b. Hamiltonian circuit
  - c. Cutset
  - d. None

- 2. A graph with only isolated vertices is called ________.
  - a. Null graph
  - b. Weighted graph
  - c. Finite graph
  - d. Infinite graph

- 3. A graph is said to be ________ if there is a path between every pair of distinct vertices $v_i, v_j$ in G.
  - a. Directed
  - b. Undirected
  - c. Connected
  - d. None

- 4. A path of length $\ge 1$ with no repeated edges and whose end vertices are the same is called ________.
  - a. Cycle
  - b. Length of path
  - c. Circuit
  - d. Degree

- 5. If every edge of graph G appears exactly once in the path, it is called ________.
  - a. Hamiltonian path
  - b. Eulerian path
  - c. Planarity
  - d. Cutset

### SHORT-ANSWER QUESTIONS

- 1. Define a graph.
- 2. Give the basic terminologies of a graph.
- 3. Discuss different types of graphs.
- 4. Explain the linked representation of graphs.
- 5. Write short notes on isomorphism.

### ESSAY QUESTIONS

- 1. Define graphs and explain their representation.

- 2. Find whether the following graphs G1 and G2 are isomorphic?

![](img/45784b9f0334626143002ec0d63692fd_336_0.png)

- 3. Discuss in detail about the operations of graphs.

- 4. Explain the traversal of graphs.

- 5. Write a program to implement the Prim algorithm.

## Priority Queues

The chapter defines priority queues and its abstract data type. It discusses about various implementations of priority queues in detail regarding heaps, insertions and deletions of min and max heaps. This chapter details external sorting using multiway merge and polyphase merge.

### 11.1 INTRODUCTION

Queues are FIFO structures in which the elements are deleted in the order in which they arrive in the queue. The order of insertion and deletion from a priority queue is determined by the element priority. The elements are removed in the decreasing or increasing order of priority of elements. A priority queue which is a data structure allows at least two operations: insert and delete. The operation insert inserts an element into the priority queue and the operation delete deletes an element from the priority queue based on priority. It is possible to add other operations to this data structure.

Basically, priority queues are of two types. They are:

- 1. Ascending priority queue (Min Priority Queue)
  - Removal of minimum-priority element
- 2. Descending priority queue (Max Priority Queue)
  - Removal of maximum-priority element

The specification view of priority queue is given in Figure 11.1(a). This view elides the implementation strategy of a priority queue.

![](img/45784b9f0334626143002ec0d63692fd_337_0.png)

Figure 11.1 Abstract model of a priority queue

```
Insert one item --> [List or binary search tree or binary heap] --> Get one item with highest/lowest priority
```

(b) Implementation view

Figure 11.1 Continued

The implementation view of a priority queue is given in Figure 11.1(b). In this view the implementation strategy of a priority queue is given.

Assume Pqueue is a priority queue with elements A, B, C, D whose priorities are given as 3, 2, 1, respectively.

Here the element A has the highest priority, i.e. 3. When the new element with the highest priority as 4 is to be inserted, it is added at the front of the queue. When elements with the same priority are to be inserted then the priority queue acts like a normal queue with FIFO principle.

Let task be the queue of tasks (t). Assume that 0, 1, 2 ... n are the priorities given to t tasks. Let t_i(n) be the i^th task with priority n. The implementation of priority queue to process these tasks is discussed for a set of tasks, insertion and task completion which is as follows:

- Initially task is with t_1, t_2, t_3 tasks with priorities 1,1,0, respectively.

| t1 | t2 | t3 |
|---|---|---|
| Front | | Rear |

Highest priority task t_1(1) is at the front, and the lowest priority t_3(0) is at the rear.

- The task t_4(2) with priority 2 comes, it is inserted at front

| t4 | t1 | t2 | t3 |
|---|---|---|---|
| Front | | | Rear |

- When task t_5(2) with priority 2 comes, t_4 and t_5 have the same priority; based on the FIFO property, t_5 is inserted after t_4.

| t4 | t5 | t1 | t2 | t3 |
|---|---|---|---|---|
| Front | | | | Rear |

The elements are removed in the decreasing or increasing order of priority of elements.

| t4 | t5 | t1 | t2 | t3 |
|---|---|---|---|---|
| Front | | | | Rear |

When the decreasing order of elements is considered, task t_4 with highest priority is deleted first.

| t5 | t1 | t2 | t3 |
|---|---|---|---|
| Front | | | Rear |

Task t_5 is deleted and then t_1, t_2, t_3 are deleted, respectively, based on the priority.

| t1 | t2 | t3 |
|---|---|---|
| Front | | Rear |
