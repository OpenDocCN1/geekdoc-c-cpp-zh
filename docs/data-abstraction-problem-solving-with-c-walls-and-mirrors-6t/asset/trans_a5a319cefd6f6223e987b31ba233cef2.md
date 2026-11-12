

// Else search the appropriate subtree
else if (the root is a leaf)
    throw NotFoundException
else
{
    child = block number of root of appropriate subtree
    return getItem(indexFile, dataFile, child, searchKey)
}

你也可以以与内部版本类似的方式执行插入和删除操作，但需要向索引文件和数据文件中插入记录并从中删除记录（如前面所述的外部哈希方案）。在向索引文件插入和删除记录的过程中，你必须像对待内部版本一样拆分和合并树的节点。你向数据文件插入和删除记录的方式——回顾，该文件以任何方式都不是有序的——与外部哈希实现中描述的完全相同。因此，你可以通过使用 2-3 树的外部版本相当好地支持字典操作。

### 外部 2-3 树已足够，但仍可改进

然而，你可以将 2-3 树推广为一种更适合外部环境的结构。回顾第 19 章中关于节点可以有多个子节点的搜索树的讨论。每个节点增加更多子节点会降低搜索树的高度，但在查找值时会增加每个节点的比较次数。

### 保持外部搜索树矮小

然而，在外部环境中，保持搜索树矮小的优势远大于在每个节点执行额外工作的劣势。在外部环境中遍历搜索树时，每访问一个节点都必须执行一次块访问。由于访问外部文件中一个块所需的时间通常远大于读取该块后处理其中数据所需的时间，因此首要关注点是减少所需的块访问次数。这一事实意味着，你应尽量降低树的高度，即使为此需要在每个节点进行更多比较。因此，在外部搜索树中，你应允许每个节点拥有尽可能多的子节点，仅以块大小作为限制因素。

固定大小的块可以容纳多少个子节点？如果一个节点要有 m 个子节点，显然你必须能在节点中容纳 m 个子指针。然而，除了子指针之外，节点还必须包含索引记录。在回答块可以容纳多少个子节点之前，你首先必须考虑这个相关问题：如果搜索树中的节点 N 有 m 个子节点，它必须包含多少个键值——以及因此多少个索引记录？

### 二叉搜索树：每个节点的记录数和子节点数

在二叉搜索树中，如果节点 N 有两个子节点，它必须包含一个键值，如图 21-11a 所示。你可以将节点 N 中的键值视为分隔 N 两个子树中键值的界限——N 左子树中的所有键值都小于 N 的键值，N 右子树中的所有键值都大于 N 的键值。在为给定键值搜索树时，N 中的键值会告诉你应该走哪个分支。

### 2-3 树：每个节点的记录数和子节点数

同样，如果 2-3 树中的节点 N 有三个子节点，它必须包含两个键值。（参见图 21-11b。）这两个值分隔 N 三个子树中的键值——左子树中的所有键值都小于 N 较小的键值，N 中间子树中的所有键值都介于 N 的两个键值之间，N 右子树中的所有键值都大于 N 较大的键值。与二叉搜索树一样，这一要求使搜索算法能够在任何给定节点知道应该走哪个分支。

### 通用搜索树：每个节点的记录数和子节点数

一般来说，如果搜索树中的节点 N 要有 m 个子节点，它必须包含 m - 1 个键值，以正确分隔其子树中的值。（参见图 21-11c。）假设你将 N 的子树表示为 S0、S1，依此类推到 Sm-1，并将 N 中的键值表示为 K1、K2，依此类推到 Km-1（且 K1 < K2 < ... < Km-1）。N 中的键值必须按以下方式分隔其子树中的值：

### 图 21-11 (a) 具有两个子节点的节点；(b) 具有三个子节点的节点；(c) 具有 m 个子节点的节点

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_683_0.png)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_683_1.png)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_683_2.png)

- 子树 S_i 中的所有值必须小于键值 K_i。
- 对于所有 i，1 <= i <= m - 2，子树 S_i 中的所有值必须介于键值 K_i 和 K_{i+1} 之间。
- 子树 S_{m-1} 中的所有值必须大于键值 K_{m-1}。

如果树中的每个节点都遵守这一属性，你可以使用搜索树检索算法的通用版本来搜索树，如下所示：

```
// Searches the data file for the record whose search key equals searchKey.
// Returns the record if found, else throws NotFoundException.
getItem(indexFile: File, dataFile: File, rootNum: Integer,
        searchKey: keyType): ItemType
    if (no blocks are left in the index file to read)
        throw NotFoundException
    else
    {
        // Read from index file into internal array buf the
        // block that contains the root of the tree
        buf.readBlock(indexFile, rootNum)
        // Search for the index record whose key value equals searchKey
        if (searchKey is one of the Ki in the root)
        {
            blockNum = number of the data-file block that index record specifies
            data.readBlock(dataFile, blockNum)
            Find data record whose search key equals searchKey
            return data.getRecord(k)
        }
        // Else search the appropriate subtree
        else if (the root is a leaf)
            throw NotFoundException
else
{
    Determine which subtree Si to search
    child = block number of the root of Si
    return getItem(indexFile, dataFile, child, searchKey)
}
}
```

### 使用通用外部搜索树进行检索

现在回到搜索树节点可以有多少个子节点的问题——也就是说，m 可以有多大？如果你希望将索引文件组织成搜索树，那么你在每个节点中存储的项目将是形式为 <key, pointer> 的记录。因此，如果树中的每个节点（回顾，它是索引文件的一个块）要有 m 个子节点，它必须足够大，以容纳 m 个子指针和 m – 1 个形式为 <key, pointer> 的记录。你应选择 m 为最大整数，使得 m 个子指针（回顾，它们是整数）和 m – 1 个 <key, pointer> 记录可以装入文件的一个块中。实际上，如果你始终为 m 选择奇数，算法会有些许简化。也就是说，你应选择 m 为最大奇整数，使得 m 个子指针和 m – 1 个索引记录可以装入一个块中。

因此，理想情况下，你应构建外部搜索树，使每个内部节点都有 m 个子节点（m 按上述方式选择），且所有叶节点位于同一层级，这与满树和 2-3 树的情况相同。例如，图 21-12a 显示了一个满树，其内部节点各有五个子节点。尽管此搜索树具有最小可能高度，但在面对插入和删除操作时，其平衡性过于难以维护。因此，你必须做出妥协。你仍可坚持要求搜索树的所有叶节点位于同一层级——即树是平衡的——但必须允许每个内部节点拥有介于 [m/2] + 1 个子节点之间。（[] 表示取最大整数。例如，[5/2] 为 2。）

### 图 21-12 (a) 内部节点各有五个子节点的满树；(b) 单个节点的格式

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_684_0.png)

