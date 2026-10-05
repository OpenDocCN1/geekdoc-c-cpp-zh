
# 第 3 章：链表

- 1. 假设程序有一个指向链表最后一个元素的指针 `bottom`，以下伪代码显示了如何向链表末尾添加元素：

```
Cell: AddToEnd(Cell: bottom, Cell: new_cell)
bottom.Next = new_cell
new_cell.Next = null

// 返回新的底部
Return new_cell
```

该算法返回新的底部，这样调用代码就可以更新指向链表最后一个元素的变量。或者，你可以将 `bottom` 指针传入算法，以便算法对其进行更新。使用 `bottom` 指针不会改变向列表中添加元素或查找元素的算法。

移除元素的操作与之前相同，除非该元素位于链表的末尾，这时你需要更新 `bottom` 指针。通过指向被前元素的指针来实现这一点很容易。以下代码显示了移除最后一个元素的修改算法：

```
Cell: DeleteAfter(Cell: after, Cell: bottom)
// 如果被移除的是最后一个，更新 bottom。
If (after.Next.Next == null) Then bottom = after

// 移除目标单元
after.Next = after.Next.Next

// 返回最后一个单元
Return bottom
```

- 2. 以下伪代码显示了在单链表中查找最大单元的算法：

```
Cell: FindLargestCell(Cell: top)
// 如果链表为空，返回 null。
If (top.Next == null) Return null

// 移动到第一个数据的单元。
begin = top.Next

// 保存此单元及其值。
Cell: best_cell = top
Integer: best_value = best_cell.Value

// 移动到下一个单元。
top = top.Next
```

```
// 检查其他单元。
While (top != null)
  // 查看此单元的值是否更大。
  If (top.Value > best_value) Then
    best_cell = top
    best_value = top.Value
  End
```

```
// 移动到下一个单元。
top = top.Next
```

```While
  Return best_cell
FindLargestCell
```

- 3. 以下伪代码显示了在双向链表顶部添加元素的算法：

```
AddAtBeginning(Cell: top, Cell: new_cell)
  // 更新 Next 指针。
  new_cell.Next = top.Next
  top.Next = new_cell

  // 更新 Prev 指针。
  new_cell.Next.Prev = new_cell
  new_cell.Prev = top
AddAtBeginning
```

- 4. 以下伪代码显示了在双向链表底部添加元素的算法：

```
AddAtEnd(Cell: bottom, Cell: new_cell)
  // 更新 Prev 指针。
  new_cell.Next.Prev = bottom.Prev
  bottom.Prev = new_cell

  // 更新 Next 指针。
  new_cell.Prev.Next = new_cell
  new_cell.Next = bottom
AddAtEnd
```

- 5. `InsertCell` 算法将新单元应该插入之后的单元作为参数。所有的 `AddAtBeginning` 和 `AddAtEnd` 算法都需要向 `InsertCell` 传递适当插入单元。以下代码显示了这些算法：

```
AddAtBeginning(Cell: top, Cell: new_cell)
  // 在顶部哨兵之后插入。
  InsertCell(top, new_cell)
End AddAtBeginning

AddAtEnd(Cell: bottom, Cell: new_cell)
  // 在更改底部哨兵之前的单元插入。
  InsertCell(bottom.Prev, new_cell)
End AddAtEnd
```

- 6. 以下伪代码显示了一个从双向链表中删除指定单元的算法：

```
DeleteCell(Cell: target_cell)
// 更新下一个单元的 Prev 链接。
target_cell.Next.Prev = target_cell.Prev

// 更新前一个单元的 Next 链接。
target_cell.Prev.Next = target_cell.Next
DeleteCell
```

图 B-5 图形化地展示了这一过程。

![](img/fefa42765c0b410af6705110aea7c0cb_522_0.png)

图 B-5：要从双向链表中删除单元，更改下一个和前一个单元的链接以“绕过”目标单元。

- 7. 如果你寻找的名字更接近字母表的末尾，而不是从字母表开头开始，你可以从底部哨兵开始反向搜索链表。这不会改变 $O(N)$ 的运行时间，但如果名称分布均匀，在实践中可能会减少一半搜索时间。

- 8. 以下伪代码显示了在双向链表中插入单元的算法：

