
注意，所有第二个版本的运算符都从其参数构造了一个 *Hour* 并调用了第一个版本。通过这种方式，运算符背后的真实逻辑保留在单一位置。重点是，额外的 `operator+` 只是让现有功能更易用。此外，注意你不应该提供此运算符的许多不同版本，每个版本具有不同的第二个参数类型；相反，只需满足常见且有意义的情况，如果需要异常情况，让类的用户采取任何额外的步骤即可。

此 `operator+` 声明了如何将一个 *Hour* 作为左操作数、*int* 作为右操作数相加。它没有声明如何将一个 *int* 作为左操作数、*Hour* 作为右操作数相加：

点击此处查看代码图像

```csharp
int a = ...;

Hour b = ...;

Hour later = a + b; // 编译错误
```

这是违背直觉的。如果你可以写表达式 `a + b`，你预期同样也能写 `b + a`。因此，你应该为 `operator+` 提供另一个重载：

点击此处查看代码图像

```csharp
struct Hour
{
    public Hour(int initialValue) => this.value = initialValue;
    public static Hour operator +(Hour lhs, int rhs) => lhs + new Hour(rhs);
    public static Hour operator +(int lhs, Hour rhs) => new Hour(lhs) + rhs;
    private int value;
}
```

> **注意** C++ 程序员应该注意，你必须自己提供重载。编译器不会为你编写重载，也不会静默地交换两个操作数的顺序以寻找匹配的运算符。

# 运算符与语言间的互操作性

并不是所有使用公共语言运行时 `CLR` 执行的语言都支持或理解运算符重载。如果你重载了运算符，你应该提供一种实现相同功能的替代机制，以便该类能够在那些不支持运算符重载的语言中使用。例如，假设你为 *Hour* 结构体实现了 `operator+`，如下所示：

点击此处查看代码图像

```csharp
public static Hour operator +(Hour lhs, int rhs)
{
}
```

如果你需要在 Microsoft Visual Basic 应用程序中使用你的类，你还应该提供一个 `Add` 方法来实现相同的功能，如下所示：

点击此处查看代码图像

```csharp
public static Hour operator +(Hour lhs, int rhs)
{
}
```

# 理解复合赋值

通常情况下，复合赋值（例如 `+=`）是自动的。当你重载了某个运算符时，C# 编译器会自动将你的代码转换为对你定义的 *operator +* 方法的调用。C# 编译器会将此代码转换（当你对两个类型为 *Hour* 的表达式使用 `+` 运算符时）：

[点击此处查看代码图像]

```csharp
Hour Example(Hour a, Hour b) => a + b;
```

转换为如下：

[点击此处查看代码图像]

```csharp
Hour Example(Hour a, Hour b) => Hour.operator+(a,b); // 伪代码
```

注意，这种语法是伪代码，不是有效的 C#。你只能在标准的中置表示法（即符号位于操作数之间）中使用二元运算符。

在声明运算符时，你必须遵循的最后一个规则：参数中至少有一个必须始终是容器类型。在之前 *Hour* 类的 *operator+* 示例中，*a* 或 *b* 必须是一个 *Hour* 对象。然而，在某些情况下，你可能想要定义 *operator+* 的额外实现，例如将一个整数（小时数）加到 *Hour* 对象上——第一个参数可以是 *Hour*，而第二个参数可以是整数。该规则使得编译器在尝试解析运算符调用时更容易知道去哪里查找，而且它确保了你无法更改内置运算符的含义。

# 声明递增和递减运算符

在 C# 中，你可以声明自己的递增（`++`）和递减（`--`）运算符。通常规则适用于这些运算符：它们必须是公共的、静态的，并且它们必须接受单个参数。这里是 *Hour* 结构的递增运算符：

```csharp
struct Hour
{
    public Hour(int initialValue) => this.value = initialValue;
    public static Hour operator ++(Hour arg)
    {
        arg.value++;
        return arg;
    }
    public static Hour operator --(Hour arg)
    {
        arg.value--;
        return arg;
    }
    private int value;
}
```

递增和递减运算符的独特之处在于它们可以以前置和后置的形式使用。C# 巧妙地使用同一个运算符来处理前置和后置版本。后置表达式的结果是操作发生前的操作数值。换句话说，编译器会将代码转换为：

点击此处查看代码图像

```csharp
Hour a = ...;
int b = ...;
Hour later = a++;
```

转换为：

```csharp
Hour a = ...;
int b = ...;
Hour later = a;
a = Hour.operator++a);
```

前置表达式的结果是运算符的返回值，所以 C# 编译器会将代码转换为：

