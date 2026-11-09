
在这段代码中，CLR 实际上会对对象的类型检查两次。`is` 运算符首先检查 `o` 是否与 `Employee` 类型兼容。如果兼容，那么在 `if` 语句内部，CLR 在执行强制转换时会再次验证 `o` 是否引用一个 `Employee`。CLR 的类型检查提高了安全性，但这当然会带来性能开销，因为 CLR 必须确定变量（`o`）所引用的对象的实际类型，然后 CLR 必须遍历继承层次结构，将每个基类型与指定类型（`Employee`）进行核对。由于这种编程范式非常常见，C# 提供了一种简化此代码并提高其性能的方法，即提供 `as` 运算符。

```csharp
Employee e = o as Employee;
if (e != null) {
    // Use e within the ‘if’ statement.
}
```

在这段代码中，CLR 检查 `o` 是否与 `Employee` 类型兼容；如果兼容，`as` 会返回指向同一对象的非 null 引用。如果 `o` 与 `Employee` 类型不兼容，`as` 运算符会返回 `null`。请注意，`as` 运算符使 CLR 只验证一次对象的类型。`if` 语句只是检查 `e` 是否为 `null`；这一检查的执行速度比验证对象类型更快。

`as` 运算符的工作方式与强制转换相同，区别在于 `as` 运算符永远不会抛出异常。相反，如果对象无法转换，结果就是 `null`。你需要检查结果引用是否为 `null`，否则尝试使用结果引用将导致抛出 `System.NullReferenceException`。以下代码演示了这一点。

```csharp
Object o = new Object();       // Creates a new Object object
Employee e = o as Employee;    // Casts o to an Employee
// The cast above fails: no exception is thrown, but e is set to null.

e.ToString();  // Accessing e throws a NullReferenceException.
```

为确保你理解了刚才介绍的所有内容，请做下面的测验。假设存在以下两个类定义。

```csharp
internal class B {    // Base class
}

internal class D : B { // Derived class
}
```

现在检查表 4-3 中的 C# 代码行。对于每一行，判断该行是能够成功编译并执行（在表 4-3 中标记为 OK）、导致编译时错误（CTE），还是导致运行时错误（RTE）。

**表 4-3** 类型安全测验

| 语句 | OK | CTE | RTE |
|---|---|---|---|
| `Object o1 = new Object();` | ✓ |  |  |
| `Object o2 = new B();` | ✓ |  |  |
| `Object o3 = new D();` | ✓ |  |  |
| `Object o4 = o3;` | ✓ |  |  |
| `B b1 = new B();` | ✓ |  |  |
| `B b2 = new D();` | ✓ |  |  |
| `D d1 = new D();` | ✓ |  |  |
| `B b3 = new Object();` |  | ✓ |  |
| `D d2 = new Object();` |  | ✓ |  |
| `B b4 = d1;` | ✓ |  |  |
| `D d3 = b2;` |  | ✓ |  |
| `D d4 = (D) d1;` | ✓ |  |  |
| `D d5 = (D) b2;` | ✓ |  |  |
| `D d6 = (D) b1;` |  |  | ✓ |
| `B b5 = (B) o1;` |  |  | ✓ |
| `B b6 = (D) b2;` | ✓ |  |  |

> **注意** C# 允许类型定义转换运算符方法，如第 8 章“方法”中的“转换运算符方法”一节所述。这些方法仅在使用强制转换表达式时调用；在使用 C# 的 `as` 或 `is` 运算符时，它们永远不会被调用。

## 命名空间与程序集

命名空间允许对相关类型进行逻辑分组，开发人员通常使用它们来更容易地定位特定类型。例如，System.Text 命名空间定义了一组用于执行字符串操作的类型，而 System.IO 命名空间定义了一组用于执行 I/O 操作的类型。下面是一些构造 System.IO.FileStream 对象和 System.Text.StringBuilder 对象的代码。

```csharp
public sealed class Program {
    public static void Main() {
        System.IO.FileStream fs = new System.IO.FileStream(...);
        System.Text.StringBuilder sb = new System.Text.StringBuilder();
    }
}
```

如你所见，这段代码相当冗长；如果有一些简写方式来引用 `FileStream` 和 `StringBuilder` 类型以减少输入，那就好了。幸运的是，许多编译器确实提供了减少程序员输入量的机制。C# 编译器通过 `using` 指令提供这种机制。以下代码与前面的示例相同。

