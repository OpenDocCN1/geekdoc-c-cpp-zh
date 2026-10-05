# Chapter 3 ■ Linked Lists 71

links visit the planets ordered by distance to the sun, the dashed links visit the planets ordered by mass, and the thick links visit the planets ordered by diameter.

![](bbox=[0.198, 0.163, 0.839, 0.368])

Figure 3-8: Visualizing all the threads through a multithreaded linked list can be confusing.

> NOTE Other data structures also can have threads. For example, a tree might provide threads to let a program visit its nodes in orders that are not typical for a tree.

# Linked Lists with Loops

A circular linked list is a linked list in which the last link points back to the first item in the list. Figure 3-9 shows a circular linked list.

![](bbox=[0.181, 0.696, 0.383, 0.893])

Figure 3-9: Circular linked lists let a program easily loop through a sequence of objects indefinitely.