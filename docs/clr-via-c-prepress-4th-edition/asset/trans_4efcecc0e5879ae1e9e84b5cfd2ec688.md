

|  |  |  |  |
|---|---|---|
| `Object o1 = new Object();` | `3` |  |  |
| `Object o2 = new B();` | `3` |  |  |
| `Object o3 = new D();` | `3` |  |  |
| `Object o4 = o3;` | `3` |  |  |
| `B b1 = new B();` | `3` |  |  |
| `B b2 = new D();` | `3` |  |  |
| `D d1 = new D();` | `3` |  |  |
| `B b3 = new Object();` |  | `3` |  |
| `D d2 = new Object();` |  | `3` |  |
| `B b4 = d1;` | `3` |  |  |
| `D d3 = b2;` |  | `3` |  |
| `D d4 = (D) d1;` | `3` |  |  |
| `D d5 = (D) b2;` | `3` |  |  |
| `D d6 = (D) b1;` |  |  | `3` |
| `B b5 = (B) o1;` |  |  | `3` |
| `B b6 = (D) b2;` | `3` |  |  |

> **注意** C# 允许类型定义转换运算符方法，如第 8 章“方法”中的“转换运算符方法”一节所述。这些方法仅在使用强制转换表达式时调用；在使用 C# 的 `as` 或 `is` 运算符时从不调用。

## 命名空间与程序集

命名空间允许对相关类型进行逻辑分组，开发人员通常使用它们来更容易地定位特定类型。例如，System.Text 命名空间定义了一组用于执行字符串操作的类型，而 System.IO 命名空间定义了一组用于执行 I/O 操作的类型。下面是一些构造 System.IO.FileStream 对象和 System.Text.StringBuilder 对象的代码：

```csharp
public sealed class Program {
    public static void Main() {
        System.IO.FileStream fs = new System.IO.FileStream(...);
        System.Text.StringBuilder sb = new System.Text.StringBuilder();
    }
}
```

如你所见，这段代码相当冗长；如果有一些简写方式来引用 FileStream 和 StringBuilder 类型以减少输入量，那就好了。幸运的是，许多编译器确实提供了减少程序员输入量的机制。C# 编译器通过 using 指令提供此机制。以下代码与上一个示例相同：

```csharp
using System.IO;    // Try prepending "System.IO."
using System.Text;  // Try prepending "System.Text."

public sealed class Program {
    public static void Main() {
        FileStream fs = new FileStream(...);
        StringBuilder sb = new StringBuilder();
    }
}
```

对编译器而言，命名空间只是一种简单方式，通过在类型名称前加上由点分隔的符号，使类型名称更长、更可能唯一。因此，编译器会将此示例中对 FileStream 的引用解释为 System.IO.FileStream。类似地，编译器会将 StringBuilder 的引用解释为 System.Text.StringBuilder。

使用 C# using 指令完全是可选的；如果你愿意，随时可以键入类型的完全限定名。C# using 指令指示编译器尝试在类型名称前添加不同前缀，直到找到匹配项。

**重要：** CLR 对命名空间一无所知。当你访问某个类型时，CLR 需要知道该类型的完整名称（可能是一个包含句点的非常长的名称），以及哪个程序集包含该类型的定义，以便运行时能够加载正确的程序集、找到该类型并对其进行操作。

在上一个代码示例中，编译器需要确保引用的每个类型都存在，并确保我的代码以正确方式使用该类型：调用存在的方法、向这些方法传递正确数量的参数、确保参数类型正确、正确使用方法返回值，等等。如果编译器在源文件或任何引用的程序集中找不到具有指定名称的类型，它会在类型名称前添加 System.IO. 并检查生成的名称是否与现有类型匹配。如果编译器仍然找不到匹配项，它会在类型名称前添加 System.Text.。前面显示的两个 using 指令让我只需在代码中键入 FileStream 和 StringBuilder——编译器会自动将引用扩展为 System.IO.FileStream 和 System.Text.StringBuilder。我相信你可以很容易地想象这节省了多少输入量，以及代码读起来要清晰多少。

检查类型定义时，必须通过 /reference 编译器开关告诉编译器要检查哪些程序集，如第 2 章“生成、打包、部署和管理应用程序及类型”和第 3 章“共享程序集和强命名程序集”所述。编译器将扫描所有引用的程序集，查找该类型的定义。一旦编译器找到正确的程序集，程序集信息和类型信息将被发出到生成的托管模块的元数据中。要获取程序集信息，必须将定义任何被引用类型的程序集传递给编译器。默认情况下，即使你没有明确告诉 C# 编译器，它也会自动查找 MSCorLib.dll 程序集。MSCorLib.dll 程序集包含所有核心框架类库（FCL）类型的定义，例如 Object、Int32、String 等。

你可能会想到，编译器处理命名空间的方式存在一些潜在问题：不同命名空间中可能存在两个（或更多）同名类型。Microsoft 强烈建议为类型定义唯一名称。然而，在某些情况下，这根本不可能。运行时会鼓励重用组件。你的应用程序可能利用 Microsoft 创建的一个组件以及 Wintellect 创建的另一个组件。这两家公司可能都提供一个名为 Widget 的类型——Microsoft 的 Widget 做一件事，而 Wintellect 的 Widget 做完全不同的事。在这种情况下，你无法控制类型的命名，因此可以在引用这两个 widget 时使用它们的完全限定名来区分它们。要引用 Microsoft 的 Widget，应使用 Microsoft.Widget；要引用 Wintellect 的 Widget，应使用 Wintellect.Widget。在以下代码中，对 Widget 的引用存在歧义，因此 C# 编译器会生成以下消息：“error CS0104: ‘Widget’ 在 ‘Microsoft.Widget’ 和 ‘Wintellect.Widget’ 之间是模糊引用。”

```csharp
using Microsoft;  // Try prepending "Microsoft."
using Wintellect; // Try prepending "Wintellect."

public sealed class Program {
    public static void Main() {
        Widget w = new Widget();// An ambiguous reference
    }
}
```

要消除歧义，必须明确告诉编译器你要创建哪个 Widget：

```csharp
using Microsoft;  // Try prepending "Microsoft."
using Wintellect; // Try prepending "Wintellect."
```

![](img/3f2c86949cdef7e2f9e27c37c607b28e_104_0.png)

图 4-1 显示某类型命名空间和程序集信息的 SDK 文档。

## 运行时各事物的关系

在本节中，我将解释类型、对象、线程栈和托管堆在运行时的关系。此外，我还将解释调用静态方法、实例方法和虚方法之间的区别。让我们从计算机的一些基础知识开始。我即将描述的内容并非 CLR 特有，但我会先描述它，以便我们有一个可用的基础，然后我会修改讨论以纳入 CLR 特有的信息。

图 4-2 显示了一个已加载 CLR 的 Microsoft Windows 进程。此进程中可能有许多线程。创建线程时，会为其分配 1 MB 的栈。此栈空间用于向方法传递参数以及存放方法内定义的局部变量。在图 4-2 中，显示了一个线程栈的内存（在右侧）。栈从高内存地址向低内存地址构建。在图中，此线程一直在执行一些代码，其栈上已经有一些数据（显示为栈顶部的阴影区域）。现在，假设该线程已执行一些调用 M1 方法的代码。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_104_1.png)

