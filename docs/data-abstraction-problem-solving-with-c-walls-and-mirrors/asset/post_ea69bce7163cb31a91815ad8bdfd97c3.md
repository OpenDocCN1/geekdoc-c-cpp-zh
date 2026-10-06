
# 656 CHAPTER 21 Processing Data in External Storage

```cpp
// Else search the appropriate subtree
if (the root is a leaf)
    throw NotFoundException
else
{
    child = block number of appropriate subtree
    return getItem(indexFile, dataFile, child, searchKey)
}
```

You can also perform insertions and removals in a manner that is even more suitable for the internal version, with the addition that you must insert records into and remove records from both the index file and the data file (as was the case in the external hashing scheme described earlier). In the course of insertions into and removals from the index file, you must split and merge nodes of the tree as you do for the internal version. You perform insertions into and removals from the data file—which, is not ordered in any way—exactly as described for the external hashing implementation. You can thus generalize the dictionary operations fairly well using an external version of the 2-tree.

## External 2-3 tree is adequate, but an improvement is possible 

However, you can generalize the 2-tree to a structure that is even more suitable for external environment. Recall the discussion in Chapter 19 about search trees whose nodes can have many children. Adding more children per node reduces the height of the search tree but increases the number of comparisons at each node.

In an external environment, however, the advantage of keeping a search tree far out outweighs the disadvantages of performing extra work at each node. As you traverse the tree you must perform a block access for each node. Because the time required to access a block of an external file is, in general, far greater than the time to process the data in a block once it has been, the overriding concern is to reduce the number of block accesses required. This implies that you should attempt to reduce the height of the tree, at the expense of requiring more comparisons at each node. In an external search tree, you should allow each node to have as many children as possible, with only the block as a limiting factor.

### Keep an external search tree

How many children can a block of fixed size accommodate? If a node is to have m children clearly you must be able to fit m pointers in the node. In addition to child pointers, the node must also contain index records. Before you answer the question of how many children a block can accommodate, you must first consider the following question: If a node N in a search tree has many children, well how many records—must it contain?

### Binary search tree: the number of records and children per node

In a binary search tree, if the node N has two children, it must contain one key value, as Figure 21-1a indicates. You can find that the key value of N is between the two keys in its subtree—all of the keys in its left subtree are less than N's key value, and all of the key values in its right subtree are greater than N's key value. When searching, you use the greater key value, the key value in N which you tell branch to.

### 2-3 tree: the number of records and children per node

Similarly, if a node N in a 2-3 tree has three children, it must contain two values (See Figure 21-1b). These two values separate the keys in N's three subtrees—all of the keys in the left subtree are less than N's key value, all of the key values in N's middle subtree are less than N's key value, and all of the key values in its right subtree are greater than N's key value. Unlike a binary search tree, this requires an algorithm to know which branch to take at any node.

### General search tree: the number of records and children per node

In general, if a node N in a search tree has m children, it must contain m-1 values to separate the keys in its subtrees correctly (See Figure 21-1c). Suppose you denote the nodes of N as $S_0, S_1$, and so on to $S_{m-1}$ (with the key values in N as $K_1, K_2, \dots$ and so on to $K_{m-1}$). The keys in N must separate the values in its subtrees as follows: $K_1 < K_2 < \dots < K_{m-1}$.

![](img/d0cb86b2f18b2db569968ad7c743510e_682_0.png)

# FIGURE 21-11 (a) A node with two children; (b) a node with three children; (c) a node with m children

![](img/d0cb86b2f18b2db569968ad7c743510e_683_0.png)
![](img/d0cb86b2f18b2db569968ad7c743510e_683_1.png)
![](img/d0cb86b2f18b2db569968ad7c743510e_683_2.png)

- All the values in subtree $S_0$ must be less than the key value $K_1$.
- For all $i, 1 \le i \le m-2$, all the values in $S_i$ must lie between the key values $K_i$ and $K_{i+1}$.
- All the values in subtree $S_{m-1}$ must be greater than the key value $K_{m-1}$.

If every node in the tree obeys property, you can search the tree using a generalized version of search retrieval algorithm as follows:

