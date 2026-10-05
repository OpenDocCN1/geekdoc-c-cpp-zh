
# Chapter 10 | Trees 241

The algorithm has finished with node B's right child, so it returns to the root node D. The algorithm has finished with D's left child, so it outputs D and then moves to its right child E.

Node E has no left child, so the algorithm visits the node and outputs E. The node has no right child, so the algorithm returns to the parent node D. The full traversal order is A, B, C, D, E. Notice that this outputs the tree's nodes in sorted order. Normally the term sorted tree means that the tree's nodes are arranged so that an inorder traversal processes them in sorted order like this.

The following pseudocode shows a recursive implementation of this algorithm:

```
TraverseInorder(BinaryNode: node)
  If (node.LeftChild != null) Then TraverseInorder(node.LeftChild)
  <Process node>
  If (node.RightChild != null) Then TraverseInorder(node.RightChild)
  End TraverseInorder
```

This algorithm simply follows the definition of an inorder traversal. It recursively processes the node's left child if it exists, processes the node, and recursively processes the node's right child if it exists.

To traverse the entire tree, a program would simply call TraverseInorder, passing it the root node as a parameter.

The following pseudocode shows the same algorithm implemented inside the BinaryNode class:

```
Class BinaryNode
  String: Name
  BinaryNode: LeftChild
  BinaryNode: RightChild

  Constructor(String: name)
    Name = name
  End Constructor

  TraverseInorder()
    If (LeftChild != null) Then TraverseInorder(LeftChild)
    <Process this node>
    If (RightChild != null) Then TraverseInorder(RightChild)
    End TraverseInorder
End Class
```

Unlike preorder traversal, it's unclear how you would define an inorder traversal for a tree with a degree greater than 2. You could define it to mean that the algorithm should process the first half of a node's children, and then the node, and then the remaining children. That's an atypical traversal, though.

# Postorder Traversal

In a postorder traversal, the algorithm processes a node's left child, and then its right child, and then the node. For the tree shown in Figure 10-5:

- 1. The algorithm starts at the root node and moves to its left child B.
- 2. The algorithm then moves to that node's left child A.
- 3. Node A has no left or right child, the algorithm outputs the node A and returns to the parent node B.
- 4. Having finished with the left child, the algorithm moves to the node's right child C.
- 5. Node C has no left or right child, so the algorithm outputs node C and returns to the parent node B.
- 6. Now that it has visited node B's left and right child, the algorithm outputs node B. It then returns to the parent node D.
- 7. The algorithm has visited node D's left child, so now it moves to the right child E.
- 8. Node E has no left or right child, so the algorithm outputs node E and returns to the parent node D.
- 9. The algorithm has finished with node D's left and right children, so the algorithm outputs D and is done.

The full traversal is A, C, B, E, D.
The following pseudocode TraversePostorder shows a recursive implementation of this algorithm:

```
TraversePostorder(BinaryNode: node)
  If (node.LeftChild != null) Then TraversePostorder(node.LeftChild)
  If (node.RightChild != null) Then TraversePostorder(node.RightChild)
<Process node>
End TraversePostorder
```

This algorithm recursively processes the node's left child and right child if they exist. It processes the node.
To traverse the entire tree, a program would simply call TraversePostorder, passing the root node as a parameter.
The following pseudocode shows the same algorithm implemented inside the BinaryNode class:

```
Class BinaryNode
  String: Name
  BinaryNode: LeftChild
  BinaryNode: RightChild

  Constructor(String: name)
    Name = name
  End Constructor

  TraverseInorder()
    If (LeftChild != null) Then TraversePostorder(LeftChild)
    If (RightChild != null) Then TraversePostorder(RightChild)
    <Process this node>
    End TraversePostorder
End Class
```

Like the preorder traversal, you can easily define a postorder traversal for trees with a degree greater than 2. The algorithm should visit all of a node's children before visiting the node itself.

# Depth-first Traversal

In a depth-first traversal, the algorithm processes all nodes at a given level of the tree in left-to-right order before processing the nodes at the next level. For the tree shown in Figure 10-5, the algorithm starts at the root node's level and outputs D.

The algorithm then moves to the next level and outputs B and E. The algorithm finishes at the bottom level by outputting the nodes A and C. The full traversal is D, B, E, A, C.

This does not naturally follow the structure of the tree as the previous traversal algorithms do. The tree shown in Figure 10-5 has no child link from E to node A, so it is not obvious how the algorithm moves from E to node A.

One solution is to add a node's children to a queue and then process the queue, after you've finished processing. The following pseudocode uses this approach:

```
TraverseDepth(BinaryNode: root)
  // Create a queue to hold children.
  Queue<BinaryNode>: children = New Queue<BinaryNode>()
  // Place the root on the queue.
  children.Enqueue(root)
  // Process the queue until it is empty.
  While (children.NotEmpty)
    // Get the next node.
    BinaryNode: node = children.Dequeue()
    // Process the node.
    <Process node>
    // Add node's children to the queue.
    If (node.LeftChild != null) children.Enqueue(node.LeftChild)
    If (node.RightChild != null) children.Enqueue(node.RightChild)
End While
```

# Traversal Times

The three algorithms for preorder, inorder, and postorder all travel down the tree. That means if the tree is very tall, it could cause a stack overflow. This isn't recursive, so it needs extra space to build its queue. In the worst case, if the tree is a perfect binary tree, its bottom level holds half the number of nodes, so it needs O(N).

More generally, a tree of arbitrary degree might consist of a root node that has every other node as a child. In that case, the queue might need N-1 nodes, so the space requirement is still O(N).

# Sorted Trees

As mentioned earlier, a sorted tree's nodes are arranged so an inorder traversal processes them in sorted order. Another way to think of this is that each node's value is larger than the value of its left child and less than (or equal to) the value of its right child. Figure 10-6 shows a sorted tree.

img/fefa2765c0b410af6705110aea7c0cb_268_0.png)

Figure 10-6: In a sorted tree, a node's value lies between the values of its left child and its right child.

To use a sorted tree, you need three algorithms to add, delete, and find nodes.

# Adding Nodes

Building a sorted tree is fairly easy. To add a value to a node's subtree, compare the new value to the node's value, and move down the left or right branch as appropriate. When you try to move down a missing branch, add the new value there.

The following pseudocode shows the algorithm for a BinaryNode class. The code assumes that the class has a Value property to hold the node's data:

```
// Add a node to this node's sorted subtree.
AddNode(Data: new value)
// See if this value is smaller than ours.
If (new_value < Value) Then
  // The new value is smaller. Add it to the left subtree.
  If (LeftChild == null) LeftChild = New BinaryNode(new_value)
  Else LeftChild.AddNode(new_value)
Else
  // The new value is not smaller. Add it to the right subtree.
  If (RightChild == null) RightChild = New BinaryNode(new_value)
  Else RightChild.AddNode(new_value)
```
