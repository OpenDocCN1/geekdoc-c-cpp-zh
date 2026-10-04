
构造函数，它可以有多个。此外，类型构造函数永远不会有参数。在 C# 中，以下是定义具有类型构造函数的引用类型和值类型的方法。

```sharp
internal sealed class SomeRefType {
    static SomeRefType() {
        // 这段代码在第一次访问 SomeRefType 时执行。
    }
}
```

```sharp
internal struct SomeValueType {
    // C# 不允许值类型定义无参数的类型构造函数。
    static SomeValueType() {
        // 这段代码在第一次访问 SomeValueType 时执行。
    }
}
```

你会发现，定义类型构造函数的方式与定义无参数的实例构造函数一样，区别在于你必须将它们标记为 `static`。此外，类型构造函数应该始终私有（private）；C# 会自动将它们设为私有。事实上，如果你在源代码中显式地将类型构造函数标记为私有（或其他修饰符），C# 编译器会发出以下错误：CS0515:'SomeValueType.SomeValueType()':静态构造函数上不允许使用访问修饰符。类型构造函数应该是私有的，以防止开发者编写的代码调用它们；而 CLR 始终能够调用类型构造函数。

> 重要：尽管你可以在值类型内部定义类型构造函数，但你实际上不会这样做，因为在某些情况下，CLR 不会调用值类型的静态类型构造函数。这里有一个示例。

```sharp
internal struct SomeValueType {
    static SomeValueType() {
        Console.WriteLine("此内容永远不会显示");
    }
    public Int32 m_x;
}
```

```sharp
public sealed class Program {
    public static void Main() {
        SomeValueType[] m_x = new SomeValueType[10];
        a[0].m_x = 123;
        Console.WriteLine(a[0].m_x); // 显示 123
    }
}
```

调用类型构造函数是一件复杂的事情。当即时编译（JIT）编译器编译方法时，它会查看代码中引用了哪些类型。如果任何一个类型定义了类型构造函数，JIT 编译器就会检查该类型的构造函数是否已经为该 AppDomain 执行过。如果构造函数从未执行过，JIT 编译器就会在 JIT 编译器生成的原生代码中嵌入对类型构造函数的调用。如果该类型的类型构造函数已经执行过，JIT 编译器就不会生成该调用，因为它知道该类型已经初始化。

现在，在方法被 JIT 编译后，线程开始执行它，并最终到达调用构造函数的代码。事实上，可能会有多个线程并发执行同一个方法。CLR 想要确保每个类型的构造函数在每个 AppDomain 中只执行一次。为了保证这一点，类型构造函数在执行时会获取一个互斥线程同步锁。如果多个线程尝试同时调用静态构造函数，只有一个线程将获取锁，而其他线程将阻塞。第一个线程将执行静态构造函数中的代码。当第一个线程离开构造函数后，等待的线程将唤醒并发现构造函数代码已经执行过了。这些线程不会再次执行该代码；它们将直接从构造函数返回。此外，如果这些方法再次再次被调用，CLR 都知道类型构造函数已经执行过，并将确保构造函数不再被再次调用。

> 注意：由于 CLR 保证类型构造函数在每个 AppDomain 只执行一次且是线程安全的，因此类型构造函数是初始化类型所需的任何单例对象的绝佳位置。

在单个线程内部，如果两个类型构造函数相互引用，可能会出现潜在问题。例如，ClassA 有一个类型构造函数，包含引用 ClassB 的代码，而 ClassB 有一个类型构造函数，包含引用 ClassA 的代码。在这种情况下，CLR 仍然保证每个类型构造函数只执行一次；但无法无法在执行 ClassB 的类型构造函数之前确保 ClassA 的类型构造函数已经运行。你应该尽量避免编写设置这种场景的代码。事实上，由于 CLR 负责调用类型构造函数，你应该始终避免编写任何要求类型构造函数按特定顺序调用的代码。

最后，如果类型构造函数抛出未处理的异常，CLR 将认为该类型不可用。尝试访问该类型的任何字段或方法将导致抛出 `System.TypeInitializationException`。

类型构造函数中的代码仅可以访问类型的静态字段，其通常用途是初始化这些字段。与实例构造函数一样，C# 提供了一句简单的语法，允许你初始化类型的静态字段。

```sharp
internal sealed class SomeType {
    private static Int32 s_x = 5;
}
```

> 注意：尽管 C# 不允许值类型对实例字段使用内联字段初始化语法，但它允许对静态字段使用它。换句话说，如果你将上面的 SomeType 从类（class）改为结构体（struct），代码将编译并按预期工作。

当编译此代码时，编译器会自动为 SomeType 生成一个类型构造函数。这就像源代码编写的形式如下：

```sharp
internal sealed class SomeType {
    private static Int32 s_x;
    static SomeType() { s_x = 5; }
}
```

使用 ILasm.exe，通过检查类型构造函数的 IL，很容易验证编译器实际生成了什么。类型构造函数方法在类型方法定义表中始终被调用为 `.cctor`（对于类构造函数）。

在下方，你可以看到 `.cctor` 方法是私有且静态的。此外，注意方法中的代码将 5 加载到静态变量 `s_x` 中。

```il
.method private hidebyname rtspecial static
    void .cctor() cil managed
```

```il
{
    // Code size      7 (0x7)
    .maxstack      8
    IL_0000:  ldc.i4.5
    IL_0001:  stfield      int32 SomeType::s_x
    IL_0006:  ret
} // end of method SomeType::.cctor
```

类型构造函数不会调用基类型的类型构造函数。除非该类型的某个静态字段是从其基类型共享或继承的，否则这种调用是没有必要的。

> 注意：某些语言（如 Java）期望访问一个类型会导致其类型构造函数及其所有基类型的类型构造函数被调用。此外，类型实现的接口也必须被调用其类型构造函数。CLR 不提供这种便利。然而，CLR 确实为编译器和开发者提供了通过 `System.Runtime.CompilerServicesHelpers` 类型提供的 `RunConstructor` 方法来实现这种行为的能力。
