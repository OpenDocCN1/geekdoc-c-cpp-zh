
**清单 9.2：演示多播委托**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MulticastDelegateExample
{
    public class MulticastDelegateDemo
    {
        public delegate void MyMulticastDelegate();

        public static void Method1()
        {
            Console.WriteLine("Hello world");
        }

        public static void Method2()
        {
            Console.WriteLine("Demonstrating a Multicast Delegate");
        }

        public static void Method3()
        {
            Console.WriteLine("Getting Invoked by a Multicast Delegate");
        }

        public static void Main(string[] args)
        {
            MyMulticastDelegate md = new MyMulticastDelegate(Method1);
            md += new MyMulticastDelegate(Method2);
            md += new MyMulticastDelegate(Method3);
            md();
            Console.ReadLine();
        }
    }
}
```

在清单 9.2 中，我们声明了一个名为 `MyMulticastDelegate` 的多播委托，它可以保存对一个以上目标方法的引用。请注意，我们定义了一个 void 委托类型，它引用返回类型为 void 的方法。

> **注意**
>
> 如果为被多播委托引用的方法指定返回类型，则仅返回委托调用的最后一个方法的结果。在这种情况下，所有返回类型为 void 的方法的结果都会被丢弃。

按 F5 键运行应用程序。MulticastDelegateExample 应用程序的输出显示如下，见图 C# 9.2：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_300_0.png)

**图 C# 9.2**

在图 C# 9.2 中，请注意方法是以添加到多播委托的顺序被调用的。您还可以使用 `-=` 运算符从委托中移除引用，如以下代码片段所示：

```csharp
md -= Method2;
```

调用委托对象时，它仅返回 Method1 和 Method3 的结果，因为 Method2 已被解除引用。

现在，让我们在下一节学习 C# 中的事件和事件处理机制。

## 使用 C# 事件

您已了解到委托可用于保存对目标方法的引用；然而，委托的用途并不仅限于引用方法。您可以使用委托在 C# 中实现事件处理机制。

在 C# 中，事件是一种机制，通过它当用户或某些程序代码或系统本身执行操作时，类会收到通知。C# 是一种事件驱动语言，其中程序的流程由用户操作控制，例如从键盘按下键或用鼠标单击某个控件。委托用于在 C# 中实现事件。

事件可以在类内部使用 `event` 关键字声明。声明事件的语法如下：

```csharp
[access_modifier] event delegate_type event_identifier;
```

引发或触发事件的类称为事件发布者，而包含处理已引发事件的代码的类则称为事件订阅者。接下来，让我们学习 C# 中事件是如何引发和处理的。

### 引发事件

如前所述，首先使用 `event` 关键字声明事件。一旦声明事件，您就可以定义一个在事件发生时被调用的委托。委托可以引用一个或多个目标方法，当事件被引发时这些方法会被调用。执行以下步骤在 C# 中创建和引发事件：

- 1. 定义委托类型，以便在创建自定义事件时，有一个可与 `event` 关键字一起使用的委托。
- 2. 定义一个将包含由委托实现的事件的类。实际触发或引发事件的代码也在该类中定义。最后，定义一个调用事件的方法。
- 3. 定义一个或多个类，以便您可以将方法连接到事件。在您定义的每个类中，使用 `+=` 运算符将方法与定义了事件的类中的事件关联，或使用 `-=` 运算符移除特定事件。还包括您已与事件关联的方法的方法定义。
- 4. 最后，触发事件。创建包含事件声明以触发事件的类的对象。此外，实例化包含事件定义的类。

现在，让我们创建一个名为 EventHandlingExample 的应用程序。执行以下步骤以引发事件：

- 1. 重复本章“创建单播委托”部分中的步骤 1 到 3。
- 2. 在名称文本框中输入 EventHandlingExample 以指定应用程序的名称，并在位置组合框中指定保存应用程序所需的位置。在此情况下，我们选择了默认位置，即 C:\Users\temp\Documents\Visual Studio 2010\Projects。
- 3. 单击“确定”按钮。EventHandlingExample 应用程序已创建。
- 4. 在 Program.cs 文件中添加清单 9.3 中给出的代码：

**清单 9.3：引发 C# 事件**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace EventHandlingExample
{
    public delegate void EventDelegate();

    public class RaiseEvent
    {
        public event EventDelegate MyEvent;

        public void OnEventOccured()
        {
            if (MyEvent != null)
            {
                MyEvent();
            }
        }

        public void FireAnEvent()
        {
            OnEventOccured();
        }
    }
}
```

