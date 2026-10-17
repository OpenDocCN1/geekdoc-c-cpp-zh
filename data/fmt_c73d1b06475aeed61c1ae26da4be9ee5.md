
```csharp
internal sealed class SomeType {
    // 不要在这里显式初始化字段
    private Int32 m_x;
    private String m_s;
    private Double m_d;
    private Byte m_b;

    // 此构造函数将所有字段设置为它们的默认值。
    // 所有其他构造函数都显式调用此构造函数。
    public SomeType() {
        m_x = 0;
        m_s = "HI there";
        m_d = 3.14159;
        m_b = 0xff;
    }

    // 此构造函数将所有字段设置为默认值，然后更改 m_x。
    public SomeType(Int32 x) : this() {
        m_x = x;
    }

    // 此构造函数将所有字段设置为默认值，然后更改 m_s。
    public SomeType(String s) : this() {
        m_s = s;
    }

    // 此构造函数将所有字段设置为默认值，然后更改 m_x & m_s。
    public SomeType(Int32 x, String s) : this() {
        m_x = x;
        m_s = s;
    }
}
```

## 实例构造函数与结构（值类型）

值类型（结构）构造函数的工作方式与引用类型（类）构造函数不同。公共语言运行时（CLR）始终允许创建值类型实例，并且没有方法可以阻止值类型被实例化。由于某些原因，值类型实际上不需要在内部定义构造函数，而且 C# 编译器不会为值类型产生默认的无参数构造函数。查看以下代码：

```csharp
internal struct Point {
    public Int32 m_x, m_y;
}
internal sealed class Rectangle {
    public Point m_topLeft, m_bottomRight;
}
```

要构造一个 `Rectangle`，必须使用 `new` 运算符，并调用 C# 编译器自动生成的默认构造函数。当为 `Rectangle` 分配内存时，该内存包含了两个 `Point` 值类型的实例。出于性能考虑，CLR 不尝试为引用类型中包含的每个值类型字段调用构造函数。但正如我之前提到的，值类型的字段被初始化为 0/null。

CLR 允许你在值类型上定义构造函数。构造函数执行的唯一方法是你编写代码显式地调用其中一个，如下所示的 `Rectangle` 构造函数：

```csharp
internal struct Point {
    public Int32 m_x, m_y;
}
public Point(Int32 x, Int32 y) {
    m_x = x;
    m_y = y;
}
internal sealed class Rectangle {
    public Point m_topLeft, m_bottomRight;
}
public Rectangle() {
    // 在 C# 中，在值类型上调用构造函数是为了
    // 初始化值的字段。
    m_topLeft = new Point(1, 2);
    m_bottomRight = new Point(100, 200);
}
```

值类型的实例构造函数仅在被显式调用时执行。因此，如果 `Rectangle` 的构造函数没有使用 `new` 运算符调用 `Point` 的构造函数来初始化其 `m_topLeft` 和 `m_bottomRight` 字段，那么 `Point` 字段中的 `m_x` 和 `m_y` 字段都将是 0。

## 第二部分 类型设计

在前面定义的 `Point` 值类型中，没有定义默认的无参数构造函数。然而，让我们将该代码重写如下：

```csharp
internal struct Point {
    public Int32 m_x, m_y;

    public Point() {
        m_x = m_y = 5;
    }
}

internal sealed class Rectangle {
    public Point m_topLeft, m_bottomRight;

    public Rectangle() {
    }
}
```

现在当构造一个 `Rectangle` 时，你认为两个 `Point` 字段 `m_topLeft` 和 `m_bottomRight` 中的 `m_x` 和 `m_y` 字段会被初始化为：0 还是 5？（提示：这是一个陷阱。）

许多开发者（特别是具有 C++ 背景的人）会期望 C# 编译器在 `Rectangle` 构造函数中生成代码，为 `Rectangle` 的两个字段调用 `Point` 的默认无参数构造函数。然而，为了提高应用程序的性能，C# 编译器不会自动生成此代码。事实上，许多编译器永远不会自动生成调用值类型默认构造函数的代码，即使值类型提供了无参数构造函数。要让值类型的无参数构造函数执行，开发者必须添加显式代码。

根据上一段的信息，你是否期望 `Rectangle` 构造函数中的 `m_x` 和 `m_y` 字段会被初始化为 0？由于 C# 不允许值类型具有无参数构造函数，编译器就不会自动调用它，以消除开发者可能产生的困惑。

> 注意：严格来说，当值类型是引用类型的内部字段时，值类型字段保证为 0/null。然而，栈上的值类型并不保证为 0/null。为了可验证性，任何栈值类型必须在读取之前被写入。如果其他编译器在写入值类型字段之前读取它，可能会发生安全漏洞。C 和其他执行可验证代码的编译器确保所有值类型都清零。在大多数情况下，这意味着你可以假设值类型字段已初始化为 0，你可以完全忽略此注释。请记住，尽管 C# 不允许值类型具有无参数构造函数，但 CLR 是允许的。如果前面的意外行为没有困扰你，可以使用任何编程语言（如 IL 汇）来定义带有无参数构造函数的值类型。

