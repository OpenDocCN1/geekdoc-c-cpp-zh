# 470 CHAPTER 16 Tree Implementations

# FIGURE 16-6 Avoiding returns to nodes B and C

![](bbox=[0.268, 0.149, 0.932, 0.483])

Nonrecursive inorder traversal

This nonrecursive traversal strategy is captured by the following pseudocode, as a link-based binary tree. Exercise 9 at the end of this chapter asks you to trace this algorithm for the tree in Figure 16-4.

```
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
```