在清单 9.3 中，我们定义了一个名为 **EventDelegate** 的委托，它引用一个方法。接下来，我们定义了一个类 **RaiseEvent**，它声明了一个由 **EventDelegate** 委托实现的事件。该类定义了一个名为 **OnEventOccured()** 的方法，它引发事件。我们有一个名为 **FireAnEvent()** 的方法，实际调用事件。请注意，在清单 9.3 中，我们使用以下代码片段检查事件的订阅者：

```csharp
if (MyEvent != null)
```

如果前述代码片段的计算结果为 true，则事件被触发。

### 为已引发的事件添加事件处理程序

引发事件后，必须有该事件的订阅者。订阅者监听已发生的事件并实现一个方法，该方法将在事件被引发时被调用。让我们在 **EventHandlingExample** 应用程序中执行以下步骤，以学习如何处理已触发的事件：

- 1. 在 **Program.cs** 文件中插入 **清单 9.4** 中给出的代码：

**清单 9.4：处理 C# 事件**

```csharp
public class HandleEvent1
{
    public void FirstEventHandler()
    {
        Console.WriteLine("Event handling inside class HandleEvent1!");
    }
}

class HandleEvent2
{
    public static void SecondEventHandler()
    {
        Console.WriteLine("Event handling inside class HandleEvent2!");
    }

    public static void Main(string[] args)
    {
        RaiseEvent re = new RaiseEvent();
        HandleEvent1 he = new HandleEvent1();
        re.MyEvent += new EventDelegate(he.FirstEventHandler);
        re.MyEvent += new EventDelegate(SecondEventHandler);
        re.FireAnEvent();
        Console.ReadLine();
    }
}
```

在清单 9.4 中，我们在类 **HandleEvent1** 和 **HandleEvent2** 中分别定义了两个事件处理程序，名为 **FirstEventHandler** 和 **SecondEventHandler**。请注意，这些事件处理程序的签名与委托 **EventDelegate** 的签名相匹配。接下来，我们使用 `+=` 运算符将事件处理程序添加到事件 **MyEvent**。最后，我们调用了方法 **FireAnEvent()** 来触发事件。

> **注意**
>
> *您也可以使用赋值运算符 `=` 将事件处理程序添加到事件，但在这种情况下，所有先前的引用都会被丢弃，只保留最后一个引用。*

- 2. 按 **F5** 键运行 **EventHandlingExample** 应用程序。输出显示如下，见图 C# 9.3：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_303_0.png)

**图 C# 9.3**

现在，让我们在下一节学习匿名方法和 lambda 表达式。

## 探索匿名函数

用作委托类型的内联语句或表达式称为匿名函数。每当您需要初始化命名委托或将其作为方法参数传递而不是命名委托类型时，都可以使用匿名函数。

在 C# 中有两种匿名函数，lambda 表达式和匿名方法，将在下面讨论。

### Lambda 表达式

在 .NET Framework 3.5 中，引入了一种名为 lambda 表达式的匿名方法新语法。包含表达式和语句以创建委托或表达式树类型的匿名函数称为 lambda 表达式。lambda 表达式使用 lambda 运算符 `=>`（读作“goes to”）。lambda 运算符具有右结合性，其优先级也与赋值 (`=`) 运算符相同。输入参数指定在 lambda 运算符的左侧，表达式或语句指定在右侧，如以下代码片段所示：

```csharp
(input parameter) => expression
```

如果 lambda 表达式只有一个参数，可以省略括号。如果有多个参数，则需要括号。如果有多个参数，则用逗号 (,) 分隔参数。如果使用 lambda 表达式，则无需在声明中添加变量，因为编译器会自动添加变量。

> **注意**
>
> *表达式树基本上用于以类似树的结构表示代码。树中的每个节点都是一个表达式，例如方法调用或二元运算，如 `x + y`。*

使用 lambda 表达式，您可以内联声明方法代码，而无需使用委托声明方法，因为 lambda 表达式具有简洁的语法。

lambda 表达式在编写 LINQ 查询表达式时非常有帮助，因为它们提供了一种非常紧凑和安全的方式来编写作为参数传递以供进一步求值的函数。
