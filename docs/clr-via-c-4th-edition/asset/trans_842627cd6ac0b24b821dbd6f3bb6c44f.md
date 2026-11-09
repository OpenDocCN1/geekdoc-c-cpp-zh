
如果你的应用程序能够容忍始终执行已检查操作带来的轻微性能损失，那么我建议你即使在发布版本中也使用 /checked 命令行选项进行编译，因为这可以防止你的应用程序在数据损坏和可能出现安全漏洞的情况下继续运行。例如，你可能执行乘法来计算数组索引；与因数学运算回绕而访问错误的数组元素相比，获得 OverflowException 要好得多。

> **重要** System.Decimal 类型是一种非常特殊的类型。尽管许多编程语言（包括 C# 和 Visual Basic）都将 Decimal 视为基元类型，但 CLR 并不这样认为。这意味着 CLR 没有知道如何操作 Decimal 值的 IL 指令。如果在 .NET Framework SDK 文档中查找 Decimal 类型，你会看到它具有名为 Add、Subtract、Multiply、Divide 等的公共静态方法。此外，Decimal 类型还为 +、-、*、/ 等提供运算符重载方法。
>
> 当你编译使用 Decimal 值的代码时，编译器会生成代码来调用 Decimal 的成员以执行实际操作。这意味着操作 Decimal 值比操作 CLR 基元值更慢。另外，由于没有用于操作 Decimal 值的 IL 指令，checked 和 unchecked 运算符、语句以及编译器开关都不会起作用。如果无法安全执行操作，对 Decimal 值的操作将始终抛出 OverflowException。
>
> 类似地，System.Numerics.BigInteger 类型也很特殊，它在内部使用 UInt32 数组来表示任意大的整数，其值没有上限或下限。因此，对 BigInteger 的操作永远不会导致 OverflowException。但是，如果值变得过大且没有足够的可用内存来调整数组大小，BigInteger 操作可能会抛出 OutOfMemoryException。

## 引用类型和值类型

CLR 支持两种类型：引用类型和值类型。尽管 FCL 中的大多数类型都是引用类型，但程序员最常使用的类型是值类型。引用类型总是从托管堆中分配，并且 C# *new* 运算符返回对象的内存地址——该内存地址指向对象的各个位。使用引用类型时，你需要牢记一些性能方面的考虑。首先，考虑以下事实：

- 内存必须从托管堆中分配。
- 在堆上分配的每个对象都关联有一些额外的开销内存，这些内存必须初始化。
- 对象中的其他字节（用于字段）总是设置为零。
- 从托管堆分配对象可能会强制发生垃圾回收。

以下代码和图 5-2 演示了引用类型和值类型有何不同。

```csharp
// Reference type (because of 'class')
class SomeRef { public Int32 x; }

// Value type (because of 'struct')
struct SomeVal { public Int32 x; }

static void ValueTypeDemo() {
    SomeRef r1 = new SomeRef();   // Allocated in heap
    SomeVal v1 = new SomeVal();   // Allocated on stack
    r1.x = 5;                     // Pointer dereference
    v1.x = 5;                     // Changed on stack
    Console.WriteLine(r1.x);      // Displays "5"
    Console.WriteLine(v1.x);      // Also displays "5"
    // The left side of Figure 5-2 reflects the situation
    // after the lines above have executed.

    SomeRef r2 = r1;              // Copies reference (pointer) only
    SomeVal v2 = v1;              // Allocate on stack & copies members
    r1.x = 8;                     // Changes r1.x and r2.x
    v1.x = 9;                     // Changes v1.x, not v2.x
    Console.WriteLine(r1.x);      // Displays "8"
    Console.WriteLine(r2.x);      // Displays "8"
    Console.WriteLine(v1.x);      // Displays "9"
    Console.WriteLine(v2.x);      // Displays "5"
    // The right side of Figure 5-2 reflects the situation
    // after ALL of the lines above have executed.
}
```

在这段代码中，SomeVal 类型使用 struct 而不是更常见的 class 声明。在 C# 中，使用 struct 声明的类型是值类型，使用 class 声明的类型是引用类型。如你所见，引用类型和值类型的行为差异很大。在代码中使用类型时，你必须注意该类型是引用类型还是值类型，因为它会极大地影响你在代码中表达意图的方式。

![](img/857bdf6cef9e242b53a37f88df9a1287_145_0.png)

**图 5-2** 在代码执行时可视化内存。

