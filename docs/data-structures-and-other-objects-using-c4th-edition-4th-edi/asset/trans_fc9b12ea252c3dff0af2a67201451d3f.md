
我们可以将此示例推广，使串行搜索的平均运行时间表示为一个表达式，其中表达式的一部分是数组的大小。使用 n 作为数组的大小，平均运行时间的表达式为

(1 + 2 + ... + n) / n = (n(n + 1)/2) / n = (n + 1) / 2

该公式中的第一个等式是根据第 19 页开发的公式得出的。我们可以总结串行搜索的平均运行时间：

## 串行搜索的平均运行时间

对于包含 n 个元素的数组，串行搜索查找数组中存在的元素的平均运行时间需要 (n + 1) / 2 次数组访问。

你可能已经注意到，最坏情况运行时间和平均运行时间都是 O(n) 表达式；尽管如此，平均情况大约是最坏情况的一半时间。

最佳情况

衡量运行时间的第三种方法称为最佳情况运行时间，正如其名称所示，它采用尽可能乐观的视角。最佳情况运行时间定义为特定输入大小下所有运行时间中的最小值。对于串行搜索，当目标位于数组前端时出现最佳情况，只需要一次数组访问：

## 串行搜索的最佳情况运行时间

对于包含 n 个元素的数组，串行搜索的最佳情况运行时间仅为一次数组访问。

除非最佳情况行为发生的概率很高，否则在分析中通常不使用最佳情况运行时间。

## 二分查找

串行搜索易于实现、易于分析，如果你只搜索几次小数组，使用它也没问题。但是，如果搜索算法会反复使用，寻找更快的算法是值得的。有时可以使用速度快得多的搜索算法。这种称为二分查找的算法仅在数组已排序时才可使用。以下是三个适用二分查找的示例：

- 搜索整数数组，其中数组从最小整数（在前端）排序到最大整数（在数组末尾）。
- 搜索字符串数组，其中字符串按字母顺序排序。
- 搜索数组，其中每个组件是包含汽车零件信息的对象，并且数组按“零件编号”从小到大排序。

为了具体起见，我们将针对这三种情况中的第一种（搜索已排序的整数数组）开发该算法，但请记住，相同的算法适用于任何其他类型的已排序数组。

我们的整数版本二分查找将使用名为 search 的函数实现。search 的原型需要六个参数。前三个参数提供数组本身、我们正在搜索的数组部分的起始索引以及要搜索的元素数量。第四个参数是我们正在搜索的目标。例如，考虑：

```
search(b, 17, 10, 42, ...
```

此示例显示了搜索数字 42 所需的前四个参数，该数字出现在从 b[17] 到 b[26] 的 10 个元素中的某个位置。

第五个和第六个参数是引用参数，用于返回搜索结果。第五个参数是布尔值，指示是否找到了目标。如果找到了目标，则第六个参数指示目标在数组中出现的索引。以下是原型：

```
void search(
    const int a[],
    size_t first,
    size_t size,
    int target,
    bool& found,
    size_t& location
);
// Precondition: The array segment starting at a[first] and containing size
// elements is sorted from smallest to largest.
// Postcondition: The array segment starting at a[first] and containing size
// elements has been searched for the target. If the target was present,
// then found is true, and location is set so that target == a[location].
// Otherwise found is set to false.
```

## 二分查找—设计

让我们制定一个算法来执行此搜索任务。以具体的方式可视化问题会有所帮助。假设数字列表是一份无效信用卡号码列表，它很长，需要一本书才能列出所有号码。事实上，无效信用卡号码就是以这种方式分发给没有

## 图 12.2 二分查找函数

## 函数实现

```
void search(
    const int a[],
    size_t first,
    size_t size,
    int target,
    bool& found,
    size_t& location
)
// Precondition: The array segment starting at a[first] and containing size elements is sorted
// from smallest to largest.
// Postcondition: The array segment starting at a[first] and containing size elements has been
// searched for the target. If the target was present, then found is true, and location is set so
// that target == a[location]. Otherwise, found is set to false.
// Library facilities used: cstdlib (provides size_t from namespace std)
{
    size_t middle;
    if (size == 0)
        found = false;
    else
    {
        middle = first + size/2;
        if (target == a[middle])
        {
            location = middle;
            found = true;
        }
        else if (target < a[middle])
        {
            // The target is less than a[middle], so search before the middle.
            search(a, first, size/2, target, found, location);
        }
        else
        {
            // The target must be greater than a[middle], so search after the middle.
            search(a, middle+1, (size-1)/2, target, found, location);
        }
    }
}
```

search(b, 2, 5, 42, ...) 的示例结果，当 b 包含

| -7 | 3 | 8 | 39 | 42 | 63 | 70 |
|---|---|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] | [5] | [6] |

found 将被设置为 true；Location 将被设置为 4。

无法使用计算机。如果你是一名店员，有人递给你一张信用卡，你必须检查它是否在列表中，因此无效。你会怎么做？把书翻到中间，看看是否在那里。如果不在那里且比中间的数字小，则向书的开头方向查找。如果比中间的数字大，则向书的后面方向查找。这个想法产生了我们算法的第一个草稿：

```
if (size == 0)
    found = false;
else
{
    middle = index of the approximate midpoint of the array segment;
    if (target == a[middle])
        the target has been found at a[middle];
    else if (target < a[middle])
        search for the target in the area before the midpoint;
    else if (target > a[middle])
        search for the target in the area after the midpoint;
}
```

为“搜索较小列表”的两个子步骤使用递归调用是很自然的，我们的实现也将如此。与任何递归函数一样，我们必须确保函数终止，而不是产生无限递归。这种保证来自这样一个观察：每个递归调用搜索一个更短的列表，当列表长度达到零时，就不会有进一步的递归调用。这种推理可以像第 9 章中那样形式化（参见第 466 页的“确保没有无限递归”）。使用第 9 章的技术，我们可以看到参数 size 是一个有效的变体表达式，阈值为零。换句话说，size 参数在每个递归调用中至少减少一，当 size 达到零时，就不会有进一步的递归。

伪代码的完整实现如图 12.2 所示。

## 二分查找实现中的常见索引错误

二分查找和类似的基于数组的算法因涉及数组索引的错误而臭名昭著。这里列出了两个最常见的问题：

为递归调用计算数组的大小。图 12.2 中的实现有两个递归调用。仔细检查递归调用中正在搜索的数组段大小的表达式非常重要。例如，其中一个递归调用搜索 a[middle] 之前的段。该段从 a[first] 开始，一直到（但不包括）a[middle]。这个段中有多少个条目？答案是 middle - first，根据这个计算，它与 size/2 相同：
