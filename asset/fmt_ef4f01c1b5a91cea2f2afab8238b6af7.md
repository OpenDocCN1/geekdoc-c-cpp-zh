
该元素可以作为应用程序配置文件的子元素放置，以便它适用于所有程序集；也可以作为应用程序配置中`<dependentAssembly>`元素的子元素，以便其适用于特定的程序集。当 CLR 处理应用程序的配置文件时，它将看到不应在 GAC 中检查发布者策略程序集。因此，CLR 将继续使用旧版本的程序集运行。但请注意，CLR 仍然会检查并应用 Machine.config 文件指定的任何策略。

> **重要** 发布者策略程序集是发布者对程序集不同版本之间的兼容性发表声明的一种。如果程序集的新版本并不打算与早期版本兼容，则发布者不应创建发布者策略程序集。通常，当你构建修复了 bug 的程序集新版本时，请使用发布者策略程序集。你应该对程序集的新版本进行向下兼容性测试。另一方面，如果你正在向程序集添加新功能，则你应该认为该程序集与之前的版本没有关系，并且你不应该发布发布者策略程序集。此外，无需对此类程序集进行任何向下兼容性测试。

# 第 4 章

## 类型基础

- 在本章中：
- 所有类型都派自 `System.Object` ........................... 91
- 类型之间的强制转换 ................................................................ 93
- 命名空间与程序集............................................................... 97
- 运行时的相互关系 ................................................ 102

在本章中，我将介绍与处理类型和公共语言运行时 `CLR` 关的基础信息。特别是，我将讨论你可以预期每个类型都具备的最小行为集。我将描述类型安全、命名空间、程序集以及将对象从一种类型转换为另一种类型的各种方法。最后，我将通过解释类型、对象、线程栈和托管堆在运行时如何相互关联来结束本章。

### 所有类型都派自 System.Object

运行时要求每个类型最终都派自 `System.Object` 类型。这意味着以下两个类型定义是相同的：

```csharp
// 隐式派自 Object // 显式派自 Object
class Employee {
class Employee : System.Object {
}
```

由于所有类型最终都派自 `System.Object`，因此可以保证每种类型的每个对象都有一组最小的方法。具体来说，`System.Object` 类提供了表 4-1 中列出的公共实例方法。

## 第二部分 类型的设计

### 表 4-1 System.Object 的公共方法

| 公共方法 | 描述 |
| --- | --- |
| `Equals` | 如果两个对象具有相同的值，则返回 true。有关此方法的更多信息，请参见第 5 章“原始类型、引用类型和值类型”中的“对象等性与标识”节。 |
| `GetHashCode` | 返回此对象值的哈希代码。如果对象的要被用作哈希表中的键，则类型应该重写此方法。该方法应该为对象提供良好的分布。遗憾的是，大多数类型并没有被用作哈希表中的键；此方法本应定义在接口中。有关此方法的更多信息，请参见第 5 章“对象哈希码”节 |
| `ToString` | 默认情况下，返回类型的全名 (`this.GetType().FullName`)。然而，通常会重写此方法，使其返回一个包含对象状态表示的字符串。例如，`Boolean` 和 `Int32` 等类型重写了此方法，以返回其值的字符串表示。为了调试目的，重写此方法也很常见；你可以调用它并获取一个显示对象字段的字符串。事实上，Microsoft Visual Studio 调试器会自动调用它来向你显示对象的字符串表示。注意，`ToString` 需要感知调用线程的 `CultureInfo`。第 14 章“字符、字符串与文本处理”更详细地讨论了 `ToString`。 |
| `GetType` | 返回 `Type` 派生对象的实例，用于标识调用 `GetType` 的对象的类型。返回的 `Type` 对象可以配合反射类用于获取有关对象类型的元数据信息。反射在第 23 章“程序集加载与反射”中讨论。`GetType` 方法是非虚拟的，这防止了类重写其类型，从而违反安全性。 |

此外，派自 `System.Object` 的类型可以访问表 4-2 中列出的保护方法。

### 表 4-2 System.Object 的保护方法

| 保护方法 | 描述 |
| --- | --- |
| `MemberwiseClone` | 此非虚拟方法创建该类型的新实例，并将实例字段设置为与当前对象的字段相同。返回指向新实例的引用。 |
| `Finalize` | 当垃圾回收器确定对象被回收时，会调用此虚拟方法。需要清理的类型应该重写此方法。我将在第 21 章“自动内存管理”中更详细地介绍此方法。 |

`CLR` 要求所有对象都使用 `new` 运算符创建。以下行显示了如何创建 `Employee`：

```csharp
Employee e = new Employee("ConstructorParam");
```

以下是 `new` 运算符的操作：

- 1. 计算所需的字节数，包括 `System.Object`。
- 2. 通过从托管堆为对象分配内存；所有这些都被设置为零 `0`。
- 3. 初始化类型指针和同步块索引。
- 4. 调用类的构造函数，传递任何参数（上例中的字符串 `"ConstructorParam"`）。大多数编译器会在构造函数中生成代码。每个构造函数负责初始化实例字段。最终，会调用 `System.Object` 的构造函数，此方法不返回。

