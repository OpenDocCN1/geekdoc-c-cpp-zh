# Chapter 10 Trees 255

The algorithm starts initializing the variable node to the root node. It also initializes the variable via_branch to True to indicate that the algorithm goes to the current node via a branch. Treating the root node in this way makes the algorithm move to the leftmost node in the next step.

The algorithm then enters a loop that continues until the variable node drops off at the end of the traversal.

If the algorithm goes to the current node via a branch, it should not necessarily process node just. If that node has a left branch, the nodes that have subtree values smaller than the current node, the algorithm must consider them first. To do that, the algorithm moves as far down the left branches as possible. (In Figure 10-12, this occurs when the algorithm moves from node 6 to node 9). The algorithm must first move down to node 7 before it processes node 9.

Next, the algorithm processes the current node.

If the node has no right branch, the algorithm follows the node's right thread. If the right thread is null, the node is set to null, and the While loop ends. The algorithm sets via_branch to False to indicate that it got to the new node via a thread, (In Figure 10-12, this happens several times, such as when the algorithm moves from node 4 to node 5. Because via_branch is False, the algorithm will process node 5.

If the current node's right branch is not null, the algorithm follows it and sets via_branch to True so that it moves down the node's subtree during the next trip through the While loop.

The following list describes the steps taken by this algorithm to traverse the tree in Figure 10-12:

+   1. Start at the root, and set via_branch to True.
2. Variable via_branch is True, so follow the left branches to 2 and then 1. Process node 1.
3. Follow the right thread to 2, and set via_branch to False.
4. Variable via_branch is False, so process node 2.
5. Follow the right branch to 4, and set via_branch to True.
6. Variable via_branch is True, so try to move down the left branches. There is no left branch here, stay at node 4 and process node 4.
7. Follow the right thread to 5, and set via_branch to False.
8. Variable via_branch is False, so process node 5.
9. Follow the right branch to 6, and set via_branch to True. There is no left branch here, stay at node 6 and process node 6.
11. Follow the right branch to 9, and set via_branch to True.