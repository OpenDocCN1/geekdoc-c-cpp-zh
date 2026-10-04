

数组（Array）是一种可以包含一系列相同类型元素的结构（例如，所有的 `int` 值或所有的 `double` 值，或者所有的 `Vehicle` 对象和 `Motor` 对象——你将在本书的第 7 章遇到后这类对象）。

## 使用数组的理由

考虑一组六个浮点数平均值的问题。这六个数中的每一个都需要自己的 `double` 存储空间：

```
double d0 = 5;
double d1 = 2;
double d2 = 7;
double d3 = 3.5;
double d4 = 6.5;
double d5 = 8;
```

（计算 `int` 变量的平均值会导致舍入误差，如本书第 2 章所述。）

计算这些变量的平均值可能如下：

```
double sum = d0 + d1 + d2 + d3 + d4 + d5;
double average = sum / 6;
```

按名称列出每个元素是枯燥的。好吧，当你只有 6 个数字需要取平均值时可能没那么枯燥，但想象一下计算 600 个（甚至 600 万个）浮点值的平均值。

## 固定值数组

幸运的是，你不需要为每个元素单独命名。C# 提供了可以存储值序列的数组结构。使用数组，你可以将所有的 `double` 放入一个变量，如下：

```
double[] doublesArray = {5, 2, 7, 3.5, 6.5, 8, 1, 9, 1, 3};
```

你也可以声明一个空数组而不进行初始化：

```
double[] doublesArray = new double[6];
```

这一行为六个 `double` 分配了空间，但没有对它们进行初始化。

所有 C# 数组都基于 `Array` 类，它提供了特殊的语法使其使其更加方便。成对的括号 `[]` 指的是访问数组中单个元素的方式：

```
doublesArray[0] // 对应 d0（即 5）
doublesArray[1] // 对应 d1（即 2）
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_133_0.png)

数组的第 0 个元素对应 a0，第 1 个元素对应 a1，第 2 个元素对应 a2，以此此类推。程序员通常将第 0 个元素称为“doublesArray sub-0”，将第一个元素称为“doublesArray sub-1”，以此此类推。

数组的元素编号——0, 1, 2, . . .被称为索引（index）。

在 C# 中，数组索引从 0 开始而不是 1。因此，你通常不会将索引 1 的元素称为第一个元素，而是称为“oneeth element”或“索引 1 处的元素”。第一个元素是第 0 个元素。如果你坚持使用普通语言，请记住第一个元素始终位于索引 0，第二个元素位于索引 1。

如果数组索引不是一个变量，那么 `doublesArray` 变量将不会太大改进。使用 `for` 循环比手动写出每个元素要简单，如下程序所示：

```
// FixedArrayAverage -- 使用循环计算固定数字数组的平均值。
namespace FixedArrayAverage
{
    using System;
    public class Program
    {
        public static void Main(string[] args)
        {
            double[] doublesArray = {5, 2, 7, 3.5, 6.5, 8, 1, 9, 1, 3};
            // 将数组中的值累加到变量 sum 中。
            double sum = 0;
            for (int i = 0; i < 10; i++)
            {
                sum += doublesArray[i];
            }
            // 计算平均值。
            double average = sum / 10;
            Console.WriteLine(average);
            Console.WriteLine("按回车退出...");
            Console.Read();
        }
    }
}
```

程序通过将变量 `sum` 初始化为 0 开始。遍历 `doublesArray` 中的值并将每一个累加。循环结束时，`sum` 累加了数组中所有值的和。结果和除以元素个数得到平均值。该程序的输出是预期的 4。（你可以用计算器检查。）

## 检查数组边界

幸运的是，`FixedArrayAverage` 程序（在之前的“固定值数组”部分）遍历了十个元素。但如果你失误没有正确遍历循环呢？你有两种情况需要考虑：

- 你只遍历了九个元素：如果你想读取一个十个元素的数组，C# 不认为这是一个错误。当然，平均值是错误的，但程序不知道。
- 你遍历了11 个（或更多）元素：现在 C# 非常在意。它不允许你索引数组范围之外，以免覆盖内存中的重要值。为了进行测试，将 `FixedArrayAverage` 循环中的比较值 10 替换为 11：

```
for(int i = 0; i < 11; i++)
```

执行程序时，你会看到一个带有此错误消息的对话框：

```
IndexRangeException was unhandled
Index was outside the bounds of the array.
```

一看，这个错误消息似乎很吓人。但你可以很快掌握要点：显然，`IndexRangeException` 告诉你程序尝试访问数组范围之外的内容——即10 个元素数组的第 11 个元素。（在本书第 9 章，我将介绍如何处理该错误。）

## 变长数组

`FixedArrayAverage` 示例使用的数组存在两个严重问题：

- 数组的大小固定为十个元素。
- 更糟糕的是，元素的值直接在程序中指定。

一个可以读取数量值的程序（可能在运行时由用户决定）会灵活得多。它不仅适用于 `FixedArrayAverage` 中的十个值，也适用于任何数量的值。

声明变长数组的格式与固定大小固定值数组略有不同：

```
double[] doublesArrayVariable = new double[N];  // 变长
double[] doublesArrayFixed = new double[10];     // 固定
```

在这里，N 代表分配的元素个数。更新后的 `VariableArrayAverage` 程序允许用户指定输入的数量（N 来自某处）。由于程序保留了输入的值，它不仅计算了平均值，还以良好的格式显示结果，如下：

![](img/6df7bb88e9302e98442acc219cfbd7fc_136_0.png)

```
// VariableArrayAverage -- 计算用户在运行时决定的数组的平均值。
// 允许频繁引用。在这种情况下，数组创建了美观的输出。
namespace VariableArrayAverage
{
    using System;
    public class Program
    {
        public static void Main(string[] args)
        {
            // 首先读取用户想要输入的 double 数量。
            Console.Write("要取平均值的数量: ");
            string numElementsInput = Console.ReadLine();
            int numElements = Convert.ToInt32(numElementsInput);
            Console.WriteLine();
            // 现在声明该大小的数组。
            double[] doublesArray = new double[numElements]; // 这里是 'N'
            // 将值累加到数组中。
            for (int i = 0; i < numElements; i++)
            {
                // 提示用户输入 double。
                Console.Write("Enter double #" + (i + 1) + ": ");
                string val = Console.ReadLine();
                double value = Convert.ToDouble(val);
                // 使用括号符号将其添加到数组。
                doublesArray[i] = value;
            }
            // 将数组中的 'numElements' 个值累加到变量 sum 中。
            double sum = 0;
            for (int i = 0; i < numElements; i++)
            {
                sum = sum + doublesArray[i];
            }
            // 现在计算平均值。
            double average = sum / numElements;
            // 以美的格式输出结果。
            Console.WriteLine();
            Console.Write(average + " is the average of (" + doublesArray[0]);
            for (int i = 1; i < numElements; i++)
            {
                Console.Write(" + " + doublesArray[i]);
            }
            Console.WriteLine(") / " + numElements);
            // 等待用户确认结果。
            Console.WriteLine("按回车退出...");
            Console.Read();
        }
    }
}
```

