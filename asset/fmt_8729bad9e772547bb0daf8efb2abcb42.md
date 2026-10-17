
```csharp
Degrees = degrees;

Minutes = minutes;

Seconds = seconds;

}

// Using C# 6.0 read-only, automatically implemented properties

public int Degrees { get; }

public int Minutes { get; }

public int Seconds { get; }

public Angle Move(int degrees, int minutes, int seconds)

{

return new Angle(

Degrees + degrees,

Minutes + minutes,

Seconds + seconds);

}

}

// Declaring a class as a reference type
// (declaring it as a struct would create a value type
//  larger than 16 bytes)
class Coordinate

{

public Angle Longitude { get; set; }

public Angle Latitude { get; set; }

}
```

此代码定义 `Angle` 为值类型，存储角度的度、分、秒，可以是经度或纬度。生成的 C# 类型是一个 `struct`。

请注意，代码清单 9.1 中的 `Angle` 结构体是不可变的，因为其所有属性都使用 C# 6.0 的只读自动实现属性功能进行声明。若要在不使用 C# 6.0 的情况下创建只读属性，程序员需要声明一个仅具有 getter 的属性，该属性从一个使用 `readonly` 修饰的字段中访问数据（参见代码清单 9.3）。在定义不可变类型时，C# 6.0 显著减少了代码量。

从 C# 7.2 开始，你可以通过将结构体声明为只读来验证你确实成功定义了一个只读结构体：

```csharp
readonly struct Angle {}
```

现在，编译器将验证整个结构体是不可变的，如果存在非只读字段或具有 setter 的属性，则报告错误。

> **注意**
> 虽然语言本身并不强制要求，但一条良好的准则是让值类型保持不可变：一旦你实例化了一个值类型，就不应该再能够修改同一个实例。在需要修改的场景中，你应该创建一个新实例。代码清单 9.1 提供了一个 `Move()` 方法，该方法不会修改 `Angle` 的实例，而是返回一个完全新的实例。
> 遵循这一准则有两个很好的理由。首先，值类型应该表示值。人们不会认为将两个整数相加会改变其中的任何一个；相反，这两个加数是不可变的，结果会产生第三个值。
> 其次，因为值类型是按值复制的，而不是按引用复制的，所以很容易混淆并错误地认为对一个值类型变量的修改可以观察到导致另一个变量的修改，就像引用类型那样。

**准则**
- 请创建不可变的值类型。

## 初始化结构体

除了属性和字段外，结构体还可以包含方法和构造函数。但是，不能定义默认构造函数。相反，C# 编译器会自动生成一个默认构造函数，将所有字段初始化为其默认值。对于引用类型数据的字段，默认值为 `null`；对于数值类型字段，为零值；对于布尔类型字段，为 `false`，等等。

为了确保本地值类型变量可以完全由构造函数初始化，结构体中的每个构造函数都必须初始化结构体内的所有字段（以及只读的自动实现属性）。（在 C# 6.0 中，通过只读自动实现属性进行初始化就足够了，因为底层字段未知，且无法对其进行初始化。）未能初始化结构体内的所有数据会导致编译时错误。为了稍微增加一些复杂性，C# 不允许在结构体中初始化字段。例如，如果取消注释代码清单 9.2 中的 `_Degrees = 42` 这一行，它就不会编译通过。

### 代码清单 9.2：在声明中初始化结构体字段，导致错误

```csharp
struct Angle
{
// ...
// 错误：字段不能在声明时初始化
// int _Degrees = 42;
// ...
}
```

如果没有通过调用 `new` 运算符的构造函数显式实例化，结构体内包含的所有数据都会隐式初始化为该数据的默认值。然而，为了避免编译器错误，必须显式初始化值类型内的所有数据。这就引出了一个疑问：什么时候值类型会被隐式初始化但不会被显式实例化？这种情况发生在实例化一个包含未分配值类型字段的引用类型，以及实例化一个没有数组初始化的值类型数组时。

为了满足结构体的初始化要求，所有显式声明的字段都必须被初始化。这种初始化必须直接完成。例如，在代码清单 9.3 中，如果取消注释，初始化属性而不是字段的构造函数会产生编译错误。

### 代码清单 9.3：在初始化所有字段之前访问属性

