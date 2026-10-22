This function explicitly handles three cases: a node with no left child, a node with no right child, and a node with two children. A node with no children can be considered a special case of a node with no left child. If the node has no left child, the code assigns the address of the right child to the parent pointer. But if the node also has no right child, that pointer is NULL, which is the proper value for the no-child case.

Notice that the code uses a temporary pointer to keep track of the address of the deleted node. After the parent pointer (*ptr) is reset, the program would lose track of where the deleted node is, but you need that information for the free() function. So the program stores the original value of *ptr in temp and then uses temp to free the memory used for the deleted node.

The code for the two-child case first uses the temp pointer in a for loop to search down the right side of the left subtree for an empty spot. When it finds an empty spot, it attaches the right subtree there. Then it reuses temp to keep track of where the deleted node is. Next, it attaches the left subtree to the parent and then frees the node pointed to by temp.

Note that because ptr is type Trnode **, *ptr is of type Trnode *, making it the same type as temp.

# Deleting an Item

The remaining part of the problem is associating a node with a particular item. You can use the SeekItem() function to do so. Recall that it returns a structure containing a pointer to the parent node and a pointer to the node containing the item. Then you can use the parent node pointer to get the proper address to pass to the DeleteNode() function. The DeleteItem() function, shown here, follows this plan:

```
bool DeleteItem(const Item * pi, Tree * ptree)
{
    Pair look;

    look = SeekItem(pi, ptree);
    if (look.child == NULL)
        return false;

    if (look.parent == NULL)    /* delete root item    */
        DeleteNode(&ptree->root);
    else if (look.parent->left == look.child)
        DeleteNode(&look.parent->left);
    else
        DeleteNode(&look.parent->right);
    ptree->size--;

    return true;
}
```

First, the return value of the SeekItem() function is assigned to the look structure variable. If look.child is NULL, the search failed to find the item, and the DeleteItem() function quits,