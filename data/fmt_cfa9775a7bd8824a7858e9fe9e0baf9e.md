
进入`/path/to/xxx`目录，找到`xxx.json`。

`buf.readBlock(dataFile, i)`

```
将读取 `dataFile` 的第 $i$ 个块并放入对象中。该对象必须适应 `dataFile` 每个块包含的许多记录。例如，如果每个块包含 100 条员工记录，则至少容纳 100 条员工记录。该对象被称为**缓冲区**（buffer），它是数据从一个过程到另一个过程中临时存储的位置。
```

一旦系统将块读入 `buf`，程序就可以处理（例如检查或修改）缓冲区中的记录。此外，缓冲区中的记录只是 `dataFile` 记录的副本，如果程序修改了缓冲区中的记录，必须写回 `dataFile`，以便文件反映这些修改。语句

```
buf.writeBlock(dataFile, i)
```

将 `buf` 的内容写入 `dataFile` 的第 $i$ 个块。如果 `dataFile` 包含 $n$ 个块，语句

```
buf.writeBlock(dataFile, n + 1)
```

将向 `dataFile` 追加一个新块，因此文件可以动态增长，就像 C++ 文件可以这样做一样。再次注意，这些输入输出命令允许你读取和写入整个块。因此，即使你需要操作文件中的单个记录，也必须访问整个块。例如，假设你想给员工 Smith 加薪 1000 元。如果 Smith 的记录在块 $i$ 中（如何确定正确的块将在本章后面讨论），将执行以下步骤：

```
// 从 dataFile 将块 i 读取到缓冲区 buf
buf.readBlock(dataFile, i)
```

# 640 第 21 章 外部存储中的数据处理

包含搜索键为 "Smith" 的记录的末尾 `buf.getRecord(j)`

```java
// 增加 Smith 记录中的薪资部分
(buf.getRecord(j)).setSalary((buf.getRecord(j)).getSalary() + 1000)
```

```java
// 将修改后的块写回文件 dataFile
buf.writeBlock(datafile, 1)
```

写入一个数据块的时间通常比当该块数据进入计算机内部内存后对该数据进行操作所需的时间长得多。例如，你插入 `buf` 中每条记录所需的时间，可能比将一个块写入该块所需的时间还要短。因此，你应该减少所需的块数。在之前的伪代码中，你应该在写入文件之前，尽可能地处理 `buf` 中的大量记录。你不应该太关注数据块一旦读入内部内存后对其进行操作所需的时间。

### 减少对块的访问次数

有趣的是，包括 C++ 在内的几种编程语言拥有某些命令，让你看起来可以一次访问一条记录。通常情况下，系统在块级别执行输入和输出，并可能向程序隐藏了这一事实。例如，如果你的编程语言包含

```c
rec.readRecord(datafile, 1) // 将 datafile 中的第 i 条记录读入 rec 中。
```

系统会访问包含第 i 条记录的整个块。我们的输入输出模型相当合理地接近现实。

在外部数据管理应用中，块访问所需占据了所有其他因素。本章的其余部分将讨论如何对外部存储的数据进行排序和搜索。目标是减少所需的块访问。

**在考虑算法效率时，文件访问是主导因素**

## 21.2 在外部文件中进行排序

本节考虑以下对位于外部文件数据进行排序的问题：

### 一个排序问题

一个外部文件包含 1,600 条员工记录。你想按照社会安全号对这些记录进行排序。每个块包含 100 条记录，文件包含 16 个块 $B_1, \dots, B_{16}$。假设程序一次只能访问内部内存来管理约 300 条记录（三个块的内容）。

对文件排序听起来可能不是一项困难的任务，因为你已经在本书中见过排序算法了。然而，这里有一个根本的区别：文件太大，无法放入内部内存中。这一限制阻止了排序，因为之前介绍的排序算法假设所有要排序的数据都一次性在内部内存中处理（例如，它们都在一个数组中）。幸运的是，我们可以为修改后的归并排序取消这个假设。

归并算法的基础是，你可以将两个已排序的段（例如数据记录数组）合并成第三个已排序段，该段是前者的组合。例如，如果 $S_1$ 和 $S_2$ 是已排序的记录段，合并的第一步是比较

