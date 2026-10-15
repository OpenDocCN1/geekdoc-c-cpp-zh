

```
var game = new Pair<string>("Redskins", "Eagles");
foreach (string name in game.GetReverseEnumerator())
{
    Console.WriteLine(name);
}
```

请注意你返回的是 IEnumerable<T>，而不是 IEnumerator<T>。这与 IEnumerable<T>.GetEnumerator() 不同，后者返回 IEnumerator<T>。Main() 中的代码演示了如何使用 foreach 循环调用 GetReverseEnumerator()。

## yield 语句要求

你只能在返回 IEnumerator<T> 或 IEnumerable<T> 类型，或其非泛型等价类型的成员中使用 yield return 语句。包含 yield return 语句的成员体不得包含简单的 return。如果成员使用 yield return 语句，C# 编译器会生成必要的代码来维护迭代器的状态。相比之下，如果成员使用 return 语句而不是 yield return，程序员则需要负责维护自己的状态机并返回迭代器接口之一的实例。此外，就像具有返回类型的方法中的所有代码路径必须包含一个伴随值的 return 语句一样，迭代器中的所有代码路径如果要返回任何数据，则必须包含 yield return 语句。

以下对 yield 语句的额外限制如果被违反将导致编译器错误：

- yield 语句只能出现在方法、用户定义运算符，或索引器或属性的 get 访问器内部。该成员不得接受任何 ref 或 out 参数。
- yield 语句不得出现在匿名方法或 lambda 表达式的任何位置（参见第 12 章）。
- yield 语句不得出现在 try 语句的 catch 和 finally 子句内部。此外，yield 语句只能出现在 try 块中，前提是该 try 块没有 catch 块。

## 17

## 反射、特性与动态编程

特性是向程序集插入额外元数据并将元数据与类、方法或属性等编程构造关联的一种手段。本章研究了框架中内置的特性的细节，并描述了如何定义自定义特性。为了利用自定义特性，有必要识别它们。这通过反射来处理。本章首先介绍反射，包括如何使用它在执行时基于名称（或元数据）动态绑定，而该名称（或元数据）在编译时进行成员调用。这通常在诸如代码生成器之类的工具中执行。此外，当调用目标未知时，反射也在执行时使用。

![](img/25683ccec0773ba5b8794b11f2b12877_721_0.png)

XmlSerializer、ValueType 和 DataBinder 是框架中用于其实现部分使用反射的几个类。

## 使用 System.Type 访问元数据

读取类型的元数据的关键是获取代表目标类型实例的 System.Type 实例。System.Type 提供了检索有关类型的信息的所有方法。你可以使用它来回答以下问题：

- 类型名称是什么（Type.Name）？
- 类型是否公开（Type.IsPublic）？
- 类型的基本类型是什么（Type.BaseType）？
- 类型是否支持任何接口（Type.GetInterfaces()）？
- 类型定义在哪个程序集中（Type.Assembly）？
- 类型的属性、方法、字段等是什么（Type.GetProperties()、Type.GetMethods()、Type.GetFields() 等）？
- 哪些特性装饰了该类型（Type.GetCustomAttributes()）？

还有更多此类成员，但它们都提供有关特定类型的信息。关键是获取对类型的 Type 对象的引用，而做到这一点的主要两种方式是通过 object.GetType() 和 typeof()。

请注意，GetMethods() 调用不会返回扩展方法。这些方法仅作为实现类型上的静态成员可用。

## GetType()

object 包含一个 GetType() 成员，因此所有类型都包含此函数。你调用 GetType() 以检索对应于原始对象的 System.Type 实例。列表 17.1 演示了此过程，使用来自 DateTime 的 Type 实例。输出 17.1 显示了结果。

## 列表 17.1：使用 Type.GetProperties() 获取对象的公共属性

```
DateTime dateTime = new DateTime();

Type type = dateTime.GetType();
foreach (
    System.Reflection.PropertyInfo property in
    type.GetProperties()
)
{
    Console.WriteLine(property.Name);
}
```

typeof 表达式在编译时解析，使得类型比较——也许比较从 GetType() 调用返回的类型——可以确定对象是否为特定类型。

## 成员调用

反射的可能性并不止于检索元数据。下一步是获取元数据并动态调用其引用的成员。考虑定义一个类来表示应用程序的命令行。像这样的 CommandLineInfo 类的困难在于用启动应用程序的实际命令行数据填充该类。然而，使用反射，你可以将命令行选项映射到属性名称，然后在运行时动态设置属性。列表 17.3 演示了此过程。

## 列表 17.3：动态调用成员

```
using System;
using System.Diagnostics;

public partial class Program
{
    public static void Main(string[] args)
    {
        string errorMessage;
        CommandLineInfo commandLine = new CommandLineInfo();
        if (!CommandLineHandler.TryParse(
            args, commandLine, out errorMessage))
        {
            Console.WriteLine(errorMessage);
            DisplayHelp();
        }

        if (commandLine.Help)
        {
            DisplayHelp();
        }
        else
        {
            if (commandLine.Priority !=
                ProcessPriorityClass.Normal)
            {
                // Change thread priority
            }
        }
        // ...
    }
```

CAS 权限在此情况下设置好以允许私有成员调用，因为程序从本地计算机运行。默认情况下，本地安装的程序属于受信任区域并被授予适当的权限。从远程位置运行的程序需要被明确授予此类权限。

## 对泛型类型的反射

CLR 2.0 版本中引入泛型类型需要额外的反射功能。对泛型的运行时反射确定类或方法是否包含泛型类型，以及它可能包含的任何类型参数或参数。

## 确定类型参数的类型

与你可以使用 typeof 运算符对非泛型类型检索 System.Type 实例的方式相同，你也可以对泛型类型或泛型方法中的类型参数使用 typeof 运算符。列表 17.4 将 typeof 运算符应用于 Stack 类的 Add 方法中的类型参数。

## 列表 17.4：声明 Stack<T> 类

```
public class Stack<T>
{
    // ...
    public void Add(T i)
    {
        // ...
        Type t = typeof(T);
        // ...
    }
    // ...
}
```

一旦你拥有了类型参数的 Type 对象的实例，你就可以对类型参数本身使用反射来确定其行为并更有效地将 Add 方法定制为特定类型。

## 确定类或方法是否支持泛型

在 CLR 2.0 版本的 System.Type 类中，添加了一些方法来确定给定类型是否支持泛型参数和参数。泛型参数是类型参数

