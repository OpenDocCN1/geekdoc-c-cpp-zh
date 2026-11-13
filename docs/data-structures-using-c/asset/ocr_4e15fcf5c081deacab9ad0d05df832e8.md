```
else
{
    *pos = curr->count;
    while((newkey < curr->data[*pos]) && (*pos > 1))
    (*pos)--;
    if(newkey == curr->data[*pos])
    return 1;
    else
    return 0;
}
```

**Searching a B-tree** In Program Code 13.3, the `search()` function traverses the B-tree.

```
PROGRAM CODE 13.3
btnode * btree :: search(int newkey, btnode *root, int
*pos)
{
    if(!root)
    {
        return null;
    }
    else if(search_node(newkey, root, pos))
    return root;
    else
    return search(newkey, root->child[*pos], pos);
}
```

If a new key is present in it, then it returns the pointer to the node and the position of the new key in it; otherwise, it returns null.

# Inserting a key into a B-tree

Binary search trees grow at their leaves, but the B-trees grow at the root. The general method of insertion is as follows:

+   1. First, the new key is searched in the tree. If the new key is not found, then the search terminates at a leaf.
+   2. Attempt to insert the new key into a leaf.
+   3. If the leaf node is not full, then the new key is added to it and the insertion is finished.
+   4. If the leaf node is full, then it splits into two nodes on the same level, except that the median key is sent up the tree to be inserted into the parent node.