```csharp
using System.IO;      // Try prepending "System.IO."
using System.Text;    // Try prepending "System.Text."

public sealed class Program {
    public static void Main() {
        FileStream fs = new FileStream(...);
        StringBuilder sb = new StringBuilder();
    }
}
```

对编译器而言，命名空间只是一种简单方式：通过在类型名称前加上由点分隔的一些符号，使类型名称更长、更可能唯一。因此，编译器将本示例中对 `FileStream` 的引用解释为 `System.IO.FileStream`。同样，编译器将对 `StringBuilder` 的引用解释为 `System.Text.StringBuilder`。

使用 C# `using` 指令完全是可选的；如果你愿意，随时可以键入类型的完全限定名。C# `using` 指令指示编译器尝试在类型名称前添加不同的前缀，直到找到匹配项。

> **重要** CLR 对命名空间一无所知。当你访问一个类型时，CLR 需要知道该类型的完整名称（这可能是一个包含句点的很长名称）以及哪个程序集包含该类型的定义，以便运行时能够加载正确的程序集、找到该类型并操作它。

在前面的代码示例中，编译器需要确保引用的每个类型都存在，并确保我的代码以正确方式使用该类型：调用存在的方法、向这些方法传递正确数量的参数、确保参数类型正确、正确使用方法返回值，等等。如果编译器在源文件或任何引用的程序集中找不到具有指定名称的类型，它会在类型名称前加上 `System.IO.`，并检查生成的名称是否与现有类型匹配。如果编译器仍然找不到匹配项，它会在类型名称前加上 `System.Text.`。前面展示的两个 `using` 指令让我可以在代码中只键入 `FileStream` 和 `StringBuilder`——编译器会自动将引用扩展为 `System.IO.FileStream` 和 `System.Text.StringBuilder`。我相信你能很容易想象这节省了多少输入，以及代码读起来整洁了多少。

在检查类型定义时，必须通过使用 `/reference` 编译器开关告诉编译器要检查哪些程序集，如第 2 章“生成、打包、部署和管理应用程序及类型”和第 3 章“共享程序集和强命名程序集”所述。编译器将扫描所有引用的程序集，以查找该类型的定义。

编译器找到正确的程序集后，会将程序集信息和类型信息发出到生成的可托管模块的元数据中。要获取程序集信息，必须将定义任何被引用类型的程序集传递给编译器。默认情况下，即使你没有明确告知，C# 编译器也会自动在 MSCorLib.dll 程序集中查找。MSCorLib.dll 程序集包含所有核心框架类库（FCL）类型的定义，例如 Object、Int32、String 等。

可以想象，编译器处理命名空间的方式存在一些潜在问题：不同命名空间中可能存在两个（或更多）同名类型。Microsoft 强烈建议为类型定义唯一名称。然而，在某些情况下，这根本不可能。运行时会鼓励组件重用。你的应用程序可能利用 Microsoft 创建的某个组件，以及 Wintellect 创建的另一个组件。这两家公司可能都提供一个名为 Widget 的类型——Microsoft 的 Widget 做一件事，而 Wintellect 的 Widget 做完全不同的事。在这种情况下，你无法控制类型的命名，因此可以在引用它们时使用完全限定名来区分这两个 widget。要引用 Microsoft 的 Widget，你会使用 Microsoft.Widget；要引用 Wintellect 的 Widget，你会使用 Wintellect.Widget。在以下代码中，对 Widget 的引用存在歧义，因此 C# 编译器生成以下消息：error CS0104: 'Widget' is an ambiguous reference between 'Microsoft.Widget' and 'Wintellect.Widget'。

```csharp
    using Microsoft;  // Try prepending "Microsoft."
    using Wintellect; // Try prepending "Wintellect."

    public sealed class Program {
        public static void Main() {
            Widget w = new Widget(); // An ambiguous reference
        }
    }
```

要消除歧义，必须明确告诉编译器你要创建哪个 Widget。

```csharp
    using Microsoft;  // Try prepending "Microsoft."
    using Wintellect; // Try prepending "Wintellect."

    public sealed class Program {
        public static void Main() {
            Wintellect.Widget w = new Wintellect.Widget(); // Not ambiguous
        }
    }
```

C# using 指令还有另一种形式，允许为单个类型或命名空间创建别名。如果你只使用某个命名空间中的少数几个类型，并且不想让该命名空间的所有类型污染全局命名空间，这会很方便。以下代码演示了解决前面代码所示歧义问题的另一种方法。

```csharp
    using Microsoft;  // Try prepending "Microsoft."
    using Wintellect; // Try prepending "Wintellect."
```
