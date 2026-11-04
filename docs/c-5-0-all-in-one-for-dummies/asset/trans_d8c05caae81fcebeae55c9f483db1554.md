
## 检查数组边界

幸运的是，FixedArrayAverage 程序（在前一节“固定值数组”中）遍历了全部十个元素。但如果你在循环迭代上出错怎么办？你需要考虑以下两种情况：

```
for(int i = 0; i < 11; i++)
```

当你执行程序时，会看到一个对话框显示以下错误信息：

```
IndexOutOfRangeException was unhandled
Index was outside the bounds of the
array.
```

**你只遍历了九个元素：** C# 不认为这是错误。如果你想读取十个元素的数组中的九个元素，C# 有什么理由说不一样呢？当然，平均值是不正确的，但程序并不知道这一点。

**你遍历了 11 个（或更多）元素：** 现在 C# 很在意。它不允许你索引超出数组末尾，担心你可能会覆盖内存中的重要值。为了测试它，将 FixedArrayAverage 的 for 循环中的比较改为以下内容，将值 10 替换为 11：

初看之下，这个错误信息似乎很吓人。然而，你可以很快抓住要点：很明显，IndexOutOfRangeException 告诉你程序尝试访问超出其范围的数组——在十个元素的数组中访问第 11 个元素。（在本迷你书的第 9 章中，我会向你展示如何了解更多关于该错误的信息。）

## 可变长度数组

FixedArrayAverage 程序示例中使用的数组存在以下两个严重问题：

- 数组的大小固定为十个元素。
- 更糟的是，元素的值直接在程序中指定。

一个能够读取可变数量值的程序，也许在执行期间由用户确定，会灵活得多。它不仅适用于 FixedArrayAverage 中指定的十个值，也适用于任何其他值集合，无论其数量多少。

声明可变大小数组的格式与固定大小、固定值的数组略有不同：

```
double[] doublesArrayVariable = new double[N]; // Variable, versus ...
double[] doublesArrayFixed = new double[10]; // Fixed
```

这里，N 代表要分配的元素数量。

更新后的程序 VariableArrayAverage 使用户能够指定要输入的值的数量。（N 必须来自某个地方。）由于程序保留了输入的值，它不仅计算平均值，还以令人愉悦的格式显示结果，如下所示：

![](img/80ff26f06fc9ab951e1cd4257b867366_136_0.png)

// VariableArrayAverage -- Average an array whose size is
// determined by the user at runtime, accumulating the values
// in an array. Allows them to be referenced as often as
// desired. In this case, the array creates an attractive output.
namespace VariableArrayAverage
{
    using System;
    public class Program
    {
        public static void Main(string[] args)
        {
            // First read in the number of doubles the user intends to enter.
            Console.Write("Enter the number of values to average: ");
            string numElementsInput = Console.ReadLine();
            int numElements = Convert.ToInt32(numElementsInput);
            Console.WriteLine();
            // Now declare an array of that size.
            double[] doublesArray = new double[numElements]; // Here's the 'N'.
            // Accumulate the values into an array.
            for (int i = 0; i < numElements; i++)
            {
                // Prompt the user for another double.
                Console.Write("enter double #" + (i + 1) + ": ");
                string val = Console.ReadLine();
                double value = Convert.ToDouble(val);
                // Add this to the array using bracket notation.
                doublesArray[i] = value;
            }
            // Accumulate 'numElements' values from
            // the array in the variable sum.
            double sum = 0;
            for (int i = 0; i < numElements; i++)
            {
                sum = sum + doublesArray[i];
            }
            // Now calculate the average.
            double average = sum / numElements;
            // Output the results in an attractive format.
            Console.WriteLine();
            Console.Write("The average of (" + doublesArray[0]);
            for (int i = 1; i < numElements; i++)
            {
                Console.Write(" " + doublesArray[i]);
            }
            Console.WriteLine(" / " + numElements);
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
}

第一册
第 6 章
用集合排列你的鸭子

查看以下在输入五个顺序值 1 到 5 且程序计算平均值为 3 的示例运行的输出：

```
Enter the number of values to average:5

enter double #1: 1
enter double #2: 2
enter double #3: 3
enter double #4: 4
enter double #5: 5

3 is the average of (1 + 2 + 3 + 4 + 5) / 5
Press Enter to terminate...
```

VariableArrayAverage 程序首先提示用户输入她打算求平均值的数量。（这就是我稍早提到的 N。）结果存储在 int 变量 numElements 中。在示例中，输入的数字是 5。

程序继续为 doublesArray 分配指定数量元素的数组。在这种情况下，程序分配了一个包含五个元素的数组。程序按 numElements 指定的次数循环，每次从用户读取一个新值。最后一次值后，程序计算平均值。

![](img/80ff26f06fc9ab951e1cd4257b867366_137_0.png)

如本例所示，让控制台输出完全正确有点棘手。请仔细跟踪 VariableArrayAverage 中的每个语句，因为程序输出左括号、等号、加号以及序列中的每个数字，并将其与输出进行比较。

VariableArrayAverage 程序可能并不能完全满足你对灵活性的渴望。你不想每次都要告诉程序你想平均多少个数字。你真正想要的是尽可能长时间地输入要平均的数字——然后告诉程序对你输入的内容进行平均。这就是 C# 集合发挥作用的地方。它们为数组提供了功能强大、灵活的替代方案。直接从用户获取输入并不是填充数组或其他集合的唯一方法。

## Length 属性

用于填充 VariableArrayAverage 程序中数组的 for 循环以这种方式开始：

// Now declare an array of that size.
double[] doublesArray = new double[numElements];
// accumulate the values into an array.
for (int i = 0; i < numElements; i++)
{
...
}

doublesArray 被声明为 numElements 项长。因此聪明的程序员使用 for 循环遍历数组中的 numElements 项。（迭代意味着一次遍历数组的一个元素，如 for 循环所示。）

必须随身携带变量 numElements 与 doublesArray 一起到处走，只是为了知道它的长度，这将是一种遗憾和犯罪。幸运的是，这不是必要的。数组有一个名为 Length 的属性，包含其长度。doublesArray.Length 的值与 numElements 相同。

以下 for 循环更可取：

// Accumulate the values into an array,
for (int i = 0; i < doublesArray.Length; i++) ...

## 初始化数组

以下行显示了一个带有初始化器的数组，然后是一个分配空间但不初始化元素值的数组：

```
double[] fixedLengthArray = {5, 2, 7, 3.5, 6.5, 8, 1, 9, 1, 3};
double[] variableLengthArray = new double[10];
```

你可以使用以下代码自行完成所有操作：

```
double[] fixedLengthArray = new double[10] {5, 2, 7, 3.5, 6.5, 8, 1, 9, 1, 3};
```

在这里，你已使用 new 专门分配了内存，然后用数组成员的初始值跟随该声明。我想我可以预测你更喜欢哪种形式。（提示：第 1 行？）

## 为每个数组定制的循环

给定一个字符串数组，以下循环计算其长度的平均值：

```
public class Student // Read about classes in Book II.
{
    public string name;
    public double gpa;      // Grade point average
}
public class Program
{
    public static void Main(string[] args)
    {
        // . . .create the array somehow . . .
        // Now average the students you have.
        double sum = 0.0;
        for (int i = 0; i < students.Length; i++)
        {
            sum += students[i].gpa;
        }
        double avg = sum / students.Length;
        // . . .do something with the average . . .
    }
}
```
