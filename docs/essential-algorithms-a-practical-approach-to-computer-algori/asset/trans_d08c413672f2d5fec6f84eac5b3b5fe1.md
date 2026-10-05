

# 第4章 数组 97

在一个有三行的三角形数组中，你已经知道如何计算那个数字了。

在目标条目 (3, 2) 之前的、且不属于完整行的条目位于该行中对应条目的左侧。在这个示例中，目标条目位于第 2 列，因此在这一行的左侧有两个条目。

通常情况下，第 $r$ 行第 $c$ 列条目的索引公式为 `((r - 1)^2 + (r - 1)) / 2 + c`。

有了这两个公式，处理三角形数组就变得简单。使用第一个公式 `(N² + N) / 2` 来确定为具有 $N$ 行的数组分配多少个元素。使用第二个公式 `((r - 1)² + (r - 1)) / 2 + c` 将行和列映射到一维数组中的索引，如下面的伪代码所示：

```
Integer: FindIndex(Integer: r, Integer c)
Return (r - 1) * (r - 1) / 2 + c
FindIndex
```

通过将三角形数组封装在一个类中，可以使其变得更容易。如果你能让该类的 `get` 和 `set` 方法处理索引，程序就可以像处理普通数组一样处理三角形数组对象。

细节在于三角形数组类如何处理对数组中不存在的条目的请求。例如，如果程序尝试访问位于数组缺失的上半部分的条目 (1, 4)，该类应该做什么？取决于具体的应用场景，你可能希望返回一个默认值、交换行和列并返回该值，或者抛出一个异常。

# 稀疏数组

如果你知道数组不会在其对角线之外存储值，三角形数组可以节省内存。如果你知道数组将包含 $f$ 个条目，你可能还可以节省更多的内存。

再次考虑一个航空公司连接矩阵，其 `[i, j]` 条目标记为 1，表示城市 $i$ 城市和城市 $j$ 之间有航班。该航空公司可能只有 600 条航班连接着 200 个城市。在这种情况下，一个包含 40,000 个条目的数组中只有 600 个非零值。如果航班是对称的（每条 $i-j$ 航班都有对应的 $j-i$ 航班），并且你用三角形数组存储连接性，那么数组总共 20,100 个条目中只有 300 个非零条目。该数组将有 99% 是未使用的。

稀疏数组通过不表示缺失的条目来节省更多内存。要获取项的值，程序会在数组中搜索该项。如果该项存在，程序返回其值。如果该项不存在，程序返回数组的默认值。（对于连接矩阵示例，默认值将为 0。）

# 第4章 数组

实现稀疏数组的一种方法是创建链表的链（嵌套列表）。第一个列表持有有关行的信息。该列表中的每个项都指向另一个链表，该链表持有数组中该行列条目的信息。

你可以使用两个单元类来构建稀疏数组——一个表示行的 `ArrayRow` 类和一个表示行中某个值的 `ArrayEntry` 类。

`ArrayRow` 存储一个行号、一个指向下一个 `ArrayRow` 的引用或指针，以及一个指向该行中第一个 `ArrayEntry` 的引用。下面显示了 `ArrayRow` 类的布局：

```
ArrayRow:
Integer: RowNumber
ArrayRow: NextRow
ArrayEntry: RowSentinel
```

`ArrayEntry` 类存储条目的列号、该条目为数组持有的任何值，以及指向该行中下一个 `ArrayEntry` 对象的引用。下面显示了 `ArrayEntry` 类的布局，其中 $T$ 是数组必须持有的数据类型：

```
ArrayEntry:
Integer: ColumnNumber
T: Value
ArrayEntry: NextEntry
```

为了方便添加和删除行，行列表可以以哨兵节点开始，每行的值列表也可以以哨兵节点开始。图 4-6 显示了带有阴影哨兵的稀疏数组。

为了更容易判断值是否在数组中缺失，`ArrayRow` 对象按 `RowNumber` 递增顺序存储。如果你在列表中搜索特定的行号，并发现一个 `RowNumber` 较小的 `ArrayRow` 对象，你就知道正在查找的行号在数组中。

同样，`ArrayEntry` 对象按 `ColumnNumber` 递增顺序存储。注意，图 4-6 中的 `RowEntry` 对象似乎是垂直对齐的，第一行的 `RowEntry` 对象可能代表相同的列。第一行的 `RowEntry` 对象和第二行的 `RowEntry` 对象可能代表列 -50。

图 4-6 中的排列看起来很复杂，但使用起来并不难。要找到特定项，向下查看行直到找到正确的行。然后横向查看该行的值列表直到找到你需要的列。如果没找到行或列，则该值不在数组中。

这种排列需要一些 `ArrayRow` 对象和哨兵节点，但如果数组是稀疏的，它仍然比三角形数组更高效。例如，在最坏情况下，三角形数组每行只包含一个值，而这种结构使用 $N+1$ 个 `ArrayRow` 对象和 $N$ 个 `ArrayEntry` 对象。在这些对象中，只有 $N$ 个包含实际值，其余都是哨兵。**图 4-6：** 如果每个列表都从哨兵开始，添加和删除单元将变得更容易。对于图 4-6 所示的数据结构，你仍然编写算法来：

1. 获取给定行和列的值，如果值不存在则返回默认值。
2. 在给定行和列设置值。
3. 删除给定行和列的值。

# 查找行或列

为了方便查找值，你可以定义以下 `FindRow` 方法。该方法找到目标行所在位置之前的 `ArrayRow` 对象。如果目标行不在数组中，该方法返回该行应该所在的 `ArrayRow`：

```
ArrayRow: FindRowBefore(Integer: row, ArrayRow: array_sentinel)
ArrayRow: array_row = array_sentinel
While (array_row.NextRow != null) And
(array_row.NextRow.RowNumber < row)
array_row = array_row.NextRow
End While
```

该算法将 `array_row` 设置为数组哨兵。然后反复移动 `array_row` 到列表中的下一个 `ArrayRow` 对象，直到下一个对象为空或下一个对象的 `RowNumber` 与目标行一样大。

如果下一个对象为空，程序已到达行列表末尾且未找到所需的行。如果该行存在，它应该位于当前 `array_row.object` 之后。

如果下一个对象的 `RowNumber` 等于目标行，算法找到了目标行。

如果下一个对象的 `RowNumber` 大于目标行，则目标行不在数组中。如果该行存在，它应该位于当前 `array_row.object` 之后。

同样，你可以定义 `FindColumnBefore` 方法来找到目标列所在位置之前的 `ArrayEntry` 对象。该方法接受目标列号和应搜索的行哨兵作为参数：

```
FindColumnBefore(Integer: column, ArrayEntry: row_sentinel)
ArrayEntry: array_entry = row_sentinel
While (array_entry.NextEntry != null) And
(array_entry.NextEntry.ColumnNumber < column)
array_entry = array_entry.NextEntry;
Return array_entry;
End FindColumnBefore
```

如果数组持有 $N$ 个 `ArrayRow` 对象，`FindRowBefore` 方法耗时为 $O(N)$。如果持有非默认值的行包含 $M$ 个此类项，`FindColumnBefore` 方法的运行时间为 $O(M)$。

