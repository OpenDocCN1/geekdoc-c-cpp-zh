# Deleting a Node

Now you can begin to plan the necessary functions, separating the job into two tasks. One is associating a particular item with the node to be deleted, and the second is actually deleting the node. One point to note is that all the cases involve modifying a pointer in the parent node, which has two important consequences:

+   - The program has to identify the parent node of the node to be deleted.
+   - To modify the pointer, the code must pass the address of that pointer to the deleting function.

We’ll come back to the first point later. Meanwhile, the pointer to be modified is itself of type Trnode *, or pointer-to-Trnode. Because the function argument is the address of that pointer, the argument will be of type Trnode **, or pointer-to-pointer-to-Trnode. Assuming you have the proper address available, you can write the deletion function as the following:

```
static void DeleteNode(Trnode **ptr)
/* ptr is address of parent member pointing to target node */
{
    Trnode * temp;

    if ( (*ptr)->left == NULL)
    {
        temp = *ptr;
        *ptr = (*ptr)->right;
        free(temp);
    }
    else if ( (*ptr)->right == NULL)
    {
        temp = *ptr;
        *ptr = (*ptr)->left;
        free(temp);
    }
    else   /* deleted node has two children */
    {
        /* find where to reattach right subtree */
        for (temp = (*ptr)->left; temp->right != NULL;
             temp = temp->right)
            continue;
        temp->right = (*ptr)->right;
        temp = *ptr;
        *ptr =(*ptr)->left;
        free(temp);
    }
}
```