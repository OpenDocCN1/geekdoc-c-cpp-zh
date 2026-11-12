
FIGURE 19-37 (a) Before; (b) and after a single left rotation that decreases the tree's height; (c) the rotation in general

![](img/288a0c22d14d2450c1e772f228f867b0_624_0.png)

FIGURE 19-38 (a) Before; (b) and after a single left rotation that does not affect the tree's height; (c) the rotation in general

![](img/288a0c22d14d2450c1e772f228f867b0_624_1.png)

subtrees of the node <40> have heights h and h + 1, respectively. After the rotation, the tree is balanced and, in this particular case, has decreased in height from h + 3 to h + 2.

Figure 19-38 shows examples of a single left rotation that restores a tree's balance but does not affect its height. An analogous single right rotation would produce mirror images of these examples.

A more complex rotation might be necessary. For example, consider the tree in Figure 19-39a, which is the result of nodes being added to or deleted from an AVL tree. The left and right subtrees of the node <40> differ in height by more than 1. A double rotation is necessary to restore this tree's balance. Figure 19-39b shows the result of a left rotation about <20>, and Figure 19-39c shows the result of a right rotation about <40>. Figure 19-39d illustrates this double rotation in a more general form. Mirror images of these figures would provide examples of other possible double rotations.

It can be proven that the height of an AVL tree with n nodes will always be very close to the theoretical minimum of ⌊log2 (n + 1)⌋. The AVL tree implementation of a dictionary is, therefore, one implementation that guarantees a binary search-like efficiency. Usually, however, implementations that use either a 2-3-4 tree or a red-black tree will be simpler.

An AVL tree implementation of a dictionary is more difficult than other implementations

FIGURE 19-39 (a) Before; (b) during; and (c) after a double rotation that decreases the tree's height; (d) the double rotation in general

![](img/288a0c22d14d2450c1e772f228f867b0_625_0.png)

## SUMMARY

- 1. A 2-3 tree and a 2-3-4 tree are variants of a binary search tree. The internal nodes of a 2-3 tree can have either two or three children. The internal nodes of a 2-3-4 tree can have either two, three, or four children. Allowing the number of children to vary permits the insertion and removal algorithms to maintain the balance of the tree easily.

- 2. The insertion and removal algorithms for a 2-3-4 tree require only a single pass from root to leaf and, thus, are more efficient than the corresponding algorithms for a 2-3 tree.

- 3. A red-black tree is a binary tree representation of a 2-3-4 tree that requires less storage than a 2-3-4 tree. Insertions and removals for a red-black tree are more efficient than the corresponding operations on a 2-3-4 tree.

- 4. An AVL tree is a binary search tree that is guaranteed to remain balanced. The insertion and removal algorithms perform rotations in the event that the tree starts to stray from a balanced shape.

## EXERCISES

- 1. Consider the following sequence of operations on an initially empty search tree:
Insert 10
Insert 100
Insert 30
Insert 80
Insert 50
Remove 10
Insert 60
Insert 70
Insert 40
Remove 80
Insert 90
Insert 20
Remove 30
Remove 70

What does the tree look like after these operations execute if the tree is

a. A Binary search tree?
b. A 2-3 tree?
c. A 2-3-4 tree?
d. A red-black tree?
e. An AVL tree?

- 2. What are the advantages of implementing the ADT dictionary with a 2-3 tree instead of a binary search tree? Why do you not, in general, maintain a completely balanced binary search tree?

- 3. Write a pseudocode function that performs a range query for a 2-3 tree. That is, the function should visit all items that are within a given range of values. For example, your function should visit all values between 100 and 1,000.

FIGURE 19-40 A 2-3 tree for Exercise 4

![](img/288a0c22d14d2450c1e772f228f867b0_627_0.png)

- 4. Given the 2-3 tree in Figure 19-40, draw the tree that results after inserting \( k, b, c, y, \) and \( w \) into the tree.

- 5. Given the 2-3 tree in Figure 19-41, draw the tree that results after removing \( t, e, k, \) and \( d \) from the tree.

- 6. Draw the 2-3-4 tree that results from inserting \( o, d, j, h, s, g, \) and \( a, \) in the order given, into a 2-3-4 tree that contains a single node whose value is \( n \).

