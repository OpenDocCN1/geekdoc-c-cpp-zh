
现在在未装箱的值类型实例上调用 `ToString`，并返回一个 `String`。`String` 对象已经是引用类型，可以直接传递给 `Concat` 方法，而不需要装箱。

让我们来看另一个演示装箱和解箱的示例。

```csharp
public static void Main() {
    Int32 v = 5;           // 创建一个未装箱的值类型。
    Object o = v;               // 指向 v 的装箱版本。

    v = 123;
    Console.WriteLine(v);    // 将未装箱的值类型更改为123
                                 // 显示 "123"

    v = (Int32)o;
    Console.WriteLine(o);    // 解箱并复制到 v
                                 // 显示 "5"
}
```

在这段代码中你调用了多少次装箱操作？答案是一个。之所以只有一个装箱操作，是因为 `System.Console` 定义了一个接受 `Int32` 作为参数的 `WriteLine` 方法。

```csharp
public static void WriteLine(Int32 value);
```

在之前的对 `WriteLine` 的调用中，变量 `v`（一个未装箱的 `Int32` 值类型）按值传递的。现在 `WriteLine` 会在内部装箱这个 `Int32`，但你无法控制这一点。重要的一点是你已经尽了所能，并消除了你自己代码中的装箱。

如果你仔细观察 FCL（框架类库），你会发现许多根据其值参数而异的重载方法。例如，`System.Console` 类型提供了 `WriteLine` 方法的多个重载版本。

```csharp
public static void WriteLine(Boolean);
public static void WriteLine(Char);
public static void WriteLine(Char[]);
public static void WriteLine(Int32);
public static void WriteLine(UInt32);
public static void WriteLine(Int64);
public static void WriteLine(UInt64);
public static void WriteLine(Single);
public static void WriteLine(Double);
public static void WriteLine(Decimal);
public static void WriteLine(Object);
public static void WriteLine(String);
```

你会发现 `System.Console` 的 `Write` 方法、`System.IO.BinaryWriter` 的 `Write` 方法、`System.IO.Text` 的 `Write` 和 `WriteLine` 方法、`System.Runtime.Serialization.SerializationInfo` 的 `AddValue` 方法、`System.Text.StringBuilder` 的 `Append` 和 `Insert` 方法都有类似的重载方法集。其中大多数方法提供重载版本的唯一目的是为了减少常用值类型的装箱操作次数。

如果你定义了自己的值类型，这些 FCL 类将不会拥有接受你的值类型的这些方法的重载。此外，FCL 中已经定义了许多值类型，它们并没有这些方法的重载。如果你调用的方法没有针对你传递的特定值类型提供重载，你将始终调用接受 `Object` 的重载方法。将值实例作为 `Object` 传递会导致装箱，从而对性能产生不利影响。如果你正在定义自己的类，你可以在类中将方法定义为泛型（可能将类型参数约束为值类型）。泛型为你提供了一种定义可以接受任何类型值类型而无需装箱的方法的方法。泛型将在第 12 章中讨论。

关于装箱的最后一点：如果你知道你编写的代码将导致编译器反复对同一个单一值类型进行装箱，那么手动装箱该值类型会让你的代码更小且运行更快。这是一个例子。

```csharp
using System;

public sealed class Program {
    public static void Main() {
        Int32 v = S; // 创建一个未装箱的值类型。
```

```csharp
// 如果效率低下
// 当编译下面这一行时，v 被装箱
// 三次，浪费了时间和内存。
Console.WriteLine("{0}, {1}, {2}", v, v, v);
#else
    // 这些行的结果相同，但执行速度
    // 快得多，且内存更少。
    Object o = v; // 手动装箱 v（仅一次）。

    // 编译下面这一行不会发生装箱。
    Console.WriteLine("{0}, {1}, {2}", o, o, o);
#endif
```

如果使用 `INEFFICIENT` 符号编译此代码，编译器将生成装箱 v 三次的代码，从而从堆上分配三个对象！这是极其浪费的，因为每个对象的内容完全相同：如果在没有定义 `INEFFICIENT` 符号的情况下编译，v 只被装箱一次，只从堆上分配了一个对象。然后，在调用 `Console.WriteLine` 时，该单个装箱对象的引用被传递了三次。第二个版本执行速度快得多，并且从堆分配的内存内存。

在这些示例中，很容易识别值类型实例何时需要装箱。基本上，如果你需要一个值类型实例的引用，该实例必须被装箱。通常是因为你有一个值类型实例，并想将其传递给一个需要引用类型的方法。然而，这种情况并不是你需要对值类型实例进行装箱的唯一情况。

回顾一下，未装箱的值类型比引用类型轻量，原因有两个：

- 它们不在托管堆上分配。
- 它们没有每个堆对象都拥有的额外开销成员：类型对象指针和同步块索引。

由于未装箱的值类型没有同步块索引，你无法让多个线程同步它们的访问。
