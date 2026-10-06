# A Link-Based Implementation of the ADT Binary Search Tree 479

```
nodePtr->setItem(newVal) // Put replacement value in node N
return nodePtr
}
// Removes the leftmost node in the left subtree of the node pointed to by nodePtr.
// Sets inorderSuccessor to this node.
// Returns a pointer to the revised
removeLeftmostNode(nodePtr, BinaryNodePointer inorderSuccessor: ItemType&)
if (nodePtr->getLeftChild() == nullptr)
{
    // This is the node you want; it has no left child, but it may have a right subtree
    inorderSuccessor = nodePtr->getitem(
    return removeNode(nodePtr)
}
else
    return removeLeftmostNode(nodePtr->getLeftChild(), inorderSuccessor)
```

The new public method calls remove and assigns the pointer back from this call to rootPtr, as the root has the given data from this binary search tree.

```
remove(target: ItemType): boolean

sccess = false
rootPtr = removeValue(rootPtr, target, success)
return success
```

Let's see how the recursive calls work. Suppose that the tree in Figure 16-1a, and we want to remove Dave. We call remove, which calls removeValue. Assuming that removeValue recursively locates Dave in Node N, it calls removeNode to N. Any change that removeNode makes to its parameter nodePtr, is returned by removeNode(Figure 16b) and then by removeValue. Because Dave is not in the tree's root, the root returned by removeValue is due to a recursive call. The method now assigns the pointer returned by removeNode—and the recursive call to removeValue—to the left child pointer of Node N. The result is shown in Figure 16-1c.

Observe that in the case of the removeNode method, the argument that corresponds to its parameter nodePtr is either one of the pointers of the parent of N, as Figure 16-14 depicts, or the external pointer to the root, in the case where N is the root of the original tree. In either case, nodePtr points to N. Thus, any change you make by calling the method removeWith the argument nodePtr must be returned so you can change it in the parent of node N or the root pointer.

> Note: The methods removeValue, removeNode, removeLeftmost are behind the wall of abstraction, since they are protected. Therefore they can use pointers as parameters, and if necessary, a reference parameter (success or inorderSuccess). Each method receives as an argument a pointer to the root of the subtree on which it is performing. When that process is complete, the method reflects—like a mirror—back to the pointer to the node that is root of subtree.\ Note that what we have done is state programming:

+   - Only one reference is used in a method, and the argument passed to it is local to the calling method.
- The calling method has a choice of whether or not to replace the pointer it has passed as an argument with the one returned—which it should do.
- Each of the three methods performs a single, clearly defined task.