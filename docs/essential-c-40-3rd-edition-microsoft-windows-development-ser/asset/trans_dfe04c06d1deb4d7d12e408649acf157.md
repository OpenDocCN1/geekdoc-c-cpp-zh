

## 4 方法和参数

到目前为止，通过你对 C# 编程的学习，你应该能够编写由一系列语句组成的简单程序，类似于 20 世纪 70 年代创建程序的方式。自 20 世纪 70 年代以来，编程已经取得了长足进步；随着程序变得更加复杂，需要新的范式来管理这种复杂性。“过程式”或“结构化”编程提供了一种结构，将语句分组在一起形成一个单元。此外，通过结构化编程，可以将数据传递给一组语句，并在语句执行后返回数据。

本章介绍如何将语句分组到方法中。此外，还介绍如何调用方法，包括如何向方法传递数据以及从方法接收数据。

![](img/ef1bd88b5fdf5fb56f8510479607fe66_197_0.png)

除了调用和定义方法的基础知识外，本章还介绍了一些稍微高级的概念——即递归和方法重载，以及一些新的 C# 4 特性，即可选参数和命名参数。迄今为止以及本章末尾讨论的所有方法调用都是静态的（第 5 章将详细探讨这一概念）。

即使早在第 1 章的 HelloWorld 程序中，你也学习了如何定义方法。在该示例中，你定义了 Main() 方法。在本章中，你将更详细地了解方法创建，包括用于向方法传递数据和从方法传回数据的特殊 C# 语法（使用单个参数 ref），以及仅将数据从方法传出的参数（out）。最后，我将简要介绍一些基本的错误处理。

### 调用方法

### 初学者主题

### 什么是方法？

到目前为止，你编写的程序中的所有语句都出现在一个称为 Main() 方法的分组中。随着程序变得稍微大一些，单个方法实现很快就会变得难以维护，并且难以阅读和理解。

方法是将一系列语句分组在一起以执行特定操作或计算特定结果的一种手段。这为构成程序的语句提供了更大的结构和组织。例如，考虑一个计算目录中源代码行数的 Main() 方法。与其拥有一个庞大的 Main() 方法，不如提供一个更短的版本，以便在必要时专注于每个方法实现的细节。清单 4.1 显示了一个示例。

```
LISTING 4.1: Grouping Statements into Methods

class LineCount
{
static void Main()
{
int lineCount;
string files;

DisplayHelpText();
    files = GetFiles();
    lineCount = CountLines(files);
    DisplayLineCount(lineCount);
}
// ...
}
```

与其将所有语句都放入 Main()，不如清单将它们分组为称为方法的组。与显示帮助文本相关的语句（一组 System.Console.WriteLine() 语句）已移动到 DisplayHelpText() 方法。所有用于确定要计算哪些文件的语句都出现在 GetFiles() 方法中。要实际计算文件，代码在使用 DisplayLineCount() 方法显示结果之前调用 CountLines() 方法。乍一看，很容易审查代码并获得概览，因为方法名称描述了实现。

方法始终与类相关联，类提供了一种将相关方法分组在一起的手段。从概念上讲，调用方法与向类发送消息相同。

方法可以通过参数接收数据。参数是用于将数据从调用者（包含方法调用的方法）传递到目标方法（Write()、WriteLine()、GetFiles()、CountLines() 等）的变量。在清单 4.1 中，files 和 lineCount 是传递给 CountLines() 和 DisplayLineCount() 方法的参数示例。方法还可以通过返回值将数据返回给调用者（在清单 4.1 中，GetFiles() 方法调用有一个返回值，该值被赋给 files）。

首先，你将重新审视第 1 章中的 System.Console.Write()、System.Console.WriteLine() 和 System.Console.ReadLine()。这次，将它们视为方法调用的一般示例，而不是关注从控制台打印和检索数据的具体细节。清单 4.2 显示了这三种方法的使用情况。

### 清单 4.2：简单的方法调用

```
class HeyYou
{
    static void Main()
    {
string firstName;
string lastName;

System.Console.WriteLine("Hey you!");

System.Console.WriteLine("Enter your first name :");
firstName = System.Console.ReadLine();
System.Console.WriteLine("Enter your last name :");
lastName = System.Console.ReadLine();
System.Console.WriteLine("Your full name is {0} {1}.",
    firstName, lastName);
}
```

方法调用的部分包括命名空间、类型名、方法名、参数和返回数据类型。句点分隔完全限定方法名的每个部分。

### 命名空间

方法调用中的第一项是命名空间。命名空间是一种分类机制，用于将与特定功能相关的所有类型分组在一起。通常，你希望外部命名空间是公司名称，然后是产品名称，然后是功能区域：Microsoft.Win32.Networking。命名空间有助于避免类型名称冲突。例如，只要每个类具有不同的命名空间，编译器就可以区分两个名为 "Program" 的类型。结果是，每个类中的 Main 方法可以使用 Awl.Windows.Program.Main() 或 Awl.Console.Program.Main() 来引用。System.Collections、System.Collections.Generic、System.IO 和 System.Runtime.Serialization.Formatters 都是有效的命名空间名称。命名空间名称中可以包含句点。这使得命名空间看起来具有层次结构。这仅提高了人类的可读性，因为编译器将所有命名空间视为单一级别。例如，System.Collections.Generic 出现在 System.Collections 命名空间层次结构中，但对编译器而言，这些只是两个完全不同的命名空间。

在清单 4.2 中，Console 类型的命名空间是 System。System 命名空间包含使程序员能够执行许多基本编程活动的类型。几乎所有 C# 程序都使用 System 命名空间中的类型。表 4.1 列出了其他常见命名空间。

### 表 4.1：常见命名空间

| 命名空间 | 描述 |
| :--- | :--- |
| System | 包含基本类型的定义、类型之间的转换、数学、程序调用和环境管理。 |
| System.Collections | 包括用于处理对象集合的类型。集合通常可以遵循列表或字典类型的存储机制。 |
| System.Collections.Generic | 这是 C# 2.0 添加的命名空间，用于处理依赖于泛型（类型参数）的强类型集合。 |
| System.Data | 包含用于处理存储在数据库中的数据的类型。 |
| System.Drawing | 包含用于绘制到显示设备和处理图像的类型。 |
| System.IO | 包含用于处理文件和目录的类型，并提供操作、加载和保存文件的功能。 |
| System.Linq | 提供类和接口，用于使用 C# 3.0 添加的 API（语言集成查询，Language Integrated Query）查询集合中的数据。 |
| System.Text | 包括用于处理字符串和各种文本编码以及在这些编码之间转换的类型。此命名空间包含一个名为 System.Text.RegularExpressions 的子命名空间，用于访问正则表达式相关 API。 |
| System.Threading | 处理线程操作和多线程编程。 |
| System.Threading.Tasks | 一组用于处理线程的类，首次出现在 .NET 4 中。 |

