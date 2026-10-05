# 334 Chapter 13 = Basic Network Algorithms

With some work, you can figure out how the nodes were added to the traversal. The algorithm started with the node labeled 0. It then added the nodes 1, 2, and 3 to its stack.

Because node 3 was added to the stack last, it was processed next, and the algorithm added nodes 4 and 5 to the stack. Because node 5 was added last, the algorithm processed it and added nodes 6, 7, 8, and 9 to the stack.

If you like, you can continue studying Figure 13-3 to figure out why the algorithm visited the nodes in the order it. But at this point you should be able to see some nodes far from the start node are processed before some of the nodes closer to the start node.

# Breadth-first Traversal

In some algorithms, it is convenient to traverse nodes closer to the start node before the nodes that are farther away. The previous algorithm visited some nodes far from the start node before it visited some closer nodes because it used a stack to process the nodes. If you use a queue instead of a stack, the nodes are processed in first-in-first-order, and the nodes closer to the start node are processed first.

Because this algorithm visits all of a node's neighbors before it visits any other nodes, this is called a breadth-first search. Figure 13-4 shows a breadth-first traversal with the nodes labeled according to the order in which they were traversed.

![](bbox=[0.137, 0.558, 0.568, 0.853])

Figure 13-4: In a breadth-first traversal, nodes close to the starting node are visited before those that are farther away.