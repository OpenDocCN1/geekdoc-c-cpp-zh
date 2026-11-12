```
nodePtr->setItem(newNodeValue) // Put replacement value in node N
return nodePtr
}
```

```
// Removes the leftmost node in the left subtree of the node pointed to by nodePtr.
// Sets inorderSuccessor to the value in this node.
// Returns a pointer to the revised subtree.
removeLeftmostNode(nodePtr: BinaryNodePointer,
                   inorderSuccessor: ItemType&): BinaryNodePointer
```

```
if (nodePtr->getLeftChildPtr() == nullPtr)
{
    // This is the node you want; it has no left child, but it might have a right subtree
    inorderSuccessor = nodePtr->getItem()
    return removeNode(nodePtr)
}
else
    return removeLeftmostNode(nodePtr->getLeftChildPtr(), inorderSuccessor)
```

Now the public method remove calls removeValue and assigns the pointer it receives back from this call to rootPtr, as the following pseudocode indicates:

```
// Removes the given data from this binary search tree.
remove(target: ItemType): boolean
    success = false
    rootPtr = removeValue(rootPtr, target, success)
    return success
```

Let's see how the recursive calls work. Suppose that we have the tree in Figure 16-14a, and we want to remove Dave. We call remove, which calls removeValue. Assuming that removeValue recursively locates Dave in Node N, it calls removeNode to remove N. Any change that removeNode makes to its parameter nodePtr is returned by removeNode (Figure 16-14b) and then by removeValue. Because Dave isn't in the tree's root, the return from removeValue is due to a recursive call. The method now assigns the pointer returned by removeNode—and the recursive call to removeValue—to the left child pointer of Node N's parent. The result is shown in Figure 16-14c.

Observe that in the case of the removeNode method, the argument that corresponds to its parameter nodePtr is either one of the pointers of the parent of N, as Figure 16-14 depicts, or the external pointer to the root, in the case where N is the root of the original tree. In either case, nodePtr points to N. Thus, any change you make to nodePtr by calling the method removeNode with the argument nodePtr must be returned so you can change either a pointer in the parent of node N or the root pointer.

**Note:** The methods removeValue, removeNode, removeLeftmostNode are behind the wall of abstraction, since they are protected. Therefore they can use pointers as parameters, and if necessary, a reference parameter (success or inorderSuccessor). Each method receives as an argument a pointer to the root of the subtree on which it is to perform its process. When that process is complete, the method reflects—like a mirror—back to the parent the pointer to the node that is now the root of that subtree.

**Note that what we have done is safe programming:**

+   * Only one reference parameter is used in a method, and the argument passed to it is local to the calling method.
+   * The calling method has a choice of whether or not to replace the pointer it has passed as an argument with the one returned—which it should do here.
+   * Each of the three methods performs a single, clearly defined task.