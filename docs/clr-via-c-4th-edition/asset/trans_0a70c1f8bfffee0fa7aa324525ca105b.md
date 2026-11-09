

```csharp
// Define WintellectWidget symbol as an alias to Wintellect.Widget
using WintellectWidget = Wintellect.Widget;

public sealed class Program {
    public static void Main() {
        WintellectWidget w = new WintellectWidget(); // No error now
    }
}
```

这些消除类型歧义的方法很有用，但在某些场景下，你需要更进一步。假设澳大利亚回旋镖公司（Australian Boomerang Company，ABC）和阿拉斯加船只公司（Alaskan Boat Corporation，ABC）各自创建了一个名为 BuyProduct 的类型，并打算将其分别放在各自程序集中。很可能两家公司都会创建一个名为 ABC 的命名空间，其中包含一个名为 BuyProduct 的类型。任何想要开发一个既需要购买回旋镖又需要购买船只的应用程序的人都会遇到麻烦，除非编程语言提供一种以编程方式区分程序集（而不仅仅是命名空间）的方法。幸运的是，C# 编译器提供了一个名为 extern alias（外部别名）的功能，帮助你绕开这个很少发生的问题。外部别名还允许你从同一程序集的两个（或更多）不同版本中访问同一个类型。有关外部别名的更多信息，请参阅 C# 语言规范。

在库中，当你设计希望第三方使用的类型时，应该将这些类型定义在命名空间中，以便编译器能够轻松地消除它们的歧义。实际上，为了减少冲突的可能性，你应该使用公司全名（而不是首字母缩写或简称）作为顶层命名空间名称。查阅 Microsoft .NET Framework SDK 文档，你会发现 Microsoft 为 Microsoft 特有的类型使用了“Microsoft”命名空间。（例如 Microsoft.CSharp、Microsoft.VisualBasic 和 Microsoft.Win32 命名空间。）

创建命名空间只需在代码中编写 namespace 声明，如下所示（C#）。

```csharp
namespace CompanyName {
    public sealed class A {        // TypeDef: CompanyName.A
    }

    namespace X {
        public sealed class B { ... }    // TypeDef: CompanyName.X.B
    }
}
```

上述类定义右侧的注释表示编译器将写入类型定义元数据表中的类型真实名称；这是从 CLR 视角看到的类型真实名称。

有些编译器根本不支持命名空间，而其他编译器则可以自由定义“命名空间”在特定语言中的含义。在 C# 中，namespace 指令只是告诉编译器将源代码中出现的每个类型名称前缀上命名空间名称，从而让程序员少打些字。

现在，让我们将讨论转向 CLR。假设我们有以下两个类定义。

```csharp
internal class Employee {
    public      Int32   GetYearsEmployed()  { ... }
    public virtual String GetProgressReport() { ... }
    public static Employee Lookup(String name) { ... }
}

internal sealed class Manager : Employee {
    public override String GetProgressReport() { ... }
}
```

我们的 Windows 进程已启动，CLR 被加载到其中，托管堆已初始化，并且一个线程已创建（连同其 1 MB 的栈空间）。该线程已经执行了一些代码，这些代码决定调用 M3 方法。所有这些都如图 4-6 所示。M3 方法包含的代码演示了 CLR 的工作方式；这不是你通常会编写的代码，因为它实际上不会做任何有用的事情。

![](img/857bdf6cef9e242b53a37f88df9a1287_129_0.png)

**图 4-6** CLR 加载到进程中、其堆已初始化，以及线程栈上即将调用 M3 方法。

当即时（JIT）编译器将 M3 的中间语言（IL）代码转换为本机 CPU 指令时，它会注意到 M3 中引用的所有类型：Employee、Int32、Manager 和 String（因为“Joe”）。此时，CLR 会确保定义这些类型的程序集被加载。然后，CLR 使用程序集的元数据提取这些类型的信息，并创建一些数据结构来表示这些类型本身。Employee 和 Manager 类型对象的数据结构如图 4-7 所示。由于该线程在调用 M3 之前已经执行了一些代码，我们假设 Int32 和 String 类型对象已经创建（这很可能，因为它们是常用类型），因此图中不再显示它们。

![](img/857bdf6cef9e242b53a37f88df9a1287_130_0.png)

**图 4-7** 就在调用 M3 时创建 Employee 和 Manager 类型对象。

让我们花点时间讨论这些类型对象。正如本章前面所讨论的，堆上的所有对象都包含两个开销成员：类型对象指针和同步块索引。如你所见，Employee 和 Manager 类型对象都包含这两个成员。当你定义一个类型时，可以在其中定义静态数据字段。支持这些静态数据字段的字节就分配在类型对象本身中。最后，每个类型对象内部都有一个方法表，类型中定义的每个方法都占有一个条目。这就是第 1 章“CLR 的执行模型”中讨论过的方法表。由于 Employee 类型定义了三个方法（GetYearsEmployed、GetProgressReport 和 Lookup），Employee 的方法表中有三个条目。由于 Manager 类型只定义了一个方法（对 GetProgressReport 的重写），Manager 的方法表中只有一个条目。

现在，在 CLR 确保该方法所需的所有类型对象都已创建、且 M3 的代码已编译之后，CLR 允许线程执行 M3 的本机代码。当 M3 的序言代码执行时，必须从线程的栈中为局部变量分配内存，如图 4-8 所示。顺便说一句，CLR 会自动将所有局部变量初始化为 null 或 0（零），这是方法序言代码的一部分。然而，如果你在源代码中编写代码试图读取一个尚未显式初始化的局部变量，C# 编译器会发出“使用了未赋值的局部变量”错误消息。

![](img/857bdf6cef9e242b53a37f88df9a1287_131_0.png)

**图 4-8** 在线程栈上分配 M3 的局部变量。

然后，M3 执行其代码来构造一个 Manager 对象。这会导致在托管堆中创建 Manager 类型的一个实例，即 Manager 对象，如图 4-9 所示。如你所见，Manager 对象（与所有对象一样）具有类型对象指针和同步块索引。该对象还包含保存 Manager 类型定义的所有实例数据字段所需的字节，以及 Manager 类型的任何基类（此处为 Employee 和 Object）定义的任何实例字段。每当在堆上创建新对象时，CLR 都会自动初始化内部的类型对象指针成员，使其引用对象对应的类型对象（此处为 Manager 类型对象）。此外，CLR 会初始化同步块索引，并在调用类型的构造函数（一个可能会修改某些实例数据字段的方法）之前将所有对象的实例字段设置为 null 或 0（零）。new 运算符返回 Manager 对象的内存地址，该地址保存在变量 e 中（位于线程栈上）。

M3 中的下一行代码调用 Employee 的静态 Lookup 方法。调用静态方法时，JIT 编译器会定位与定义该静态方法的类型对应的类型对象。然后，JIT 编译器在类型对象的方法表中定位引用被调用方法的条目，对方法进行 JIT 编译（如有必要），并调用编译后的代码。就我们的讨论而言，假设 Employee 的 Lookup 方法查询数据库以查找 Joe。再假设数据库表明 Joe 是公司的经理，因此，在内部，Lookup 方法在堆上构造一个新的 Manager 对象，为 Joe 初始化该对象，并返回此对象的地址。该地址保存在局部变量 e 中。此操作的结果如图 4-10 所示。

