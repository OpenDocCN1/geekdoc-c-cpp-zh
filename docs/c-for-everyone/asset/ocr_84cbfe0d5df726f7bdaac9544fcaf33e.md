**P14.18** Modify the implementation of the Heap class so that the parent and child index positions are computed directly, without calling helper functions.

**P14.19** Modify the implementation of the Heap class so that the 0 element of the array is not wasted.

**P14.20** Modify the implementation of the Heap class so that it stores strings, not integers. Test your implementation with the tasks from the **queue.cpp** program.

# ANSWERS TO SELF-CHECK QUESTIONS

+   1. Efficient set implementations can quickly test whether a given element is a member of the set.

+   2. Sets do not have an ordering, so it doesn’t make sense to add an element at a particular iterator position, or to traverse a set backwards.

+   3. −4 −3 −2 −1 1 4 9 16

+   4. 2 4 8 10 14 16

+   5. It sets c to the intersection of a and b, that is, the set of elements that are present in both a and b.

+   6. In a tree, each node can have any number of children. In a binary tree, a node has at most two children. In a balanced binary tree, all nodes have approximately as many descendants to the left as to the right.

+   7. For example, Sarah. Any string between Romeo and Tom will do.

+   8. The tree at this point is

![](bbox=[0.26, 0.532, 0.34, 0.604])

The call of the `BinarySearchTree::insert` function allocates a node holding the string “C”, and then calls `TreeNode::insert_node` on the root node (whose data is “D”). Since “C” < “D” and its left node is not NULL, the `TreeNode::insert_node` is called on the node whose data is “B”. Now “B” < “C”, so the second branch of the if statement is executed. Since right is NULL, right is set to the new node, and the result is

![](bbox=[0.26, 0.701, 0.34, 0.772])

+   9. D B A C F E G and A B C D E F G

+   10.

![](bbox=[0.25, 0.798, 0.28, 0.836])

+   11.

```
map<string, int> names;
names["one"] = 1; names["two"] = 2; names["three"] = 3; names["four"] = 4;
names["five"] = 5;
```

+   12.

```
for (map<string, int>::iterator pos = names.begin; pos != names.end(); pos++)
{
}
```