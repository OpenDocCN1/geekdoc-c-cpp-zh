
在这里，`type` 是指针将指向的对象类型，且它必须是非引用类型。`var_name` 是指针变量的。例如，要声明 `ip` 为指向 `int` 的指针，使用此声明：

```c
int* ip;
```

对于 `float` 指针，使用：

```c
float* fp;
```

通常，在声明语句中，在类型名后跟一个 `*` 会创建一个指针类型。指针将指向的数据类型由其引用类型（referent type）决定，这通常也被称为指针的基类型。因此，在前面的示例中，`ip` 可以指向一个 `int`，而 `fp` 可以指向一个 `float`。然而，要理解，没有任何东西阻止指针指向其他东西。这就是为什么指针潜在是不安全的。

记住，指针类型只能为非引用类型声明。这意味着指针的引用类型可以是任何简单类型，如 `int`、`double`、`char`；枚举类型；或结构体（struct）（只要其字段是非引用类型）。

有两个关键的指针运算符：`*` 和 `&`。`&` 是一个返回操作数内存地址的一元运算符。（记住一元运算符只需要一个操作数）。例如：

```c
int* ip;
int num = 10;
```

```c
ip = &num;
```

将变量 `num` 的内存地址放入 `ip`。该地址是变量在计算机内部内存中的位置。它与 `num` 的值无关。因此，`ip` 不包含值 10（`num` 的初始值）。它包含 `num` 存储的地址。`&` 操作可以记忆为返回其前置变量的“地址”。因此，上面的赋值语句可以口述为“ip 接收了 num 的地址”。

第二个运算符是 `*`，它是 `&` 的补补。它是一个解引用（dereferences）指针的一元运算符。换句话说，它求值操作数所指定地址的变量。继续同样的示例，如果 `ip` 包含变量 `num` 的内存地址，那么：

```c
int val;
val = *ip;
```

将值 10 放入 `val`，这是 `num` 的值（被 `ip` 指向的值）。`*` 操作可以记忆为“在地址处”。在这种情况下，该语句可以读作“val 接收了 ip 处的值”。

指针可以与结构体一起使用。当通过指针访问结构体的成员时，必须使用 `->` 运算符而不是点 (`.`) 运算符。`->` 非正式地称为箭头运算符。例如，给定此结构：

```c
struct MyStruct {
    public int x;
    public int y;
    public int sum() { return x + y; }
}
```

```c
MyStruct o = new MyStruct();
MyStruct* p;
p = &o; // 将 o 的地址放入 p
p->x = 10; // 通过 p 赋值 x
p->y = 20; // 通过 p 赋值 y
Console.WriteLine("Sum is " + p->sum());
```

指针可以进行算运算。例如，你可以增加或减少指针。这允许你遍历数组。

```csharp
int[] numbers = { 10, 20, 30 };
int* p = numbers;
for (int i = 0; i < 3; i++) {
    Console.WriteLine(*p);
    p++;
}
```

### unsafe 关键字

任何使用指针的代码都必须使用 `unsafe` 关键字进行标记。你可以将类型（如类和结构体）、成员（如方法和运算符）或单独的代码块标记为 `unsafe`。例如，这里有一个在 `Main()` 中使用指针的程序：

```c
// 演示指针和 unsafe。
// 你需要通过 /unsafe 选项编译此程序。
using System;
class UnsafeCode {
    // 将 Main 标记为 unsafe。
    unsafe static void Main() {
        int count = 99;
        int* p; // 创建一个 int 指针
        p = &count; // 将 count 的地址放入 p
        Console.WriteLine("Initial value of count is " + *p);
        *p = 10; // 通过 p 给 count赋值
        Console.WriteLine("New value of count is " + *p);
    }
}
```

此程序的输出在此处：

Initial value of count is 99
New value of count is 10

此程序使用指针 p 获取 `count` 包含的值，即 p 指向的对象。由于指针操作，它必须标记为 `unsafe` 才能编译。

## 使用 fixed

`fixed` 关键字有两个用途。第一个是防止托管对象被垃圾回收器移动。当指针引用此类内部的字段时，这是需要的。由于指针不知道垃圾回收器的操作，如果对象移动，指针将指向错误的位置。这里是 `fixed` 的通用形式：

