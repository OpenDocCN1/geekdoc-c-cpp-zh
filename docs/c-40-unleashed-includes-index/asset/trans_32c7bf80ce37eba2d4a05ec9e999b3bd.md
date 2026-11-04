
一个常见问题涉及动态对象的调试。在以静态类型为标准的环境中，执行调试任务时可以直接看到对象的成员。不必担心，`GetDynamicMemberNames` 方法可供你重写，以提供调试信息：

```
public override IEnumerable<string> GetDynamicMemberNames()
{
    return _bag.Keys;
}
```

Visual Studio 2010 已经能够识别可提供动态成员名称列表的对象，如图 22.19 所示。展开成员列表时，会调用前面的方法，随后进行一系列调用以获取这些成员的值。说到调试，甚至可以使用即时窗口执行动态操作。由于这些特性，调试动态类型化代码相对容易。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1173_0.png)

图 22.19 支持 C# 4.0 动态功能的一些调试特性。

## DynamicMetaObject 入门

正如你之前所见，使用 `DynamicObject` 可以让对象参与各种操作的绑定过程。这实际上与 DLR 中的一条通用设计理念一致：对象有机会首先为绑定操作定义含义，然后才由特定语言的绑定器介入协助。

这类动态对象的核心优势之一是，它们遵循一种允许跨不同语言使用的协议。因此，我们自己编写的 `Bag` 对象可以在 C# 之外的语言中使用（例如，在 IronPython 中使用，如图 22.20 所示）。

不过，这种用于与动态对象互操作的通用协议位于比 `DynamicObject` 基类型更低的层级。这里就轮到 `IDynamicMetaObjectProvider` 接口和辅助的 `DynamicMetaObject` 类型登场了。这两个类型的定义如图 22.21 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1174_0.png)

图 22.20 在 IronPython 中使用我们的 `Bag` 动态对象。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1174_1.png)

图 22.21 动态对象互操作性的核心类型。

`DynamicObject` 与 `DynamicMetaObject` 的关键差异之一在于 `Bind` 操作的签名不同，这些操作对应于 `DynamicObject` 中的 `Try` 方法族。尽管这些方法也会接收一个 `Binder` 对象，但它们的参数和返回类型使用 `DynamicMetaObject` 对象。

`DynamicMetaObject` 实例包含的关键信息是一个表达式树，它表示为了计算其值而必须执行的代码。DLR 的职责是将此类表达式树拼接起来，构成高效的调用点，而这些调用点可在运行时编译为 IL 代码。在这里，对象可以完全控制定义将产生其值的操作的语义，从而能够发出非常高效的代码。

除了保存在 `Expression` 属性中的表达式树之外，`DynamicMetaObject` 还可以有一组绑定限制，用于确定何时允许绑定到该对象。此类限制可以基于类型，可以写成执行某种检查的表达式树，或者限制绑定到特定实例的有效性。

前面在本章的“动态调用点与绑定器”一节中查看调用点时，我们看到为动态调度点生成的代码具有以下形式：

```
(CallSite site, object a, object b) =>
{
    if (a is int && b is int)
        return (int)a + (int)b;
    if (a is DateTime && b is TimeSpan)
        return (DateTime)a + (TimeSpan)b;
    return site.Update(site, a, b);
}
```

回想一下，这段代码的生成方式基于绑定器与 DLR 之间的交互。一旦遇到 `a` 和 `b` 是两个 `Int32` 值的情况，DLR 就会将请求交给 C# 运行时绑定器。如果存在动态对象（基于 `IDynamicMetaObjectProvider` 进行检查），则请求会被交给重写后的 `BindBinaryOperation` 方法。图 22.22 展示了绑定限制与生成的分支指令之间的关系。

