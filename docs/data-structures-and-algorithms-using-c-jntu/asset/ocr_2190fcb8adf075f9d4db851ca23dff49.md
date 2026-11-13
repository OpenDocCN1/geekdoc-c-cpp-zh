```
Which Element You Want To Delete10
ITEM 10 Is Successfully Deleted
BINARY TREE OPERATIONS
1.CREATION
2.INSERTION
3.DELETION
4.TRAVERSE
5.SEARCHING
6.EXIT
Enter Your Choice 6
```

# ## 9.7 BINARY TREE TRAVERSALS

To perform an operation on the element of a node it needs to be visited only once, and visiting a node of a binary tree is known as *traversal*.

During traversal the three tasks that are performed are visiting a node (v), traversing the left subtree (l) and traversing the right subtree (R). Various combinations of these three tasks lead to six different traversals. They are VLR, VRL, LVL, RVL, LRV and RLV. Among these the traversals that move from left to right are very significant. The following are familiar ways of traversals:

+   1. Inorder traversal
+   2. Preorder traversal
+   3. Postorder traversal
+   4. Level-order traversal

# ## 9.7.1 INORDER TRAVERSAL (LVR)

The inorder traversal starts with the root node and traverses the left subtree. In the left subtree if a node has a left child then it is treated if it does not have any left child then it is visited and traverses its right child in the same way. If it does not have any right child then it traces back by one node and proceeds the traversal in the same manner till all the nodes of the binary tree are visited.

Algorithm 9.1 explains the recursive procedure to perform the inorder traversal of a binary tree.

```
inorder_traversal (NODE)
if NODE!=NILL then
{
    inorder_traversal(LCHILD(NODE)); //traverse the left subtree(L)
    visit (DATA (NODE)); //visit the node
    inorder_traversal( RCHILD(NODE)); //traversal the (Right subtree(R))
}
end if
End inorder_traversal.
```

The inorder traversal of the binary tree starts with the root node traversing the left subtree, visiting the node and traversing the right subtree.