```c
fixed (type* p = &fixedVar) {
    // 使用对象
}
```

在这里，`p` 是一个被赋值变量地址的指针。在代码块执行之前，该变量将保持在当前的内存位置。

# 第 15 章：预处理器、RTTI、可空类型及其他高级主题

用于固定语句的目标语句。`fixed` 关键字只能在不安全（unsafe）上下文中使用。
以下是 `fixed` 的示例：

```cs
// Demonstrate fixed.
using System;
class Test {
    public int num;
    public Test(int i) { num = i; }
}
class UseFixed {
    // 标记为 unsafe.
    unsafe static void Main() {
        Test o = new Test(19);
        fixed (int* p = &o.num) { // 使用 fixed 将 o.num 的地址放入 p
            Console.WriteLine("Initial value of o.num is " + *p);
            *p = 10; // 通过 p 赋值给 o.num
            Console.WriteLine("New value of o.num is " + *p);
        }
    }
}
```

该程序的输出所示：
Initial value of o.num is 19
New value of o.num is 10

`fixed` 的第二个用途是创建固定大小的一维数组。这些被称为固定大小缓冲区（fixed-size buffers）。固定大小缓冲区始终结构体（struct）的成员。固定大小缓冲区的目的是创建一个结构体，其中组成缓冲区的数组元素包含在结构体内部。通常，当你在结构体中包含数组成员时，结构体内实际上只持有数组的引用。通过使用固定大小缓冲区，你可以使整个数组包含在结构体中。这导致生成的结构可以在结构体大小重要的情况下使用，例如混合语言编程、与非 C# 程序创建的数据进行交互，或者任何需要包含数组的非托管结构体的场景。固定大小缓冲区只能在不安全（unsafe）上下文中使用。

## C# 3.0：学者指南

要创建固定大小缓冲区，请使用 `fixed` 这种形式的形式：
`fixed type buf-name[size];`

在这里，`type` 是数组的数据类型，`buf-name` 是固定大小缓冲区的名称，`size` 是缓冲区中元素的数量。固定大小缓冲区只能在结构体内部指定。

正如本节开头所述，不安全代码（unsafe code）的创建和使用是一个高级主题，涉及的问题比这里讨论的要多。如果编写不安全代码将成为你编程未来的一部分，那么你将需要进一步学习。

### 属性（Attributes）

C# 允许你以属性（attribute）的形式为程序添加声明性信息。属性定义了与类、结构体、方法等关联的附加信息。例如，你可以定义一个属性来确定类将显示的的按钮类型。

属性指定在方括号之间，位于其所适用的项目之前。你可以定义自己的属性，也可以使用 C# 提供的属性。虽然创建自己的属性超出了本书的范围，但你可以很容易使用 C# 的两个内置属性：`Conditional` 和 `Obsolete`。它们将在接下来的节中进行检查。

### Conditional 特性（The Conditional Attribute）

`Conditional` 特性是 C# 最有趣的属性。它允许你创建条件方法（conditional methods）。条件方法只有在通过 `#define` 定义了特定符号时才会被调用。否则，方法将被跳过。因此，条件方法提供了使用 `#if` 进行条件编译的替代方案。使用 `Conditional` 特性时，必须包含 `System.Diagnostics` 命名空间。

让我们从一个示例开始：

```cs
// Demonstrate the Conditional attribute.
#define TRIAL
```

```cs
using System;
using System.Diagnostics;
```

```cs
class Test {
    [Conditional("TRIAL")]
    void Trial() { // 只有在定义 TRIAL 时执行。
        Console.WriteLine("Trial version, not for distribution.");
    }
    [Conditional("RELEASE")]
    void Release() { // 只有在定义 RELEASE 时执行。
        Console.WriteLine("Final release version.");
    }
}
```

```cs
static void Main() {
    Test t = new Test();
    t.Trial(); // 只有在定义 TRIAL 时调用
    t.Release(); // 只有在定义 RELEASE 时调用
}
}
```

该程序的输出所示：

Trial version, not for distribution.

