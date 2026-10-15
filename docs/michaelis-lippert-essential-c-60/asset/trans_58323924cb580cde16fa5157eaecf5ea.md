

// Seconds = seconds;
// }

public Angle(int degrees, int minutes, int seconds)
{
    _Degrees = degrees;
    _Minutes = minutes;
    _Seconds = seconds;
}

public int Degrees { get { return _Degrees; } }
readonly private int _Degrees;

public int Minutes { get { return _Minutes; } }
readonly private int _Minutes;

public int Seconds { get { return _Seconds; } }
readonly private int _Seconds;

// ...
}

在编译器知道所有字段都已初始化之前访问它是非法的；使用 Degrees 隐式为 this.Degrees。为了解决这个问题，你需要直接初始化字段，正如在未被注释掉的第 8.3 节的构造函数中所演示的那样。

由于结构体的字段初始化要求、C# 6.0 的只读自动实现属性支持的简洁性，以及避免从其包装属性外部访问字段的指导原则，从 C# 6.0 开始，你应该在结构体中优先使用只读自动实现属性而不是字段。

## Guidelines

DO 确保结构体的默认值是有效的；始终可以获得结构体的默认“全零”值。

## ADVANCED TOPIC

## Using new with Value Types

使用 new 运算符对引用类型进行调用时，运行时会在垃圾回收堆上创建一个对象的新实例，将其所有字段初始化为默认值，并调用构造函数，将实例的引用作为 this 传递。结果是实例的引用，然后可以将其复制到最终位置。相比之下，使用 new 运算符对值类型进行调用时，运行时会在临时存储池上创建一个对象的新实例，将其所有字段初始化为默认值，并调用构造函数（将临时存储位置作为 ref 变量作为 this 传递），结果是值存储在临时存储位置中，然后可以将其复制到最终位置。

与类不同，结构体不支持终结器。结构体按值复制；它们不像引用类型那样具有“引用标识”。因此，很难知道何时可以安全地执行终结器并释放结构体拥有的非托管资源。垃圾收集器知道何时没有对引用类型实例的“活动”引用，并且可以在没有更多活动引用后随时选择为引用类型实例运行终结器。尽管如此，运行时没有任何部分跟踪在任何时刻存在多少个给定值类型的副本。

## Language Contrast: C++—struct Defines Type with Public Members

在 C++ 中，使用 struct 声明的类型与使用 class 声明的类型之间的区别在于默认访问性是 public 还是 private。在 C# 中，对比要大得多，其中区别在于类型的实例是按值复制还是按引用复制。

## Using the default Operator

如前所述，如果没有提供默认构造函数（这仅在 C# 6.0 起才可能），所有值类型都有一个自动定义的默认构造函数，将值类型的存储初始化为其默认状态。因此，使用 new 运算符创建值类型实例始终是合法的。作为替代语法，你可以使用 default 运算符来生成结构体的默认值。在第 8.4 节中，我们向 Angle 结构体添加了第二个构造函数，该构造函数使用 default 运算符对 int 作为参数传递给之前声明的三个参数构造函数。

## LISTING 8.4: Using the default Operator to Obtain the Default Value of a Type

```
// Use keyword struct to declare a value type.
struct Angle
{
    public Angle(int degrees, int minutes)
        : this( degrees, minutes, default(int) )
    {
    }

    // ...
}
```

表达式 default(int) 和 new int() 都产生相同的值。相比之下，如果构造函数是 C# 6.0 自定义默认构造函数，对于自定义定义的值类型则不一定如此。在 C# 6.0 中，默认构造函数将其数据初始化为非默认值。结果是，对默认构造函数的调用——需要 new 运算符——不会产生与 default(T) 相同的值。与引用类型一样，自定义默认构造函数仅通过 new 运算符显式调用。但是，与引用类型不同，其默认值为空，值类型的隐式初始化会产生一个清零的内存块，等同于 default 运算符的结果。因此，当值类型具有默认构造函数时，default(T) 不一定等同于 new T()。此外，访问隐式初始化的值类型是一个有效操作；相比之下，访问引用类型的默认值会产生 NullReferenceException。因此，如果 default(T) 值不是类型的有效状态，你应注意显式初始化具有自定义默认构造函数的 value 类型。