每个段的第一条记录，并选择排序键较小的那条记录。

![](img/d0cb86b2f18b2db569968ad7c743510e_666_0.png)

**视频笔记：排序文件数据**

> * 数据进入或离开缓冲区的速度与记录处理速度不同。（因此，两个进程之间的缓冲区可以补偿它们运行速度的差异。）

# 在外部文件中对数据排序 641

每个段的第一条记录。如果选择了来自 $S_i$ 的记录，下一步是比较 $S_i$ 的第二条记录和 $S_j$ 的第一条记录。这个过程一直持续直到所有记录考虑完毕。关键观察是，在任何一步中，合并都需要看越每个段的*前缘*。

如果你相应地修改了算法，这一观察可能需要一种适用于外部文件排序问题的归并排序。假设 1,600 条记录要在文件 $F$ 中进行排序，且你不允许访问该文件。你将使用两个工作文件 $F_1$ 和 $F_2$。算法结束时，其中一个文件将包含排序后的记录。该算法有两个阶段：阶段 1 排序每个块的记录，阶段 2 执行一系列归并。

**阶段 1。** 从 $F$ 读取一个块到内部内存，使用内部排序对其记录进行排序，并将排序后的块写入 $F_1$；在读取 $F$ 的下一个块之前完成。在处理完 $F$ 的 16 个块后，$F_1$ 中有了 16 个已排序的运行序列 $R_1, \dots, R_{16}$；也就是说，$F_1$ 包含 16 个块的记录，这些记录在内部已排序，如图 21-3a 所示。

**阶段 2。** 是一系列归并步骤。每个归并步骤将成对的排序运行合并以形成更大的排序运行，直到已排序运行的总数减半。如图 21-3b 所示，第一个

![](img/d0cb86b2f18b2db569968ad7c743510e_667_0.png)

# **图 21-3**

- (a) 文件 $F_1$ 中的 16 个已排序运行，每个一个块；(b) 文件 $F_2$ 中的 8 个已排序运行，每个两个块；(c) 文件 $F_3$ 中的 4 个已排序运行，每个四个块；(d) 文件 $F_2$ 中的 2 个已排序运行，每个八个块

![](img/d0cb86b2f18b2db569968ad7c743510e_667_1.png)

![](img/d0cb86b2f18b2db569968ad7c743510e_667_2.png)

![](img/d0cb86b2f18b2db569968ad7c743510e_667_3.png)

![](img/d0cb86b2f18b2db569968ad7c743510e_667_4.png)

# 第 21 章 外部存储中的数据处理

合并步骤将 $F_1$ 中的成对的已排序运行（$R_1$ 与 $R_2$，$R_3$ 与 $R_4$，$\dots，$R_{15}$ 与 $R_{16}$）合并，形成每个两个块长的排序运行，并写入 $F_2$。下一步将 $F_2$ 中的成对的已排序运行合并，形成每个四个块长的排序运行，并写入 $F_3$。下一步将 $F_3$ 中的成对的已排序运行合并，形成每个八个块长的排序运行，并写入 $F_4$。

**在阶段 2 中合并运行**

给定这一总体策略，你如何合并这些排序的运行？最后的合并将是排序后的文件。

# 644 第21 章

// 简化假设：未排序文件中的块数是 2 的精确幂次。
`externalMergesort(unsortedFileName: string, sortedFileName: string)`

将 `unsortedFileName` 与变量 `inFile` 关联
将 `sortedFileName` 与变量 `outFile` 关联

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

注意 `externalMergesort` 调用了 `blockSort` 和 `mergeFile`，而 `mergeFile` 又调用了 `mergeRuns`。这些函数的伪代码如下：

- 对文件中的每个记录块进行排序。
// 前置条件：文件变量 `inFile` 已与待排序的文件关联。
// 后置条件：与文件 `outFile` 关联的文件
// `outFile` 包含了 `inFile` 的块。每个块都已通过处理。
// 两个文件均已关闭。
// 调用：`readBlock` 和 `writeBlock` 以执行直接访问输入输出，
// 以及 `sortBuffer` 以对数组进行排序。
`blockSort(inFile: File, outFile: File, numberOfBlocks: integer)`