```csharp
struct Angle
{
// 错误：在分配其所有字段之前不能使用 "this" 对象
// public Angle(int degrees, int minutes, int seconds)
// {
//     Degrees = degrees;
//     Minutes = minutes;
//     Seconds = seconds;
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
```

在编译器知道所有字段都已初始化之前，访问 `this` 是不合法的；`Degrees` 的使用隐式为 `this.Degrees`。为了解决这个问题，你需要直接初始化字段，如代码清单 9.3 中未注释掉的构造函数所示。

由于结构体的字段初始化要求、C# 6.0 中只读自动实现属性支持的简洁性，以及避免从外部访问字段的准则（即访问应通过其包裹的属性进行），从 C# 6.0 开始，你应该在结构体中优先使用只读自动实现属性而不是字段。

## 准则

- 请确保结构体的默认值是有效的；总是可以获得结构体的默认“全零”值。

## 高级主题

### 对值类型使用 new

对引用类型调用 `new` 运算符会使运行时在垃圾回收堆上创建对象的新实例，将其所有字段初始化为默认值，并调用构造函数，将实例的引用作为 `this` 传递。结果是实例的引用，然后可以复制到其最终目标。相比之下，对值类型调用 `new` 运算符会使运行时在临时存储池中创建对象的新实例，将其所有字段初始化为默认值，并调用构造函数（将临时存储位置作为 `ref` 变量作为 `this` 传递），导致值存储在临时存储位置中，然后可以复制到其最终目标。

与类不同，结构体不支持终结器。结构体是按值复制的；它们没有引用类型那样的引用身份。因此，很难知道何时执行终结器并释放结构体拥有的非托管资源是安全的。垃圾回收器知道何时没有引用类型的“活动”引用，并可以在没有更多活动引用后的任何时间选择为引用类型实例运行终结器。尽管如此，运行时没有部分跟踪任意时刻存在给定值类型的多少副本。

> **语言对比：C++——struct 定义具有公共成员的类型**
>
> 在 C++ 中，使用 `struct` 声明的类型与使用 `class` 声明的类型之间的区别在于默认可访问性是公共的还是私有的。在 C# 中，这种对比更为显著，区别在于类型的实例是按值复制还是按引用复制。

### 使用 default 运算符

如上所述，不能在结构体上定义默认构造函数。相反，所有值类型都有一个自动定义的默认构造函数，它将值类型的存储初始化为其默认状态。因此，使用 `new` 运算符创建值类型实例总是合法的。

作为一种替代语法，你可以使用 `default` 运算符来生成结构体的默认值。在代码清单 9.4 中，我们为 `Angle` 结构体添加了一个第二个构造函数，该构造函数将 `int` 的 `default` 运算符作为参数传递给先前声明的三参数构造函数。

### 代码清单 9.4：使用 default 运算符获取类型的默认值

```csharp
// 使用关键字 struct 声明值类型
struct Angle
{
    public Angle(int degrees, int minutes)
        : this( degrees, minutes, default(int) )
    {
    }
    // ...
}
```

表达式 `default(int)` 和 `new int()` 都产生相同的值。此外，访问隐式初始化的值类型是有效操作；相比之下，访问引用类型的默认值将产生 `NullReferenceException`。因此，如果 `default(T)` 值对于该类型不是有效状态，你应该在实例化后小心地显式初始化值类型。

请注意，在 C# 7.1 中，`default` 可以不带 `(int)` 使用，如下所示：

```csharp
public Angle(int degrees, int minutes)
    : this( degrees, minutes, default ) { ... }
```

有关 `default` 运算符的更多信息，请参见第 12 章。

## 值类型的继承和接口

所有值类型都隐式地被密封。此外，所有非枚举值类型都派生自 `System.ValueType`。因此，结构体的继承链始终是从 `object` 到 `System.ValueType`，再到该结构体。

值类型也可以实现接口。框架内置的许多值类型实现了诸如 `IComparable` 和 `IFormattable` 等接口。

`System.ValueType` 带来了值类型的行为，但不包含任何额外的成员。`System.ValueType` 的自定义专注于重写 `object` 的所有虚成员。在结构体中重写这些方法的规则与类几乎相同（参见第 10 章）。然而，一个区别是，对于值类型，`GetHashCode()` 的默认实现是将调用转发到结构体内的第一个非空字段。此外，`Equals()` 大量使用反射。因此，如果值类型经常用于集合内部，特别是使用哈希代码的字典类型集合，值类型应包含 `Equals()` 和 `GetHashCode()` 的重写，以确保良好的性能。更多详情请参见第 10 章。

