
```cpp
template <typename Key, typename E>
E BPtree<Key, E>::findhelp(BPNode<Key,E>* rt, const Key k)
const {
	int currec = binaryle(rt->keys(), rt->numrecs(), k);
	if (rt->isLeaf())
		if (((BPLeaf<Key,E>* )rt)->keys())[currec] == k
			return ((BPLeaf<Key,E>* )rt)->recs(currec);
		else return NULL;
	else
		return findhelp(((BPInternal<Key,E>* )rt)->
		pointers(currec), k);
}
```

## Figure 10.19 Implementation for the B+-tree search method.

access to the actual record. To find a record with key value 33 in the B+-tree of Figure 10.18, search begins at the root. The value 33 stored in the root merely serves as a placeholder, indicating that keys with values greater than or equal to 33 are found in the second subtree. From the second child of the root, the first branch is taken to reach the leaf node containing the actual record (or a pointer to the actual record) with key value 33. Figure 10.19 shows a pseudocode sketch of the B+-tree search algorithm.

B+-tree insertion is similar to B-tree insertion. First, the leaf L that should contain the record is found. If L is not full, then the new record is added, and no other B+-tree nodes are affected. If L is already full, split it in two (dividing the records evenly among the two nodes) and promote a copy of the least-valued key in the newly formed right node. As with the 2-3 tree, promotion might cause the parent to split in turn, perhaps eventually leading to splitting the root and causing the B+-tree to gain a new level. B+-tree insertion keeps all leaf nodes at equal depth. Figure 10.20 illustrates the insertion process through several examples. Figure 10.21 shows a C++-like pseudocode sketch of the B+-tree insert algorithm.

To delete record R from the B+-tree, first locate the leaf L that contains R. If L is more than half full, then we need only remove R, leaving L still at least half full. This is demonstrated by Figure 10.22.

If deleting a record reduces the number of records in the node below the minimum threshold (called an underflow), then we must do something to keep the node sufficiently full. The first choice is to look at the node’s adjacent siblings to determine if they have a spare record that can be used to fill the gap. If so, then enough records are transferred from the sibling so that both nodes have about the same number of records. This is done so as to delay as long as possible the next time when a delete causes this node to underflow again. This process might require that the parent node has its placeholder key value revised to reflect the true first key value in each node. Figure 10.23 illustrates the process.

Figure 10.20 Examples of B⁺-tree insertion. (a) A B⁺-tree containing five records. (b) The result of inserting a record with key value 50 into the tree of (a). The leaf node splits, causing creation of the first internal node. (c) The B⁺-tree of (b) after further insertions. (d) The result of inserting a record with key value 30 into the tree of (c). The second leaf node splits, which causes the internal node to split in turn, creating a new root.

```cpp
template <typename Key, typename E>
BPNode<Key,E>* BPTree<Key, E>::inserthelp(BPNode<Key,E>* rt,
    const Key& k, const E& e) {
    if (rt->isLeaf() // At leaf node: insert here
        return ((BPLeaf<Key,E>*)rt)->add(k, e);
    // Add to internal node
    int currec = binaryle(rt->keys(), rt->numrecs(), k);
    BPNode<Key,E>* temp = inserthelp(
        ((BPInternal<Key,E>*)root)->pointers(currec), k, e);
    if (temp != ((BPInternal<Key,E>*)rt)->pointers(currec))
        return ((BPInternal<Key,E>*)rt)->
            add(k, (BPInternal<Key,E>*)temp);
    else
        return rt;
}
```

Figure 10.21 A C++-like pseudocode sketch of the B⁺-tree insert algorithm.

Figure 10.22 Simple deletion from a B⁺-tree. The record with key value 18 is removed from the tree of Figure 10.18. Note that even though 18 is also a placeholder used to direct search in the parent node, that value need not be removed from internal nodes even if no record in the tree has key value 18. Thus, the leftmost node at level one in this example retains the key with value 18 after the record with key value 18 has been removed from the second leaf node.

Figure 10.23 Deletion from the B⁺-tree of Figure 10.18 via borrowing from a sibling. The key with value 12 is deleted from the leftmost leaf, causing the record with key value 18 to shift to the leftmost leaf to take its place. Note that the parent must be updated to properly indicate the key range within the subtrees. In this example, the parent node has its leftmost key value changed to 19.