点击此处查看代码图像

```csharp
Hour a = ...;
int b = ...;
Hour prefix = ++a;
```

转换为：

```csharp
Hour a = ...;
int b = ...;
a = Hour.operator++(a);
Hour prefix = a;
```

这种等价性意味着递增和递减运算符的返回类型必须与参数类型相同。

# 比较结构体和类中的运算符

注意，`Hour` 结构中的递增运算符实现之所以有效，是因为 `Hour` 是一个结构体。如果你将 `Hour` 改为类但保持递增运算符实现不变，你会发现后置翻译将无法给出正确答案。如果你记得类是引用类型，并回顾之前的编译器翻译，你可以在下面的示例中看到 `Hour` 类的运算符不再按预期工作：

```csharp
Hour a = ...;
int b = ...;
Hour later = a++;
```

如果 `Hour` 是类，赋值语句 `postfix = now` 会使 `postfix` 指向与 `now` 相同的对象。更新 `now` 会更新 `postfix`！如果 `Hour` 是结构体，赋值语句会在 `postfix` 中创建一个副本，并且对 `now` 的任何更改都不会影响 `postfix`，这正是你想要的。

当 `Hour` 是类时，正确的递增运算符实现是

如下：

点击此处查看代码

```csharp
class Hour
{
    public Hour(int initialValue) => this.value = initialValue;
    ...
    public static Hour operator++(Hour arg) => new Hour(arg.value + 1);
    private int value;
}
```

注意，`operator ++` 会根据原始对象中的数据创建一个新对象。新对象中的数据增加了 1，但原始对象中的数据保持不变。虽然这种方法可行之，但编译器对递增运算符的翻译会导致每次使用它时都创建一个新对象。这在内存使用和垃圾回收开销方面可能是昂昂的。因此，建议在定义类型时限制运算符重载。此项建议适用于所有运算符，而不仅仅是递增运算符。

## 定义运算符对

某些运算符自然是成对出现的。例如，如果你可以使用 `!=` 运算符比较 `Hour` 值，那么你可能希望可以使用 `==` 运算符比较两个 `Hour` 值。C# 编译器通过强制执行这一非常合理的预期，坚持认为如果你定义了 `operator ==` 或 `operator !=`，就必须定义两者。这种“非此即彼或两者皆有”的规则适用于 `<` 和 `>` 运算符以及 `<=` 和 `>=` 运算符。C# 编译器不会为你编写任何这些运算符伙伴。无论它们看起来有多明显，你都必须显式地编写它们。以下是 `Hour` 结构体的 `==` 和 `!=` 运算符：

点击此处查看代码

```csharp
struct Hour
{
    public Hour(int initialValue) => this.value = initialValue;
    public static bool operator ==(Hour lhs, Hour rhs) => lhs.value == rhs.value;
    public static bool operator !=(Hour lhs, Hour rhs) => lhs.value != rhs.value;
    ...
    private int value;
}
```

这些运算符的返回类型实际上并不必须是布尔值。然而，你应该有一个充分的理由使用其他类型，否则这些运算符可能会变得非常令人混乱。

## 重写相等运算符

如果你在类中定义了 `operator ==` 和 `operator !=`，你还应该重写继承自 `System.Object`（如果你正在创建结构体，则继承自 `System.ValueType`）的 `Equals` 和 `GetHashCode` 方法。`Equals` 方法应该表现出与 `operator ==` 相同的行为。（你应该根据其中一个来定义另一个）。`GetHashCode` 方法由 Microsoft .NET Framework 中的其他类调用。（例如，当用对象作为哈希表中的键时，会在对象上调用 `GetHashCode` 方法来帮助计算哈希值。更多信息请参阅 Visual Studio 2017 提供的 .NET Framework 参考文档。）所有这些方法只需要返回一个区分性的整数值。然而，不要从所有对象的 `GetHashCode` 方法中返回相同的整数，因为这将消除哈希算法的有效性。

## 实现运算符

在下面的练习中，你将开发一个模拟复数的类。

复数有两个元素：实部和虚部。通常，复数以 `(x + iy)` 的形式表示，其中 `x` 是实部，`iy` 中的 `y` 是普通整数，而 `i` 代表 -1 的平方根（这就是为什么 `iy` 是虚部的）。尽管它们感觉相当晦涩且理论化，但复数在电子学、应用数学、物理领域以及工程的许多方面都有大量用途。如果你想了解更多关于复数如何有用以及为什么有信息，维基百科提供了一篇实用且信息丰富的文章。