在 `new` 完成所有这些操作后，它返回新创建对象的引用（或指针）。在前面的代码示例中，引用位于变量 `e`，其类型为 `Employee`。

顺便说一下，`new` 运算符没有对应的 `delete` 运算符；没有办法显式释放为它分配的内存。`CLR` 使用垃圾回收环境，自动检测对象不再被使用或访问，并释放对象的内存。

### 类型之间的强制转换

`CLR` 最重要的特性之一是类型安全。在运行时，`CLR` 始终知道对象是什么类型。你可以通过调用 `GetType` 方法发现对象的确切类型。由于此方法是非虚拟的，一个类型无法伪造另一个类型。例如，`Employee` 类型永远无法重写 `GetType` 方法并使其返回 `SuperHero` 类型。

开发者发现有必要将对象强制转换为各种类型。`CLR` 允许将对象强制转换为其任何基类型。你选择的编程语言决定了如何向开发者暴露强制转换操作。例如，`C#` 不需要特殊语法即可将对象强制转换为其任何基类型，因为到类型的转换被认为是安全的隐式转换。然而，`C#` 要求开发者显式将对象强制转换为其任何派生类型，因为此类强制转换在运行时可能会失败。以下代码演示了基类型和派生类型的强制转换：

# 94 第二部分 设计类型

```csharp
// 此类型隐式派自 System.Object。
internal class Employee {
...
}
```

```csharp
public sealed class Program {
    public static void Main() {
        // 不需要强制转换，因为 new 返回一个 Employee
        // 并且 Object 是 Employee 的基类型。
        Object o = new Employee();
        // 需要强制转换，因为 Employee 派自 Object。
        // 其他语言（如 Visual Basic）可能不需要
        // 这种转换即可编译。
        Employee e = (Employee)o;
    }
}
```

此示例展示了你的编译器编译代码所必需的内容。在运行时，`CLR` 会检查强制转换操作，以确保转换始终指向对象的实际类型或其任何基类。例如，以下代码可以编译，但在运行时将抛出 `InvalidCastException`：

```csharp
internal class Employee {
}
internal class Manager : Employee {
}
```

```csharp
public sealed class Program {
    public static void Main() {
        // 构建一个 Manager 对象并将其传递给 PromoteEmployee。
        // Manager 是一个 Object：PromoteEmployee 正常运行。
        Manager m = new Manager();
        PromoteEmployee(m);
        // 构建一个 DateTime 对象并将其传递给 PromoteEmployee。
        // DateTime 并没有派自 Employee。PromoteEmployee
        // 会抛出 System.InvalidCastException 异常。
        DateTime dateTimeYears = new DateTime(2010, 1, 1);
        PromoteEmployee(dateTimeYears);
    }
}
```

```csharp
public static void PromoteEmployee(Object o) {
    // 在此点，编译器并不知道确定 o 指向什么
    // 类型。因此编译器允许代码编译。然而，在运行时，
    // CL晓 o 指向的类型（每次执行转换时），
    // 它会检查对象的类型是否为 Employee 或任何
    // 派自 Employee 的类型。
}
```

# 第4章 类型基础 95

`Employee e = (Employee) o;`
...

在 `Main` 方法中，构建了一个 `Manager` 对象并将其传递给 `PromoteEmployee`。这段代码可以编译并执行，因为 `Manager` 最终派自 `Object`，这正是 `PromoteEmployee` 所预期的。`CLR` 确认 `o` 指向的是一个 `Employee` 或派自 `Employee` 的类型。因为 `Manager` 派自 `Employee`，`CLR` 执行了转换并允许 `PromoteEmployee` 继续执行。

在 `PromoteEmployee` 返回后，`Main` 构建了一个 `DateTime` 对象并将其传递给 `PromoteEmployee`。同样，`DateTime` 派自 `Object`，编译器没有问题地编译调用 `PromoteEmployee` 代码。然而，在 `PromoteEmployee` 内部，`CLR` 检查并检测到 `o` 指向一个 `DateTime` 对象，而不是 `Employee` 或任何派自 `Employee` 的类型。在此处，强制转换抛出了 `System.InvalidCastException`。

如果 `CLR` 允许这种转换，将没有任何类型安全，结果将是不可预测的，包括由于类型能够轻易伪造其他类型而导致应用程序崩溃和安全违露的可能性。类型伪造是许多安全违露的原因，并会损害应用程序的稳定性和健壮性。因此，类型安全是 `CLR` 极其关重要的部分。

正确的声明方式应该是让 `PromoteEmployee` 方法指定 `Employee` 类型而不是 `Object` 类型作为其参数，这样编译器就会产生一个编译时错误，避免开发者等到运行时发生异常时才发现问题。我之所以使用 `Object` 是为了演示 `C#` 编译器和 `CLR` 如何处理强制转换和类型安全。

### 使用 C# 中的 is 和 as 运算符进行转换

在 `C#` 语言中转换的另一种方法是使用 `is` 运算符。`is` 运算符检查对象是否与给定类型兼容，评估结果为布尔值：`true` 或 `false`。`is` 运算符永远不会抛出异常。以下代码演示了：

