
图 3.16：显示 `MyException` 应用程序的输出

图 3.16 显示，当 100 被 0 除时，会发生 `DivideByZeroException`；因此，程序控制被转移到 `catch` 块并执行 `catch` 块内的语句，最后显示结果。

## 抛出异常

您可以使用 `throw` 语句抛出用户定义的异常。`throw` 语句只接受一个参数来抛出异常。当遇到 `throw` 语句时，程序会终止。让我们创建一个名为 `MyThrowException` 的控制台应用程序（也在 CD 上提供）来展示如何抛出异常。列表 3.15 显示了 `MyThrowException` 应用程序的代码：

### 列表 3.15：显示 `MyThrowException` 应用程序的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MyThrowException
{
    class Program
    {
        static void Main(string[] args)
        {
            int number;
            Console.Write("Enter a Number:");
            number = int.Parse(Console.ReadLine());
            try
            {
                if (number > 10)
                    throw new Exception("Maximum Limit is 10");
            }
            catch (Exception e)
            {
                Console.WriteLine("Exception has been Occured");
            }
            finally
            {
                Console.WriteLine("This is the Last Statement");
                Console.Write("\nPress ENTER to quit...");
                Console.ReadLine();
            }
        }
    }
}
```

在列表 3.15 中，您可以看到在 `try` 块中，`if` 语句检查 `number` 变量的值是否大于 10。如果条件满足，就会抛出一个新异常 Maximum Limit is 10。

图 3.17 显示了列表 3.15 的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_176_0.png)

图 3.17：显示 `MyThrowException` 应用程序的输出

在图 3.17 中，您可以看到抛出了一个用户定义的异常。每当输入的数字超过 10 时就会引发异常，然后在 `catch` 块中捕获。

## 使用 `checked` 和 `unchecked` 语句

如 In Depth 部分所述，`checked` 和 `unchecked` 语句用于检查内存溢出异常。让我们创建一个名为 `CheckOverflow` 的控制台应用程序（也在 CD 上提供）来展示 `checked` 和 `unchecked` 语句的使用。列表 3.16 显示了 `CheckOverflow` 应用程序的代码：

### 列表 3.16：显示 `CheckOverflow` 应用程序的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace CheckOverflow
{
    class Program
    {
        static void Main(string[] args)
        {
            byte number1, number2;
            byte result;

            number1 = 127;
            number2 = 127;

            try
            {
                result = unchecked((byte)(number1 * number2));
                Console.WriteLine("Unchecked result: " + result);

                result = checked((byte)(number1 * number2));
                Console.WriteLine("Checked result: " + result);
            }
            catch (OverflowException exc)
            {
                Console.WriteLine(exc);
            }
            finally
            {
                Console.Write("\nPress ENTER to quit...");
                Console.ReadLine();
            }
        }
    }
}
```

在列表 3.16 中，你可以看到我们取了两个字节类型变量 `number1` 和 `number2` 并将值 127 分别赋给它们。在 `try` 块中，两个变量相乘的结果被存储到另一个字节类型变量 `result` 中。由于 `number1` 和 `number2` 变量中存储的值相乘后超过了 `result` 变量可以存储的值的限制；因此会发生异常。在这种情况下，`checked` 语句会导致溢出异常并显示异常消息；然而 `unchecked` 语句不会导致任何异常并显示结果。

图 3.18 显示了列表 3.16 的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_177_0.png)

图 3.18：使用 Checked 和 Unchecked 语句后的输出显示

至此，本章结束。现在让我们总结一下本章的主要要点。

## Summary

在本章中，你学习了控制流语句，例如选择语句、迭代语句和跳转语句。你还学习了在程序执行期间可能引发的各种异常以及处理这些异常的方法。此外，你还学习了 `checked` 和 `unchecked` 语句。本章的 Immediate Solutions 部分中，每个语句都通过适当的示例进行了解释。

在下一章中，你将学习命名空间、类、对象和结构体。

## 4 Namespaces, Classes, Objects, and Structs

