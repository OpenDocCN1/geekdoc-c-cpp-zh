
Insert 80 and 15. These insertions do not require split nodes and result in the tree in Figure 19-25.

### FIGURE 19-25 After inserting 80 and 15 into the tree in Figure 19-24b

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_615_0.png)

Insert 90. As you search Figure 19-25 for 90's insertion point, you traverse the root's right subtree, because 90 is greater than 50, and encounter the 4-node <60 70 80>. You split this 4-node into two nodes and move 70 up to the root, as Figure 19-26a indicates. Finally, because 90 is greater than 70, you insert 90 into the leaf <80> to get the tree in Figure 19-26b.

### FIGURE 19-26 The steps for inserting 90 into the tree in Figure 19-25

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_615_1.png)

Insert 100. As you begin to search Figure 19-26b, you immediately encounter a 4-node at the tree's root. You split this node into two nodes and move 50 up to a new root, as Figure 19-27a indicates. After continuing the search, you insert 100 into <80 90> to get the tree in Figure 19-27b.

### FIGURE 19-27 The steps for inserting 100 into the tree in Figure 19-26b

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_615_2.png)

Splitting 4-nodes during insertion. As you have just seen, you split each 4-node as soon as you encounter it during your search from the root to the leaf that will accommodate the new item to be inserted. As a result, each 4-node either will

- Be the root,
- Have a 2-node parent, or
- Have a 3-node parent

Figure 19-28 illustrates how to split a 4-node that is the tree's root. You have seen two previous examples of this: We split <10 30 60> in Figure 19-22a, resulting in the tree in Figure 19-22b. We also split <30 50 70> during the insertion of 100 into the tree in Figure 19-26b, giving us the tree in Figure 19-27a.

### FIGURE 19-28 Splitting a 4-node root during insertion into a 2-3-4 tree

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_616_0.png)

Figure 19-29 illustrates the two possible situations that can occur when you split a 4-node whose parent is a 2-node. For example, when you split <40 50 60> during the insertion of 70 into the tree in Figure 19-23, you get the tree in Figure 19-24a.

### FIGURE 19-29 Splitting a 4-node whose parent is a 2-node during insertion into a 2-3-4 tree, when the 4-node is a (a) left child; (b) right child

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_616_1.png)

Figure 19-30 illustrates the three possible situations that can occur when you split a 4-node whose parent is a 3-node. For example, when you split <60 70 80> during the insertion of 90 into the tree in Figure 19-25, you get the tree in Figure 19-26a.

Question 5 Insert 25 into the 2-3-4 tree in Figure 19-27b.

Question 6 Insert 3 and 4 into the 2-3-4 tree that you created in the previous question.

### FIGURE 19-30 Splitting a 4-node whose parent is a 3-node during insertion into a 2-3-4 tree, when the 4-node is a (a) left child; (b) middle child; (c) right child

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_617_0.png)

## 19.3.3 Removing Data from a 2-3-4 Tree

The removal algorithm for a 2-3-4 tree has the same beginning as the removal algorithm for a 2-3 tree. You first locate the node n that contains the item I that you want to remove. You then find I's inorder successor and swap it with I so that the removal will always be at a leaf. If that leaf is either a 3-node or a 4-node, you simply remove I. If you can ensure that I does not occur in a 2-node, you can perform the removal in one pass through the tree from root to leaf, unlike removal from a 2-3 tree. That is, you will not have to back away from the leaf and restructure the tree.

### Transform each 2-node into a 3-node or a 4-node

In fact, you can guarantee that I does not occur in a 2-node by transforming each 2-node that you encounter during the search for I into either a 3-node or a 4-node. Several cases are possible, depending on the configuration of the 2-node's parent and its nearest sibling. (Arbitrarily, a node's nearest sibling is its left sibling, unless the node is a left child, in which case its nearest sibling is to its right.) That is, either the parent or the sibling could be a 2-node, a 3-node, or a 4-node. For example, if the next node that you encounter is a 2-node and both its parent and nearest sibling are 2-nodes, apply the transformation that Figure 19-28 illustrates, but in reverse; however, if the parent is a 3-node, apply the transformation that Figure 19-29 illustrates, but in reverse; and if the parent is a 4-node, apply the transformation that Figure 19-30 illustrates, but in reverse.