准备 `inFile` 输入
准备 `outFile` 输出

```
numberOfBlocks = 0
while (blocks in inFile 仍未处理完)
  numberOfBlocks++
  buffer.readBlock(inFile, numberOfBlocks)
sortArray(buffer) // 使用某种内部排序排序
  buffer.writeBlock(outFile, numberOfBlocks)
```

关闭 `inFile` 和 `outFile`

```
// 将块从一个文件合并到另一个文件。
// 前置条件：inFile 是一个外部文件，包含
// numberOfBlocks 个已排序的块，这些块按每组 runSize 个组织成运行（runs）。
// 后置条件：outFile 包含了 inFile 合并后的运行。
// 两个文件均已关闭。
// 调用：mergeRuns。
mergeFile(inFile: File, outFile: File, runSize: integer, numberOfBlocks: integer)
```

准备 `inFile` 输入
准备 `outFile` 输出

```
for (next = 1 to numberOfBlocks 步长 2 *runSize)
    // 不变性：outFile 中的运行是有序的
    mergeRuns(inFile, outFile, next)
```

关闭 `inputFile` 和 `outFile`

// 合并文件中的两个连续的运行记录。
// 前置条件：`fromFile` 是一个包含排序运行的外部文件，
// 已打开输入；`toFile` 是一个包含排序运行的外部文件
// 已打开输出；`start` 是 `fromFile` 上要合并的第一个
// 运行块编号，该运行包含 `size` 个块：
// 运行 1：从 `start` 到 `start + size - 1` 的块
// 运行 2：从 `start` 到 `start + (2 * size) - 1` 的块
// 后置条件：来自 `fromFile` 的合并运行已应用到
// `toFile`。文件保持打开状态。
`mergeRuns(fromFile: File, toFile: File, start: integer, size: integer)`

// 初始化运行 1 和运行 2 的缓冲区
`in1.readBlock(fromFile, 运行1 的第一个块)`
`in2.readBlock(fromFile, 运行2 的第一个块)`

// 一直合并直到其中一个运行结束。每当
// 输入缓冲区耗尽时，就会读取下一个块。
// 每当输出缓冲区满时，就会进行写入。
```
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
```

// 断言：两个运行中恰好有一个完成
// 将未完成的输入缓冲区剩余部分
// 追加到输出缓冲区并写入
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

## 21.3 外部字典

![](img/d0cb86b2f18b2db569968ad7c743510e_672_0.png)

本节将讨论了在外部存储中组织记录的技术，以便能够高效地执行 ADT 字典操作，如检索、插入、删除和遍历。虽然这些讨论仅触及该主题的表面，但你已经有了基础：两个最重要的外部字典实现是哈希和 2-3 树的变体，你在第 18 章和第 19 章中学习过它们。

### 简单的外部字典实现：按搜索键顺序存储记录

假设你有一个直接访问文件，其中的记录将作为字典项。该文件被划分为块，正如本章前面描述的那样。最简单的字典实现之一是根据其搜索键存储记录，也许可以使用上一节中开发的外部合并排序算法对文件进行排序。一旦完成排序，你就可以以下算法轻松地按有序顺序遍历文件：

#### 有序遍历

```
// 按有序顺序遍历排序后的文件 dataFile；
// 为每个项目调用一次函数 visit
traverse(dataFile: file, numberOfBlocks: integer, recordsPerBlock: integer, visit: FunctionType)
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
// 如果找到则返回记录，否则抛出 NotFoundException。
getItem(dataFile: File, recordsPerBlock: integer, first: integer, last: integer, searchKey: KeyType): ItemType
if (first > last 或 dataFile 没有可读内容)
    throw NotFoundException
else {
    // 将 dataFile 的中间块读入数组 buf
    mid = (first + last) / 2
    buf.readBlock(dataFile, mid)
    if (searchKey < buf.get(0).getKey() && searchKey < buf.get(recordsPerBlock-1).getKey()) {
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
