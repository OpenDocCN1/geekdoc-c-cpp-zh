```
template <typename Key, typename E>
TTNode<Key,E>* TTTree<Key, E>::
inserthelp(TTNode<Key,E>* rt, const Key k, const E e) {
    TTNode<Key,E>* retval;
    if (rt == NULL) // Empty tree: create a leaf node for root
        return new TTNode<Key,E>(k, e, EMPTYKEY, NULL,
            NULL, NULL, NULL);
    if (rt->isLeaf() ) // At leaf node: insert here
        return rt->add(new TTNode<Key,E>(k, e, EMPTYKEY, NULL,
            NULL, NULL, NULL));

    // Add to internal node
    if (k < rt->lkey) {
        retval = inserthelp(rt->left, k, e);
        if (retval == rt->left) return rt;
        else return rt->add(retval);
    }
    else if((rt->rkey == EMPTYKEY) || (k < rt->rkey)) {
        retval = inserthelp(rt->center, k, e);
        if (retval == rt->center) return rt;
        else return rt->add(retval);
    }
    else { // Insert right
        retval = inserthelp(rt->right, k, e);
        if (retval == rt->right) return rt;
        else return rt->add(retval);
    }
}
```

# Figure 10.15 The 2-3 tree insert routine.

placed virtually all large-file access methods other than hashing. B-trees, or some variant of B-trees, are the standard file organization for applications requiring insertion, deletion, and key range searches. They are used to implement most modern file systems. B-trees address effectively all of the major problems encountered when implementing disk-based search trees:

+   1. B-trees are always height balanced, with all leaf nodes at the same level.
+   2. Update and search operations affect only a few disk blocks. The fewer the number of disk blocks affected, the less disk I/O is required.
+   3. B-trees keep related records (that is, records with similar key values) on the same disk block, which helps to minimize disk I/O on searches due to locality of reference.
+   4. B-trees guarantee that every node in the tree will be full at least to a certain minimum percentage. This improves space efficiency while reducing the typical number of disk fetches necessary during a search or update operation.

A B-tree of order m is defined to have the following shape properties:

+   - The root is either a leaf or has at least two children.
+   - Each internal node, except for the root, has between ⌈m/2⌉ and m children.