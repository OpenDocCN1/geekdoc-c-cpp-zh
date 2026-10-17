
在代码中，CLR 实际上检查了两次对象的类型：该运算符首先检查 `o` 是否与 `Employee` 类型兼容。如果是，在 `if` 语句内部，CLR 在执行转换时会验证 `o` 指向的是一个 `Employee`。CLR 的检查提高了安全性，但无疑是以性能损失为代价的，因为 CLR 必须确定变量 (`o`) 指向的对象的实际类型，然后 CLR 必须遍历继承层次结构，将每个基类型与指定的类型 (`Employee`) 进行对比。由于这种编程范式非常常见，它通过提供运算符提供了一种简化代码并提高性能的方法。

```csharp
Employee e = o as Employee;
if (e != null) {
    // 在 'if' 语句中使用。
}
```

在此代码中，CLR 检查 `o` 是否与 `Employee` 类型兼容，如果是，则返回指向相同对象的非空引用。如果 `o` 与 `Employee` 类型不，`as` 运算符返回 `null`。注意，该运算符导致 CLR 只需验证一次对象的类型；`if` 语句仅检查 `e` 是否为 `null`；这种检查可以比验证对象的类型快得多。

该运算符的作用与转换相同，不同之处在于运算符永远不会抛出异常。如果对象无法转换，结果为 `null`。你可能需要检查结果引用是否为 `null`，否则尝试使用结果引用会导致抛出 `System.NullReferenceException`。以下代码演示了：

```csharp
Object o = new Object(); // 创建一个新的 Object 对象
Employee e = o as Employee; // 转换为 Employee。如果转换失败，结果为 null。
```

当编译器找到正确的程序集后，程序集信息和类型信息会被发射到生成的托管模块的元数据中。要获取程序集信息，你必须将定义任何引用类型的程序集传递给编译器。默认情况下，`C#` 编译器即使在你没有显式告诉它时也会自动在 `MSCorlib.dll` 程序集中查找。`MSCorlib.dll` 包含了所有核心框架类库 (`FCL`) 类型的定义，例如 `Object`、`Int32`、`String` 等。

正如你可能想象的，编译器在处理不同命名空间中的相同名称时存在一些潜在问题。微软强烈建议为类型使用唯一名称。然而，在某些情况下，这实际上是不可能的。运行时鼓励使用组件。你的应用程序可能会利用由微软创建的组件，也会利用由 Intellect 创建的另一个组件。这两家公司可能都提供一种名为 `Widget` 的类型——微软的 `Widget` 执行某件事，而 Intellect 的 `Widget` 执行的是完全不同的事情。在这种情况下，你无法控制类型的命名，因此你可以在引用它们时通过它们的完全限定名来区分这两个 `Widget`。要引用微软的 `Widget`，你将使用 `Microsoft.Widget`；要引用 Intellect 的 `Widget`，你将使用 `Intellect.Widget`。在下面的代码中，对 `Widget` 的引用是歧义的，`C#` 编译器会生成以下消息：`CS0104`：'`Widget`' 在 '`Microsoft.Widget`' 和 '`Intellect.Widget`' 之间存在歧义引用。

```c
using Microsoft; // Try prepending "Microsoft."
using Intellect; // Try prepending "Intellect."

public sealed class Program {
    public static void Main() {
        Widget w = new Widget(); // 一个歧义的引用
    }
}
```

要消除歧义，你必须明确告诉编译器你想创建哪个 `Widget`。

```csharp
using Microsoft; // Try prepending "Microsoft."
using Intellect; // Try prepending "Intellect."

public sealed class Program {
    public static void Main() {
        Intellect.Widget w = new Intellect.Widget(); // 不再歧义
    }
}
```

还有另一种形式的 `C#` 指令，允许你为单个类型或命名空间创建别名。如果你只需要使用命名空间中的几个类型，不想用该命名空间的所有类型来污染全局命名空间，这种方法非常有用。下面的代码演示了解决前面代码中所示歧义问题的另一种方法。