```csharp
Object o = new Object();
Boolean b1 = (o is Object); // b1 为 true。
Boolean b2 = (o is Employee); // b2 为 false。
```

如果对象引用为 `null`，`is` 运算符始终返回 `false`，因为没有可用对象来检查其类型。

# 第二部分 设计类型

`is` 运算符通常用法如下：

```csharp
if (o is Employee) {
    Employee e = (Employee) o;
    // 在 if 的剩余部分使用 e
}
```

# 第二部分 设计类型

如你所见，代码非常冗长；如果有一些简写方式来引用 `FileStream` 和 `StringBuilder` 类型以减少输入量，那就太好了。幸运的是，许多编译器确实提供了减少程序员输入量的机制。`C#` 编译器使用 `using` 指令提供了这种机制。以下代码与之前的示例相同：

```csharp
using System.IO; // 尝试在前面加上 "System.IO."
using System.Text; // 尝试在前面加上 "System.Text."
public sealed class Program {
    public static void Main() {
        FileStream fs = new FileStream(...);
        StringBuilder sb = new StringBuilder();
    }
}
```

命名空间 `Namespace` 是一种让类型名称变长并通过在前面添加某些符号来增加唯一性的简单方法。因此，编译器会将对 `FileStream` 的引用解释为 `System.IO.FileStream`。同样，编译器将对 `StringBuilder` 的引用解释为 `System.Text.StringBuilder`。

使用 `C#` 指令完全是可选的；如果你愿意，始终可以输入类型的完全限定名。`C#` 的 `using` 指令指示编译器尝试为名称添加不同的前缀，直到找到匹配项为止。

> 重要：`CLR` 对命名空间一无知。当你访问一个类型时，`CLR` 需要知道类型的全名（这可能是一个包含点的很长的名称）以及哪个程序集包含了该类型的定义，以便运行时可以加载正确的程序集、找到该类型并对其进行操作。

在这个代码示例中，编译器需要确保引用的每个类型都存在，并且我的代码以正确的方式使用了该类型：例如调用存在的方法、向这些方法传递正确数量的参数、确保参数是正确的类型、正确地使用方法的返回值等等等。如果编译器在源文件或任何引用的程序集中找不到具有指定名称的类型，它会在类型名称前面加上 `System.IO.` 并检查生成的名称是否与现有的类型匹配。如果编译器仍然找不到匹配项，它会在类型名称前面加上 `System.Text.`。早些展示的两个 `using` 指令仅用于允许在我的代码中直接输入 `FileStream` 和 `StringBuilder`——编译器会自动将这些引用扩展为 `System.IO.FileStream` 和 `System.Text.StringBuilder`。我确定你完全想象这节省了多少时间，以及你的代码变得多整洁。

在检查类型定义时，必须使用 `/reference` 选项告诉编译器要包含哪些程序集，正如第2章“构建、打包、部署和管理应用程序与类型”以及第3章“共享程序集和强命名程序集”中所讨论。编译器将扫描所有引用的程序集以寻找类型定义。一旦编译器找到正确的程序集，程序集和类型信息就会发射到生成的托管元数据中。获取程序集信息，你必须将定义任何引用类型的程序集传递给编译器。默认情况下，如果你不明确告诉它，`C#` 编译器会自动在 `MSCorLib dll` 中查找。`MSCorLib dll` 程序集包含了所有核心框架库 `FCL` 类型的定义，例如 `Object`、`Int32`、`String` 等。

正如你所想象的，编译器处理命名空间的方式存在一些潜在问题：不同的命名空间可能存在两个（或多个）同名的类型。微软强烈建议为类型定义唯一的名称。然而，在某些情况下，这是不可能的。运行时鼓励重用组件。你的应用程序可能会利用微软的一个组件和一个 Intellect 创建的另一个组件。这两家公司可能都提供名为 `Widget` 的类型——微软的 `Widget` 执行某项功能，而 Intellect 的 `Widget` 执行的是完全不同的功能。在这种情况下，你无法控制类型的名称，因此你可以在引用它们时通过它们的完全限定名来区分这两个 widget。要引用微软的 `Widget`，你需要使用 `Microsoft.Widget`；要引用 Intellect.Widget，你需要使用 `Intellect.Widget`。在代码中，对 `Widget` 的引用是歧义的，因此 `C#` 编译器生成了以下消息：“error CS0104: 'Widget' is an ambiguous reference”

```csharp
using Microsoft; // 尝试在前面加上 "Microsoft."
using Intellect; // 尝试在前面加上 "Intellect."
```

```csharp
public sealed class Program {
    public static void Main() {
        Widget w = new Widget(); // 歧义引用
    }
}
```

为了消除歧义，你必须明确告诉编译器你想创建哪个 `Widget`：

```csharp
using Microsoft; // 尝试在前面加上 "Microsoft."
using Intellect; // 尝试在前面加上 "Intellect."
```

```csharp
public sealed class Program {
    public static void Main() {
        Intellect.Widget w = new Intellect.Widget(); // 无歧义
    }
}
```
