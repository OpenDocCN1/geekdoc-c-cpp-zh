
Let’s create a Console application, named `FiringEvent` (also available in the CD). Listing 6.18 shows the code of the `Program.cs` file of the `FiringEvent` application:

### Listing 6.18: Showing the Code of the `Program.cs` File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

public delegate Boolean AccountEventHandler(object sender, double amt);

namespace FiringEvent
{
    public class Account
    {
        private double Total;
        public AccountEventHandler ah = null;

        public Account()
        {
            Total = 0;
        }

        public double getTotal()
        {
            return Total;
        }

        public void AddOnPost(AccountEventHandler handler)
        {
            ah = (AccountEventHandler)Delegate.Combine(ah, handler);
        }

        public void RemoveOnPost(AccountEventHandler handler)
        {
            ah = (AccountEventHandler)Delegate.Remove(ah, handler);
        }

        public Boolean OnPost(double amt)
        {
            if (ah != null)
                return ah(this, amt);
            return true;
        }

        public void PostDebit(double amt)
        {
            // Fire the event, checking to see if the return is ok
            Boolean okToSubtract = OnPost(amt);
            if (okToSubtract)
            {
                Console.WriteLine("Debit ok!");
                Total -= amt;
            }
            else
            {
                Console.WriteLine("Debit NOT ok! Not posting");
            }
        }

        public void PostCredit(double amt)
        {
            Total += amt;
        }
    }

    class Program
    {
        public static Boolean CheckPost(object o, double d)
        {
            // See if it went negative
            Account a = (Account)o;
            if (d > a.getTotal())
                return false;
            return true;
        }

