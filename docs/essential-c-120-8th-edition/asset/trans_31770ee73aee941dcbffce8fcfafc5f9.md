

# 初学者主题

# 使用空格格式化代码

使用空格对代码进行缩进对于提高可读性至关重要。在你开始编写代码时，需要遵循既定的编码标准和规范，以增强代码的可读性。

本书使用的惯例是将大括号单独放在一行，并对大括号对之间包含的代码进行缩进。如果在第一对大括号内部出现另一对大括号，则第二组大括号内的所有代码也都要进行缩进。

这并不是统一的 C# 标准，而是一种风格偏好。

# 变量操作

现在你已经接触了最基础的 C# 程序，是时候声明一个局部变量了。一旦声明了变量，你就可以给它赋值，将其替换为新值，并在计算、输出等地方使用它。然而，你不能更改变量的数据类型。在列表 1.12 中，`string max` 是一个变量声明。

> 列表 1.12：声明和赋值变量

```c
public class MiracleMax
{
    public static void Main()
    {
        string max;      // "string" 标识数据类型
                       // "max" 是变量

        max = "Have fun storing the castle!";
        Console.WriteLine(max);
    }
}
```

# 初学者主题

# 局部变量

变量是一个指向可以随时间改变的值的名称。局部（Local）表示程序员在方法内部声明了变量。

声明变量就是定义它，你通过以下方式完成定义：

- 指定变量将包含的数据类型
- 为它分配一个标识符（名称）

# 介绍数据类型

列表 1.12 声明了一个数据类型为 `string` 的变量。本章使用的其他常用数据类型是 `int` 和 `char`。

- `int` 是 C# 中整数类型的指代，大小为 32 位。
- `char` 用于字符类型。它是 16 位，足以容纳（非代理）Unicode 字符。下一章将更详细地介绍这些和其他常用数据类型。

# 初学者主题

# 什么是数据类型？

变量声明指定的数据类型称为数据类型（或对象类型）。数据类型，或简单称为类型，是对具有相似特征和行为的类型的分类。例如，“动物”是一种类型。它分类了所有具有动物特征（猴子、野猪和鸭嘴兽等）的事。同样，在编程语言中，类型是对若干具有相似特性的项的定义。

# 26 第1章：介绍 C#

# 声明变量

在列表 1.12 中，`string max` 是一个 `string` 类型变量声明，其名称为 `max`。可以通过指定一次数据类型并用逗号分隔每个标识符，在同一条语句中声明多个变量。列表 1.13 展示了此类声明。

列表 1.13：在一个语句中声明两个变量

```c
string message1, message2;
```

由于多变量声明语句允许开发者在声明中提供一次数据类型，因此所有变量将具有相同的类型。

在 C# 中，变量名可以以任意字母或下划线 (_) 开头，随后是任意数量的字母、数字和/或下划线。根据惯例，局部变量名使用驼峰命名（每个单词的首字母大写，第一个单词除外）且不包含下划线。

> 指南
局部变量名使用驼峰命名法。

# 赋值

在声明局部变量后，在读取它之前必须对其赋值。实现此点的方法之一是使用 `=` ，也称为简单赋值运算符。列表 1.14 展示了如何使用赋值运算符将字符串值指定给 `miracleMax` 和 `valerie` 将指向的变量。

列表 1.14：更改变量的值

```c
public class StormingTheCastle
{
    public static void Main()
    {
        string valerie = "Have fun storming the castle!";
        string miracleMax = "";

        valerie = "Think it will work?";
        Console.WriteLine(miracleMax);
        Console.WriteLine(valerie);

        miracleMax = "It would take a miracle.";
        Console.WriteLine(miracleMax);
    }
}
```

从此列表中观察到，可以在变量声明的一部分进行赋值（如 `miracleMax` 所示），或者在之后的单独语句中进行赋值（如变量 `valerie`）。赋值的值必须始终在声明的右侧。

运行编译后的程序会产生输出 1.3 所示的代码。

# 输出 1.3

```
>dotnet run
Have fun storming the castle!
Think it will work?
It would take a miracle.
```

在这个示例中，我们显式地显示了 `dotnet run` 命令。在未来的输出列表中，我们将省略此行，除非执行程序使用的命令有特殊之处。

C# 要求局部变量在被读取之前（由编译器确定）必须是“确定赋值”的。此外，赋值会产生一个值。因此，C# 允许在同一条语句中两次两次，如列表 1.15 所示。

# 列表 1.15：返回可再次赋值之值的赋值

```c
public class StormingTheCastle
{
    public static void Main()
    {
        // ...
        string requirements, miracleMax = "It would take a miracle.";
        // ...
    }
}
```

# 使用变量

赋值的结果当然是你可以使用变量标识符来引用该值。因此，当你在 `Console.WriteLine(miracleMax)` 语句中使用变量 `miracleMax` 时，程序会显示“Have fun storming the castle!”——即 `miracleMax` 的值。

# 高级主题

# 字符串是不可变的

所有 `string` 类型的值（无论是字符串字面量还是其他）都是不可变的（或不可修改的）。例如，无法更改字符串本身。更改需要重新为变量赋值，而不是修改变量原始指向的数据。

# 控制台输入和输出

本章已经多次使用 `Console.WriteLine` 向控制台写入文本。除了能够输出数据外，程序还需要能够接受用户可能输入的数据。

# 从控制台获取输入

获取在控制台输入的文本的一种方法是使用 `Console.ReadLine()`。该方法会停止程序执行，使用户可以输入字符。当用户按下 Enter 键产生换行时，程序继续执行。来自 `Console.ReadLine()` 方法的输出（也称为返回值）是输入的文本字符串。考虑列表 1.16 以及在输出 1.4 中显示的相应输出。

# 列表 1.16：使用 Console.ReadLine()

```c
public class HeyYou {
    public static void Main() {
        string firstName;
        string lastName;

        Console.WriteLine("Hey you!");

        Console.Write("Enter your first name: ");
        firstName = Console.ReadLine();

        Console.Write("Enter your last name: ");
        lastName = Console.ReadLine();
    }
}
```

# 输出 1.4

Hey you!
Enter your first name: Inigo
Enter your last name: Montoya
```

