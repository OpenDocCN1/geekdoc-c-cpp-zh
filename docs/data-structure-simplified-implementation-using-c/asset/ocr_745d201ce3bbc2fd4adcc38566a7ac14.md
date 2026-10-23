![](bbox=[0.18, 0.12, 0.92, 0.55])

Figure 7-8: Pre-order traversal in a BST

# 7.4.3 Non-recursive traversal

We can also traverse in pre-order by using non-recursive approach. Traversal method in non-recursive method is not different with the one using the recursive approach. However, it is much more complex relative to the recursive approach defined earlier. In the non-recursive function, we initialize the pointer of root into the new pointer 'x'. To simplify our work, we can import the file that enumerates the dynamic stack defined in the stack chapter.

In the pre-order non-recursive approach, we use the stack to push the tree node explicitly. In this approach, we visit the node and move towards left by inserting the node into the stack. If the NULL is encountered, the node that is pushed at last is pop first. We set the flag as visited to avoid traversal again towards the left side. The node that is popped will be checked for the presence of right node, if the right side is present then it traverses towards the right. After visiting the right, there is possibility that it may have left node(s), consequently, the visit flag is set to false again- Now, traversal will continue towards left. This process will continue till the stack will not become empty. The entire function has been depicted in the following program.