```csharp
using Microsoft; // Try prepending "Microsoft."
using Intellect; // Try prepending "Intellect.",

// 将 IntellectWidget 符号定义为 Intellect.Widget 的别名
using IntellectWidget = Intellect.Widget;

public sealed class Program {
    public static void Main() {
        IntellectWidget w = new IntellectWidget(); // 现在没有错误了
    }
}
```

这些消除类型差异的方法很有用，但在某些场景下，你需要更进一步。想象澳大利亚回镖公司 (`ABC`) 和阿拉斯加船只公司 (`ABC`) 分别创建了一个名为 `BuyProduct` 的类型，并打算将其发布在各自的程序集中。很可能，两者都会创建一个包含名为 `BuyProduct` 类型的 `ABC` 命名空间。任何尝试开发需要既买回镖又买船只的应用程序的人都会遇到麻烦——编程语言提供了一种通过编程区分命名空间的方法。坦率地说，`C#` 编译器提供了一个 `extern alias` 功能，它为你提供了一种解决这种罕见问题的方法。`extern alias` 还允许你从两个（或多个）不同版本的同一个程序集中访问单个类型。有关关于 `extern alias` 的更多信息，请参阅 `C#` 语言规范。

在你的库中，当你设计预计第三方会使用的类型时，你应该将这些类型定义在命名空间中，以便编译器可以轻松地消除歧义。事实上，为了减少冲突的可能性，你应该使用你的公司全称（而不是缩写或简写）作为你的顶层命名空间名称。参考微软 `.NET Framework` 文档，你可以看到微软使用 "`Microsoft`" 命名空间处理微软特定的类型。（参见 `Microsoft.CSharp`、`Microsoft.VisualBasic` 和 `Microsoft.Win32` 命名空间作为示例。）

创建命名空间只需是在你的代码中按如下方式编写命名空间声明（在 `C#` 中）。

```csharp
namespace CompanyName {
    public sealed class A { // 类型定义: CompanyName.A
}

namespace X {
    public sealed class B { ... } // 类型定义: CompanyName.X.B
}
```

上述类定义右侧的注释指示了编译器将发射到类型定义元数据表中的类型真实名称；这是从 `CLR` 角度来看类型的真实名称。

某些编译器完全不支持命名空间，而其他编译器可以自由定义“命名空间”对于特定语言的含义。在 `C#` 中，命名空间指令只是告诉编译器为源代码中出现的每个类型名称加上前缀，以便程序员可以少打一些字。

# 命名空间与程序集的关系

请注意，命名空间和程序集（实现类型的文件）并不一定相关。特别是，属于单个命名空间的各种类型可能实现在多个程序集中。例如，`System.IO.FileStream` 类型实现在 `MSCLib.dll` 程序集中，而 `System.IO.FileSystemWatcher` 类型实现在 `System.dll` 程序集中。

一个程序集可以包含来自不同命名空间的类型。例如，，`System.Int32` 和 `System.Text.StringBuilder` 类型都在 `MSCLib.dll` 程序集中。

当你查询 `.NET Framework SDK` 文档时，文档将清楚地指示该类型所属的命名空间以及实现该类型的程序集。在图 4-1 中，你可以看到右侧（语法部分上方）`ResXFileRef` 类型是 `System.Resources` 的一部分，且该类型实现在 `System.Windows.dll` 程序集中。要编译引用 `ResXFileRef` 类型的代码，你需要在源代码中添加 `System.Resources;` 指令，并使用编译器开关 `/r:System.Windows.dll`。

![](img/0ce3b788d061e3d3095fa554b1a34adf_126_0.png)

图 4-1 显示类型命名空间和程序集信息的 SDK 文档。

# 运行时的关系

在本节中，我将解释运行时、类型、对象、线程栈和托管堆之间的关系。此外，我还将解释调用静态方法、实例方法和虚方法之间的区别。让我们先从计算机的一些基础知识开始。

