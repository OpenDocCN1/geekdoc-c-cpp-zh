

在第 9 章中，你编写了第一个真正的基于 Windows 的应用程序，并了解到使用 C# 和 Visual Studio 的拖放构建方式开发图形用户界面是多么容易。此外，你还了解到，.NET Framework `class` 库中包含许多位于 `System.Windows.Forms` 命名空间中的预定义类，它们使你能够将 `Label`、`Button` 和 `TextBox` 等控件对象添加到 Windows Form 容器类的对象中。最后，你学习了一种新的编程方式，它基于对按钮单击等事件进行交互式响应。

在本章中，你将通过编写额外的事件处理方法来扩展这些知识，以捕获并响应用户输入。你将创建带有菜单和其他小部件的应用程序，例如列表框、单选按钮、组合框和复选框，并能够显示和响应它们。你将探索为 Windows 应用程序触发或引发的其他类型事件。

本章首先介绍委托。理解委托的用途会让你更清楚事件背后发生了什么。本章其余部分重点介绍如何向 Windows 应用程序添加控件并为其事件编程。完成本章时，你将能够创建非常复杂、高度交互的基于 Windows 的应用程序。

## 委托

委托构成了 C# 中事件的基础。**委托**是一种特殊的 .NET 类，其实例存储的是对方法的引用（地址），而不是实际数据。你已经习惯通过参数将数据传入方法。委托使你能将方法作为参数传入其他方法。除了响应 GUI 事件的 Windows 应用程序之外，委托也用于其他应用程序；然而，正是它们与事件的关系，使它们有趣并值得在本节中介绍。

### 定义委托

`delegate` 基类类型定义在 `System` 命名空间中。委托与你已经使用过的其他预定义类和用户定义类之间存在一些语法差异。首先，委托的声明看起来更像方法声明，而不是类定义；不过它没有方法体。它以关键字 `delegate` 开头，以带括号的参数列表后跟分号结尾。每个 `delegate` 类型都有一个签名，其中可以包含零个或多个参数。请记住，方法的**签名**包括其名称、参数数量和参数类型。方法的签名不包括 `return` 类型。与方法类似，委托的标头中可以包含 `return` 类型或关键字 `void`。然而，与方法不同，委托的 `return` 类型会成为其标识签名的一部分。示例 10-1 定义了一个不接受参数并返回 `string` 的委托类型。

**示例 10.1**

```csharp
delegate string ReturnsSimpleString( );
```

定义 `delegate` 类型时，你指明了该 `delegate` 表示哪些类型的方法。这种指明是通过 `delegate` 签名完成的，这一点非常重要。它规定了方法若要被该 `delegate` 引用，其签名必须是什么样子。

> **注意**
>
> 在 C# 中，你可以把 `delegate` 视为定义或命名方法签名的一种方式。

给定示例 10-1 中定义的 `delegate` 签名，任何具有零个参数并返回 `string` 的方法都可以由 `ReturnsSimpleString` `delegate` 引用。示例 10-2 展示了一个候选方法的标头和方法体。

**示例 10.2**

```csharp
// Method that returns a string.
static string EndStatement( )
{
    return " in 10 years.";
}
```

将示例 10-2 中 `EndStatement( )` 方法的标头与示例 10-1 中的 `delegate` 进行比较。两者都返回字符串。两者都有零个参数。`delegate` 不规定方法体中必须有哪些语句，也不规定方法名称必须是什么，只规定签名必须是什么样子。

> **注意**
>
> 在 C# 中，`delegate` 是作为 `class` 实现的；不过，`delegate` 类的实例也被称为 `delegate`，而不是称为对象。`class` 类型和实例类型使用同一个名称，这一点可能会令人困惑。

### 创建委托实例

要将 `delegate` 与方法关联起来，需要定义一个 `delegate` 实例，并将方法名作为括号内的参数。你以前从字段和属性实例中识别方法的一种方式，是识别出方法名标识符后面跟着一对括号。当你写出不带括号的方法名时，你引用的是该方法的地址。示例 10-3 使用 `EndStatement()` 方法作为参数来实例化 `ReturnsSimpleString` 委托。

**示例 10.3**

```csharp
ReturnsSimpleString saying3 = new ReturnsSimpleString(EndStatement);
```

> **注意** `delegate` 类中委托的构造函数始终只接受一个参数。这是因为你发送的是供构造函数引用的方法名。

注意，尽管 `EndStatement` 是一个方法，`EndStatement` 参数并不包含括号。作为参数发送的是对方法地址的引用。所存储的地址是方法被调用时在内存中的入口点。

### 使用委托

完成示例 10-3 中的实例化后，`delegate` 标识符 `saying3` 引用 `EndStatement()` 方法。任何对 `saying3()` 的使用都会调用 `EndStatement()` 方法。示例 10-4 说明了这一点。

**示例 10.4**

```csharp
MessageBox.Show(saying3());
```

调用 `MessageBox` 类的 `Show()` 方法会调用 `delegate` 实例 `saying3()`，而后者会调用 `EndStatement()` 方法来显示“in 10 years.”。在 `Show()` 方法中调用 `EndStatement()` 方法会产生相同的输出。这是一个简单的示例，但说明了如何使用 `delegate` 调用方法。示例 10-4 并没有直接调用 `EndStatement()` 方法；不过，执行的是其方法体中的语句。

> **注意** 回想一下，要使用 `MessageBox.Show()` 方法，必须添加对 `System.Windows.Forms` 的引用。你可以从**解决方案资源管理器**窗口访问**引用管理器**。为了避免在程序语句中完全限定名称，你还应添加另一条 `using` 语句，
>
> `using System.Windows.Forms;`

示例 10-5 中的程序演示了定义单个 `delegate` 类型、实例化三个 `delegate` 实例以及调用这三个委托。如果不仔细看，`Show( )` 方法的参数看起来像是普通的方法调用。实际上，这些方法是通过委托调用的。注意，`delegate` 实例名和一对括号构成了 `Show( )` 方法的参数。

**示例 10.5**

```csharp
// DelegateExample.cs             Author: Doyle
// After defining a delegate class, three delegate
// instances are instantiated. Delegates are
// used as arguments for the Show( ) method.

using System;
using System.Windows.Forms;

namespace DelegateExample
{
    delegate string ReturnsSimpleString( );

    class DelegateExample
    {
        static void Main ( )
        {
            int age = 18;
            ReturnsSimpleString saying1 =
                new ReturnsSimpleString(AHeading);
            ReturnsSimpleString saying2 =
                new ReturnsSimpleString((age + 10).ToString);
            ReturnsSimpleString saying3=
                new ReturnsSimpleString(EndStatement);
            MessageBox.Show(saying1( ) +
                saying2( ) + saying3( ));
        }

        // Method that returns a string.
        static string AHeading()
        {
            return "Your age will be ";
        }

        // Method that returns a string.
        static string EndStatement( )
        {
            return " in 10 years.";
        }
    }
}
```