在前面的代码中，你看到了这一行。

```
    SomeVal v1 = new SomeVal();   // Allocated on stack
```

这一行的写法看起来好像会在托管堆上分配一个 SomeVal 实例。然而，C# 编译器知道 SomeVal 是值类型，并生成在线程栈上分配 SomeVal 实例的代码。C# 还确保值类型实例中的所有字段都置零。

前面那一行也可以改为这样写。

```
    SomeVal v1;   // Allocated on stack
```

这一行也会生成 IL，将实例分配到线程栈上并将字段置零。唯一的区别是，如果你使用 new 运算符，C#“认为”该实例已初始化。以下代码将清楚说明这一点。

```
    // These two lines compile because C# thinks that
    // v1's fields have been initialized to 0.
    SomeVal v1 = new SomeVal();
    Int32 a = v1.x;

    // These two lines don't compile because C# doesn't think that
    // v1's fields have been initialized to 0.
    SomeVal v1;
    Int32 a = v1.x;  // error CS0170: Use of possibly unassigned field 'x'
```

设计自己的类型时，请仔细考虑是否应将类型定义为值类型而不是引用类型。在某些情况下，值类型可以提供更好的性能。特别是，如果以下所有陈述都为真，则应将类型声明为值类型：

- 该类型充当基元类型。具体来说，这意味着它是一个相当简单的类型，没有任何成员会修改其任何实例字段。当一个类型不提供任何可更改其字段的成员时，我们说该类型是不可变的。事实上，建议许多值类型将其所有字段标记为 readonly（在第 7 章“常量和字段”中讨论）。
- 该类型不需要从任何其他类型继承。
- 该类型不会有任何其他类型从它派生。

类型实例的大小也是需要考虑的条件，因为默认情况下参数按值传递，这会导致值类型实例中的字段被复制，从而损害性能。同样，返回值类型的方法会在方法返回时将实例中的字段复制到调用方分配的内存中，从而损害性能。因此，除了前面的条件之外，如果以下陈述之一为真，则应将类型声明为值类型：

- 该类型的实例较小（大约 16 字节或更小）。
- 该类型的实例较大（大于 16 字节），并且不作为方法参数传递，也不从方法返回。

值类型的主要优点是它们不会作为对象在托管堆中分配。当然，与引用类型相比，值类型自身也有若干限制。以下是值类型和引用类型不同的一些方面：

- 值类型对象有两种表示形式：未装箱形式和装箱形式（在下一节中讨论）。引用类型始终处于装箱形式。

- 值类型派生自 System.ValueType。此类型提供与 System.Object 定义的方法相同的方法。但是，如果两个对象字段的值匹配，System.ValueType 会重写 Equals 方法使其返回 true。此外，System.ValueType 会重写 GetHashCode 方法，使用一种考虑对象实例字段中值的算法来生成哈希代码值。由于此默认实现存在性能问题，在定义自己的值类型时，应重写并为 Equals 和 GetHashCode 方法提供显式实现。我将在本章末尾介绍 Equals 和 GetHashCode 方法。

- 由于不能使用值类型作为基类来定义新的值类型或新的引用类型，因此不应将任何新的虚方法引入值类型。任何方法都不能是抽象的，并且所有方法都隐式密封（不能重写）。

- 引用类型变量包含堆中对象的内存地址。默认情况下，创建引用类型变量时，它被初始化为 null，表示该引用类型变量当前不指向有效对象。尝试使用 null 引用类型变量会导致抛出 NullReferenceException。相比之下，值类型变量始终包含基础类型的值，并且值类型的所有成员都初始化为 0。由于值类型变量不是指针，因此访问值类型时不可能生成 NullReferenceException。CLR 确实提供了一种特殊功能，可为值类型添加可空性概念。此功能称为可空类型，将在第 19 章“可空值类型”中讨论。

- 将一个值类型变量赋给另一个值类型变量时，会进行逐字段复制。将一个引用类型变量赋给另一个引用类型变量时，仅复制内存地址。

- 由于上一点，两个或更多引用类型变量可以引用堆中的单个对象，从而允许对一个变量的操作影响另一个变量所引用的对象。另一方面，值类型变量是不同的对象，对一个值类型变量的操作不可能影响另一个值类型变量。

- 由于未装箱的值类型不在堆上分配，因此为它们分配的存储空间会在定义该类型实例的方法不再活动时立即释放，而不是等待垃圾回收。
