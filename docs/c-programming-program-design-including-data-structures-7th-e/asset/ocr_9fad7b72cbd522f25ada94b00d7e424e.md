**Case 1:** Suppose that we want to delete 45 from the binary search tree in Figure 19–9. We search the binary tree and arrive at the node containing 45. Because this node is a leaf and is the left child of its parent, we can simply set the lLink of the parent node to `nullPtr` and deallocate the memory occupied by this node. After deleting this node, Figure 19–10(a) shows the resulting binary search tree.

**Case 2:** Suppose that we want to delete 30 from the binary search tree in Figure 19–9. In this case, the node to be deleted has no left subtree. Because 30 is the left child of its parent node, we make the lLink of the parent node point to the right child of 30 and then deallocate the memory occupied by 30. Figure 19–10(b) shows the resulting binary tree.

**Case 3:** Suppose that we want to delete 80 from the binary search tree of Figure 19–9. The node containing 80 has no right child and is the right child of its parent. Thus, we make the rLink of the parent of 80—that is, 70—point to the left child of 80. Figure 19–10(c) shows the resulting binary tree.

**Case 4:** Suppose that we want to delete 50 from the binary search tree in Figure 19–9. The node with info 50 has a nonempty left subtree and a nonempty right subtree. Here, we first reduce this case to either case 2 or case 3 as follows. To be specific, suppose that we reduce it to case 3—that is, the node to be deleted has no right subtree. For this case, we find the immediate predecessor of 50 in this binary tree, which is 48. This is done by first going to the left child of 50 and then locating the rightmost node of the left subtree of 50. To do so, we follow the rLink of the nodes. Because the binary search tree is finite, we eventually arrive at a node that has no right subtree. Next, we swap the info in the node to be deleted with the info of its immediate predecessor. In this case, we swap 48 with 50. This reduces the case wherein the node to be deleted has no right subtree. We now apply case 3 to delete the node. (Note: Because we will delete the immediate predecessor from the binary tree, we, in fact, copy only the info of the immediate predecessor into the node to be deleted.) After deleting 50 from the binary search tree in Figure 19–9, the resulting binary tree is as shown in Figure 19–10(d).

In each case, we clearly see that the resulting binary tree is again a binary search tree. From this discussion, it follows that to delete an item from the binary search tree, we must do the following:

+   1. Find the node containing the item (if any) to be deleted.
+   2. Delete the node.

We accomplish the second step by a separate function, which we will call deleteFromTree. Given a pointer to the node to be deleted, this function deletes the node by taking into account the previous four cases.

From the preceding examples, it is clear that whenever we delete a node from the binary tree, we adjust one of the pointers of the parent node. Because the adjustment has to be made in the parent node, we must call the function deleteFromTree by using an appropriate pointer of the parent node. For example, suppose that the node to be deleted is 35, which is the right child of its parent node. Suppose that trailCurrent points to the node containing 30, the parent node of 35. A call to the function deleteFromTree is:

```
deleteFromTree(trailCurrent->rLink);
```