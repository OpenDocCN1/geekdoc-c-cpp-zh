When an internal node would contain three items, split it into two nodes and accommodate its children

On the other hand, if the parent cannot accommodate the item moving up, you must split the parent, as follows. You split an internal node n that contains three items by using the process just described for a leaf, except that you must also take care of n's four children. As Figure 19-13 illustrates, you split n into n1 and n2, place n's smallest items S into n1, attach n's two leftmost children to n1, place n's largest item L into n2, attach n's two rightmost children to n2, and move n's middle item M up to n's parent.

# FIGURE 19-13 Splitting an internal node in a 2-3 tree when the node is a (a) left child; (b) right child

![](bbox=[0.223, 0.23, 0.933, 0.47])

After this, the process of splitting a node and moving an item up to the parent continues recursively until a node is reached that had only one item before the insertion and thus has only two items after it takes on a new item. Notice in the previous sequence of insertions that the tree's height never increased from its original value of 3. In general, an insertion will not increase the height of the tree as long as there is at least one node containing only one item on the path from the root to the leaf into which the new item is inserted. The insertion strategy of a 2-3 tree has thus postponed the growth of the tree's height much more effectively than the strategy of a basic binary search tree did.

When the root would contain three items, split it into two nodes and create a new root node

When the height of a 2-3 tree does grow, it does so from the top. An increase in the height of a 2-3 tree will occur if every node on the path from the root of the tree to the leaf into which the new item is inserted contains two items. In this case, the recursive process of splitting a node and moving an item up to the node's parent will eventually reach the root r. When this occurs you must split r into r1 and r2 exactly as you would any other internal node. However, you must create a new node that contains the middle item of r and becomes the parent of r1 and r2. Thus, the new node is the new root of the tree, as Figure 19-14 illustrates.

# FIGURE 19-14 Splitting the root of a 2-3 tree

![](bbox=[0.223, 0.775, 0.933, 0.91])