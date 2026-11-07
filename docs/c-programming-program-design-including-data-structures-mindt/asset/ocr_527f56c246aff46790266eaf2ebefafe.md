![](bbox=[0.178, 0.074, 0.911, 0.373])

FIGURE 19-12 Binary tree; the leftmost node is 28

null. From this point, we back up to the parent node, visit the node, and then move to the right node. Because links go in only one direction, to get back to a node, we must save a pointer to the node before moving to the child node. Moreover, the nodes must be backtracked in the order they were traversed. It follows that while backtracking, the nodes must be visited in a last-in first-out manner. This can be done by using a stack. We, therefore, save a pointer to a node in a stack. The general algorithm is as follows:

+   1. `current = root; //start the traversal at the root node`
+   
+   2. 
+       ```
+       while (current is not nullptr and stack is nonempty)
+           if (current is not nullptr)
+           {
+               push current onto stack;
+               current = current->lLink;
+           }
+           else
+           {
+               current = stack.top();
+               pop stack;
+               visit current;            //visit the node
+               current = current->rLink; //move to the right child
+           }
+       ```

The following function implements the nonrecursive inorder traversal of a binary tree:

```
template <class elemType>
void binaryTreeType<elemType>::nonRecursiveInTraversal() const
{
    stackType<nodeType<elemType>*> stack;
    nodeType<elemType> *current;
    current = root;
```