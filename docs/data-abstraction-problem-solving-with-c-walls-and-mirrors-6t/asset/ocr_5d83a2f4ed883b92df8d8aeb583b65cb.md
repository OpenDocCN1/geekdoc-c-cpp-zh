# FIGURE 21-15 (a through e) The steps for removing 73 ; (f) removing the root (continued)

![](bbox=[0.25, 0.13, 0.85, 0.61])

+   2. Remove the data record from the data file. Prior to removing the index record, you noted the value of p of its pointer. Block p of the data file contains the data record to be removed. Thus, you simply access block p, remove the data record, and write the block back to the file. The high-level pseudocode for the insertion and removal algorithms parallels that of the 2-3 tree and is left as an exercise.

> Accessing only the search key of each record, but not the data file

# 21.3.4 Traversals

Now consider the operation traverse in sorted order, which is one of the operations that hashing does not support at all efficiently. Often an application requires only that the traversal display the search keys of the records. If such is the case, the B-tree implementation can efficiently support the operation, because you do not have to access the data file. You can visit the search keys in sorted order by using an inorder traversal of the B-tree, as follows:

```
// Traverses in sorted order an index file that is organized as a B-tree of degree m.
// blockNum is the block number of the root of the B-tree in the index file.
```