![](bbox=[0.22, 0.1, 0.78, 0.8])

In each case, we must sort the nodes and their children. Once we have the seven references n1, n2, n3, t1, t2, t3, and t4, the remainder of the procedure is straightforward. We build the replacement tree, change the reds to black, and subtract one from the color of the grandparent (which might be a double-black node when this function is called during node removal). If we find that we introduced another double-red violation, we continue fixing it. Eventually, the violation is removed, or we reach the root, in which case the root is simply colored black:

```
/**
Fixes a "double red" violation.
@param child the child with a red parent
*/
void RedBlackTree::fix_double_red(Node* child)
{
```