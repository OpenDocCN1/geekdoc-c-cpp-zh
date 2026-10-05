# Sec. 10.5 B+-Trees

# 371

![](bbox=[0.209, 0.196, 0.753, 0.506])

Figure **10.20** Examples of B+-tree insertion. (a) A B+-tree containing five records, (b) The result of inserting a record with key value 50 into the tree of (a). The leaf nodes split, causing creation of the first internal node. (c) The B+-tree of after further insertions. (d) The result of inserting a record with key value 30 into the tree of (c). The second leaf node splits, which causes the internal node to split in turn, creating a new node.

```
template <typename Key, typename E>
BNode<Key, E>* BTree<Key, E>::insertleaf(BNode<Key, E>* rt, 
    const Key& k, const E& e) {
    if (rt->isLeaf()) // // at leaf node: insert here
        return ((BLeaf<Key, E>*)rt)->add(k, e);
    // add to internal node
    int currec = binarySearch(rt->keys(), rt->numrecs(), k);
    BNode<Key, E>* temp = inserthelp(
        ((BInternal<Key, E>*)root)->pointers(currec), k, e);
    if (temp != ((BInternal<Key, E>*)rt)->pointers(currec))
        return ((BInternal<Key, E>*)rt)->
            add(k, ((BInternal<Key, E>*)temp);
    else
        return rt;
    return rt;
}
```

Figure **10.21** A C++like pseudocode of the B+-tree insert algorithm.