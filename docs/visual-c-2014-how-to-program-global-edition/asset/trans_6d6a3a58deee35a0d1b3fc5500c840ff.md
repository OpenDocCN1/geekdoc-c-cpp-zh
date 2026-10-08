

## 第 10 章 类与对象：深入观察

对象浏览器（Object Browser）在右上窗格中列出了 `Math` 类提供的所有方法——为您提供有关各种对象功能的“即时访问”。点击右上窗格中成员的名称，会在右下窗格中显示该成员的描述。可以使用对象浏览器快速学习某个类或其其中一个方法。您也可以通过在对象浏览器中选择类型或成员并按 F1，在在线文档中查看该类或方法的完整描述。

## 10.12 对象初始化器

对象初始化器允许你在同一条语句中创建对象并初始化其公共属性（以及任何公共实例变量）。当一个类没有提供满足你需求的合适构造函数，但提供了一个可以无参数调用的构造函数以及你可以用于设置类数据的属性时，这种方法会非常有用。以下语句通过使用 10.5 节中的 `Time2` 类演示了对象初始化器。

```
// 创建一个 Time2 对象并初始化其属性
var aTime = new Time2 {Hour = 14, Minute = 30, Second = 12};

// 创建一个 Time2 对象并仅初始化其 Minute 属性
var another = new Time2 {Minute = 45};
```

第一条语句创建一个 `Time2` 对象 (aTime)，使用可以无参数调用的 Time2 构造函数对其初始化，然后使用对象初始化器设置其 `Hour`、`Minute` 和 `Second` 属性。注意，`new Time2` 后面紧跟着一个对象初始化列表——这是一个位于 `{ }` 中的逗号分隔的属性及其值的列表。每个属性名称在对象初始化列表中只出现一次。对象初始化器按照初始化器出现的顺序执行初始化操作。

第二条语句创建一个新的 `Time2` 对象 (another)，使用可以无参数调用的 Time2 构造函数对其初始化，然后使用对象初始化器仅初始化其 `Minute` 属性。当无参数调用 Time2 构造函数时，它会将时间初始化为午夜。随后对象初始化器将每个属性设置为提供的值。在这种情况下，`Minute` 属性被设置为 45。`Hour` 和 `Second` 属性保留了它们的默认值，因为对象初始化器中没有设置这些值。

## 10.13 运算符重载；引入 struct

对于某些操作（如算术运算），方法调用可能非常繁琐。在这种情况下，使用 C# 丰富的内置运算符集会非常方便。本节展示了如何通过一个名为“运算符重载”的过程，为你类型的对象创建运算符。

你可以重载大多数运算符。某些运算符的重载频率比其他高，特别是算术运算符，例如 `+` 和 `-`，在此时使用运算符符号比调用方法更自然。可重载运算符的列表请参阅：

> https://msdn.microsoft.com/library/8edha9s

## 10.13 运算符重载：引入 struct

### 10.13.1 使用 struct 创建值类型

为了演示运算符重载，我们将定义类型 `ComplexNumber`（第 10.13.2 节）。复数具有：

```
realPart + imaginaryPart *
```

其中 $i$ 是 $\sqrt{-1}$。整数、浮点数和复数都是计算中常用的算术类型。如你所知，C# 的简单数值类型是值类型。为了模拟简单数值类型，我们将使用 `struct`（“structure”的缩写）而不是类将 `ComplexNumber` 定义为值类型。C# 的简单类型如 `int` 和 `double` 是类型的别名——`int` 由结构体 `System.Int32` 定义，`long` 由 `System.Int64` 定义，`double` 由 `System.Double` 定义等。第 10.13.2 节中所示的运算符重载技术也可以应用于类。

#### 何时声明 struct 类型

微软建议对大多数类型使用类，但在以下情况下建议使用 `struct`：

- 该类型表示单一值——复数代表一个恰好具有实部和虚部的数字。
- 对象的大小为 16 字节或更——我们将使用两个 `double` 来表示复数的实部和虚部（16 字节）。

关于 `struct` 建议的完整列表，请使用：

> https://msdn.microsoft.com/library/ms229017

### 10.13.2 值类型 ComplexNumber

值类型 `ComplexNumber`（图 10.14）重载了加 (`+`)、减 (`-`) 和乘 (`*`) 运算符，用于对 `ComplexNumber` 实例进行加、减、乘运算。

```
// 图 10.14: ComplexNumber.cs
// 用于加、减、乘重载的值类型。
using System;

public struct ComplexNumber
{
    // 只读属性
    public double Real { get; }
    public double Imaginary { get; }

    // 构造函数
    public ComplexNumber(double real, double imaginary)
    {
        Real = real;
        Imaginary = imaginary;
    }

    // 重载运算符
    public static ComplexNumber operator +(ComplexNumber a, ComplexNumber b)
    {
        return new ComplexNumber(a.Real + b.Real, a.Imaginary + b.Imaginary);
    }

    public static ComplexNumber operator -(ComplexNumber a, ComplexNumber b)
    {
        return new ComplexNumber(a.Real - b.Real, a.Imaginary - b.Imaginary);
    }

    public static ComplexNumber operator *(ComplexNumber a, ComplexNumber b)
    {
        return new ComplexNumber(a.Real * b.Real - a.Imaginary * b.Imaginary, a.Real * b.Imaginary + a.Imaginary * b.Real);
    }
}
```

与类不同，你不能为 `struct` 定义无参数构造函数——编译器始终提供一个默认构造函数，将实例变量初始化为默认值。重载二元运算符的方法必须接受两个参数——第一个是左操作数，第二个是右操作数。方法体相加参数并返回一个表示参数之和的新 `ComplexNumber`。我们没有修改作为参数传递的原始操作数 `x` 和 `y` 的内容。这符合我们对运算符行为的直觉感受——加两个数字不会修改原始的任何一个值。

### 10.13.3 ComplexTest

`ComplexTest`（图 10.15）演示了重载的 `ComplexNumber` 运算符 `+` 和 `*`。第 10–21 行提示用户输入两个复数的实部和虚部，然后使用这些输入创建用于计算的 `ComplexNumber` 对象。

```
// 图 10.15: ComplexTest
// 为复数重载运算符。
class ComplexTest
{
    // 提示用户输入第一个复数
    Console.Write("Enter the real part of complex number x: ");
    double realPart = double.Parse(Console.ReadLine());
    Console.Write("Enter the imaginary part of complex number x: ");
    double imaginaryPart = double.Parse(Console.ReadLine());
    var x = new ComplexNumber(realPart, imaginaryPart);

    // 提示用户输入第二个复数
    Console.Write("Enter the real part of complex number y: ");
    double realPart = double.Parse(Console.ReadLine());
    Console.Write("Enter the imaginary part of complex number y: ");
    double imaginaryPart = double.Parse(Console.ReadLine());
    var y = new ComplexNumber(realPart, imaginaryPart);

    // 显示 x 和 y 的计算结果
    Console.WriteLine();
}
```

