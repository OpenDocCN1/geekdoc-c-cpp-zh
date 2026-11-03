# 16.4 GRAPH REPRESENTATION IN C

A graph can be represented as an array or as a linked list in C. Consider the following graph (Fig. 16.6):

![](bbox=[0.32, 0.26, 0.7, 0.6])

Fig. 16.6 Sample graph

Let us have a convention by which, we write:

+   - 1 if there is an edge between any two nodes, and
+   - 0 if there is no edge between any two nodes

Thus, we will have the following representation:

|   | A | B | C | D | E | F |
|---|---|---|---|---|---|---|
| A | 0 | 1 | 0 | 0 | 0 | 1 |
| B | 1 | 0 | 1 | 0 | 0 | 0 |
| C | 0 | 0 | 0 | 1 | 1 | 0 |
| D | 0 | 0 | 1 | 0 | 1 | 0 |
| E | 1 | 0 | 1 | 1 | 0 | 1 |
| F | 1 | 0 | 0 | 0 | 1 | 0 |

Fig. 16.7 Array representation of a graph

As we can see, a '1' in the first row between A-B and A-F indicates that there is an edge between A-B and A-F. All other zeroes indicate that there is no edge between the said nodes (e.g. there is no edge between nodes A-C, indicated by a '0').

A graph can also be represented in the form of a linked list. There are two types of list nodes in such a case, a header node (also called as graph node), and a list node.

+   - A header node contains the actual information of the node, a pointer to the next node, as well as a pointer to an arc.
+   - A list node contains a pointer to a node and a pointer to the next arc.