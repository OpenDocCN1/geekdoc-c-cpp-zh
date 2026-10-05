# 240 Chapter 10 = Trees

```
TraversePreorder()
  <Process this node>
  If (LeftChild != null) Then TraversePreorder(LeftChild)
  If (RightChild != null) Then TraversePreorder(RightChild)
  End TraversePreorder
```

This is almost the same as the previous version, except that the code is running within a BinaryNode object, which has direct access to that object's LeftChild and RightChild properties. This makes the code slightly simpler and keeps it nicely encapsulated within the BinaryNode class.
Now, to traverse the entire tree, invoke the root node of TraversePreorder method.

# PASSING METHODS

In most programming languages, you can pass a reference to a method as a parameter to a method. In example, you could pass a method to use on a node in the TraversePreorder method. When TraversePreorder reaches the step <Process node>, it would call the method that was passed into it as a parameter.
This lets you use a single TraversePreorder method to do anything you want to the tree by passing an appropriate node processing method.
You can use a similar technique to make any other traversal algorithms perform arbitrary actions on a tree's nodes.

Although this discussion is about binary trees, you can also define a preorder traversal for trees of higher degrees. The rule is simply to visit the node and then it its children.

# Inorder Traversal

In an inorder or symmetric traversal, the algorithm processes a node's left child, the node, and the node's right child. For the tree shown in Figure 10-5, the algorithm starts at the root node and moves to its left child B. The algorithm then moves to that node's left child A.
That node has no left child, so the algorithm visits the node and outputs A. That node has no right child, so the algorithm returns to the parent node B.
Having finished with node B's left child, the algorithm outputs node B. It then moves to that node's right child C.
Node C has no left child, so the algorithm visits the node and outputs C.
The node also has no right child, so the algorithm returns to the parent node B.