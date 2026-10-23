```
gp->right=rrotate (parent);
gp=lrotate (gp);
return gp;
}
```

If we consider the AVL tree given in the above figure 8.8, it has been observed that due to insertion of the node having the value 92 to the node 94. Its grandparent 90 has the balancing factor of 2 which is out of the tolerance limit. But when we considered the parent of 92, it has been observed that it is having the balance factor of -1. This indicates that the node is left heavy, so both are differently balanced AVL. In such cases, we have to give double rotation. Initially, the parent has to be given right rotation whereas the grandparent will be given left rotation after the first rotation only.

# 8.9.2 Inserting the elements in an AVL tree

Inserting the element(s) in the AVL tree is a complex procedure and requires a number of considerations. For instance, when the item is inserted in a balance tree, where the balance factor is ‘0’, in such cases the element inserted will not result in the imbalance of the AVL.

In case if the balance factor is already 1, in that case a number of probability will exist. Consequently, rotation if needed would be govern by the rule of the rotations already specified in the section 8.7

![](bbox=[0.21, 0.58, 0.88, 0.86])