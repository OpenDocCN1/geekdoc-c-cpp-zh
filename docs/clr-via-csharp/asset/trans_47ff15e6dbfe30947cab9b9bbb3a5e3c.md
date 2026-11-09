

```csharp
        Employee e = (Employee) o;
        ...
    }
}
```

在 **Main** 方法中，会构造一个 **Manager** 对象并将其传递给 **PromoteEmployee**。这段代码可以编译并执行，因为 **Manager** 最终派生自 **Object**，而 **PromoteEmployee** 期望的正是 **Object**。进入 **PromoteEmployee** 后，CLR 会确认 `o` 引用的对象要么是 **Employee**，要么是派生自 **Employee** 的类型。由于 **Manager** 派生自 **Employee**，所以 CLR 执行强制转换，并允许 **PromoteEmployee** 继续执行。

在 **PromoteEmployee** 返回后，**Main** 会构造一个 **DateTime** 对象并将其传递给 **PromoteEmployee**。同样，**DateTime** 派生自 **Object**，编译器可以毫无问题地编译调用 **PromoteEmployee** 的代码。然而，在 **PromoteEmployee** 内部，CLR 会检查强制转换，并检测到 `o` 引用的是 **DateTime** 对象，因此它不是 **Employee**，也不是派生自 **Employee** 的任何类型。此时，CLR 不允许该强制转换，并抛出 `System.InvalidCastException`。

如果 CLR 允许该强制转换，就不会有类型安全，结果也将不可预测，包括可能因类型能够轻易伪装成其他类型而导致应用程序崩溃和安全漏洞。类型伪装是许多安全漏洞的根源，并会损害应用程序的稳定性和健壮性。因此，类型安全是 CLR 极其重要的一部分。

顺便说一句，声明 **PromoteEmployee** 方法的正确方式是指定 **Employee** 类型而不是 **Object** 类型作为其参数，这样编译器就会产生编译时错误，使开发人员不必等到运行时异常发生才发现问题。我使用 **Object** 是为了演示 C# 编译器和 CLR 如何处理强制转换和类型安全。

### 使用 C# 的 **is** 和 **as** 运算符进行强制转换

在 C# 语言中，另一种强制转换的方法是使用 **is** 运算符。**is** 运算符检查对象是否与给定类型兼容，其求值结果是 **Boolean**：**true** 或 **false**。**is** 运算符永远不会抛出异常。以下代码演示了这一点：

```csharp
Object o = new Object();
Boolean b1 = (o is Object);    // b1 is true.
Boolean b2 = (o is Employee);  // b2 is false.
```

如果对象引用为 `null`，**is** 运算符始终返回 **false**，因为没有可用于检查其类型的对象。

**is** 运算符通常按如下方式使用：

```csharp
if (o is Employee) {
    Employee e = (Employee) o;
    // Use e within the remainder of the 'if' statement.
}
```

在这段代码中，CLR 实际上会检查对象的类型两次：**is** 运算符首先检查 **o** 是否与 **Employee** 类型兼容。如果兼容，则在 **if** 语句内部，CLR 在执行强制转换时再次验证 **o** 引用的是 **Employee**。CLR 的类型检查提高了安全性，但确实会带来性能开销，因为 CLR 必须确定变量（**o**）所引用对象的实际类型，然后 CLR 必须遍历继承层次结构，将每个基类型与指定类型（**Employee**）进行对比检查。由于这种编程范式非常常见，C# 提供了一种简化此代码并提高其性能的方法，即提供 **as** 运算符：

```csharp
Employee e = o as Employee;
if (e != null) {
    // Use e within the 'if' statement.
}
```

在这段代码中，CLR 会检查 **o** 是否与 **Employee** 类型兼容；如果兼容，**as** 会返回对同一对象的非 **null** 引用。如果 **o** 与 **Employee** 类型不兼容，**as** 运算符返回 **null**。请注意，**as** 运算符会使 CLR 仅验证一次对象的类型。**if** 语句只是检查 **e** 是否为 **null**；这种检查比验证对象类型执行得更快。

**as** 运算符的工作方式与强制转换相同，不同之处在于 **as** 运算符永远不会抛出异常。相反，如果对象无法强制转换，结果就是 **null**。你需要检查结果引用是否为 **null**，否则尝试使用结果引用将导致抛出 **System.NullReferenceException**。以下代码演示了这一点：

```csharp
Object o = new Object();    // Creates a new Object object
Employee e = o as Employee; // Casts o to an Employee
// The cast above fails: no exception is thrown, but e is set to null.

e.ToString();  // Accessing e throws a NullReferenceException.
```