由于 C# 不允许值类型带有构造函数，编译以下内容会产生以下消息：“错误 CS0573：'SomeValType.m_x'：结构体中不能有字段初始化器”。

```csharp
internal struct SomeValType {
    // 不能在值类型中内联字段初始化
    private Int32 m_x = 5;
}
```

此外，可验证代码要求值类型的每个字段在读取任何字段之前都必须写入，你拥有的任何构造函数必须初始化类型的所有字段。以下类型定义了值类型的构造函数但未能初始化所有字段：

```csharp
internal struct SomeValType {
    private Int32 m_x, m_y;

    // C# 允许值类型具有带参数的构造函数。
    public SomeValType(Int32 x) {
        m_x = x;
        // 注意这里没有初始化 m_y。
    }
}
```

编译此类型时，C# 编译器会产生以下消息：“错误 CS0171：字段 'SomeValType.m_y' 在构造返回之前未完全赋值。”要解决此问题，请在构造函数为 y 分配值（通常为 0）。

作为初始化值类型所有字段的另一种替代方法，你实际上可以这样做：

```csharp
// C# 允许值类型具有带参数的构造函数。
public SomeValueType(Int32 x) {
    // 看起来很奇怪，但可以正常编译并将所有字段初始化为 0/null
    this = new SomeValueType();
    m_x = x; //用 x 覆盖 m_x
    // 注意到 m_y 已被初始化为 0
}
```

在值类型的构造函数中，`this` 代表该值类型本身的实例，你实际上可以将其赋值给 `new` 一个值类型实例的结果，这会将所有字段置零。在引用类型的构造函数中，此项被认为是只读的，因此你完全无法对其进行赋值。

# 类型构造函数

除了构造函数外，CLR 还支持类型构造函数（也称为静态构造函数、类构造函数或类型初始化器）。类型构造函数可以应用于接口（尽管 C# 不允许这样做）、引用类型和值类型。实例构造函数用于设置类型实例的初始状态，而类型构造函数则用于设置类型的初始状态。默认情况下，类型内部没有定义类型构造函数。如果一个类型定义了类型构造函数，它最多有一个。此外，类型构造函数永远不会有参数。在 C# 中，以下是定义带有构造函数的引用类型和值类型的方法：

```csharp
internal sealed class SomeRefType {
    static SomeRefType() {
        // 这在第一次使用 SomeRefType 时执行
    }
}
internal struct SomeValueType {
    // C# 确实允许值类型定义无参数的类型构造函数。
    static SomeValueType() {
        // 这在第一次使用 SomeValueType 时执行
    }
}
```

你会发现，定义类型构造函数的方式与定义无参数实例构造函数一样，只不过你必须将其标记为 `static`。此外，类型构造函数应该始终是 `private`；C# 会自动将它们设为私有。事实上，如果你显式地将构造函数标记为 `private`（或源代码中的任何其他内容），C# 编译器会发出以下错误：“error CS0515: 'SomeValueType.SomeValueType()': 静态构造函数不允许使用访问修饰符。” 类型构造函数应该是私有的，以防止任何开发者编写的代码调用它们；而 CLR 总是能够调用类型构造函数的。

> 虽然你可以在值类型内部定义类型构造函数，但你永远不应该这样做，因为某些时刻 CLR 不会调用值类型的静态类型构造函数。这是一个示例：

```csharp
internal struct SomeValType {
    static SomeValType() {
        Console.WriteLine("这永远不会显示");
    }
    public Int32 m_x;
}

public sealed class Program {
    static void Main() {
        SomeValType[] a = new SomeValType[10];
        a[0].m_x = 123; // 显示 123
        Console.WriteLine(a[0].m_x);
    }
}
```

调用类型构造函数是一件微妙的事情。当即时（JIT)编译器在编译一个方法时，它会查看代码中引用的类型。如果任何类型定义了类型构造函数，JIT 编译器会检查该类型的类型构造函数对于当前 AppDomain 是否已经执行过。如果构造函数从未执行过，JIT 将将对类型构造函数的调用存入由 JIT 生成的原生代码中。如果该类型的类型构造函数已经执行，JIT 则不会生成调用，因为它知道该类型已经初始化。（有关此的示例，请参阅本章后后的“类型构造函数性能”部分）

现在，在方法被 JIT 编译后，线程开始执行它并最终到达调用类型构造函数的代码。事实上，可能会有多个线程并发执行同一个方法。CLR 想要确保类型的构造函数被调用，调用线程会获取排斥线程同步锁。如果多个线程尝试同时调用类型的静态构造函数，只有一个线程将获取锁，而其他线程将阻塞。第一个线程将执行静态构造函数中的代码。当第一个线程离开构造函数后，等待的线程将唤醒并发现构造函数代码已经执行。这些线程将不再再次执行代码；

