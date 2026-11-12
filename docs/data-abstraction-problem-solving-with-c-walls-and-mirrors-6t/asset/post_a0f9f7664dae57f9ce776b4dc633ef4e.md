
### FIGURE 16-3 Adding nodes to an initially empty binary tree

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_492_0.png)

the pointer treePtr, which, due to the recursive calls, eventually points to every node in the tree. The definition of inorder follows:

### Protected methods that enable recursive traversals

```
template<class ItemType>
void BinaryNodeTree<ItemType>::
inorder(void visit(ItemType&), BinaryNode<ItemType>* treePtr) const
{
if (treePtr != nullptr)
{
   inorder(visit, treePtr->getLeftChildPtr());
   ItemType theItem = treePtr->getItem();
   visit(theItem);
   inorder(visit, treePtr->getRightChildPtr());
} // end if
} // end inorder
```

Now the definition of the public method inorderTraverse contains only the call

```
inorder(visit, rootPtr);
```

The other traversals have similar definitions.

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_493_0.png)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_493_1.png)

Nonrecursive traversal (optional). Before leaving the topic of traversals, let's develop a nonrecursive traversal algorithm to illustrate further the relationship between stacks and recursion that was discussed in Chapter 6. In particular, we will develop a nonrecursive inorder traversal for the link-based implementation of a binary tree.

The conceptually difficult part of a nonrecursive traversal is determining where to go next after a particular node has been visited. To gain some insight into this problem, consider how the recursive inorder method works:

```
if (treePtr != nullptr)
{
   inorder(visit, treePtr->getLeftChildPtr()); // Point 1
   ItemType theItem = treePtr->getItem();
   visit(theItem);
   inorder(visit, treePtr->getRightChildPtr()); // Point 2
} // end if
```

### Recursive calls from points 1 and 2

The method has its recursive calls marked as points 1 and 2.

During the course of the method's execution, the value of the pointer treePtr actually marks the current position in the tree. Each time inorder makes a recursive call, the traversal moves to another node. In terms of the stack that is implicit to recursive methods, a call to inorder pushes the new

### FIGURE 16-4 Contents of the implicit stack as treePtr progresses through a given tree during a recursive inorder traversal

(The notation →60 means “a pointer to the node containing 60.”)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_494_0.png)

### Recursive inorder's implicit stack gives insight into a nonrecursive traversal

value of treePtr—that is, a pointer to the new current node—onto the stack. At any given time, the stack contains pointers to the nodes along the path from the tree's root to the current node n, with the pointer to n at the top of the stack and the pointer to the root at the bottom. Note that n is possibly “empty”—that is, it may be indicated by a nullPtr value for treePtr at the top of the stack. Such an occurrence corresponds to the base case of the recursion.

Figure 16-4 partially traces the execution of inorder and shows the contents of the implicit stack. The first four steps of the trace show as treePtr points first to 60, then to 20, then to 10, and then becomes nullPtr. The recursive calls for these four steps are from point 1 in inorder.

Now consider what happens when inorder returns from a recursive call. The traversal retraces its steps by backing up the tree from a node n to its parent p, from which the recursive call to n was made. Thus, the pointer to n is popped from the stack and the pointer to p comes to the top of the stack, as occurs in step 5 of the trace in Figure 16-4. In this case, n happens to be empty, so nullPtr is popped from the stack.

What happens next depends on which subtree of p has just been traversed. If you have just finished traversing p's left subtree—that is, if n is the left child of p and thus the return is made to point 1 in inorder—control is returned to the statement that visits node p. Such is the case for steps 6 and 10 of the trace in Figure 16-4. Figure 16-5a illustrates steps 9 and 10 in more detail.

After node p has been visited, a recursive call is made from point 2 and the right subtree of p is traversed. However, if, as Figure 16-5b illustrates, you have just traversed p's right subtree—that is, if n is the right child of p and thus the return is made to point 2—control is returned to the end of the method. As a consequence another return is made, the pointer to p is popped off the stack, and you go back up the tree to p's parent, from which the recursive call to p was made. In this latter case, node p is not visited—it was visited before the recursive call to n was made from point 2.

### FIGURE 16-5 Traversing (a) the left subtree (steps 9 and 10 in Figure 16-4) and (b) the right subtree of 20

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_495_0.png)

Left subtree of 20 has been traversed. Pop the reference to 10 from the stack, visit 20.

Right subtree of 20 has been traversed. Pop the reference to 40 from stack.

Thus, two facts emerge from the recursive version of `inorder` when a return is made from a recursive call:

- The implicit recursive stack of pointers is used to find the node p that the traversal must go back to.
- Once the traversal backs up to node p, it either visits p (for example, displays its data) or backs farther up the tree. It visits p if p's left subtree has just been traversed; it backs up if its right subtree has just been traversed. The appropriate action is taken simply as a consequence of the point—1 or 2—to which control is returned.

### Actions upon a return from a recursive call to `inorder`

You could directly mimic this action by using an iterative method and an explicit stack, as long as some bookkeeping device kept track of which subtree of a node had just been traversed. However, you can use the following observation both to eliminate the need for the bookkeeping device and to speed up the traversal somewhat. Consider the tree in Figure 16-6. After you have finished traversing the subtree rooted at node R, there is no need to return to nodes C and B, because the right subtrees of these nodes have already been traversed. You can instead return directly to node A, which is the nearest ancestor of R whose right subtree has not yet been traversed.

This strategy of not returning to a node after its right subtree has been traversed is simple to implement: You place a pointer to a node in the stack only before the node's left subtree is traversed, but not before its right subtree is traversed. Thus, in Figure 16-6, when you are at node R, the stack contains A and R, with R on top. Nodes B and C are not in the stack, because you have visited them already and are currently traversing their right subtrees. On the other hand, A is in the stack because you are currently traversing its left subtree. When you return from node R, nodes B and C are thus bypassed because you have finished with their right subtrees and do not need to return to these nodes. Thus, you pop R's pointer from the stack and go directly to node A, whose left subtree has just been traversed. You then visit A, pop its pointer from the stack, and traverse A's right subtree.

### FIGURE 16-6 Avoiding returns to nodes B and C

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_496_0.png)

### Nonrecursive inorder traversal

This nonrecursive traversal strategy is captured by the following pseudocode, assuming a link-based implementation. Exercise 9 at the end of this chapter asks you to trace this algorithm for the tree in Figure 16-4.

```
// Nonrecursively traverses a binary tree in inorder:
// traverse(visit: ItemType): void inorder:
// Initialize
curPtr = rootPtr // Start at root
done = false
while (!done)
{
    if (curPtr != nullPtr)
    {
        // Place pointer to node on stack before traversing the node's left subtree
        nodeStack.push(curPtr)
        // Traverse the left subtree
        curPtr = curPtr->getLeftChildPtr()
    }
    else // Backtrack from the empty subtree and visit the node at the top of
         // the stack; however, if the stack is empty, you are done
    {
        if (!nodeStack.isEmpty())
        {
            nodeStack.peek(curPtr)
```