## 指南

- **应当**在值类型上重载相等运算符（`Equals()`、`=` 和 `!=`），如果相等性是有意义的。（也请考虑实现 `IEquatable<T>` 接口。）

## 装箱

我们知道，值类型变量直接包含其数据，而引用类型变量包含对另一个存储位置的引用。但是，当值类型被转换为其实现的接口之一或其根基类 `object` 时会发生什么？转换的结果必须是一个指向包含某种看起来像引用类型实例的内容的存储位置的引用，但该变量包含的是值类型数据。这种被称为**装箱**的转换具有特殊的行为。将一个直接引用其数据的值类型变量转换为引用垃圾回收堆上位置的引用类型涉及几个步骤。

- 在堆上分配内存，该内存将包含值类型的数据以及使该对象看起来像其他引用类型托管对象实例所必需的其他开销（即 `SyncBlockIndex` 和方法表指针）。
- 值类型的数据从其当前位置复制到堆上新分配的内存位置。
- 转换的结果是堆上新存储位置的引用。

逆操作是**拆箱**。拆箱转换检查装箱值的类型是否要与被拆箱值的类型兼容，然后结果是堆位置中存储值的副本。

装箱和拆箱是必须重点考虑的因素，因为装箱会带来一些性能和行为上的影响。除了学习如何在 C# 代码中识别这些转换之外，开发人员还可以通过查看通用中间语言（CIL）来统计特定代码片段中的装箱/拆箱指令数量。每个操作都有特定的指令，如表 9.1 所示。

### 表 9.1：CIL 中的装箱代码

| C# 代码 | CIL 代码 |
| :--- | :--- |
| `static void` Main() | .method private hidesig<br>static void Main() cil managed<br>{<br>.entrypoint<br>// Code size 21 (0x15)<br>.maxstack 1<br>`int` number;<br>`object` thing; | .locals init ([0] int32 number,<br>[1] object thing)<br>IL_0000: nop<br>IL_0001: ldc.i4.s 42<br>IL_0003: stloc.0<br>// Boxing<br>IL_0004: ldloc.0<br>IL_0005: box [mscorlib]System.Int32<br>IL_000a: stloc.1<br>// Unboxing<br>IL_000c: ldloc.1<br>IL_000c: unbox.any [mscorlib]System.Int32<br>IL_0011: stloc.0<br>`return`;<br>IL_0012: br.s IL_0014<br>IL_0014: ret<br>} |

当装箱和拆箱不频繁发生时，其对性能的影响无关紧要。然而，装箱可能会发生在某些意想不到的情况下，且频繁发生会对性能产生重大影响。请考虑清单 9.5 和输出 9.1。`ArrayList` 类型维护一个对象引用列表，因此向列表中添加整数或浮点数会对该值进行装箱，以便获得引用。

### 清单 9.5：微妙的装箱和拆箱指令

```csharp
class DisplayFibonacci
{
    static void Main()
    {
        int totalCount;
        System.Collections.ArrayList list = new System.Collections.ArrayList();
        Console.Write("Enter a number between 2 and 1000:");
        totalCount = int.Parse(Console.ReadLine());
        // Execution-time error:
        // list.Add(0); // Cast to double or 'D' suffix required.
        // Whether cast or using 'D' suffix,
        // CIL is identical.
        list.Add((double)0);
        list.Add((double)1);
        for (int count = 2; count < totalCount; count++)
        {
            list.Add(
                ((double)list[count - 1] +
                (double)list[count - 2]) );
        }
        foreach (double count in list)
        {
            Console.Write("{0}, ", count);
        }
    }
}
```

输出 9.1

```text
Enter a number between 2 and 1000:42
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, 1597,
2584, 4181, 6765, 10946, 17711, 28657, 46368, 75025, 121393, 196418,
317811, 514229, 832040, 1346269, 2178309, 3524578, 5702887, 9227465,
14930352, 24157817, 39088169, 63245986, 102334155, 165580141,
```