我将要描述的内容完全不是针对 `CLR` 的，但我将这样描述以便我们有一个基础，然后我将修改讨论以包含 `CLR` 特有的信息。

图 4-2 显示了一个加载了 `CLR` 的单个 Windows 进程。在该过程中可能有许多线程。当创建线程时，它会被分配一个 1 MB 的栈。该空间用于向方法传递参数以及方法内部局部变量。在图 4-2 中，显示了一个线程的内存（右侧）。栈从高内存地址向低内存地址构建。在图中，该线程已经执行了某些代码，其栈上已经有一些数据（显示为栈顶部的阴影区域）。现在，想象该线程执行了调用 `M1` 方法的代码。

## 线程栈

![](img/0ce3b788d061e3d3095fa554b1a34adf_127_0.png)

图 4-2 即调用 `M1` 方法的栈

除了最简单的方法外，所有方法都包含一些序言代码，在开始工作之前初始化方法。这些方法还包含尾声代码，在执行工作后清理方法以便返回调用者。当 `M1` 方法开始执行时，其序言代码从线程栈上为局部变量分配内存（见图 4-3）。

## 线程栈

![](img/0ce3b788d061e3d3095fa554b1a34adf_127_1.png)

图 4-3 在线程栈上分配 `M1` 的局部变量

然后，`M1` 调用 `M2` 方法，并将 `name` 作为参数传入。这导致 `name` 中的地址被推入栈中（见图 4-4）。在 `M2` 方法内部，栈位置将使用参数名 `s` 来标识。（注意，某些架构通过寄存器传递参数以提高性能，但这种区别对于并不

（此处讨论。）此外，当一个方法被调用时，指示被调用方法应返回到调用方法的地址会被推入栈中（如图 4-4 所示）。

## 线程栈

```void M1() {
  String name = "Joe";
  M2(name);
  ***
  return;
}
```

```
void M2(String s) {
  Int32 length = s.Length;
  Int32 tally;
  ***
  return;
}
```

**图 4-4** `M1` 在调用 `M2` 时，将参数和返回地址推入线程的栈中。

当 `M2` 方法开始时，它的序言部分从线程栈中为局部变量 `length` 和 `tally` 分配内存（见图 4-5）。然后，方法 `M2` 内部的代码开始执行。最终，`M2` 运行到它的 `return` 语句，这会导致 CPU 的指令指针被设置为栈中的返回地址，并且 `M2` 的栈帧会被展开（unwound），使其看起来与图 4-3 所示。此时，`M1` 继续执行紧随调用 `M2` 之后的代码，且它的栈帧准确地反映了 `M1` 所需的状态。

最终，`M1` 通过将 CPU 的指令指针设置为返回地址（图中未显示，但它就在栈上 `name` 参数的上方）来返回到它的调用者，并且 `M1` 的栈帧会被展开，使其看起来与图 4-2 所示。此时，方法 `M1` 继续执行紧随调用 `M1` 之后的代码，且它的栈帧准确地反映了该方法所需的状态。

## 线程栈

```
void M1() {
  String name = "Joe";
  M2(name);
  ***
  return;
}
```

```
void M2(String s) {
  Int32 length = s.Length;
  Int32 tally;
  ***
  return;
}
```

**图 4-5** 在线程栈上为 `M2` 的局部变量分配内存。

第 4 章 类型基础 103 页

现在，让我们把讨论转向 `CLR`。假设我们有两个类定义。

```
internal class Employee {
    public Int32 GetYearsEmployed() {}
    public virtual String GetProgressReport() {}
    public static Employee Lookup(String name) { }
}
```

```
internal sealed class Manager : Employee {
    public override String GetProgressReport() {}
}
```

我们的 Windows 进程启动，`CLR` 被加载其中，堆被初始化，并且创建了一个线程（连同其 1 MB 的栈空间）。该线程已经执行了一些代码，而这些代码决定调用 `M3` 方法。所有这些内容如图 4-6 所示。`M3` 方法包含了演示 `CLR` 如何工作的代码；这些并不是你通常会编写的代码，因为它们实际上并没有做任何有用的事情。

