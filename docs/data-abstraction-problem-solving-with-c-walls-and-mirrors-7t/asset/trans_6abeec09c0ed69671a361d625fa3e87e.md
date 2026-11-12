

**图 21-8 哈希索引文件**

![](img/288a0c22d14d2450c1e772f228f867b0_678_0.png)

说明。（在许多应用中，数组表本身非常大，以至于你必须将其保存在外部存储中——例如，保存在索引文件的前 K 个块中。为了避免这个额外细节，你可以在此假设数组表是一个内部数组。）

与每个条目 table[i] 关联的是索引文件块的一个链式结构，如图 21-8 所示。table[i] 的链式结构中的每个块包含索引记录，其键（因此其对应的数据记录的搜索键）哈希到位置 i。要形成这些链式结构，你必须在每个块中为块指针保留空间——即链中下一个块的整数块编号，如图 21-9 所示。也就是说，在这个链式结构中，指针是整数，而不是 C++ 指针。指针值 -1 用作空指针。

## 外部哈希下的索引文件检索

检索操作的伪代码如下：

```
// Searches the data file for the record whose search key equals searchKey.
// Returns the record if found, else throws NotFoundException.
getItem(indexFile: File, dataFile: File,
        searchKey: KeyType): ItemType
```

**图 21-9 带指针的单个块**

![](img/288a0c22d14d2450c1e772f228f867b0_678_1.png)

```
// Apply the hash function to the search key
i = h(searchKey)
// Find the first block in the chain of index blocks -
// these blocks contain index records that hash into location i
p = table[i]
// if p == -1, no values have hashed into location i
if (p == -1)
    buf.readBlock(indexFile, p)
// Search for the block with the desired index record
while (p != -1 and buf does not contain an index record whose key value equals searchKey)
{
    p = number of next block in chain
    // if p equals -1, you are at the last block in the chain
    if (p == -1)
        buf.readBlock(indexFile, p)
}
// Retrieve the data item if present
if (p == -1)
{
    // buf.getRecord(j) is the index record whose key value equals searchKey
    blockNum = number of the data-file block to which buf.getRecord(j) points
    data.readBlock(dataFile, blockNum)
    Find data.getRecord(k) whose search key equals searchKey
    return data.getRecord(k)
}
else
    throw NotFoundException
```

## 外部哈希下的索引文件插入

外部哈希的插入和删除操作版本也与内部哈希版本相似。主要区别在于，在外部环境中，你必须同时插入或删除一条数据记录及其对应的索引记录。

要插入一条搜索键为 searchKey 的新数据记录，请执行以下步骤：

- 1. 将数据记录插入数据文件。由于数据文件是无序的，新记录可以放在你想要的任何位置。如果之前的删除操作在数据文件中间留下了一个空闲槽，你可以将其插入其中。如果没有空闲槽，则将新数据记录插入最后一个块的末尾，或者，如果必要，在数据文件末尾追加一个新块并将记录存储在那里。无论哪种情况，都让 p 表示包含此新数据记录的块的编号。

- 2. 将相应的索引记录插入索引文件。你需要向索引文件插入一个键值为 searchKey 且指针值为 p 的索引记录。（回顾，p 是你在其中插入新数据记录的数据文件块的编号。）由于索引文件是哈希的，你首先对 searchKey 应用哈希函数，令 i = h(searchKey)

然后，你将索引记录 <searchKey, p> 插入条目 table[i] 指向的块链中。你可以将此记录插入链中包含空闲槽的任何块中，或者，如果必要，可以分配一个新块并将其链接到链的开头。

## 外部哈希下的索引文件删除

要删除搜索键为 searchKey 的数据记录，请执行以下步骤：

- 1. 在索引文件中搜索相应的索引记录。你对 searchKey 应用哈希函数，令 i = h(searchKey)

然后，你搜索条目 table[i] 指向的索引块链，查找键值等于 searchKey 的索引记录。如果找不到这样的记录，你可以得出结论：数据文件不包含搜索键等于 searchKey 的记录。但是，如果你找到索引记录 <searchKey, p>，则在记下块编号 p 后将其从索引文件中删除，该块编号指示了在数据文件中可以找到要删除的数据记录的位置。

- 2. 从数据文件中删除数据记录。你知道数据记录位于数据文件的块 p 中。你只需访问此块，在块中搜索该记录，删除该记录，并将块写回文件。

请注意，对于 getItem、add 和 remove 等每个操作，块访问次数都非常低。你永远不需要访问超过一个数据文件块，最坏情况下，你需要访问索引文件沿单个哈希链的所有块。你可以采取措施，使每个链的长度保持相当短（例如，一两个块长），这与内部哈希的情况一样。你应该使数组表的大小足够大，以使链的平均长度接近一个块，并且哈希函数应将键均匀分散。如果必要，你甚至可以使用下一节中描述的技术，将每个链结构化为外部平衡搜索树。

当你需要在大型外部字典上执行检索、插入和删除操作时，哈希实现是首选。然而，与内部哈希的情况一样，此实现不适用于某些其他操作，例如有序遍历、检索最小或最大项，以及需要有序数据的范围查询。当将这些类型的操作添加到基本字典操作时，你应该使用搜索树实现而不是哈希。

## 为基本字典操作选择外部哈希

## 将索引文件组织为外部 2-3 树

## 21.3.3 B 树

搜索外部字典的另一种方法是将其组织为平衡搜索树。正如你可以将外部哈希应用于索引文件一样，你可以将索引文件（而非数据文件）组织为外部搜索树。此处开发的实现是第 19 章中 2-3 树的推广。

你可以通过使用块编号作为子指针，将外部文件的块组织成树结构。例如，在图 21-10a 中，块被组织成一棵 2-3 树。文件的每个块都是树中的一个节点，包含三个子指针，每个子指针都是子节点的整数块编号。子指针值 -1 扮演空指针的角色，因此，例如，叶节点将包含三个值为 -1 的子指针。

如果将索引文件组织为 2-3 树，则每个节点（索引文件的块）将包含一条或两条索引记录，每条记录的形式为 <key, pointer>，以及三个子指针。索引记录的指针部分与索引文件的树结构无关；指针指示数据文件中包含搜索键等于 key 的数据记录的块。（参见图 21-10b。）为了避免混淆，索引文件树结构中的指针将被称为子指针。

**图 21-10 (a) 组织为 2-3 树的块；(b) 2-3 树的单个节点**

![](img/288a0c22d14d2450c1e772f228f867b0_681_0.png)

你必须在树中组织索引记录，使其键遵循与内部 2-3 树相同的搜索树排序属性。这种组织使你可以按以下方式检索具有给定搜索键值的数据记录：

```
// Searches the data file for the record whose search key equals searchKey.
// Returns the record if found, else throws NotFoundException.
// rootNum is the block number (of the index file) that contains the root of the tree.
getItem(indexFile: File, dataFile: File, rootNum: integer,
    searchKey: KeyType): ItemType {
    if (no blocks are left in the index file to read)
        throw NotFoundException
    else {
        // Read from index file into internal array buf the block that contains the root of the 2-3 tree
        buf.readBlock(indexFile, rootNum)
        // Search for the index root whose key value equals searchKey
        if (searchKey is in the root) {
            blockNum = number of the data-file block that index record specifies
            data.readBlock(dataFile, blockNum)
            Find data.getRecord(k) whose search key equals searchKey
            return data.getRecord(k)
        }
    }
```