> **NOTE**
> 
> 值类型上的默认构造函数仅由 new 运算符的显式使用调用。

## Inheritance and Interfaces with Value Types

所有值类型都是隐式密封的。此外，所有非枚举值类型都派生自 System.ValueType。因此，结构体的继承链始终是从 object 到 System.ValueType 再到结构体。

值类型也可以实现接口。框架中内置的许多值类型实现了 IComparable 和 IFormattable 等接口。System.ValueType 带来了值类型的行为，但它不包含任何额外成员。System.ValueType 的自定义主要集中在重写 object 的所有虚成员上。在结构体中重写基类方法的规则几乎与类相同（参见第 9 章）。然而，一个区别是，对于值类型，GetHashCode() 的默认实现是将调用转发给结构体中第一个非空字段。此外，Equals() 大量使用反射。因此，如果值类型经常在集合内部使用，尤其是在使用哈希码的字典类型集合中，值类型应包含 Equals() 和 GetHashCode() 的重写以确保良好的性能。有关更多详细信息，请参阅第 9 章。

## Guidelines

DO 在值类型上重载相等运算符（Equals()、== 和 !=），如果相等是有意义的。（还应考虑实现 IEquatable<T> 接口。）

## Boxing

我们知道值类型变量直接包含其数据，而引用类型变量包含对另一个存储位置的引用。但当值类型转换为其实现的其中一个接口或其根基类 object 时会发生什么？转换的结果必须是对包含看起来像引用类型实例的东西的存储位置的引用，但变量包含值类型的值。这种转换称为装箱，具有特殊行为。将直接引用其数据的 value 类型变量转换为引用垃圾回收堆上位置的引用类型涉及几个步骤。

- 1. 在堆上分配内存，该内存将包含值类型的数据以及使对象看起来像每个托管引用类型实例一样所需的其他开销（即 SyncBlockIndex 和方法表指针）。
- 2. 值类型的值从其当前存储位置复制到堆上新分配的位置。
- 3. 转换的结果是对堆上新存储位置的引用。

反向操作是拆箱。拆箱转换检查装箱值的类型是否与值正在拆箱到的类型兼容，然后导致堆位置中存储的值的副本。

装箱和拆箱很重要，因为装箱具有一些性能和行为影响。除了学习如何在 C# 代码中识别这些转换外，开发人员还可以通过查看 CIL 来统计特定代码片段中的 box/unbox 指令。每个操作都有特定的指令，如表 8.1 所示。

## TABLE 8.1: Boxing Code in CIL

| C# Code | CIL Code |
|---|---|
| static void Main() { | .method private hidebysig static void Main() cil managed { |
|  | .entrypoint |
|  | // Code size 21 (0x15) |
|  | .maxstack 1 |
| int number; | .locals init ([0] int32 number, |
| object thing; | [1] object thing) |
|  | IL_0000: nop |
| number = 42; | IL_0001: ldc.i4.s 42 |
|  | IL_0003: stloc.0 |
| // Boxing | IL_0004: ldloc.0 |
| thing = number; | IL_0005: box [mscorlib]System.Int32 |
|  | IL_000a: stloc.1 |
| // Unboxing | IL_000b: ldloc.1 |
| number = (int)thing; | IL_000c: unbox.any [mscorlib]System.Int32 |
|  | IL_0011: stloc.0 |
|  | IL_0012: br.s IL_0014 |
| return; | IL_0014: ret |
| } | } // end of method Program::Main |

当装箱和拆箱很少发生时，它们对性能的影响无关紧要。然而，装箱可能在一些意想不到的情况下发生，频繁发生会对性能产生重大影响。请考虑第 8.5 节和输出 8.1。ArrayList 类型维护

