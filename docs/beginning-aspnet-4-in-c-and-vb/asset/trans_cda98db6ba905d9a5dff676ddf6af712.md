
```csharp
MemberInfo [] Members = t.GetMembers();

foreach (MemberInfo NextMember in Members)
{
    AddToOutput(NextMember.DeclaringType + " " +
    NextMember.MemberType + " " + NextMember.Name);
}
```

你通过调用 Type 对象的各种属性来实现 AnalyzeType() 方法，以获取有关类型名称所需的信息，然后调用 GetMembers() 方法获取 MemberInfo 对象数组，可用于显示每个成员的详细信息。请注意，你使用辅助方法 AddToOutput() 来构建要在消息框中显示的文本：

```csharp
static void AddToOutput(string Text)
{
    OutputText.Append("\n" + Text);
}
```

使用以下命令编译 TypeView 程序集：

```
csc /reference:System.Windows.Forms.dll Program.cs
```

## 程序集类

Assembly 类定义在 System.Reflection 命名空间中，并提供对给定程序集元数据的访问。它还包含方法，允许你加载甚至执行一个程序集——前提是该程序集是可执行的。与 Type 类一样，Assembly 包含大量方法和属性——太多无法在此全部涵盖。相反，本节仅限于介绍你入门所需并将用于完成 WhatsNewAttributes 示例的方法和属性。

在对 Assembly 实例执行任何操作之前，你需要将相应的程序集加载到正在运行的进程中。你可以使用静态成员 Assembly.Load() 或 Assembly.LoadFrom() 来完成此操作。这两种方法的区别在于，Load() 接受程序集的名称，并且运行时会在多种位置搜索以尝试定位程序集。这些位置包括本地目录和全局程序集缓存。LoadFrom() 接受程序集的完整路径名，并且不会尝试在其他位置查找程序集：

```csharp
Assembly assembly1 = Assembly.Load("SomeAssembly");
Assembly assembly2 = Assembly.LoadFrom
    ("C:\My Projects\Software\SomeOtherAssembly");
```

这两种方法还存在许多其他重载，提供额外的安全信息。加载程序集后，你可以使用其上的各种属性来查找信息，例如其完整名称：

```csharp
string name = assembly1.FullName;
```

## 查找程序集中定义的类型

Assembly 类的一个不错特性是它允许你获取对应程序集中定义的所有类型的详细信息。你只需调用 Assembly.GetTypes() 方法，它返回包含所有类型详细信息的 System.Type 引用数组。然后你可以按照上一节所述操作这些 Type 引用：

```csharp
Type[] types = theAssembly.GetTypes();

foreach(Type definedType in types)
{
    DoSomethingWith(definedType);
}
```

VectorClass。虽然这将是一个命令行应用程序，但由于输出文本很多——太多无法在控制台窗口截图中显示——你将遵循之前的 TypeView 示例，实际上在消息框中显示结果。

该文件名为 LookUpWhatsNew.cs，编译它的命令是：

```
csc /reference:WhatNewAttributes.dll /reference:VectorClass.dll LookUpWhatsNew.cs
```

在该文件源代码中，你首先指明想要引用的命名空间。System.Text 在此是因为你需要再次使用 StringBuilder 对象：

```
using System;
using System.Reflection;
using System.Windows.Forms;
using System.Text;
using WhatsNewAttributes;

namespace LookUpWhatsNew
{
```

包含主程序入口点以及其他方法的类是 WhatsNewChecker。你定义的所有方法都在此类中，该类还包含两个静态字段：outputText，其中包含你在准备写入消息框时逐步构建的文本；backDateTo，存储你选择的日期。自该日期以来所做的所有修改都将被显示。通常，你会显示一个对话框邀请用户选择此日期，但我们不想被这类代码分散注意力。因此，backDateTo 被硬编码为 2010 年 2 月 1 日的值。你在下载代码时可以轻松更改此日期：

