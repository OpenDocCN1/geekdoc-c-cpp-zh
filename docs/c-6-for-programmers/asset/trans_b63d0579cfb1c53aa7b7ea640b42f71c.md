
```csharp
5   // Main method begins app execution
6   static void Main()
7   {
8       // rectangular array of student grades
9       int[,] gradesArray = {{87, 95, 70},
10                           {68, 87, 90},
11                           {94, 100, 90},
12                           {100, 81, 82},
13                           {83, 65, 85},
14                           {78, 87, 65},
15                           {85, 75, 83},
16                           {91, 94, 100},
17                           {76, 72, 84},
18                           {87, 93, 73}};
19
20      GradeBook myGradeBook = new GradeBook(
21         "CS101 Introduction to C# Programming", gradesArray);
22      myGradeBook.DisplayMessage();
23      myGradeBook.ProcessGrades();
24  }
25 }
```

**图 8.22** | 使用矩形成绩数组创建 GradeBook 对象。（第 2 部分，共 2 部分。）

## 8.11 可变长度参数列表

可变长度参数列表允许你创建接收任意数量参数的方法。在方法的参数列表中，由关键字 *params* 开头的一维数组类型参数表示该方法接收与数组元素类型相同、数量可变的参数。*params* 修饰符的这种用法只能出现在参数列表的最后一个参数。虽然你可以使用方法重载和数组传递来完成可变长度参数列表所能完成的许多工作，但使用 *params* 修饰符更为简洁。

图 8.23 演示了 Average 方法（第 8–19 行），它接收一个可变长度的 double 序列（第 8 行）。C# 将可变长度参数列表视为一维数组，其元素类型全部相同。因此，方法体可以将参数 numbers 作为 double 数组来处理。第 13–16 行使用 foreach 循环遍历数组，并计算数组中 double 值的总和。第 18 行访问 numbers.Length 以获取 numbers 数组的大小，用于平均值计算。Main 中的第 30、32 和 34 行分别用两个、三个和四个参数调用 Average 方法。由于 Average 方法具有可变长度参数列表，因此它可以对调用者传入的任意多个 double 参数求平均值。输出表明，每次对 Average 方法的调用都返回了正确的值。

### 常见编程错误 8.7

*params* 修饰符只能用于参数列表的最后一个参数。

```csharp
// Fig. 8.23: ParamArrayTest.cs
// Using variable-length argument lists.
using System;

class ParamArrayTest
{
    // calculate average
    static double Average(params double[] numbers)
    {
        var total = 0.0; // initialize total

        // calculate total using the foreach statement
        foreach (var d in numbers)
        {
            total += d;
        }

        return numbers.Length != 0 ? total / numbers.Length : 0.0;
    }

    static void Main()
    {
        var d1 = 10.0;
        var d2 = 20.0;
        var d3 = 30.0;
        var d4 = 40.0;

        Console.WriteLine(
            $"d1 = {d1:F1}\nd2 = {d2:F1}\nd3 = {d3:F1}\nd4 = {d4:F1}");
        Console.WriteLine($"Average of d1 and d2 is {Average(d1, d2):F1}");
        Console.WriteLine(
            $"Average of d1, d2 and d3 is {Average(d1, d2, d3):F1}");
        Console.WriteLine(
            $"Average of d1, d2, d3 and d4 is {Average(d1, d2, d3, d4):F1}");
    }
}
```

```text
d1 = 10.0
d2 = 20.0
d3 = 30.0
d4 = 40.0

Average of d1 and d2 is 15.0
Average of d1, d2 and d3 is 20.0
Average of d1, d2, d3 and d4 is 25.0
```

图 8.23 | 使用可变长度参数列表。

## 8.12 使用命令行参数

在许多系统上，可以通过在 Main 的参数列表中包含一个 string[]（即字符串数组）类型的参数，从命令行向应用传递参数（这些参数称为命令行参数）。按照惯例，此参数命名为

args（图 8.24，第 7 行）。你可以通过切换到包含应用 .exe 文件的目录，键入文件名（可能后跟命令行参数）并按 Enter 键，直接从命令提示符执行应用。执行时，运行环境将应用名称后出现的任何命令行参数作为字符串传递给应用的 Main 方法，存储在一维数组 args 中。通过访问数组的 Length 属性可获取从命令行传递的参数个数。例如，命令“MyApp a b”向应用 MyApp 传递两个命令行参数。必须使用空白字符（而不是逗号）分隔命令行参数。执行上述命令时，Main 方法入口点接收包含两个元素的数组 args（即 args.Length 为 2），其中 args[0] 包含字符串 "a"，args[1] 包含字符串 "b"。命令行参数的常见用途包括向应用传递选项和文件名。

```csharp
// Fig. 8.24: InitArray.cs
// Using command-line arguments to initialize an array.
using System;

class InitArray
{
    static void Main(string[] args)
    {
        // check number of command-line arguments
        if (args.Length != 3)
        {
            Console.WriteLine(
                "Error: Please re-enter the entire command, including\n" +
                "an array size, initial value and increment.");
        }
        else
        {
            // get array size from first command-line argument
            var arrayLength = int.Parse(args[0]);
            var array = new int[arrayLength]; // create array

            // get initial value and increment from command-line argument
            var initialValue = int.Parse(args[1]);
            var increment = int.Parse(args[2]);

            // calculate value for each array element
            for (var counter = 0; counter < arrayLength; ++counter)
            {
                array[counter] = initialValue + increment * counter;
            }

            Console.WriteLine($"{"Index"}{"Value",8}");

            // display array index and value
            for (int counter = 0; counter < array.Length; ++counter)
            {
                Console.WriteLine($"{counter,5}{array[counter],8}");
            }
        }
    }
}
```

C:\Users\PaulDeitel\Documents\examples\ch08\fig08_24\InitArray.exe
Error: Please re-enter the entire command, including
an array size, initial value and increment.

C:\Users\PaulDeitel\Documents\examples\ch08\fig08_24\InitArray.exe 5 0 4

| 索引 | 值 |
|-------|-------|
| 0 | 0 |
| 1 | 4 |
| 2 | 8 |
| 3 | 12 |
| 4 | 16 |

C:\Users\PaulDeitel\Documents\examples\ch08\fig08_24\InitArray.exe 10 1 2

| 索引 | 值 |
|-------|-------|
| 0 | 1 |
| 1 | 3 |
| 2 | 5 |
| 3 | 7 |
| 4 | 9 |
| 5 | 11 |
| 6 | 13 |
| 7 | 15 |
| 8 | 17 |
| 9 | 19 |

图 8.24 | 使用命令行参数初始化数组。（第 2 部分，共 2 部分。）

图 8.24 使用三个命令行参数初始化数组。应用执行时，如果 args.Length 不是 3，应用将显示错误消息并终止（第 10–15 行）。否则，第 16–39 行根据命令行参数的值初始化并显示数组。

命令行参数以字符串形式通过 args 提供给 Main。第 19 行获取 args[0]——一个指定数组大小的字符串——并将其转换为 int 值，应用在第 20 行使用该值创建数组。

第 23–24 行将 args[1] 和 args[2] 命令行参数转换为 int 值，并分别存储到 initialValue 和 increment 中——与往常一样，如果用户没有输入有效的整数，这些行可能会导致异常。第 29 行计算每个数组元素的值。

第一次示例执行表明应用收到的命令行参数数量不足。第二次示例执行使用命令行参数 5、0 和 4，分别指定数组大小（5）、第一个元素的值（0）和数组中每个值的增量（4）。对应的输出表明，这些值创建了一个包含整数 0、4、8、12 和 16 的数组。以下输出