        static void Main(string[] args)
        {
            Account a = new Account();
            AccountEventHandler evh = new AccountEventHandler(CheckPost);
            a.AddOnPost(evh);
            // Can we debit 100?
            if (a.OnPost(100.00))
                a.PostDebit(100.00);
            else
                Console.WriteLine("Cannot debit 100.0");
            Console.Write("\nPress ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```

正如你在清单 6.18 中突出显示的部分所见，`Account` 类的事件处理系统的大部分功能都已公开，而无需将事件处理程序委托设为 `public`。此操作允许你公开 `OnPost()` 方法，该方法将事件触发给调用者。

图 6.20 显示了上述代码的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_283_0.png)

图 6.20：触发事件

现在，让我们在总结中回顾一下要点。

## 总结

在本章中，你已经了解了 C# 2010 中事件处理的概念，即如何在程序中处理单个和多个事件。本章还涉及指针、指针的声明、指针运算和指针的转换。你还学习了委托的重要概念，例如委托的声明、实例化、调用和多播。接下来，你学习了协变、逆变和匿名方法。在本章的“即时解决方案”部分，每一个概念都借助相应的示例进行了解释。

在下一章中，你将学习 C# 2010 中的动态数据类型和动态语言运行时（DLR）。

# 7 动态数据类型和动态语言运行时（DLR）

| 如果你需要以下问题的即时解决方案： | 参见页码： |
|---|---|
| 使用动态数据类型 | 249 |
| 转换数据类型 | 250 |
| 使用 `ExpandoObject` 类 | 251 |
| 使用 `DynamicObject` 类 | 252 |

## 深入探讨

C# 2010 中发生了一些超越以前版本 C# 的技术增强。这些增强包括动态数据类型和动态语言运行时（DLR）。在以前版本的 C# 中，你只能在应用程序编译后检查代码的准确性。如果代码中存在错误，则需要重新构建整个应用程序。动态数据类型的引入就是为了克服这个问题。它是一种引用类型，在运行时而非编译时进行检查；因此，你只能在运行时检测错误。你可以轻松地将动态数据类型转换为非动态数据类型，反之亦然。C# 的 DLR 功能使得将动态编程语言（如 Python 和 Ruby）与公共语言运行时（CLR）集成成为可能。这些语言可以在运行时识别对象的数据类型。DLR 提供了一个环境，使静态类型语言无需丧失自身属性即可表现得像动态语言一样。

在本章中，你首先会了解动态数据类型以及如何在 C# 应用程序中使用它们。你还将学习如何将动态数据类型转换为非动态数据类型，反之亦然。接下来，本章讨论 DLR、其优点和体系结构。最后，你将学习 `ExpandoObject` 和 `DynamicObject` 类。

让我们从讨论动态数据类型开始。

## 理解动态数据类型

动态数据类型是 C# 2010 中引入的一种支持后期绑定的新数据类型。这意味着与 `dynamic` 关键字关联的所有成员函数和成员变量（如字段、方法和属性）在编译时都会被忽略。编译器会保留有关表达式的所有信息（如数据类型），这些信息随后用于在运行时计算表达式。动态数据类型与 `var` 数据类型类似。`var` 和 `dynamic` 数据类型之间的区别在于，`var` 在编译时进行强类型检查；而 `dynamic` 数据类型仅在运行时由编译器进行类型检查。声明 `var` 数据类型后，在整个程序执行过程中无法显式更改其类型。以下代码片段演示了动态数据类型的声明：

```
// In this case, intDyn, floatDyn and stringDyn
// are the name of variables whose data type is dynamic
dynamic intDyn = 4;
Console.WriteLine(intDyn);

dynamic floatDyn = 4.46;
Console.WriteLine (floatDyn);

dynamic stringDyn = "EnhancedType";
Console.WriteLine (stringDyn);
```

在上述代码片段中，即使你将 `dynamic` 关键字替换为 `var` 关键字，结果也是一样的。以下代码片段演示了 `var` 关键字的工作方式：

```
class Program
{
    static void Main(string[] args)
    {
        string a = "EnhancedType";
        var str = a;
        Console.WriteLine(str.NonExistingFunction());
    }
}
```

在上述代码片段中，`NonExistingFunction()` 方法没有在类中的任何位置声明或定义，尽管在 `Main(string[] args)` 函数中，类型为 `var` 的 `str` 变量调用了此方法。编译器针对上述代码片段生成的错误如图 7.1 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_286_0.png)

图 7.1：显示错误消息

编译器生成的错误表明 `var` 关键字能够识别赋给它的值、运算符和方法。现在，让我们通过将 `var` 关键字替换为 `dynamic` 关键字来编译相同的代码片段，如下面的代码片段所示：

```
class Program
{
    static void Main(string[] args)
    {
        string a = "EnhancedType";
        dynamic str = a;
        Console.WriteLine(str.NonExistingFunction());
    }
}
```

在上述代码片段中，`NonExistingFunction()` 方法由类型为 `dynamic` 的 `str` 变量调用。在这种情况下，由于该方法与 `dynamic` 关键字关联，编译器不会检查该方法是否存在。因此，编译器不会引发任何错误，并成功编译应用程序。当程序员希望在运行时分配变量的数据类型或存储程序在运行时生成的值时，动态数据类型非常有用。

现在让我们学习如何将一种数据类型转换为另一种数据类型。

## 转换数据类型

在 C# 中，`System.Convert` 类提供了一整套用于转换数据类型的方法。该类以语言中立的方式提供转换，以便在所有支持 CLR 的语言中执行转换。另一方面，无需使用 `System.Convert` 类即可轻松地将动态数据类型的对象转换为非动态数据类型的对象。动态对象会隐式转换为动态数据类型，这使你可以轻松地在动态数据类型和非动态数据类型之间切换。以下代码片段演示了如何将非动态数据类型转换为动态数据类型：

```
dynamic dynDouble = 5.46;
dynamic dynString = "test string";
dynamic dynBool = true;
dynamic dynToday = System.DateTime.Today;
```

在上述代码片段中，我们声明了四个动态变量，并为它们赋予了不同类型的值，如 `double`、`string`、`bool` 和 `DateTime`。类似地，你也可以将动态数据类型的变量转换为非动态数据类型的变量，如下面的代码片段所示：

```
double f = dynDouble;
string str = dynString;
bool check = dynBool;
DateTime date = dynToday;
```

在上述代码片段中，动态数据类型变量的值已赋给 `double`、`string`、`bool` 和 `DateTime` 变量。如果程序中使用的参数、变量或对象属于动态数据类型，则重载解析将在运行时而非编译时进行。这是因为编译器不会对与 `dynamic` 关键字关联的变量、方法和对象进行类型检查。清单 7.1 演示了如何使用动态数据类型：

### 列表 7.1：展示动态数据类型的用法

```
class Program
{
    static dynamic dyn = 1;
    public void Method1(string str)
    {
        Console.WriteLine(str);
    }
    static void Main(string[] args)
    {
        Program p = new Program();
        //This method compiles and runs successfully.
        p.Method1("Hello");
        //This compiles successfully but, shows an error at run time.
        //The value type of dynamic dyn variable is int.
        p.Method1(dyn);
    }
}
```

在列表 7.1 中，你可以看到 `Method1` 方法在编译时无法识别动态数据类型的取值类型。`dyn` 参数的数据类型为 `int`，该类型在运行时才被识别。

## 探索动态语言运行时

DLR 添加了一组服务，例如表达式树、调用站点缓存和动态对象互操作性，用于将 Python 和 Ruby 等动态语言集成到 CLR。动态语言的主要优势在于它可以在运行时识别对象的数据类型。然而，对于 C# 或 Visual Basic 等静态类型语言而言，对象的数据类型必须在设计时指定；否则编译器会报错。

在 Visual Studio 2010 中，除了使动态语言能够在 .NET Framework 上运行之外，DLR 还为静态类型语言提供动态功能，以实现其与动态语言的互操作。支持动态互操作性的库也可以使用 DLR 创建。这使用户能够为操作对象和访问对象成员编写简单的代码。例如，以下代码片段可用于在 C# 中递增 XML 中的计数器：

```
obj.SetProperty("Count", ((int)GetProperty("Count")) + 1);
```

以下代码片段展示了使用 DLR 执行相同操作的替代方法：

```
obj.Count += 1;
```

与 CLR 类似，DLR 也是 .NET Framework 的一部分，其安装包随 Visual Studio 2010 提供。`System.Dynamic` 和 `System.Runtime.CompilerServices` 命名空间包含 DLR 的类。

让我们简要讨论 DLR 提供的各种优势。

## DLR 的优势

你已经了解到 DLR 允许你将动态语言与 CLR 集成。DLR 允许你通过为这些语言添加动态功能来开发动态语言。例如，微软开发了 IronRuby 和 IronPython 语言，它们基于动态语言 Ruby 和 Python。DLR 提供的各种优势如下：

- 允许你轻松地将动态语言实现到 .NET Framework。要使用 DLR，语言需要创建表达式树，其中包含以树形结构表示的语言级代码、运行时辅助例程，以及可选的动态对象，该对象实现 `IDynamicMetaObjectProvider` 接口。DLR 和 .NET Framework 一起自动执行大量的代码分析和代码生成，这有助于你专注于独有的语言特性。

- 为静态类型语言提供动态功能。静态类型的 .NET Framework 语言，例如 C# 和 Visual Basic 可以创建动态对象并将其与静态类型对象一起使用。

