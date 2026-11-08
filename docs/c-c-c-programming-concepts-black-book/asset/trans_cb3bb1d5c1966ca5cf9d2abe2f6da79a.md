
![](img/43c5f409f9b17790a628c4b4df854b61_524_0.png)

## 17 C# 基础

| 如果你需要以下信息： | 参见页码： |
|---|---:|
| C# Hello World 程序 | 484 |
| 数据类型 | 487 |
| 变量声明 | 489 |
| 表达式、运算符和运算符优先级 | 490 |
| 类型转换 | 492 |
| 数组 | 494 |
| 字符串 | 498 |
| 结构 | 505 |
| 集合 | 508 |
| 引用类型 | 513 |
| 值类型 | 515 |
| 流程控制语句 | 516 |
| 变量作用域 | 525 |
| 参数传递 | 527 |
| 命名参数和可选参数 | 530 |
| 命名空间 | 532 |

C#（读作 C Sharp）是 C/C++ 家族中第一种面向组件的语言。它被称为面向组件语言，因为其编码的基本单元是类。C# 是一种通用、高级、面向对象的编程语言，它借鉴了其他语言的主要概念。然而，就其提供的功能而言，C# 与 Java 更为相似。我们可以在任何文本编辑器中编写 C# 代码，并借助 C# 编译器进行编译，但这种编程语言主要用于 .NET 环境。因此，开发 Web 应用程序或 Web 服务时，最常用的编程语言是 C#。有时它也被称为 .NET 语言，因为 C# 的设计与 .NET 环境的设计是并行进行的。

C# 是微软对 Java 的回应。该语言的主要设计者是 Anders Hejlsberg 和 Scott Wiltamuth。C# 于 2000 年正式发布，其名称灵感来自音符 C#，它表示比 C/C++ 高一个音级。然而，这种语言无意与 C 或任何汇编级语言竞争。

如果考虑语言性能，那么与 Java 相比，C# 不需要额外的性能成本。我们只需安装 .NET Framework，然后就可以用它来创建软件组件、网页和 Web 服务。C# 提高了程序员的生产力以及软件的健壮性。此外，如果程序员熟悉 C++ 和 Java，他们可以轻松适应 C#。

本章主要讨论 C# 的基本功能。我们通过编写一个小程序来开始本章，该程序有助于理解 C# 的代码结构。之后，我们将学习 C# 中的数据类型、变量声明、表达式、运算符和运算符优先级。此外，我们还会讨论类型转换、数组、字符串、结构、集合、引用类型和值类型。本章还借助程序解释流程控制语句、变量作用域、参数传递以及命名参数和可选参数的用法。最后，我们将学习命名空间，它提供了类、接口、结构和枚举器的集合。

让我们通过编写一个有助于理解 C# 总体结构的 C# 程序来开始本章。

### C# Hello World 程序

C# 程序的结构与 Java 和 C++ 程序有些相似。因此，C# 程序也以命名空间引用开始，这些引用通过使用指令 "using" 给出。此外，整个代码主体位于多个类定义内部。请注意，至少有一个类必须包含一个名为 Main() 的方法，它是编译器编译代码的主要入口点。现在让我们编写一个简单的 C# 程序，名为 HelloWorld.cs，它只在控制台上输出 "Hello World!!!!!!!!!!"。代码清单 17.1 展示了 HelloWorld.cs 程序的代码：

### 代码清单 17.1：展示 HelloWorld.cs 程序的代码

```csharp
using System;

namespace HelloWorld
{
    class Program
    {
        public static void Main()
        {
            Console.WriteLine("Hello world!!!!!!!!!!");
        }
    }
}
```

编译上述程序后，控制台窗口将显示输出，如图 17.1 所示：

![](img/43c5f409f9b17790a628c4b4df854b61_526_0.png)

### 图 17.1：展示 HelloWorld.cs 程序的输出

现在让我们参考图 17.2，以更好地理解 C# 的代码结构：

![](img/43c5f409f9b17790a628c4b4df854b61_526_1.png)

### 图 17.2：展示 C# 代码的结构