## 线程栈

![](img/0ce3b788d061e3d3095fa554b1a34adf_129_0.png)

## 堆

![](img/0ce3b788d061e3d3095fa554b1a34adf_129_1.png)

```
void M3() {
    Employee e;
    Int32 year;
    e = new Manager();
    e = Employee.Lookup("Joe");
    year = e.GetYearsEmployed();
    e.GetProgressReport();
}
```

图 **4-6** 加载在进程中的 `CLR`，其堆已初始化，以及带有待调用 `M3` 方法的线程栈。

即时编译（`JIT`）编译器将 `M3` 的中间语言（`IL`）代码转换为原生 CPU 指令，它注意到了 `M3` 内部引用的所有类型：`Employee`、`Int32`、`Manager` 和 `String`（即 "`Joe`"）。此时，`CLR` 确保定义这些类型的程序集已加载。然后，通过使用程序集的元数据，`CLR` 提取有关这些类型的信息，并创建一些数据结构来表示类型本身。`Employee` 和 `Manager` 类型对象的数据结构如图 4-7 所示。由于该线程在调用 `M3` 之前已经执行了一些代码，让我们假设 `Int32` 和 `String` 类型对象已经创建完成（这很可能是因为这些是常用类型），因此我不在图中显示它们。

## 线程栈

## 堆

| | Manager 类型对象 |

|---|---|

| 类型对象指针 | |

| 同步块索引 | |

| 静态字段 | |

| GetProgressReport | |

| Employee 类型对象 | |

| 类型对象指针 | |

| 同步块索引 | |

| 静态字段 | |

| GetYearsEmployed | |

| GetProgressReport | |

| Lookup | |

```
void M3() {
    Employee e;
    Int32 year;
    e = new Manager();
    e = Employee.Lookup("Joe");
    year = e.GetYearsEmployed();
    e.GetProgressReport();
}
```

图 4-7 在 `M3` 调用时创建的 `Employee` 和 `Manager` 类型对象。

让我们花点时间讨论这些类型对象。正如本章早期提到的，堆上的所有对象都包含两个开销成员：类型指针和同步块索引。当你定义一个类型时，你可以在其中定义静态数据字段。这些静态字段位于类型对象内部。最后，每个类型对象都是包含方法的字节，这是我们在第 1 章“`CLR` 的执行模型”中讨论过的。`Employee` 类型定义三个方法（`GetYearsEmployed`、`GetProgressReport` 和 `Lookup`），因此方法 表中有三条目。由于 `Manager` 类型定义了一个方法（`GetProgressReport` 的重写），因此方法 表中只有一条目。

当调用静态方法时，`JIT` 编译器会定位定义该静态方法的类型对应的类型。然后，`JIT` 在类型对象的方法表中找到引用被调用方法的条目，对该方法进行 `JIT`（如有必要），并调用 `JIT` 后的代码。对于我们的讨论，假设 `Employee` 的静态 `Lookup` 方法查询数据库查找 `Joe`。让我们也假设数据库指示 `Joe` 是公司的经理，并且内部，`Lookup` 方法在堆上构造了一个新的 `Manager` 对象，并返回该对象的地址。该地址保存在局部变量 `e` 中。此操作的结果如图 4-10 所示。

第 4 章 类型基础

105 页

## 线程栈

## 堆

| | Manager 类型对象 |

|---|---|

| 类型对象指针 | |

| 同步块索引 | |

| 静态字段 | |

| ---------------- |

| GetProgressReport | |

```
void M3() {
  Employee e;
  Int32 year;
  e = new Manager();
  e = Employee.Lookup("Joe");
  year = e.GetYearsEmployed();
  e.GetProgressReport();
}
```

| | null |

| --- | --- |

| e (Employee) | |

| year (int32) | 0 |

图 4-8 在栈上为 `M3` 的局部变量分配内存。