If neither sibling can lend a record to the under-full node (call it N), then N must give its records to a sibling and be removed from the tree. There is certainly room to do this, because the sibling is at most half full (remember that it had no records to contribute to the current node), and N has become less than half full because it is under-flowing. This merge process combines two subtrees of the parent, which might cause it to underflow in turn. If the last two children of the root merge together, then the tree loses a level. Figure 10.24 illustrates the node-merge deletion process. Figure 10.25 shows C++-like pseudocode for the B⁺-tree delete algorithm.

The B⁺-tree requires that all nodes be at least half full (except for the root). Thus, the storage utilization must be at least 50%. This is satisfactory for many implementations, but note that keeping nodes fuller will result both in less space required (because there is less empty space in the disk file) and in more efficient processing (fewer blocks on average will be read into memory because the amount of information in each block is greater). Because B-trees have become so popular, many algorithm designers have tried to improve B-tree performance. One method

![](img/7ea3c39173f146f675b63b146d1535f3_390_0.png)

![](img/7ea3c39173f146f675b63b146d1535f3_390_1.png)

![](img/7ea3c39173f146f675b63b146d1535f3_391_0.png)

![](img/7ea3c39173f146f675b63b146d1535f3_391_1.png)

Figure 10.24 Deleting the record with key value 33 from the B⁺-tree of Figure 10.18 via collapsing siblings. (a) The two leftmost leaf nodes merge together to form a single leaf. Unfortunately, the parent node now has only one child. (b) Because the left subtree has a spare leaf node, that node is passed to the right subtree. The placeholder values of the root and the right internal node are updated to reflect the changes. Value 23 moves to the root, and old root value 33 moves to the rightmost internal node.

```
/** Delete a record with the given key value, and
    return true if the root underflows */
template <typename Key, typename E>
bool BPTree<Key, E>::removehelp(BPNode<Key,E>* rt,
                                const Key& k) {
    int currec = binaryle(rt->keys(), rt->numrecs(), k);
    if (rt->isLeaf())
        if (((BPLeaf<Key,E>*)rt)->keys()[currec] == k)
            return ((BPLeaf<Key,E>*)rt)->del(currec);
        else return false;
    else // Process internal node
        if (removehelp(((BPInternal<Key,E>*)rt)->
                       pointers(currec), k))
            // Child will merge if necessary
            return ((BPInternal<Key,E>*)rt)->underflow(currec);
        else return false;
}
```

Figure 10.25 C++-like pseudocode for the B⁺-tree delete algorithm.

for doing so is to use the B⁺-tree variant known as the B*-tree. The B*-tree is identical to the B⁺-tree, except for the rules used to split and merge nodes. Instead of splitting a node in half when it overflows, the B*-tree gives some records to its neighboring sibling, if possible. If the sibling is also full, then these two nodes split into three. Similarly, when a node underflows, it is combined with its two siblings, and the total reduced to two nodes. Thus, the nodes are always at least two thirds full.²

## 10.5.2 B-Tree Analysis

The asymptotic cost of search, insertion, and deletion of records from B-trees, B⁺-trees, and B*-trees is Θ(log n) where n is the total number of records in the tree. However, the base of the log is the (average) branching factor of the tree. Typical database applications use extremely high branching factors, perhaps 100 or more. Thus, in practice the B-tree and its variants are extremely shallow.

As an illustration, consider a B⁺-tree of order 100 and leaf nodes that contain up to 100 records. A B⁺-tree with height one (that is, just a single leaf node) can have at most 100 records. A B⁺-tree with height two (a root internal node whose children are leaves) must have at least 100 records (2 leaves with 50 records each). It has at most 10,000 records (100 leaves with 100 records each). A B⁺-tree with height three must have at least 5000 records (two second-level nodes with 50 children containing 50 records each) and at most one million records (100 second-level nodes with 100 full children each). A B⁺-tree with height four must have at least 250,000 records and at most 100 million records. Thus, it would require an extremely large database to generate a B⁺-tree of more than height four.

The B⁺-tree split and insert rules guarantee that every node (except perhaps the root) is at least half full. So they are on average about 3/4 full. But the internal nodes are purely overhead, since the keys stored there are used only by the tree to direct search, rather than store actual data. Does this overhead amount to a significant use of space? No, because once again the high fan-out rate of the tree structure means that the vast majority of nodes are leaf nodes. Recall (from Section 6.4) that a full K-ary tree has approximately 1/K of its nodes as internal nodes. This means that while half of a full binary tree’s nodes are internal nodes, in a B⁺-tree of order 100 probably only about 1/75 of its nodes are internal nodes. This means that the overhead associated with internal nodes is very low.

We can reduce the number of disk fetches required for the B-tree even more by using the following methods. First, the upper levels of the tree can be stored in
