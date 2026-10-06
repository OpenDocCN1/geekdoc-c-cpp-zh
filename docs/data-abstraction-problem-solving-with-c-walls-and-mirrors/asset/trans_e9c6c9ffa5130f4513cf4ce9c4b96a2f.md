

# 644 第21 章

// 简化假设：未排序文件中的块数是 2 的精确幂次。
externalMergesort(unsortedFileName: string,
sortedFileName: string)

将 unsortedFileName 与变量 inFile 关联
将 sortedFileName 与变量 outFile 关联

```
// 阶段 1：按块计数对文件进行排序
blockSort(inFile, tempFile1, numberOfBlocks)
// 阶段 2：合并大小为 1, 2, 4, 8..., numberOfBlocks/2 的运行记录
// (使用两个临时文件和一个用于为每次合并保留文件的切换开关)
toggle = 1
for size = 1 through numberOfBlocks/2 (步长为 size)
  if (toggle == 1)
    mergeFile(tempFile1, tempFile2, size, numberOfBlocks)
  else
    mergeFile(tempFile2, tempFile1, size, numberOfBlocks)
    toggle = -toggle
```

```
// 将当前临时文件拷贝到 outFile
if (toggle == 1)
  copyFile(tempFile1, outFile)
else
  copyFile(tempFile2, outFile)
```

注意 externalMergesort 调用了 blockSort 和 mergeFile，而 mergeFile 又调用了 mergeRuns。这些函数的伪代码如下：

- 对文件中的每个记录块进行排序。
// 前置条件：文件变量 inFile 已与待排序的文件关联。
// 后置条件：与文件 outFile 关联的文件
// outFile 包含了 inFile 的块。每个块都已通过处理。
// 两个文件均已关闭。
// 调用：readBlock 和 writeBlock 以执行直接访问输入输出，
// 以及 sortBuffer 以对数组进行排序。
blockSort(inFile: File, outFile: File, numberOfBlocks: integer)

准备 inFile 输入
准备 outFile 输出

```
numberOfBlocks = 0
while (blocks in inFile 仍未处理完)
  numberOfBlocks++
  buffer.readBlock(inFile, numberOfBlocks)
sortArray(buffer) // 使用某种内部排序排序
  buffer.writeBlock(outFile, numberOfBlocks)
```

关闭 inFile 和 outFile

```
// 将块从一个文件合并到另一个文件。
// 前置条件：inFile 是一个外部文件，包含
// numberOfBlocks 个已排序的块，这些块按每组 runSize 个组织成运行（runs）。
// 后置条件：outFile 包含了 inFile 合并后的运行。
// 两个文件均已关闭。
// 调用：mergeRuns。
mergeFile(inFile: File, outFile: File,
    runSize: integer, numberOfBlocks: integer)

准备 inFile 输入
准备 outFile 输出

for (next = 1 to numberOfBlocks 步长 2 *runSize)
    // 不变性：outFile 中的运行是有序的
    mergeRuns(inFile, outFile, next)
关闭 inputFile 和 outFile

// 合并文件中的两个连续的运行记录。
// 前置条件：fromFile 是一个包含排序运行的外部文件，
// 已打开输入；toFile 是一个包含排序运行的外部文件
// 已打开输出；start 是 fromFile 上要合并的第一个
// 运行块编号，该运行包含 size 个块：
    // 运行 1：从 start 到 start + size - 1 的块
    // 运行 2：从 start 到 start + (2 * size) - 1 的块
// 后置条件：来自 fromFile 的合并运行已应用到
// toFile。文件保持打开状态。
mergeRuns(fromFile: File, toFile: File,
    start: integer, size: integer)

// 初始化运行 1 和运行 2 的缓冲区
in1.readBlock(fromFile, 运行1 的第一个块)
in2.readBlock(fromFile, 运行2 的第一个块)

// 一直合并直到其中一个运行结束。每当
// 输入缓冲区耗尽时，就会读取下一个块。
// 每当输出缓冲区满时，就会进行写入。
while (两个运行均未结束)
    // 不变性：out 和 toFile 中的每个块都是有序的
    选择 in1 和 in2 中较小的“前导边缘”，
    将其放入 out 的下一个位置
    if (out 是满的)
        out.writeBlock(toFile, toFile 的下一个块)
    if (in1 耗尽且运行 1 中仍有块)
        in1.readBlock(fromFile, 运行1 的下一个块)
    if (in2 耗尽且运行 2 中仍有块)
        in2.readBlock(fromFile, 运行2 的下一个块)

// 断言：两个运行中恰好有一个完成
// 将未完成的输入缓冲区剩余部分
// 追加到输出缓冲区并写入
```

