# 7.7.3 Postorder Traversal

In this traversal, the left subtree is visited first in postorder followed by the right subtree in postorder and then the root. This is defined as the following:

# Postorder (LRD) Algorithm

+   1. Traverse the root's left child (subtree) of the root node in postorder.
+   2. Traverse the root's right child (subtree) of the root node in postorder.
+   3. Visit the root node.

Let us consider the binary tree in Fig. 7.34. The postorder traversal yields the following sequence:

**Postorder sequence: D G E B F C A** For the expression tree in Fig. 7.35, the postorder traversal yields a postfix expression as the following:
= A x B x D +

For the tree in Fig. 7.36, the postfix expression by the postorder traversal is ABCx// DxE+. The postorder traversal says, “traverse left and continue again. When you cannot continue, move right and begin again or move back until you can move right and visit the node.”

```
void BinaryTree :: Postorder(TreeNode*)
{
    if(Root != Null)
    {
        Postorder(Root->LChild);
        Postorder(Root->RChild);
        cout << Root->Data;
    }
}
```

![](bbox=[0.738, 0.511, 0.902, 0.615])

# 7.7.4 Non-recursive Implementation of Traversals

We have defined the recursive traversals. These are easy to read and understand. However, a language translator such as a compiler will be burdened to carry out the execution. Let us go for the other non-recursive approach for these algorithms. Let us write a non-recursive implementation using stacks. Here, at the time of left or right traversal, when the left or right node is the root of the other subtree, the current node is to be stacked for further traversal.

# Non-recursive Preorder Algorithm

+   1. Tmp = Root
+   2. while(stack not empty) do
+      begin
+      if(Tmp is not null) then
+      begin
+      visit(Tmp->data)
+      Push(Tmp->LChild)