The details of removal from a 2-3-4 tree are left to you as a challenging exercise (Exercise 8).

### 2-3 and 2-3-4 trees are attractive because their balance is easy to maintain

**Note: 2-3 trees versus 2-3-4 trees**

The advantage of both 2-3 and 2-3-4 trees is their easy-to-maintain balance, not their shorter height. Even if a 2-3 tree is shorter than a balanced binary search tree, the reduction in height is offset by the increased number of comparisons that the search algorithm might require at each node. The situation is similar for a 2-3-4 tree, but its insertion and removal algorithms require only one pass through the tree and so are more efficient than those for a 2-3 tree. This decrease in effort makes the 2-3-4 tree more attractive than the 2-3 tree.

### Insertion and removal algorithms for a 2-3-4 tree require fewer steps than those for a 2-3 tree

**Note: Nodes with more than four children?**

Should we consider trees whose nodes have even more than four children? Although a tree whose nodes can each have 100 children would be shorter than a 2-3-4 tree, its search algorithm would require more comparisons at each node to determine which subtree to search. Thus, allowing the nodes of a tree to have many children is counterproductive. Such a search tree is appropriate, however, when it is implemented in external storage, because moving from node to node is far more expensive than comparing the data values in a node. In such cases, a search tree with the minimum possible height is desired, even at the expense of additional comparisons at each node. Chapter 21 will discuss external search trees further.

## 19.4 Red-Black Trees

### A 2-3-4 tree requires more storage than a binary search tree

A 2-3-4 tree is appealing because it is balanced and because its insertion and removal operations use only one pass from root to leaf. On the other hand, a 2-3-4 tree requires more storage than a binary search tree that contains the same data because a 2-3-4 tree has nodes that must accommodate up to three data items. A typical binary search tree, however, might not be balanced.

### A red-black tree has the advantages of a 2-3-4 tree but requires less storage

You can use a special binary search tree—a red-black tree—to represent a 2-3-4 tree that retains the advantages of a 2-3-4 tree without the storage overhead. The idea is to represent each 3-node and 4-node in a 2-3-4 tree as an equivalent binary search tree. To distinguish between 2-nodes that appeared in the original 2-3-4 tree and 2-nodes that were generated from 3-nodes and 4-nodes, you use red and black child pointers. Let all the child pointers in the original 2-3-4 tree be black, and use red child pointers to link the 2-nodes that result when you split 3-nodes and 4-nodes.

**Note: In a red-black tree, red pointers link the 2-nodes that now contain the values that were in a 3-node or a 4-node.**

Figure 19-31 indicates how to represent a 4-node and a 3-node as binary trees. Because there are two possible ways to represent a 3-node as a binary tree, a red-black representation of a 2-3-4 tree is not unique. Figure 19-32 gives a red-black representation for the 2-3-4 tree in Figure 19-20. In all of these figures, a dashed blue line represents a red pointer and a solid black line represents a black pointer.

### FIGURE 19-31 Red-black representation of (a) a 4-node; (b) a 3-node

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_619_0.png)

### FIGURE 19-32 A red-black tree that represents the 2-3-4 tree in Figure 19-20

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_619_1.png)

A node in a red-black tree is similar to a node in a binary search tree, but it must also store the pointer colors, as the following C++ statements indicate:

```
enum Color {RED, BLACK};
template<class ItemType>
class RedBlackNode : public BinaryNode<ItemType>
{
private:
   Color leftColor, rightColor;
public:
   // Get and set methods for leftColor and rightColor
   // ...
}; // end RedBlackNode
```

A node in a red-black tree

**Note: Even with the pointer colors, a node in a red-black tree requires less storage than a node in a 2-3-4 tree. Keep in mind that the transformations in Figure 19-31 imply a change in the structure of the nodes.**