为了确保你理解了刚刚介绍的所有内容，请做下面的小测验。假设存在以下两个类定义：

```csharp
internal class B {   // Base class
}

internal class D : B { // Derived class
}
```

现在检查表 4-3 中的 C# 代码行。对于每一行，判断该行是能够成功编译并执行（下表中标记为 OK）、导致编译时错误（CTE），还是导致运行时错误（RTE）。

表 4-3 **类型安全测验**

| 语句 | OK | CTE | RTE |
| :--- | :---: | :---: | :---: |
| Object o1 = new Object(); | ✓ | | |
| Object o2 = new B(); | ✓ | | |
| Object o3 = new D(); | ✓ | | |
| Object o4 = o3; | ✓ | | |
| B b1 = new B(); | ✓ | | |
| B b2 = new D(); | ✓ | | |
| D d1 = new D(); | ✓ | | |
| B b3 = new Object(); | | ✓ | |
| D d2 = new Object(); | | ✓ | |
| B b4 = d1; | ✓ | | |
| D d3 = b2; | | ✓ | |
| D d4 = (D) d1; | ✓ | | |
| D d5 = (D) b2; | ✓ | | |
| D d6 = (D) b1; | | | ✓ |
| B b5 = (B) o1; | | | ✓ |
| B b6 = (D) b2; | ✓ | | |

> **注意** C# 允许类型定义转换运算符方法，如第 9 章“参数”中的“转换运算符方法”一节所述。这些方法仅在使用强制转换表达式时调用；使用 C# 的 **as** 或 **is** 运算符时永远不会调用它们。

### 命名空间和程序集

命名空间允许对相关类型进行逻辑分组，开发人员通常使用它们来更容易地定位特定类型。例如，**System.Text** 命名空间定义了一组用于执行字符串操作的类型，**System.IO** 命名空间定义了一组用于执行 I/O 操作的类型。以下代码构造了一个 **System.IO.FileStream** 对象和一个 **System.Text.StringBuilder** 对象：

```csharp
public sealed class Program {
    public static void Main() {
        System.IO.FileStream fs = new System.IO.FileStream(...);
        System.Text.StringBuilder sb = new System.Text.StringBuilder();
    }
}
```

如你所见，这段代码相当冗长；如果有一些简写方式来引用 **FileStream** 和 **StringBuilder** 类型以减少键入，那就好了。幸运的是，许多编译器确实提供了减少程序员键入的机制。C# 编译器通过 **using** 指令提供此机制。以下代码与前面的示例相同：

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

对编译器而言，命名空间只是一种简单方式，通过在类型名称前加上由点分隔的一些符号，使类型名称更长、更可能唯一。因此，编译器会将此示例中对 **FileStream** 的引用解释为 **System.IO.FileStream**。同样，编译器会将 **StringBuilder** 的引用解释为 **System.Text.StringBuilder**。

使用 C# 的 **using** 指令完全是可选的；如果你愿意，随时可以键入类型的完全限定名。C# 的 **using** 指令会指示编译器尝试在类型名称前添加不同的前缀，直到找到匹配项。

> **重要** CLR 对命名空间一无所知。当你访问某个类型时，CLR 需要知道该类型的完整名称（可能是一个包含句点的很长名称）以及哪个程序集包含该类型的定义，以便运行时能够加载正确的程序集、找到该类型并对其进行操作。

在前面的代码示例中，编译器需要确保引用的每个类型都存在，并且我的代码以正确方式使用该类型：调用存在的方法、向这些方法传递正确数量的参数、确保参数类型正确、正确使用方法返回值等。如果编译器在源文件或任何引用的程序集中找不到具有指定名称的类型，它会将 **System.IO.** 添加到类型名称前，并检查生成的名称是否与现有类型匹配。如果编译器仍然找不到匹配项，它会将 **System.Text.** 添加到类型名称前。前面显示的两个 **using** 指令让我可以直接在代码中键入 **FileStream** 和 **StringBuilder**——编译器会自动将引用扩展为 **System.IO.FileStream** 和 **System.Text.StringBuilder**。我相信你可以很容易地想象这节省了多少键入，以及代码读起来整洁了多少。

在检查类型定义时，必须通过使用 **/reference** 编译器开关告诉编译器要检查哪些程序集，如第 2 章“生成、打包、部署和管理应用程序及类型”和第 3 章“共享程序集”中所述