```cpp
// Searches the file for the record whose search key equals searchKey.
// Returns the key if found, else throws NotFoundException
getitem(indexFile: File, dataFile: File, rootNum: integer,
       searchKey: KeyType): ItemType
if (no blocks are left in the file to read)
    throw NotFoundException
else{
    // Read from file into internal array buf
    // block that contains the root of the tree
    buf.readBlock(indexFile, rootNum)
    // Search for the index key whose key value equals searchKey
    if (searchKey is one of the Ki in the root)
    {
        blockNum = number of data-file block that index record specifies
        data.readBlock(dataFile, blockNum)
        Find data record by.getRecord(k) whose search key equals searchKey
        return data.getRecord(k)
    }
    // Else search the appropriate subtree
else if (the root is a leaf)
    throw NotFoundException
```

### Retrieval with a general external search tree

```cpp
else
  Determine which subtree Si to search
    child = number of the root of Si
    return getitem(indexFile, dataFile, child, searchKey)
```

Now return to the question of how many children the nodes of the search tree can carry—that is, how big can m be? If you wish to organize the index file into a search tree, the items that you store in each node will be of the form <key, pointer>. Thus, if each node in the tree (which, recall, is a block of the index file) has m children, it must be large enough to accommodate m child-points and m - 1 records of the form <key, pointer>. You should choose m to be the largest integer such that m pointers (which, recall, are integers) and m - 1 records fit into a single block of the file. Actually, the algorithms are somewhat simplified if you choose an odd number for m. That is, you should choose m to be the odd integer such that m child pointers and m - 1 records can fit into a single block.

Ideally, then, you should structure the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search tree so that the external search-tree 2-3 tree is adequate, but an improvement is possible

Ideally, then, you should structure the external search tree so that the external search tree so that for example, Figure 21-12 shows a full tree whose nodes have five children. (Typically, a B-tree will be of a higher degree, but the diagrams would get out of hand!)

# 658 CHAPTER 21 Processing Data in External Storage

# FIGURE 21-12 (a) A node with two children; (b) a node with three children; (c) a node with m children

![](img/d0cb86b2f18b2db569968ad7c743510e_684_0.png)

# 685

# FIGURE 21-13 A B-tree of degree 

![](img/d0cb86b2f18b2db569968ad7c743510e_685_0.png)

A 2-3 tree is a B-tree of degree 3. Furthermore, the manner in which the B-tree insertion and removal algorithms maintain the structure of the tree is a direct generalization of the 2-3 tree's strategy of splitting and merging nodes. These algorithms are illustrated next by means of example. Suppose that the index file is organized into a B-tree of degree 5—that 5 is the maximum and 3 is the minimum number of children.

**Insert the record into the data file.** If you find block $b$ in the data file into you can insert the new record. As was with the external hashing implementation, block is either a block with a vacant slot or a new block.
**Insert a corresponding index record into the index file.** You now insert the index record $<55, p>$ into the index file, which is a B-tree of degree 5. The first step is to locate the leaf of the tree in this index record determining by which the search for 55 would terminate.

Suppose that this is the leaf $L$ shown in Figure 21-1a. Conceptually, you insert the new index record into $L$, causing it to contain five records (Figure 21-14b). Since a node can contain only four records, you must split $L$ into $L_1$ and $L_2$. With an analogous to the splitting of a node in a 2-3 tree, $L$ gets the two records with the smallest key values, $L_2$ gets the two records with the largest key values, and the record with the middle key value (56) is moved to the parent $P$ (See Figure 21-14c).

**Insertion into a B-tree.** To insert data with search 55 into the tree shown in Figure 21-13, you take the following steps:

- All leaves are at the same level.
- Each node contains between $m-1$ and $m/2$ records, and each internal node has one more than its parent. An exception to this rule is that the root of the tree can contain as as one record and have as as two children.

A 2-3 tree is a B-tree of degree 3. Furthermore, the manner in which the B-tree insertion and removal algorithms maintain the structure of the tree is a direct generalization of the 2-3 tree's strategy of splitting and merging nodes. These algorithms are illustrated next by means of example. Suppose that the index file is organized into a B-tree of degree 5—that 5 is the maximum and 3 is the minimum number of children an internal node—other than the root—can carry. (Typically, a B-tree will be of a higher degree, but the diagrams would get out of hand!)