- 7. Assume that the tree in Figure 19-5b is a 2-3-4 tree, and insert 39, 38, 37, 36, 35, 34, 33, and 32 into it. What 2-3-4 tree results?

- *8. Write pseudocode for the insertion, removal, retrieval, and traversal operations for a 2-3-4 tree.

- 9. Figure 19-32 is a red-black tree that represents the 2-3-4 tree in Figure 19-20. Draw another red-black tree that also represents the same 2-3-4 tree.

- 10. What 2-3-4 tree does the red-black tree in Figure 19-42 represent?

- 11. Write pseudocode for the insertion, removal, retrieval, and traversal operations for a red-black tree.

- 12. Write a C++ function that converts a 2-3-4 tree to a red-black tree.

FIGURE 19-41 A 2-3 tree for Exercise 5

![](img/288a0c22d14d2450c1e772f228f867b0_627_1.png)

FIGURE 19-42 A red-black tree for Exercise 10

![](img/288a0c22d14d2450c1e772f228f867b0_628_0.png)

## PROGRAMMING PROBLEMS

- 1. Implement the ADT dictionary by using a 2-3-4 tree.

- *2. Implement the ADT dictionary by using a 2-3 tree. (This implementation is more difficult than the 2-3-4 implementation.)

- 3. Implement the ADT dictionary by using a red-black tree.

- 4. Repeat Programming Problem 5 of Chapter 16 using a dictionary implemented with a balanced search tree.

## Contents

- 20.1 Terminology 604
- 20.2 Graphs as ADTs 606
- 20.2.1 Implementing Graphs 608
- 20.3 Graph Traversals 611
- 20.3.1 Depth-First Search 611
- 20.3.2 Breadth-First Search 613
- 20.4 Applications of Graphs 615
- 20.4.1 Topological Sorting 615
- 20.4.2 Spanning Trees 618
- 20.4.3 Minimum Spanning Trees 621
- 20.4.4 Shortest Paths 624
- 20.4.5 Circuits 627
- 20.4.6 Some Difficult Problems 629
- Summary 631
- Exercises 632
- Programming Problems 635

## Prerequisites

- Chapter 5 Recursion as a Problem-Solving Technique
- Chapter 6 Stacks
- Chapter 15 Trees

Graphs are an important mathematical concept with significant applications not only in computer science, but also in many other fields. You can view a graph as a mathematical construct, a data structure, or an abstract data type. This chapter provides an introduction to graphs that allows you to view a graph in any of these three ways. It also presents the major operations and applications of graphs that are relevant to the computer scientist.

## 20.1 Terminology

You are undoubtedly familiar with graphs: Line graphs, bar graphs, and pie charts are in common use. The simple line graph in Figure 20-1 is an example of the type of graph that this chapter considers: a set of points that are joined by lines. Clearly, graphs provide a way to illustrate data. However, graphs also represent the relationships among data items, and it is this feature of graphs that is important here.

A graph G consists of two sets: a set V of vertices, or nodes, and a set E of edges that connect the vertices. For example, the campus map in Figure 20-2a is a graph whose vertices represent buildings and whose edges represent the sidewalks between the buildings. This definition of a graph is more general than the definition of a line graph. In fact, a line graph, with its points and lines, is a special case of the general definition of a graph.

FIGURE 20-1 An ordinary line graph

![](img/288a0c22d14d2450c1e772f228f867b0_630_0.png)

FIGURE 20-2 (a) A campus map as a graph; (b) a subgraph

![](img/288a0c22d14d2450c1e772f228f867b0_630_1.png)

A subgraph consists of a subset of a graph's vertices and a subset of its edges. Figure 20-2b shows a subgraph of the graph in Figure 20-2a. Two vertices of a graph are adjacent if they are joined by an edge. In Figure 20-2b, the Library and Student Union are adjacent. A path between two vertices is a sequence of edges that begins at one vertex and ends at another vertex. For example, there is a path in Figure 20-2a that begins at the Dormitory, leads first to the Library, then to the Student

- G = (V, E); that is, a graph is a set of vertices and edges
- Adjacent vertices are joined by an edge
- A path between two vertices is a sequence of edges
