

# C# 数组 111

doublesArray[0] // 对应 d0（即 5）
doubleArray[1] // 对应 d1（即 2）

数组的第 0 个元素对应 d0，第 1 个元素对应 d1，第 2 个元素对应 d2，依此类推。程序员通常将第 0 个元素称为 "doublesArray sub-0"，将第一个元素称为 "doublesArray sub-1"，依此类推。

数组的元素 — 0, 1, 2, ... 被称为**索引 (index)**。

在 C# 中，数组索引从 0 开始而不是从 1 开始。因此，你通常不会将索引处的元素称为第一个元素，而是称其为“起始”或“索引为 1 的元素”。**第一个元素是第 0 个元素。**如果你坚持使用普通口语，请注意第一个元素始终位于索引 0，第二个元素是索引 1。

如果不是数组的索引是一个变量，那么 `doublesArray` 变量也就没有改进了。使用 **for** 循环比手动编写每个元素要容易得多，正如这个程序所示的：

```csharp
// FixedArrayAverage -- 使用循环计算固定数字数组的平均值。
namespace FixedArrayAverage
{
    public class Program
    {
        public static void Main(string[] args)
        {
            double[] doublesArray = { 5, 2, 7, 3.5, 6.5, 8, 1, 9, 3 };
            // 将数组中的值累加到变量 sum。
            double sum = 0;
            for (int i = 0; i < 10; i++)
            {
                sum = sum + doublesArray[i];
            }
            // 计算平均值。
            double average = sum / 10;
            Console.WriteLine(average);
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
}
```

程序首先初始化变量 `sum` 为 0。然后遍历存储在 `doublesArray` 中的值，将每个值加到 `sum` 中。循环结束时，`sum` 累加了数组中所有值的总和。得到的总和除以元素个数，生成平均值。执行此程序的输出结果是预期的 4.6。（你可以用计算器检查一下。）

# 112 C# 数组

## 检查数组边界

幸运的是，前一节“固定值数组”中的 `FixedArrayAverage` 程序遍历了所有元素。但如果你没有正确地迭代循环怎么办？你有两种情况需要考虑：

```csharp
for (int i = 0; i < 11; i++)
```

当你执行该程序时，你会看到一个带有此错误消息的对话框：

**你遍历了九个元素：**  C# 并不认为这是一个错误。如果你想读取一个包含十个元素的数组的十一个个元素，C# 会给出什么不同的提示吗？显然，数组是不正确的，但程序并不知道。

*IndexOutOfRangeException: 索引超出数组边界（Index was outside the bounds of the array）。*

**你遍历了 11 个（更多）元素：** 现在 C# 非常在乎。它不允许你访问数组末尾之外索引，以免你可能覆盖内存中的重要值。要进行测试，请将 `FixedArrayAverage` 循环中的比较改为以下内容，将值 10 替换为 11：

起初，这个错误消息看起来并不妥当。然而，你可以很快掌握要领：显然，`IndexRangeException` 表明你尝试访问超出范围的数组 — 在一个包含 10 个元素的数组中访问第 11 个元素。（在本微型书籍的第 9 章中，我将向你展示如何找到它。）