> 注意：Microsoft .NET Framework 4.0 及更高版本在 `System.Numerics` 命名空间包含一个名为 `Complex` 的类型，它实现了复数，因此你没有必要再定义该类型的自定义版本了。然而，查看如何实现该类型的某些常用运算符仍然具有启发意义。

你将复数实现为一对整数，代表实部和虚部元素的系数 `x` 和 `y`。你还将实现使用复数进行简单算术运算所需的运算符。下表总结了如何对一对复数 `(a + bi)` 和 `(c + di)` 执行四种主要的算术运算。

| 运算 | 计算 |
| --- | --- |
| (a + bi) + (c + di) | ((a + c) + (b + d)i) |
| (a + bi) - (c + di) | ((a - c) - (b - d)i) |
| (a + bi) * (c + di) | ((a*c-b*d) + (b*c+a*d)i) |
| (a + bi) / (c + di) | (((a*c+b*d)/(c*c+d*d)) + ((b*c-a*d)/(c*c+d*d))i) |

### 创建 Complex 类并实现算术运算符

- 1. 如果 Visual Studio 2017 未运行，请启动它。
- 2. 打开 `ComplexNumbers` 解决方案，它位于文档文件夹中的 `\Microsoft Press\VCSBS\Complex22\ComplexNumbers` 文件夹。这是一个控制应用程序，你将用它来构建和测试代码。`Program.cs` 文件包含熟悉的 `doWork`。
- 3. 在解决方案管理器中，点击 `ComplexNumbers` 项目。在项目菜单上，点击“添加类”。在“添加新建项 - ComplexNumbers”对话框中，在“名称”框中输入 `Complex.cs`，然后点击“添加”。

Visual Studio 会创建 `Complex` 类并在代码和文本编辑器窗口中打开 `Complex.cs` 文件。

- 4. 为 `Complex` 类添加自动整数属性 `Real` 和 `Imaginary`。

```csharp
class Complex
{
    public int Real { get; set; }
    public int Imaginary { get; set; }
}
```

这些属性将持有实部虚部。

- 5. 为 `Complex` 类添加构造函数。

```csharp
public Complex(int real, int imaginary)
{
    Real = real;
    Imaginary = imaginary;
}
```

- 6. 在 `Complex` 类中重写 `ToString` 方法。

```csharp
public override string ToString()
{
    return "(" + Real + " + " + Imaginary + ")";
}
```

- 7. 为 `Complex` 类添加重载的 `+` 运算符。

```csharp
public static Complex operator+(Complex lhs, Complex rhs)
{
    return new Complex(lhs.Real + rhs.Real, lhs.Imaginary + rhs.Imaginary);
}
```

- 8. 为 `Complex` 类添加重载的 `-` 运算符。

```csharp
public static Complex operator-(Complex lhs, Complex rhs)
{
    return new Complex(lhs.Real - rhs.Real, lhs.Imaginary - rhs.Imaginary);
}
```

- 9. 通过向 `Complex` 类添加代码实现 `*` 和 `/` 运算符。

```csharp
public static Complex operator*(Complex lhs, Complex rhs)
{
    return new Complex(lhs.Real * rhs.Real - lhs.Imaginary * rhs.Imaginary, lhs.Real * rhs.Imaginary + lhs.Imaginary * rhs.Real);
}
public static Complex operator/(Complex lhs, Complex rhs)
{
    int realElement = (lhs.Real * rhs.Real + lhs.Imaginary * rhs.Imaginary) / (rhs.Real * rhs.Real + rhs.Imaginary * rhs.Imaginary);
    int imaginaryElement = (lhs.Imaginary * rhs.Real - lhs.Real * rhs.Imaginary) / (rhs.Real * rhs.Real + rhs.Imaginary * rhs.Imaginary);
    return new Complex(realElement, imaginaryElement);
}
```

- 1. 在代码和文本编辑器窗口中显示 `Program.cs` 文件。在 `Program` 类的 `doWork` 方法中添加以下语句并删除 `// TODO:` 注释：

```csharp
static void doWork()
{
    Complex first = new Complex(10, 4);
    Complex second = new Complex(5, 2);
    Console.WriteLine("first is " + first);
    Console.WriteLine("second is " + second);
    Complex temp = first + second;
    Console.WriteLine("Add: result is " + temp);
    temp = first - second;
    Console.WriteLine("Subtract: result is " + temp);
    temp = first * second;
    Console.WriteLine("Multiply: result is " + temp);
    temp = first / second;
    Console.WriteLine("Divide: result is " + temp);
}
```
