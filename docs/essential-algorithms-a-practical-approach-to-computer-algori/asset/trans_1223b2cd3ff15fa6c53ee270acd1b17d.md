

## 第 9 章 = 递归

```
For i = 0 To <selections 中的最大索引>
    result.Add(items[selections[i]])
Next i
results.Add(result)
Else
    // 获取用于下一次选择的最小值。
    Integer: start = 0 // 如果是第一个索引，则使用此值。
    If (index > 0) Then start = selections[index-1]

    // 进行下一次赋值。
    For i = start To <items 中的最大索引>
        将 i 加入选择中。
        selections[index] = i

    // 递归地进行其他选择。
    SelectKofWithDuplicates(index + 1, selections, items, results)
Next i
SelectKofWithDuplicates
```

该算法根据选择中项的索引来决定该递归调用应该设置哪个项。如果 index 为 2，则此对算法的调用将填充 selections[2]。

- selections 是一个数组，用于存储选择中项的索引。例如，如果 selections 包含两个项且其值为 2 和 3，则该选择包含了索引为 2 和 3 的项。
- items 是一个数组，选择应从中从中产生。
- results 是一个列表的列表，表示完整的选择。例如，如果一个选择是 [A, B, C, D]，results 包含一个包含 A、B 和 D 索引的列表。

当算法开始时，它会检查它应该做的选择中项的索引。如果此值大于 selections 数组的长度，则选择已完成，算法将其添加到 results 列表中。
如果选择未完成，算法会确定 items 数组中可以用于下一次选择的最小索引。如果此对算法的调用正在填充 selections 数组第一个位置，可以使用 items 数组中的任何值，因此 start 设置为 0。如果此调用没有设置选择中的第一个项，算法会将 start 设置为上一个被选值的索引。

例如，假设项为 [A, B, C, D, E]，且算法已经填充了第三个选择。假设前两个选择是索引为 0 和 2 的项，因此当前选择是 [A, C]。在这种情况下，算法将 start 设置为 3，因此它考虑下一个位置的索引为 3 或 4 的项。这使得它在该选择中从 D 和 E 挑选一个。

## 第 9 章 递归 213

这样设置 start 可以保持选择中项的顺序。在这个示例中，这意味着选择中的字母始终按字母顺序排列。它防止了算法选取两个如 [A, C, D] 和 [A, D, C] 的选择，它们是不同顺序的相同项。

设置好 start 后，算法从 start 循环到 items 数组的最后一个索引。对于这些值中的每一个，算法都会将该值放在 selections 数组中，并将相应的项添加到选择中，然后递归地调用自己为 selections 数组中的其他条目赋值。

## 不包含重复的选择

要产生不包含重复的选择，你只需要对上一个算法进行一处细微的修改。不要让 start 变量等于添加到 selections 数组的索引，而是将其设置为该索引加 1。这防止了算法再次选择相同的值。

接下来的伪代码显示了带有修改行的数算法：

```
// 生成允许重复的组合
SelectKofNWithoutDuplicates(Integer: index, Integer: selections[])
Data: items[], List<Data> results
 // 检查我们是否已经完成了最后赋值。
 If index == <selections 的长度> Then
 // 将结果添加到结果列表。
 List-Data = New List<Data>()
 For i = 0 To <selections 中的最大索引>
  Result.Add(items[selections[i]])
 Next i
 results.Add(result)
Else // 获取用于下一次选择的最小值。
 Integer: start = 0 // 如果是第一个索引，则使用此值。
 If (index > 0) Then start = selections[index-1] + 1

 // 进行下一次赋值。
 For i = start To <items 中的最大索引>
  将 i 加入选择中。
  selections[index] = i

  // 递归地进行其他选择。
  SelectKofWithoutDuplicates(index + 1, selections, items, results)
 Next i
 End If
```

该算法的工作与之前相同，但这次选择中的每个选项都必须在其上一个之后。例如，假设项为 {A, B, C, D}；算法已经为选择选择了 [A, B]，现在只考虑 B 之后的项，即 C 和 D。

## 包含重复的排列

生成重复项的算法与上一个非常相似。接下来的伪代码显示：

```
// 生成排列。
SelectKofWithDuplicates(Integer: index, Integer: selections[])
Data: items[], List<Data> results
 // 检查我们是否已经完成了最后赋值。
 If index == <selections 的长度> Then
 // 将结果添加到结果列表。
 List-Data = New List<Data>()
 For i = 0 To <selections 中的最大索引>
  Result.Add(items[selections[i]])
 Next i
 results.Add(result)
Else // 获取用于下一次选择的最小值。
 Integer: start = 0 // 如果是第一个索引，则使用此值。
 If (index > 0) Then start = selections[index-1]

 // 进行下一次赋值。
 For i = start To <items 中的最大索引>
  将 i 加入选择中。
  selections[index] = i

  // 递归地进行其他选择。
  SelectKofWithDuplicates(index + 1, selections, items, results)
 Next i
 End If
```

## 包含重复的排列计数

生成重复项的算法与上一个非常相似。假设我们正在对 items 进行 k 个的排列。对于第一个项，它可以选择任何项。对于第二个项，它可以选择任何剩余的 n-1 个项。在 k = n 的特殊情况下，该公式变为 n × (n - 1) × ... × (n+1) = n! 这是大多数人认为的排列数。

## 不包含重复的排列计数

要产生不包含重复的选择，你只需要对上一个算法进行一处细微的修改。不要让 start 变量等于添加到 selections 数组的索引，而是将其设置为该索引加 1。这防止了算法再次选择相同的值。

接下来的伪代码显示了带有修改行的算法：

```
// 生成允许重复的组合
SelectKofNWithoutDuplicates(Integer: index, Integer: selections[])
Data: items[], List<Data> results
 // 检查我们是否已经完成了最后赋值。
 If index == <selections 的长度> Then
 // 将结果添加到结果列表。
 List-Data = New List<Data>()
 For i = 0 To <selections 中的最大索引>
  Result.Add(items[selections[i]])
 Next i
 results.Add(result)
Else // 获取用于下一次选择的最小值。
 Integer: start = 0 // 如果是第一个索引，则使用此值。
 If (index > 0) Then start = selections[index-1] + 1

 // 进行下一次赋值。
 For i = start To <items 中的最大索引>
  将 i 加入选择中。
  selections[index] = i

  // 递归地进行其他选择。
  SelectKofWithoutDuplicates(index + 1, selections, items, results)
 Next i
 End If
```

## 移除递归

递归使得某些问题更容易理解。例如，汉诺塔问题的递归解决方案简单且优雅。
不幸的是，递归也有一些缺点。有时它会导致自然但效率下的解决方案。例如，生成斐波那契数的递归算法需要程序多次计算相同的值。这使得速度变慢，以至于计算 50 个以上是不现实的。
其他递归算法还会产生深层调用，并可能导致程序耗尽其栈调用。使用沃斯多夫启发式的骑士巡游展示了这个问题。该启发式可以在我的计算机上解决直到 57×57 的棋盘，但超过此范围它就会耗尽栈调用。
幸运的是，你可以采取一些措施来解决这些问题。接下来的章节描述了你可以用来重构或移除递归以提高性能的方法。

## 移除尾递归

尾递归发生在单递归算法在返回之前最后执行的操作是调用自己时。例如，考虑以下 Factorial 的实现：

```
Integer: Factorial(Integer: n)
  If (n == 0) Then Return 1
  Integer: result = n * Factorial(n - 1)
    Return result
```

End Factorial
```