| If you need an Immediate Solution to: | See page: |
|---|---|
| Creating a Namespace | 152 |
| Adding a Reference to the Namespace | 153 |
| Accessing a Predefined Namespace through the using Directive | 155 |
| Creating a Class | 156 |
| Declaring a Partial Class | 156 |
| Creating an Object | 157 |
| Using this Keyword | 159 |
| Creating an Array of Objects | 160 |
| Using a Method with Parameters | 162 |
| Using a Method with Arguments | 163 |
| Passing a Reference Argument to a Method | 164 |
| Passing an Object as an Argument to a Method | 165 |
| Returning a Value from a Method | 167 |
| Creating a Partial Method | 167 |
| Using a Parameterized Constructor in a Class | 169 |
| Creating a Copy Constructor | 169 |
| Calling the Destructor of a Class | 171 |
| Creating a Static Class | 171 |
| Using a Static Method in Classes | 172 |
| Assigning and Retrieving Values Using a Property | 173 |

![](img/e073a4882197be4ab61103cbe0bcb394_178_0.png)

| If you need an Immediate Solution to: | See page: |
|---|---|
| Using Object Initializers | 174 |
| Retrieving Values using a Read-Only Property | 176 |
| Creating a Static Property | 177 |
| Creating an Anonymous Type | 178 |
| Using an Indexer | 178 |
| Using a String Indexer | 179 |
| Using Nested Classes | 181 |
| Using a Struct | 181 |

## In Depth

C# 是一种平台中立的语言，意味着它与任何编程语言兼容。C# 编程语言提供了一套丰富的功能和强大的构造，允许你用最少的代码快速轻松地创建新应用程序。编程最基本方面涉及以下内容的使用：

- Namespaces — 允许将不同的实体（如类、对象和函数）分组在同一个名称下
- Classes — 表示可能包含数据成员（如常量和字段）、函数成员（如方法、属性和事件）以及嵌套类型的结构
- Objects — 表示一个构建块，帮助你访问类的成员，如字段、方法和属性
- Structs — 表示可包含数据成员和函数成员的数据结构

在本章中，你将探索 C# 的一些新特性并尝试理解 C# 与其他语言（如 C++ 和 Java）之间的差异。本章首先探讨命名空间的概念以及如何在 C# 中创建程序时使用它们。接下来，你将探讨类和对象的概念。最后，本章讨论结构体以及如何使用访问修饰符使用它们。

让我们现在开始本章，讨论命名空间。

## Exploring Namespaces

命名空间的概念对 C# 来说并不新鲜，因为它已在 C++ 和 Java 中广泛使用。命名空间是一个包装器，包裹在一个或多个结构元素周围，使其唯一并与其他元素区分开来。命名空间的示例显示在以下代码片段中：

```
namespace XYZcorporation
{
    public class Corp1 { }
    enum CorpEnum { }
}
```

在前面的代码片段中，`XYZCorporation` 是一个包含类 `Corp1` 和枚举 `CorpEnum` 的命名空间。如果公司从另一家软件供应商处购买第三方软件，该软件在其程序中实现了相同的类名，命名空间允许开发人员引用代码中现有的类。这可以通过使用完整的命名约定，例如 `namespace.classname` 来完成。

你编写的所有代码都保留在为代码当前上下文存在的隐式命名空间中。关于命名空间的另一点值得提及的是，它们用 `using` 关键字替换了 C++ `#include` 记法（类似于 Java 中的 `import` 语句）。这意味着使用 `using` 关键字，你可以告诉编译器你希望在系统中使用的代码的哪些命名空间和库。`using` 关键字最常见的用途是在程序中包含 `System` 命名空间，以便你可以使用 `System` 命名空间的大多数常用功能。要使用 `System` 命名空间，你可以编写以下代码片段：

```
using System;
// Call the console class in the System namespace
Console.WriteLine("Hello world");
```

或者，你可以编写以下代码片段：

```
System.Console.WriteLine("Hello world");
```

前面两个代码片段中显示的语句是等效的，可用于调用 `Console` 类的 `WriteLine` 方法。通常，每次你想在程序中使用其包含的类时都需要添加一个命名空间。但是，如果命名空间在代码顶部使用 `using` 关键字指定，你就不必在代码的每个实例中指定它。