```
internal class WhatsNewChecker
{
    private static readonly StringBuilder outputText = new StringBuilder(1000);
    private static DateTime backDateTo = new DateTime(2010, 2, 1);

    static void Main()
    {
        Assembly theAssembly = Assembly.Load("VectorClass");
        Attribute supportsAttribute =
            Attribute.GetCustomAttribute(
                theAssembly, typeof(SupportsWhatsNewAttribute));
        string name = theAssembly.FullName;

        AddToMessage("*Assembly: " + name);

        if (supportsAttribute == null)
        {
            AddToMessage(
                "This assembly does not support WhatsNew attributes");
            return;
        }
        else
        {
            AddToMessage("Defined Types:");
        }

        Type[] types = theAssembly.GetTypes();

        foreach(Type definedType in types)
            DisplayTypeInfo(definedType);

        MessageBox.Show(outputText.ToString(),
```

![](img/d7d2ffa0a76feaab821930e95daace93_410_0.png)

## 图 14-2

请注意，当你列出 VectorClass 程序集中定义的类型时，你实际上获取了两个类：Vector 和嵌入的 VectorEnumerator 类。另请注意，由于本示例中 backDateTo 日期 2 月 1 日是硬编码的，你实际上获取的是 2 月 14 日（添加集合支持时）的属性，但不获取 2 月 10 日（添加 IFormattable 接口时）的属性。

## 摘要

本章并未试图涵盖反射的全部主题。反射是一个广泛的主题，值得单独写一本书。相反，它说明了 Type 和 Assembly 类，它们是通过反射访问广泛功能的主要入口点。

此外，本章演示了反射的一个特定方面，你可能比其他任何方面都更频繁地使用它——自定义属性的检查。你学习了如何定义和应用自己的自定义属性，以及如何在运行时检索有关自定义属性的信息。

第 15 章“错误和异常”探讨了异常和结构化异常处理。

（步骤 5）。然而，如果 try 块内确实发生错误，执行会跳转到 catch 块（步骤 3）。

- 3. 错误条件在 catch 块中处理。
- 4. 在 catch 块结束时，如果存在 finally 块，执行会自动转移到 finally 块。
- 5. finally 块被执行（如果存在）。

实现这一切所使用的 C# 语法大致如下：

```
try
{
    // code for normal execution
}
catch
{
    // error handling
}
finally
{
    // clean up
}
```

实际上，这个主题存在一些变体：

- 你可以省略 finally 块，因为它是可选的。
- 你也可以提供任意数量的 catch 块来处理特定类型的错误。然而，不应过度使用并拥有大量 catch 块，因为这会损害应用程序的性能。
- 你可以完全省略 catch 块，在这种情况下，语法不是用于识别异常，而是作为一种保证当执行离开 try 块时 finally 块中的代码将被执行的方式。这在 try 块包含多个退出点时很有用。

到目前为止一切都很好，但尚未回答的问题是： 如果代码正在 try 块中运行，它如何知道何时在发生错误时切换到 catch 块？如果检测到错误，代码会执行称为抛出异常的操作。换句话说，它实例化一个异常对象类并抛出它：

```
throw new OverflowException();
```

这里，你实例化了 OverflowException 类的异常对象。一旦计算机在 try 块内遇到 throw 语句，它会立即查找与该 try 块关联的 catch 块。如果 try 块关联了多个 catch 块，它会通过检查 catch 块关联的是哪个异常类来识别正确的 catch 块。例如，当 OverflowException 对象被抛出时，执行会跳转到以下 catch 块：

```
catch (OverflowException ex)
{
    // exception handling here
}
```

换句话说，计算机查找指示与同一类（或基类）匹配的异常类实例的 catch 块。

借助这些额外信息，你可以扩展刚刚演示的 try 块。假设为了论证，try 块中可能发生两种严重的错误：溢出和数组越界。假设你的代码包含两个布尔变量 Overflow 和 OutOfBounds，用来指示这些条件是否存在。你已经看到存在一个预定义的异常类来指示溢出（OverflowException）；同样，IndexOutOfRangeException 类存在来处理数组越界的情况。