  例如，C# 和 Visual Basic 可以使用动态对象进行 .NET 反射 HTML 和文档对象模型 DOM。

- 改善 DLR 和 .NET Framework 的未来发展。DLR 实现的语言可以有利于 DLR 和 .NET Framework 的未来改进。例如，如果微软发布了具有各种改进功能的新版 .NET Framework，例如改进的垃圾回收器或更快的程序集加载时间，使用 DLR 的语言可以立即获得这些功能的好处。即使 DLR 改进了编译或任何其他优化，使用 DLR 实现的语言的性能也会得到提升。

- 实现库和对象的共享，这意味着在一个语言中实现的对象和库可以使用 DLR 被其他语言使用。此外，DLR 还实现了静态类型和动态语言之间的互操作性。例如，C# 可以创建一个动态对象，该对象使用用动态语言编写的库。同时，.NET Framework 的库也可以被动态语言使用。

- 通过支持高级缓存实现动态操作的快速执行。DLR 为在运行时实现中使用对象访问操作创建规则，然后缓存这些规则，以限制在对同一类型对象执行相同代码的后续执行期间耗尽资源的绑定计算。

现在，让我们讨论 DLR 的架构。

## DLR 的架构

动态语言编译器在 DLR 之上实现，并生成抽象语法树，该树由 DLR 库使用。DLR 为 CLR 提供一些服务，例如表达式树、调用站点缓存和动态对象互操作性。DLR 使用表达式树表示语言语义，这有助于绑定器封装语言的语义并指定在调用站点执行的运算。调用站点是指在代码中对动态对象执行逻辑和数学运算，例如 `a + b` 或 `a.b()` 的区域。

图 7.2 显示了 DLR 的架构：

![](img/e073a4882197be4ab61103cbe0bcb394_288_0.png)

图 7.2：展示 DLR 的架构

DLR 为 CLR 提供的服务用于支持动态语言。这些服务包括以下内容：
