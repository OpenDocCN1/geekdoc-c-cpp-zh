# FIGURE 16-5 Traversing (a) the left subtree (steps 9 and 10 in Figure 16-4) and (b) the right subtree of 20

![](bbox=[0.065, 0.145, 0.85, 0.475])

Thus, two facts emerge from the recursive version of `inorder` when a return is made from a recursive call:

+   - The implicit recursive stack of pointers is used to find the node p that the traversal must go back to.
+   - Once the traversal backs up to node p, it either visits p (for example, displays its data) or backs farther up the tree. It visits p if p’s left subtree has just been traversed; it backs up if its right subtree has just been traversed. The appropriate action is taken simply as a consequence of the point—1 or 2—to which control is returned.

> Actions upon a return from a recursive call to inorder

You could directly mimic this action by using an iterative method and an explicit stack, as long as some bookkeeping device kept track of which subtree of a node had just been traversed. However, you can use the following observation both to eliminate the need for the bookkeeping device and to speed up the traversal somewhat. Consider the tree in Figure 16-6. After you have finished traversing the subtree rooted at node R, there is no need to return to nodes C and B, because the right subtrees of these nodes have already been traversed. You can instead return directly to node A, which is the nearest ancestor of R whose right subtree has not yet been traversed.

This strategy of not returning to a node after its right subtree has been traversed is simple to implement: You place a pointer to a node in the stack only before the node’s left subtree is traversed, but not before its right subtree is traversed. Thus, in Figure 16-6, when you are at node R, the stack contains A and R, with R on top. Nodes B and C are not in the stack, because you have visited them already and are currently traversing their right subtrees. On the other hand, A is in the stack because you are currently traversing its left subtree. When you return from node R, nodes B and C are thus bypassed because you have finished with their right subtrees and do not need to return to these nodes. Thus, you pop R’s pointer from the stack and go directly to node A, whose left subtree has just been traversed. You then visit A, pop its pointer from the stack, and traverse A’s right subtree.