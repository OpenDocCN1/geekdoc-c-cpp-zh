![](bbox=[0.2, 0.09, 0.8, 0.29])

**Figure 4.8** Unix directory with file sizes obtained via postorder traversal

```
int FileSystem::size() const
{
    int totalSize = sizeOfThisFile( );

    if( isDirectory( ) )
        for each file c in this directory ( for each child )
            totalSize += c.size( );

    return totalSize;
}
```

**Figure 4.9** Pseudocode to calculate the size of a directory

subdirectories (71) plus the one block used by /usr, for a total of 72. The pseudocode method size in Figure 4.9 implements this strategy.

If the current object is not a directory, then size merely returns the number of blocks it uses in the current object. Otherwise, the number of blocks used by the directory is added to the number of blocks (recursively) found in all the children. To see the difference between the postorder traversal strategy and the preorder traversal strategy, Figure 4.10 shows how the size of each directory or file is produced by the algorithm.

# 4.2 Binary Trees

A binary tree is a tree in which no node can have more than two children.

Figure 4.11 shows that a binary tree consists of a root and two subtrees, $T_L$ and $T_R$, both of which could possibly be empty.

A property of a binary tree that is sometimes important is that the depth of an average binary tree is considerably smaller than N. An analysis shows that the average depth is $O(\sqrt{N})$, and that for a special type of binary tree, namely the *binary search tree*, the average value of the depth is $O(\log N)$. Unfortunately, the depth can be as large as $N - 1$, as the example in Figure 4.12 shows.