# 第 8 章 方法 195

## 第二部分 类型设计

# 类型构造函数的性能

在上一节中，我提到过调用类型构造函数是一件棘手的事情。我解释了其中的一些棘手之处：JIT 编译器必须决定是否生成调用它的代码，而 CLR 则要确保对它的调用是线程安全的。事实证明，这只是棘手问题的冰一角。关于这一点还有更多与性能相关的内容。

正如已经讨论过的，在编译时，JIT 编译器会确定它是否必须在方法中生成一个执行类型构造函数的调用。如果 JIT 编译器决定生成该调用，它就必须决定在何处生成该调用。这里有两种可能性：

- JIT 编译器可以在创建该类型第一个实例的代码之前，或者在访问该类非继承字段或成员的代码之前，立即生成该调用。这被称为**精确语义（precise semantics）**，因为 CLR 将在恰好正确的时间调用类型构造函数。
- JIT 编译器可以在代码首次访问静态字段、静态方法或实例方法，或者调用实例构造函数之前生成该调用。这被称为**字段初始化前语义（before-field-init semantics）**，因为 CLR 仅保证静态构造函数会在成员被访问之前运行；它可能在晚得多的运行。

字段初始化前语义是被优的，因为它为 CLR 何何时调用类型构造函数提供了极大的自由，而 CLR 会尽可能利用这种自由来生成执行速度更快的代码。例如，CLR 可能会根据类型是加载在 AppDomain 中还是加载在领域中性域中，或者代码是经过 JIT 编译还是通过 NGen 的，选择不同的时间来调用类型构造函数。

默认情况下，语言编译器会选择哪种语义对于你定义的类型最合理，并通过在类型定义元数据表的行中设置 `beforefieldinit` 标志来通知 CLR 这一选择。在本节中，我将重点关注 C# 编译器做了什么以及它是如何影响性能的。让我们查看以下代码：

```csharp
using System;
using System.Diagnostics;

// 由于此类没有显式定义类型构造函数，
// C# 在元数据中将类型定义标记为 BeforeFieldInit。
internal sealed class BeforeFieldInit {
    public static int32 s_x = 123;
}

// 由于此类显式定义了类型构造函数，
// C# 不会在元数据中将类型定义标记为 BeforeFieldInit。
internal sealed class Precise {
    public static int32 s_x;
    static Precise() { s_x = 123; }
}

////////////////////////////////////////////////////////////////////
public sealed class Program {
  public static void Main() {
    const Int32 iterations = 1000 * 1000 * 1000;
    PerfTest1(iterations);
    PerfTest2(iterations);
  }

  // 当此方法被 JIT 编译时，
  // BeforeFieldInit 和 Precise 类的类型构造函数尚未执行
  // 因此，对这些构造函数的调用被嵌入到  // 此方法的代码中，导致其运行较慢
  private static void PerfTest1(Int32 iterations) {
    Stopwatch sw = Stopwatch.StartNew();
    for (Int32 x = 0; x < iterations; x++) {
      // JIT 编译器提升了调用 BeforeFieldInit 的代码
      BeforeFieldInit.s_x = 1;
    }
    Console.WriteLine("PerfTest1: {0} BeforeFieldInit", sw.Elapsed);

    sw = Stopwatch.StartNew();
    for (Int32 x = 0; x < iterations; x++) {
      // JIT 编译器在这里生成调用 Precise
      // 类型构造函数的代码，以便它检查是否
      // 需要在每次循环迭代中调用构造函数
      Precise.s_x = 1;
    }
    Console.WriteLine("PerfTest1: {0} Precise", sw.Elapsed);
  }

  // 当此方法被 JIT 编译时，
  // BeforeFieldInit 和 Precise 类的类型构造函数已经执行
  // 因此，对这些构造函数的调用没有嵌入到
  // 此方法的代码中，导致其运行更快
  private static void PerfTest2(Int32 iterations) {
    Stopwatch sw = Stopwatch.StartNew();
    for (Int32 x = 0; x < iterations; x++) {
      BeforeFieldInit.s_x = 2;
    }
    Console.WriteLine("PerfTest2: {0} BeforeFieldInit", sw.Elapsed);

    sw = Stopwatch.StartNew();
    for (Int32 x = 0; x < iterations; x++) {
      Precise.s_x = 1;
    }
    Console.WriteLine("PerfTest2: {0} Precise", sw.Elapsed);
  }
}
////////////////////////////////////////////////////////////////////// 文件结束 ///////////////////////////////////////////////////
```

# 第二部分：设计类型

当我构建并运行代码时，我得到了以下输出：