```
在双向链表中插入一个单元。
InsertCell(Cell: top, Cell: new_cell)
// 在它所属的位置之前插入。
While (top.Next.Value < new_cell.Value)
  top = top.Next
End While

// 更新 Next 链接。
new_cell.Next = top.Next

// 更新 Prev 链接。
new_cell.Prev = top
top = top
End InsertCell
```

该算法与用于单链表的算法相似，区别仅于更新 Prev 链接的行。

- 9. 以下伪代码确定链表是否有序：

```
Boolean: IsSorted(Cell: sentinel)
// 如果链表有 0 或 1 个单元，它是有序的。
If (sentinel.Next == null) Return true
If (sentinel.Next.Next == null) Return true

// 比较其他单元。
sentinel = sentinel.Next
While (sentinel.Next != null)
  // 比较此单元与下一个。
  If (sentinel.Value > sentinel.Next.Value) Then false
  // 移动到下一个单元。
  sentinel = sentinel.Next
End While

// 如果到达这里，链表是有序的。
Return true
End IsSorted
```

- 10. 插入获取输入列表第一个元素，然后在有序列表中找到它的位置。根据其值，元素有时位于开头，有时位于末尾。该算法总是搜索整个链表，除非新元素比列表中的所有元素都大。相比之下，选择排序必须搜索整个列表。与插入不同，它可以提前停止。

- 11.  List 程序可以在网站下载，提供了一种解决方案。

- 12. `TortoiseAndHare` 程序可以在网站下载，提供了一种 C 语言解决方案。

# 第 4 章：数组

- 1. 以下算法计算数组的方差：

```
Double: FindSampleVariance(Integer: array[])
  // 计算平均值。
  Integer: total = 0
  For i = 0 To array.Length - 1
    total = total + array[i]
  Next i
  Double: average = total / array.Length

  // 计算方差。
  Double: sum_of_squares = 0
  For i = 0 To array.Length - 1
    sum_of_squares = sum_of_squares + (array[i] - average)^2
  Next i
  Return sum_of_squares / array.Length
FindSampleVariance
```

- 2. 以下算法使用前面的算法计算标准差：

```
Integer: FindSampleDeviation(Integer: array[])
  // 计算样本方差。
  Double: variance = FindSampleVariance(array)
  // 返回标准差。
  Return Sqrt(variance)
FindSampleDeviation
```

- 3. 因为数组是有序的，中位数是数组中间的元素。有两个问题需要考虑：首先，你需要处理奇偶长度数组；其次，在计算中间元素的索引时需要小心，保持索引从 0 开始。

```
Double: Median(Integer: array[])
If (array.Length Mod 2 == 0) Then
  // 数组长度为偶数。
  // 返回两个中间元素的平均值。
  Integer: middle = array.Length / 2
  Return (array[middle - 1] + array[middle]) / 2
Else
  // 数组长度为奇数。
  // 返回中间元素。
  Integer: middle = (array.Length - 1) / 2
  Return array[middle]
End If
EndMedian
```

- 4. 以下伪代码从线性数组中移除一个元素：

```
RemoveItem(Integer: array[], Integer: index)
// 将元素向左移动 1 个位置以填充元素所在的位置。
For i = index + 1 To array.Length - 1
  Array[i - 1] = Array[i]
Next i

// 调整大小以移除最后一个条目。
<调整数组以删除末尾的 1 个元素>
EndRemoveItem
```

- 5. 在原始三角形类中，你真正需要更改的是使用行和列计算一维存储数组中索引的方法。以下伪代码显示了该方法：

```
Integer: FindIndex(Integer: r, Integer: c)
Return ((r - 1) * (r + 1) + (r - 1)) / 2 + c
EndIndex
```

以下伪代码显示了行和列交换后的版本：

```
Integer: FindIndex(Integer: r, Integer: c)
Return ((c - 1) * (c + 1) + (c - 1)) / 2 + r
EndIndex
```

- 6. $N \times N$ 数组中非空元素的行和列之间的关系是 $row + column < N$。你可以重构行和列到一维存储数组的方程，但更容易的方法是将行和列映射到符合原始左三角形排列的新行和列。你可以通过将 $r$ 替换为 $N - 1$ 来实现，如下伪代码所示：

```
Integer: FindIndex(Integer: r, Integer: c)
r = N - 1 - r
Return ((r - 1) * (r + 1) + (r - 1)) / 2 + c
EndIndex
```