根据图 17.2，一个 C# 程序可以由多个文件组成，其中应有一个类文件包含 Main() 方法，该方法调用其他某个类的方法来执行所需的工作。每个类都包含一个命名空间列表；不过，System 命名空间应写在类文件的第一位，因为它是 C# 语言的主要命名空间。请注意，一个类文件可以包含多个类定义。然而，为简单起见，我们可以考虑每个类文件一个类。代码清单 17.2 展示了一个处理多个类文件的 C# 代码示例：

### 代码清单 17.2：展示处理多个类文件的 C# 代码

Program.cs

```csharp
using System;
namespace Program
{
    class Program
    {
        public static void Main()
        {
            Addition addition = new Addition(10, 30);
            Console.WriteLine("The result of addition is {0}", addition.Add());
        }
    }
}
```

Addition.cs

```csharp
using System;
namespace Addition
{
    class Addition
    {
        public int item1 = 0;
        public int item2 = 0;

        public Addition(int a, int b)
        {
            this.item1 = a;
            this.item2 = b;
        }
        public int Add()
        {
            int result = this.item1 + this.item2;
            return result;
        }
    }
}
```

如代码清单 17.2 所示，名为 Addition 的类用于加法运算；而名为 Program 的类用于执行加法运算。Program.cs 文件包含 Main() 方法，该方法通过声明 Addition 类的对象来执行加法运算。要执行代码，我们需要分别编译这两个类文件以获得所需输出。尽管我们将这些类写在两个单独的文件中，但这些类也可以合并到一个类文件中。这简化了编译过程，因为为此只需编译一个文件。代码清单 17.3 展示了在单个类文件中处理多个类的 C# 代码：

### 代码清单 17.3：在单个类文件中处理多个类

```csharp
using System;
namespace Program
{
    class Program
    {
        public static void Main()
        {
            Addition addition = new Addition(10, 30);
            Console.WriteLine("The result of addition is {0}", addition.Add());
        }
    }
    class Addition
    {
        public int item1 = 0;
        public int item2 = 0;

        public Addition(int a, int b)
        {
            this.item1 = a;
            this.item2 = b;
        }
        public int Add()
        {
            int result = this.item1 + this.item2;
            return result;
        }
    }
}
```

在代码清单 17.3 中，我们在 Program 命名空间内定义了两个类，名为 Program 和 Addition。在 Addition 类中进行加法运算；在 Program 类中调用 Main() 方法，将 10 和 30 两个数字相加，然后在控制台上打印结果。

现在让我们讨论 C# 中的各种数据类型。

### 数据类型

C# 被称为强类型语言。当每个变量和对象都具有声明的类型时，这种语言就被称为强类型语言。因此，每当我们在 C# 中声明对象或变量时，它必须具有声明的类型。

在 C# 中，存在三种数据类型，如下所示：

- 内置数据类型
- 用户定义数据类型
- 匿名类型

让我们从内置数据类型开始详细了解这些数据类型。

### 内置数据类型

内置数据类型属于 System 命名空间，它是 .NET Framework 中所有其他命名空间的根命名空间。一些基本的内置数据类型是 int、char 和 bool。所有这些数据类型都是类的对象。在 .NET Framework 中，根数据类型是 object 数据类型。表 17.1 列出了 C# 中的内置数据类型：

| 类名 | 数据类型 | 描述 |
|---|---|---|
| 类别：整数 | | |
| Byte | byte | 表示 8 位无符号整数 |
| SByte | sbyte | 表示 8 位有符号整数 |
| Int16 | short | 表示 16 位有符号整数 |
| Int32 | int | 表示 32 位有符号整数 |
| Int64 | long | 表示 64 位有符号整数 |
| UInt16 | ushort | 表示 16 位无符号整数 |
| UInt32 | uint | 表示 32 位无符号整数 |
| UInt64 | ulong | 表示 64 位无符号整数 |
| 类别：浮点数 | | |
| Single | float | 表示 32 位（单精度）浮点数 |
| Double | double | 表示 64 位（双精度）浮点数 |
| 类别：逻辑 | | |
| Boolean | bool | 表示真/假布尔值 |