```
public class DynamicMetaObject
{
    public BindingRestrictions Restrictions { get; }
    public Expression Expression { get; }
    ...
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1175_0.png)

图 22.22 限制与表达式如何关联到调用点。

无论采用哪条路径，底层都遵循这种互操作协议，将绑定限制和表达式交回给 DLR。在 C# 运行时库提供协助的情况下，它会把绑定限制和用于计算值的表达式交还给我们。

有了这些信息，DLR 可以采用不同的策略来优化调用点，这些策略称为不同的缓存级别。我们不会详细讨论这些实现细节，而是请参阅 dlr.codeplex.com 上的 DLR 文档。可以说，手动实现 `DynamicMetaObject` 类型将为执行动态操作时运行的代码带来极大的灵活性。

使用高效代码生成的一个示例是缓存很少更改的结果值。不可变类型是这一做法的极端情况：获取成员的操作（甚至基于对象中保存的不可变数据计算值的实例方法）都可以简化为返回常量值。尽管对对象操作的首次命中可能需要一段时间来计算结果值，但不可变性保证它永远不会改变，因此发出的表达式树可以简单地返回一个常量。

在可变性谱系的另一类中，是很少更改的对象。对于这些对象，可以应用相同的缓存技巧，但需要结合某种失效逻辑。为实现这一点，重写的 `BindSetMember` 会设置一个与该成员名称关联的标志，以指示该值已失效。为 `BindGetMember` 发出的代码将包含对失效标志的检查。根据该标志的值，返回常量的表达式将受到使用限制。当该标志被设置时，将触发一条重新计算该值的路径。

## 动态操作

为了结束对 `DynamicObject` 和 `DynamicMetaObject` 的概述，我们将快速看一下可以通过重写这些基类上的方法来特化的各种操作。其中一些操作具有 C# 表示法，而另一些仅存在于动态语言中。

- 二元操作，例如数学逻辑运算符和（不）相等运算符。例如，a + b、a > b、a && b。
- 一元操作，例如逻辑非、按位取反或数值负号/正号。例如，-a、!a。
- 获取和设置成员，这对应于 CLR 术语中的属性或字段。例如，a.Foo 或 a.Bar = 5。
- 获取和设置索引，以便对集合、向量等对象进行索引访问。例如，a[0] 或 vector["x*"] = 1。
- 将对象转换为某种指定类型，可以是显式转换（如强制转换语法）或隐式转换。例如，(Hashtable)bag。
- 调用成员，这对应于 CLR 术语中的方法（例如，a.Print("Hello")）。C# 中的方法调用语法映射到此操作。在某些动态语言中，不存在调用成员这回事，而是将所有“方法”编码为包含函数对象的可获取成员。要调用这些成员，需使用直接调用操作，如下所述。
- 对对象的直接调用类似于 C# 中的委托调用。例如，a(42)。一等动态函数可由该操作驱动。
- 以动态方式创建实例在 C# 中不直接支持，但在各种动态语言中受支持。例如，dynamic new Bag。
- 删除成员和索引是另一种在 C# 中缺少某些语法表现的操作，但它在动态语言中早已存在。例如，在 Python 中，你会编写 del bag.Name。

例如，要处理删除成员操作，可以用 `TryDeleteMember` 的重写来扩展我们的 `Bag` 动态对象：

```
public override bool TryDeleteMember(DeleteMemberBinder binder)
{
    return _bag.Remove(binder.Name);
}
```

为了演示这个专用操作的实际效果，我们可以再次使用 IronPython 控制台，甚至可以通过将调试器附加到 ipy.exe 进程来进行调试。启动 REPL 循环后，在 Visual Studio 2010 中转到“工具”>“附加到进程”，并在 `TryDeleteMember` 方法上设置断点。现在在 IronPython 中输入以下代码：

```
import sys
sys.path.append(r"c:\temp")              #wherever the Bag assembly lives

import clr
clr.AddReferenceToFile("CS40Dynamic.exe") #whatever the Bag assembly file is
from CS40Dynamic import *                  #the namespace containing Bag

person = Bag()
person.Name = "Lisa"
del person.Name
```

图 22.23 显示，一旦我们使用 Python 的 `del` 关键字删除成员，调试器就命中了断点。这体现了 DLR 以跨语言方式统一动态对象和动态操作的能力。

## 总体架构

为了结束对 DLR 内部的讨论，让我们看一下可用基础设施的概览图。图 22.24 展示了 DLR 处于支持动态功能的语言与目标对象域之间。

