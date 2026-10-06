
# FIGURE 16-3 Adding nodes to an initially empty binary tree

![](img/d0cb86b2f18b2db569968ad7c743510e_492_0.png)

the pointer treePtr, which, due to the recursive calls, eventually points to every node in the tree.
The definition of inorder follows:

```cpp
template<class ItemType>
void BinaryNode<ItemType>::
inorder(void visit(ItemType&), BinaryNode<ItemType>* treePtr) const
```

```cpp
if (treePtr != nullptr) {
    inorder(visit, treePtr->getLeftChildPtr());
    ItemType item = treePtr->getItem();
    visit(item);
    inorder(visit, treePtr->getRightChildPtr());
} // end if
// end inorder
```

Now the definition of the public method inorderTraverse contains only the call
 inorder(visit, rootPtr);

The other traversals have similar definitions.

> **Programming Tip:** Why did we write
> `ItemType item = treePtr->getItem();`
> `visit(item);`
> instead of
> `visit(treePtr->getItem());`
> in the definition of inorder? Because visit has a reference parameter, we need an lvalue to reference. The variable item serves this purpose.

# Question 6 Define the protected method postorder.

**Nonrecursive traversal (optional).** Before leaving the topic of traversals, let's develop a non-recursive traversal algorithm to illustrate further the relationship between stacks and recursion that was discussed in Chapter 6. In particular, we will develop a nonrecursive traversal for the link-based implementation of a binary tree.

The conceptually difficult part of a non-recursive traversal is determining where to go after a particular node has been visited. To gain some insight into this problem, consider how the recursive inorder method works:

```cpp
if (treePtr != nullptr) {
    inorder(visit, treePtr->getLeftChildPtr()); // Point 1
    ItemType item = treePtr->getItem();
    visit(item);
    inorder(visit, treePtr->getRightChildPtr()); // Point 2
} // end if
```

Recursive calls from points 1 and 2

The method has its recursive calls marked as points 1 and 2.

During the course of the method's execution, the value of the pointer treePtr actually marks the current position in the tree. Each time inorder makes a recursive call, the traversal moves to another node. Nodes of the stack that is implicit to recursive methods, a call to inorder pushes the new

# 468 CHAPTER 16 Tree Implementations

FIGURE 16-4 Contents of the implicit stack as treePtr progresses through a given tree during a recursive inorder traversal

(The notation $o$ means "a pointer to the node containing 60.")

| | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| | | | | nullptr | | nullptr | | | | |
| $o$60 | | $o$20 | | $o$10 | $o$10 | Visit 10 | | $o$10 | $o$10 | $o$20 Visit 20 |
| | | | $o$20 | | $o$20 | $o$20 | | $o$20 | $o$20 | | |
| | | | $o$60 | | $o$60 | $o$60 | | | $o$60 | | |

Step:

- treePtr at step 1
- treePtr at steps 2, 9, and 10
- treePtr at steps 3, 5, 6, and 8
- treePtr is nullptr at steps 4 and 7

![](img/d0cb86b2f18b2db569968ad7c743510e_494_0.png)

Recursive inorder's implicit stack gives insight into a non-recursive traversal value of treePtr—that is, a pointer to the current node—onto the stack. The stack contains pointers to the nodes along the path from the root to the current node $n$, with the pointer $n$ at the top of the stack and the pointer to the root at the bottom. When $n$ is possibly “empty”—that is, it may be indicated by a nullptr value for treePtr at the top of the stack. Such an occurrence corresponds to the base case of recursion.

Figure 16-4 partially traces the show stack as treePtr first to 60, then to 20, then to 10, and becomes nullptr. The recursive calls are for each parent of $i$ in inorder.

Now what happens when inorder returns from a recursive call? The traversal retraces its steps by backing up the tree from a node to its parent $p$, from the recursive call to was made. Thus, the pointer to $n$ is popped from the stack and the pointer to $p$ comes to the top of the stack, as occurs in step 5 of the trace in Figure 16-4. In this case, $n$ happens to be empty, so nullptr is popped from the stack.

What depends on which subtree of $p$ has been traversed. If you have finished traversing $p$'s left subtree—that is, if $l$ is the left child of $p$ and then the return to 1 inorder-control is returned to the statement that shows node $p$. This is the case for steps 6 and 10 of the trace in Figure 16-4. Figure 16-5b illustrates steps 9 and 10 in more detail.

After node $p$ has been visited, a recursive call returns the pointer from 2 and the right subtree of $p$ is traversed. However, if, Figure 16-5b illustrates, you have just traversed $p$'s right subtree—that is, if $n$ is the right child of $p$ and then the return to 2—control is returned to the end of the method. As a consequence another return, the pointer to $p$ is popped off the stack, and you go back the tree to $p$'s parent, from which the recursive call to $p$ was made. In this case, node $p$ is not visited—it was visited before the recursive call to $n$ was made from point 2.

# FIGURE 16-5 Traversing (a) the left subtree (steps 9 and 10 in and (b) the right subtree of 20

![](img/d0cb86b2f18b2db569968ad7c743510e_495_0.png)

Left subtree of 20 has been traversed. Right subtree of 20 has been traversed.

Thus, two facts emerge from the recursive version of inorder:

- The recursive stack is used to find the nearest ancestor $p$ whose right subtree has not yet been traversed.
- Once you return from $R$, the stack contains $A$, whose left subtree is.

# 470 CHAPTER 16 Tree Implementations

# FIGURE 16-6 Avoiding returns to B and C

![](img/d0cb86b2f18b2db569968ad7c743510e_496_0.png)

Nonrecursive traversal

This nonrecursive traversal strategy is captured by the following pseudocode, as a link-based binary tree. Exercise 9 at the end of this chapter asks you to trace this algorithm for the tree in Figure 16-4.

```cpp
// Noncursively traverses a binary tree in inorder.
traverse(visit: ItemType): void {
  // Initialize;
  nodeStack = A new, empty stack
  curPtr = rootPtr() // Start at root
  done = false
  while (!idone) {
    if (curPtr != nullptr) {
      // Place pointer to node on stack before traversing the node's left subtree
      nodeStack.push(curPtr)
      // Traverse the left subtree
      curPtr = curPtr->getLeftChildPtr()
    } else {
      // Backtrack from the empty stack and visit the node at the top of
      // the stack; however, if the stack is empty, you are done
      if (!nodeStack.isEmpty()) {
        nodeStack.peek(curPtr)
      }
    }
  }
}
```