在嵌套命名空间或具有某些公共方法的命名空间的情况下，你可以为命名空间创建别名。假设你的公司坚持在你创建的每个类周围包裹三个级别的命名空间——`Corporation`、`Dept` 和 `Project`。以下代码片段显示了这些命名空间使用时的级别：

```
namespace Corporation {
    namespace Dept {
        namespace Project
        {
            class InternalClass { }
        }
    }
}
```

在前面的代码片段中，你可以看到我们还创建了 `InternalClass` 类。你需要使用以下代码片段中显示的语法来引用程序中的 `InternalClass` 类：

```
Corporation.Dept.Project.InternalClass
```

在你使用 `InternalClass` 类的所有地方输入前面的代码片段既复杂又耗时。C# 提供了一种替代选项，允许你为 `Corporation.Dept.Project` 命名空间指定别名，如以下代码片段所示：

```
using DCN=Corporation.Dept.Project;
```

现在，指定别名后，你可以通过使用以下代码片段访问为其创建别名的指定命名空间的成员：

```
DCN.InternalClass
```

在前面的代码片段中，`DCN` 是 `Corporation.Dept.Project` 命名空间的别名。以下代码片段显示了如何在程序中使用别名 `DCN` 代替 `Corporation.Dept.Project` 命名空间：

```
using System;
using DCN = Corporation.Dept.Project;
namespace Corporation
{
    namespace Dept
    {
        namespace Project
        {
            class InternalClass
            {
                public static void Display()
                {
                    Console.WriteLine("Hello world");
                }
            }
        }
    }
}
public class MainClass
{
    public static void Main()
    {
        DCN.InternalClass.Display();
    }
}
```

在前面的代码片段中定义别名名的技术减少了代码的复杂性，并最大限度地减少了输入完整命名空间所花费的时间。

以下是 .NET Framework 类库提供的一些常见命名空间：

- `System`—包括定义常用数据类型、事件、事件处理程序、接口、属性和异常的基本类和基本类。
- `System.Collections`—包括定义各种对象集合的接口和类，包括列表、队列、数组、哈希表和字典。
- `System.Data`—包括构成 ADO.NET 的类，允许你构建数据处理组件以管理来自多个分布式数据源的数据。
- `System.Data.OleDb`——包含支持 OLE DB .NET 数据提供程序的类。
- `System.Data.SqlClient`——包含支持 SQL Server .NET 数据提供程序的类。
- `System.Data.OracleClient`——包含用于实现 Oracle 数据提供程序的类。
- `System.Data.Odbc`——包含用于实现开放数据库连接（ODBC）数据提供程序的类。
- `System.Diagnostics`——包含允许你在调试应用程序时调试代码并单步执行代码的类。它还包含启动系统进程、读写事件日志以及监视系统性能的方法。
- `System.Drawing`—提供对 GDI+ 图形功能的访问。更高级的功能在 `System.Drawing.Drawing2D`、`System.Drawing.Imaging` 和 `System.Drawing.Text` 命名空间中提供。
- `System.Drawing.Drawing2D`——包含支持高级二维和矢量图形的类。
- `System.Drawing.Imaging`——包含支持高级 GDI+ 图像处理的类。
- `System.Drawing.Printing`——包含为应用程序提供打印相关服务的类。
- `System.Drawing.Text`——包含支持高级 GDI+ 排版操作的类。此命名空间中的类允许用户创建和使用字体集合。
- `System.Globalization`——包含指定与文化相关的信息的类，包括语言、国家/地区、日历、日期、货币和数字的格式模式。
- `System.IO`——包含支持对数据流和文件进行同步和异步读写操作的类型。
- `System.Net`——为 Internet 上使用的许多协议提供简单的编程接口。
- `System.Net.Sockets`——包含支持 Windows 套接字接口的类。如果你使用过 Winsock API，那么应该能够使用 `Socket` 类开发应用程序。
- `System.Reflection`——包含返回有关类型、方法和字段信息的类和接口。`System.Reflection` 命名空间还具有动态创建和调用类型的能力。
- `System.Runtime.Remoting`——提供允许开发人员创建和配置分布式应用程序的类和接口。
- `System.Security`——包含支持公共语言运行时（CLR）安全系统结构的类。
