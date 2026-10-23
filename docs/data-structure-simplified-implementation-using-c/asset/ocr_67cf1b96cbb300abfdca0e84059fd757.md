```
{
q1.enqueue(x->right);  // insert the right node in q
count++; // count the right node
}
    }
    return count;
}
```

# 7.7.3 Counting all the nodes in a BST

To count the total number of nodes in a BST, we can compute the left half node as well as right half node of a BST. Afterwards, we can compute the total number of nodes by performing the sum of left half and right half. However, we have not counted the root node. Therefore, total node in a BST can be computed by

Total number of node=total number of left node + total number of right node +root node

Consequently, we can use the functions written above, to compute the total number of nodes.

+   - leftTotal= int bst:: leftCount();
+   - rightTotal=int bst:: rightCount();
+   - Total no. of nodes=leftTotal + rightTotal +1;

# 7.8 DETERMINING THE HEIGHT OF A TREE

Height of a tree is important to understand the exact depth of a tree. Efficiency of a tree is governed by the height o a tree. If a tree is containing so many branches which are not full in that case the height of a tree will grow tremendously where as the performance of the tree will reduce drastically. Therefore, we need to understand the height of a tree and how it can be controlled.

Height of a BST is the longest path existing in its left or the right side. For instance, the maximum path may be available towards the right side of the left node. Height of a BST has been explained with the help of following examples.

# 7.8.1 Non-recursive method

In the non-recursive approach of determining the height of a tree, we are visiting the tree level by level. Once new level is reached, height is incremented by one. To traverse the level by level, we can utilize the dynamic queue already created in the previous chapter. In this method, if the tree exists the root node is inserted into the queue. This is followed by counting the number of nodes in a queue. We can figure out the total number of nodes at a particular level with the help of a queue function ‘size ()’ that determine the number of nodes in a queue. Initially, number of nodes are 1 (only the root node). We can dequeue the root and