```
while (in1 未耗尽)
// 不变性：out 是有序的
将 in1 的项放入 out 的下一个位置

while (in2 未耗尽)
// 不变性：out 是有序的
将 in2 的项放入 out 的下一个位置

out.writeBlock(toFile, toFile 的下一个块)
// 处理完剩余的完整块

while (运行 1 中仍有块)
  // 不变性：toFile 中的每个块都是有序的
  in1.readBlock(fromFile, 运行1 的下一个块)
  in1.writeBlock(toFile, toFile 的下一个块)


while (运行 2 中仍有块)
  // 不变性：toFile 中的每个块都是有序的
  in2.readBlock(fromFile, 运行2 的下一个块)
  in2.writeBlock(toFile, toFile 的下一个块)
```

# 21.3 外部字典

![](img/d0cb86b2f18b2db569968ad7c743510e_672_0.png)

本节将讨论了在外部存储中组织记录的技术，以便能够高效地执行 ADT 字典操作，如检索、插入、删除和遍历。虽然这些讨论仅触及该主题的表面，但你已经有了基础：两个最重要的外部字典实现是哈希和 2-3 树的变体，你在第 18 章和第 19 章中学习过它们。

### 简单的外部字典实现：按搜索键顺序存储记录

假设你有一个直接访问文件，其中的记录将作为字典项。该文件被划分为块，正如本章前面描述的那样。最简单的字典实现之一是根据其搜索键存储记录，也许可以使用上一节中开发的外部合并排序算法对文件进行排序。一旦完成排序，你就可以以下算法轻松地按有序顺序遍历文件：

#### 有序遍历

```
// 按有序顺序遍历排序后的文件 dataFile；
// 为每个项目调用一次函数 visit
traverse(dataFile: file, numberOfBlocks: integer,
        recordsPerBlock: integer, visit: FunctionType)
// 将 dataFile 的每个块读入缓冲区
for (blockNumber = 1; blockNumber <= numberOfBlocks)
  buf.readBlock(dataFile, blockNumber)
  // 访问块中的每个记录
  for (recordNumber = 1; recordNumber <= recordsPerBlock)
    visit buf.getRecord(recordNumber-1)
```

要在排序文件上执行检索，可以使用以下二分查找算法：

```
// 在 dataFile 中搜索
// 搜索键等于 searchkey 的记录
```

```
// 如果找到则返回记录，否则抛出 NotFoundException。
getItem(dataFile: File, recordsPerBlock: integer,
    first: integer, last: integer,
    searchKey: KeyType): ItemType

if (first > last 或 dataFile 没有可读内容)
    throw NotFoundException
else {
    // 将 dataFile 的中间块读入数组 buf
    mid = (first + last) / 2
    buf.readBlock(dataFile, mid)

    if (searchKey < buf.get(0).getKey() &&
        searchKey < buf.get(recordsPerBlock-1).getKey()) {
        // 找到了目标块
        // 在缓冲区 buf 中搜索键等于 searchKey 的 get(j)
        if (找到记录)
            return buf.get(j)
        else
            throw NotFoundException
    }
    // 搜索文件的另一部分
    else if (searchKey < buf.get(0).getKey())
        return getItem(dataFile, recordsPerBlock, mid-1, last, searchKey)
    else
        return getItem(dataFile, recordsPerBlock, mid+1, last, searchKey)
}
```

检索算法递归地平分文件并将中间块读入内部缓冲区。分割文件需要知道分段的起始和结束块。你会将这些值连同文件变量传递给 getItem。

这种 ADT 的外部实现与基于数组的内部实现非常不同。它具有许多相同的优点和缺点。它的主要优势是由于记录是顺序排序的，你可以使用二分查找来定位包含给定搜索键的块。该实现的主要缺点是

