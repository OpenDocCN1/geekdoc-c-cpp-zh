
They should only be available to users who have the rights for creating rooms. The last two can be written as recursive algorithms that run from room to room following the exits that connect them.

- 2. A good recursive problem for the web spider is to determine how many clicks it takes to get from one page to another. Closely related to that, you can measure distances, in clicks, between different data elements in a data set.

- 3. Recursion can be used for a number of different tasks in graphical games. Which you pick really depends on what your game is like. All are at least roughly related to the maze algorithm. If your game has multiple screens that are connected (picture classic Zelda) it could be useful to have a tool that tells you how different screens are connected.
If your game has computer-controlled characters and obstacles that can block movement, then a recursive algorithm can be used to find a route from the character to the player. Note that in general, you do not want to allow an Artificial Intelligence (AI) to follow the shortest route to the player. The reason being that it becomes impossible for the player to evade the enemy.

- 4. If you are doing the math worksheet project, you should add the ability for the user to define functions with names. Then make it so that the definition of one function can include a call to another function. This will use recursion in your code. You do not have to go all the way of including conditionals in the functions so that the functions themselves can be recursive. You are certainly allowed to try, but that is functionality that you will be able to add in later.

- 5. Every good paint program needs a flood fill option. Your Photoshop® project is no exception. Flood fill can be written in a very compact form using recursion. You should implement this and try it. What you will find if you have a large image is that you can easily overflow the stack by clicking in an open area.
To avoid this, you have to switch from using recursion to using a loop with a manual stack or queue for keeping track of things. If you use a stack, the order of the fill will match what happens in recursion. If you use a queue, you get a breadth-first ordering instead. For this application, the difference will not be significant.

- 6. In chapter 26 you added a collisional simulation to the simulation workbench using a priority queue. That code has two different aspects that force every step to take $O(n^2)$ time, the comparison of particles to determine collision times, and the inserting of items into a sorted linked list priority queue. We will look at one way to improve on the first of these.
Currently your code finds collisions by doing comparisons between every pair of particles in the simulation. In reality, collisions are localized. During the fairly short period of time represented by a timestep in the simulation, it generally is not possible for a particle to collide with other particles on the opposite side of the simulation area. Technically, you can only collide with particles where $d < \Delta t|\vec{v}_{1} - \vec{v}_{2}|$, where $d$ is the distance between the particles, $\Delta t$ is the length of the timestep, and $\vec{v}_{1}$ and $\vec{v}_{2}$ are the velocities of the two particles. For this reason, you really only need to compare to things that are close by. The problem is, you do not know in advance what is close by. One way to deal with this is to maintain in each particle knowledge of its nearest neighbors. Have each particle keep track of the closest $m$ other particles. The value of $m$ should probably be at least four for a 2-D simulation and six to eight for a

3-D simulation. Building those connections initially requires a full search and O(n²) checks. After it has been built, searches for particles to do collision checks against can be done with a recursive search running through the connections. The search can stop anytime it gets to a particle that is too far away.

This same method can also be used to maintain the closest m particles. If the recursive search ever hits a particle that is closer than one of the one currently being tracked, the new one can replace it. Every so often another O(n²) search can be done to make sure the connections are all good, but this allows most of the steps to be done with each particle compared to a significant smaller number of other particles.

## Chapter 29
## Trees
29.1 General Trees ......................................................... 735
29.1.1 Implementations ....................................................... 736
29.1.2 Traversals ............................................................. 737
29.2 Project Integration: Formula Parsing ......................................... 740
29.2.1 Formula Tree Traversals and In-order Traversal ........................... 744
29.3 Binary Search Trees: Binary Trees as Maps .................................... 745
29.3.1 Order Analysis ....................................................... 751
29.3.2 Immutable BSTs ....................................................... 752
29.4 End of Chapter Material ................................................... 755
29.4.1 Summary of Concepts ................................................... 755
29.4.2 Exercises .............................................................. 756
29.4.3 Projects ............................................................... 757

> "I think that I shall never see
> A poem as lovely as a tree." - Joyce Kilmer

In this chapter you will learn about the concept of a tree as they are known in Computer Science. While we will not be writing poems about them, we will construct some lovely code to provide efficient implementations of some Abstract Data Type (ADT).

### 29.1 General Trees

Chapter 25 introduced the concept of the linked structure using the simplest form of a linked list. The most general expression of a linked structure is the graph that was briefly presented in chapter 28. A tree is a linked structure that falls somewhere between these two extremes. Like the other two, a tree is formed of nodes with edges between them. We consider these edges to have a direction, pointing from one node to another. Unlike a graph, where we can do pretty much anything we want with with the edges between the nodes, to qualify as a tree, there are certain limitations. We will run through these and introduce the basic terminology, which is largely a mixture of metaphors from biology and genealogy.

A tree can include any number of nodes. One node is the ROOT of the tree. Consider that you have a node C and another node P such that there is an edge from P to C. See figure 29.1 for an example. We call P the PARENT of C and C is the CHILD of P. To qualify as a tree, every node has one incoming edge except the root, which has zero. As a result, there is one and only one path from the root to any given node. Other nodes that have an edge going from P to them are the SIBLINGS of C. Going further with the genealogy metaphor, the nodes can can be reached going down edges from a node are called the DESCENDANTS of that node. Similarly, the nodes that are on the path from a node to the root, including the root, are the ANCESTORS of the node.

![](img/157fcf510c119278e4b1267c62717fa8_771_0.png)

FIGURE 29.1: This figure shows a sample tree with some of the nodes labeled. Node P is the parent of nodes C, D, and E. D and E are siblings of C. Node P has a depth of 1 and a height of 2, while node C has a depth of 2 and a height of 1. The size of node P is six, while the size of node C is 2.

Following the biology metaphor, any node that does not have outgoing edges is called a LEAF. The number of edges between the root and a node is called the DEPTH of the node. The number of edges between a node and the deepest leaf is called the HEIGHT of that node. The term SIZE refers to the number of descendants of a node, plus itself.

We can also define a tree in a recursive way. Using this definition, a tree is either an empty node or a node with edges to zero or more non-empty subtrees under it. This definition will be directly reflected in some of the implementations.

Note that for all these definitions, when you draw out a tree, there are no loops of any kind. This is probably the key image to have in your mind when you think about trees, they do not allow loops. You should also note from this description that a linked list is actually a perfectly happy tree. The root of the tree is equivalent to the head of the list, and each node has only one outgoing edge to a child. It might be a boring tree, but the standard, singly-linked list definitely qualifies as a tree.

### 29.1.1 Implementations

A general tree allows each node to have an arbitrary number of children. This leads to a number of different implementation strategies. One approach is to have the node store whatever data is needed along with a sequence of children. Our Drawable type defines a node in a tree and we used this approach. Recall that Drawable actually inherits from javax.swing.tree.TreeNode. This was done so that we could use it with the javax.swing.JTree in our Graphical User Interface (GUI). In that tree, the internal nodes are all of the DrawTransform type while the leaves extend DrawLeaf. The DrawTransform contains the following line of code.

```
private val subnodes = mutable.Buffer[Drawable]()
```