让我们仔细观察程序以理解为什么会产生这种输出。首先注意程序定义了符号 `TRIAL`。接下来，看 `Trial()` 和 `Release()` 方法是如何编写的。它们前面都有 `Conditional` 特性，该特性具有以下通用形式：

`[Conditional symbol]`

其中 `symbol` 是决定方法是否将执行的符号。如果符号已定义，则方法将被调用并执行。该属性只能用于方法。如果符号未定义，则方法将不执行。在 `Main()` 中，`Trial()` 和 `Release()` 都被调用了，但只定义了 `TRIAL`。因此，执行了 `Trial()`。`Release()` 的调用被忽略。如果你定义了 `RELEASE`，那么 `Release()` 也会被调用。如果你删除了 `TRIAL` 的定义，`Trial()` 将不会被调用。

方法有一些限制：它们必须返回 `void`；它们必须是类或结构体的成员，而不是接口；并且它们前面不能有 `override` 关键字。

### Obsolete 特性（The Obsolete Attribute）

`Obsolete` 特性允许你将程序元素标记为过时。它有两个基本形式。第一种是：

`[Obsolete "message"]`

在这里，`message` 是元素被使用时显示的消息。这是一个简短的示例：

```cs
// Demonstrate the obsolete attribute.
using System;
class Test {
    [Obsolete("Use MyMethod instead.")]
    void MyMethod() { }
}
```

# 转换运算符（Conversion Operators）

在某些情况下，你希望将类对象转换为数值，以便在表达式中使用。为了实现这一点，你可以使用转换运算符。转换运算符有两种形式：隐式（implicit）和显式（explicit）。

如果运算符指定为隐式，则在表达式中使用时自动调用。当运算符指定为显式时，在使用强制转换时调用。你不能对相同的源类型同时定义隐性和显式转换运算符。

为了说明转换，我们将使用在第 7 章中创建的 `ThreeD` 类。记得 `ThreeD` 存储三维坐标。假设你想将 `ThreeD` 类型的对象转换为其到原点的距离。

```cs
// An implicit conversion from ThreeD to double.
// It returns the distance from the origin to the
// specified point.
public static implicit operator double(ThreeD opl) {
    return Math.Sqrt(opl.x * opl.x + opl.y * opl.y + opl.z * opl.z);
}
```

以下是一个说明此转换运算符的示例：

```cs
// An example that uses an implicit conversion
using System;
// A three-dimensional coordinate class.
class ThreeD {
    int x, y, z; // 3-D coordinates
    public ThreeD() { x = y = z = 0; }
    public ThreeD(int i, int j, int k) { x = i; y = j; z = k; }
    // Overload binary +.
    public static ThreeD operator+(ThreeD opl, ThreeD op2) {
        ThreeD result = new ThreeD();
        result.x = opl.x + op2.x;
        result.y = opl.y + op2.y;
        result.z = opl.z + op2.z;
        return result;
    }
    // An implicit conversion from ThreeD to double.
    // It returns the distance from the origin to the
    // specified point.
    public static implicit operator double(ThreeD opl) {
        return Math.Sqrt(opl.x * opl.x + opl.y * opl.y + opl.z * opl.z);
    }
    // Show X, Y, Z coordinates.
    public void Show() {
        Console.WriteLine(x + " , " + y + " , " + z);
    }
}
```

# C# 3.0: 初学者指南

```cs
class ConversionOpDemo {
    static void Main() {
        ThreeD alpha = new ThreeD(12, 3, 4);
        ThreeD beta = new ThreeD(10, 10, 10);
        ThreeD gamma = new ThreeD();
        double dist;
        Console.Write("Here is alpha: ");
        alpha.Show();
        Console.WriteLine();
        Console.Write("Here is beta: ");
        beta.Show();
        Console.WriteLine();
        // Add alpha and beta together. This does NOT invoke
        // the conversion operator because no conversion to
        // double is needed
        gamma = alpha + beta;
        Console.Write("Result of alpha + beta: ");
        gamma.Show();
        Console.WriteLine();
        // The following statement invokes the conversion
        // operator because the value of a is assigned
        // to dist, which is a double.
        dist = alpha; // convert to double
        Console.WriteLine("Result of dist = " + dist);
        Console.WriteLine();
        // This also invokes the conversion operator
