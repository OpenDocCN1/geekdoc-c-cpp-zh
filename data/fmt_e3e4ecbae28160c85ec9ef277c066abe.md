
- 2. 在“调试”菜单上，点击“不调试启动”。

验证应用程序显示了如下所示的结果：

![](img/74dd8343b56b72576ea64f076a8146e6_719_0.png)

12. 关闭应用程序，返回 Visual Studio 2017 编程环境。

你现在已经创建了一个模拟复数并支持基本算术运算的类型。在下一个练习中，你将扩展 `Complex` 类并提供相等运算符 `==` 和 `!=`。

## 实现相等运算符

- 1. 在 Visual Studio 2017 中，在代码和文本编辑器窗口中显示 `Complex.cs` 文件。

- 2. 正如示例中粗体所示，向 `Complex` 类中添加 `==` 和 `!=` 运算符。

点击此处查看代码图像

```
class Complex
{
....
public static bool operator ==(Complex lhs, Complex rhs) => lhs.Equals(rhs);
public static bool operator !=(Complex lhs, Complex rhs) => !lhs.Equals(rhs);
}
```

注意，这两个运算符都使用了 `Equals` 方法。`Equals` 方法将类实例与作为参数指定的另一个实例进行比较。如果它们具有等效的值，则返回 `true`，否则返回 `false`。为了让相等运算符正常工作，你需要为该方法提供你自己的实现。

- 3. 通过向 `Complex` 类中添加此处所示的内容来重写 `Equals` 方法：

点击此处查看代码图像

```
class Complex
{
....
public override bool Equals(Object obj)
{
if (obj is Complex)
{
Complex compare = (Complex)obj;
return (this.Real == compare.Real) &&
this.Imaginary == compare.Imaginary);
}
else{
  return false;
}
}
}
```

`Equals` 方法接受一个 `Object` 参数。此代码验证参数的类型是否确实为 `Complex` 对象。如果是，此代码将比较当前实例和传递参数的 `Real` 和 `Imaginary` 属性中的值。如果它们相同，则方法返回 `true`；否则返回 `false`。如果传递的参数不是 `Complex` 对象，则方法返回 `false`。

> 重要：很容易像这样写 `Equals` 方法：
点击此处查看代码图像
```csharp
public override bool Equals(Object obj)
{
  Complex compare = obj as Complex;
  if (compare != null) {
    return (this.Real == compare.Real && (this.Imaginary == compare.Imaginary));
  }
  else {
    return false;
  }
}
```

然而，表达式 `compare != null` 会调用 `Complex` 类的 `!=` 运算符，这会再次调用 `Equals` 方法，导致递归循环。

## 4. 在“生成”菜单上，点击“重新生成解决方案”。

“错误列表”窗口显示以下警告消息：

点击此处查看代码图像

'ComplexNumbers.Complex' overrides Object.Equals(object o) but does not override Object.GetHashCode()
'ComplexNumbers.Complex' defines operator == or operator != but does not override Object.GetHashCode()

如果你定义了 `!=` 和 `==` 运算符，你应该重写自 `System.Object` 的 `GetHashCode` 方法。

> 注意：如果“错误列表”窗口不可见，请点击“视图”菜单上的“错误列表”。

- 5. 通过添加此处粗体所示的内容为 `Complex` 类重写 `GetHashCode` 方法。此实现简单地调用了继承自 `Object` 类的方法，但如果你愿意，也可以提供你自己的机制来为对象生成哈希码。

点击此处查看代码图像

```
Class Complex
{
...\public override int GetHashCode()
{
return base.GetHashCode();
}
}
```

- 6. 在“生成”菜单上，点击“重新生成解决方案”。

验证解决方案现在构建时没有报告任何警告。

- 7. 在代码和文本编辑器窗口中显示 `Program.cs` 文件。在 `doWork` 方法末尾添加此处粗体所示的代码：

点击此处查看代码图像
```csharp
static void dowork()
{
...\if (temp == first)
{
Console.WriteLine("Comparison: temp == first");
}
else
{
Console.WriteLine("Comparison: temp != first");
}
if (temp != first)
{
    Console.WriteLine("Comparison: temp != first");
}
else
{
    Console.WriteLine("Comparison: temp == first");
}
```

如果 `temp == first`，则将输出 `Comparison: temp == first`；否则，将输出 `Comparison: temp != first`。

如果 `temp != first`，则将输出 `Comparison: temp != first`；否则，将将输出 `Comparison: temp == first`。

- 8. 在“调试”菜单上，点击“开始调试”。

验证输出：

Comparison: temp == first
Comparison: temp != first
Comparison: temp != first
Comparison: temp == first

- 9. 关闭应用程序，返回 Visual Studio 2017 编程环境。

## 理解转换运算符

有时，你需要将一个类型转换为另一种类型。例如，`int` 转换为 `double` 如下所示的定义方法：

```csharp
class Example
{
    public static void MyDoubleMethod(double parameter)
    {
    }
}
```

你可能会期望 `MyDoubleMethod` 可以接受 `int`，但情况并非如此。`double` 隐式转换为 `int` 是 C# 允许的。

## 提供内置转换

`int` 转换为 `double` 是隐式转换，因为 `double` 的范围大于 `int`，且 `int` 转换为 `double` 不需要特殊语法。然而，反之则如此，`double` 转换为 `int` 不能进行隐式转换：

```csharp
class Example
{
    public static void MyIntMethod(int parameter)
    {
    }
}
```

```csharp
Example.MyIntMethod(42.0); // 编译错误
```

当你将 `double` 转换为 `int` 时，会面临丢失信息的风险，因此转换不会自动执行。`double` 转换为 `int` 需要显式符号（强制转换）。

```csharp
Example.MyIntMethod((int)42.0);
```

显式转换有时被称为缩小转换，因为结果比原始值窄（包含更少的信息），并且如果结果超出目标类型的范围，可能会抛出 `OverflowException`。在 C# 中，你可以为自定义类型创建转换运算符，以控制转换为其他类型是否合理，并可以指定这些转换是隐式的还是显式的。

## 实现自定义转换运算符

声明自定义转换运算符的语法与声明重载运算符的语法有一些相似之处，但也有一些重要的区别。这里有一个允许 `Hour` 对象隐式转换为 `int` 的转换运算符：

```csharp
struct Hour
{
    public static implicit operator int (Hour from)
    {
        return from.value;
    }
    private int value;
}
```

转换运算符必须是公共的，并且必须是静态的。从源转换的类型被声明为参数（此处为 `Hour`），而转换为的目标的类型被声明为 `operator` 关键字之后的类型（此处为 `int`）。在 `operator` 关键字之前没有指定返回类型。

在声明转换运算符时，必须指定它们是隐式转换运算符还是显式转换运算符。你可以通过 `implicit` 和 `explicit` 关键字来实现。上述示例中 `Hour` 到 `int` 的转换运算符是隐式的，这意味着 C# 编译器可以在不需要强制类型转换的情况下使用它。

```csharp
public static void Main()
{
    Hour lunch = new Hour(12);
    Example.MyOtherMethod(lunch); // 隐式 Hour 到 int 的转换
}
```

如果转换运算符使用 *explicit*（显式）声明，那么前面的示例将无法编译，因为显式转换运算符需要强制转换。

点击此处查看代码图像

Example.MyOtherMethod((int)lunch); // 显式 Hour 到 int 的转换

何时应该将转换运算符声明为显式或隐式？如果转换总是安全的、没有丢失信息的风险，并且不会抛出异常，则可以将其定义为*implicit*（隐式）转换。否则，从 Hour 转换为 int 总是安全的——每个 Hour 都有一个对应的 int 值——因此将其设为隐式是合理的。将 *string*（字符串）转换为 *Hour* 的运算符应该是显式的，因为并不是所有的字符串都代表 Hour。（字符串“7”是可以的，但你如何将字符串“Hello, World”转换为 Hour 呢？）

## 重新审视对称运算符

转换运算符为你提供了一种解决提供对称运算符问题的替代方案。例如，与其像之前所示，为 Hour 结构体提供三个版本的 operator+（Hour + Hour、Hour + int 和 int + Hour），你可以提供一个版本的 operator+（接收两个参数）以及一个从 int 到 *Hour* 的隐式转换，如下所示：

点击此处查看代码图像
```csharp
struct Hour
{
    public Hour(int initialValue) => this.value = initialValue;
    public static Hour operator+(Hour lhs, Hour rhs) => new Hour(lhs.value + rhs.value);
    public static implicit operator Hour(int from) => new Hour(from);
    ...
    private int value;
}
```

如果你向一个 int 添加一个 Hour（无论什么种顺序），C# 编译器会自动将 int 转换为 Hour，然后使用两个 Hour 参数调用 operator+，此处所示：

点击此处查看代码图像
```csharp
void Example(Hour a, int b)
{
    Hour eg1 = a + b; // b 转换为 Hour
    Hour eg2 = b + a; // b 转换为 Hour
}
```

## 编写转换运算符

在本章的最后一个练习中，你将为 Complex 类添加一对转换运算符，用于在 int 类型和 Complex 类型之间进行转换。将 int 转换为 Complex 对象始终是一个安全的过程，并且不会丢失信息（因为 int 实际上只是一个没有虚部的复数）。你将将其实现为隐式转换运算符。然而，反之则不然——要将 Complex 对象转换为 int，你必须丢弃虚部。因此，你将此转换运算符实现为显式。

## 实现转换运算符

- 1. 返回到 Visual Studio 2017 并在代码和文本编辑器中显示 Complex.cs 文件。将后续代码中**加粗**所示的构造函数添加到 Complex 类，紧跟在现有构造函数之后、ToString 方法之前。这个新构造函数接收单个 int 参数，并用它初始化 Real 属性。Imaginary 属性被设置为 0。

点击此处查看代码图像
```csharp
class Complex
{
...
    public Complex(int real)
    {
        this.Real = real;
        this.Imaginary = 0;
    }
...
}
```

- 2. 在 Complex 类中添加以下**加粗**所示的隐式转换运算符。

点击此处查看代码图像
```csharp
class Complex
{
...
    public static implicit operator Complex(int from) => new Complex(from);
...
}
```

此运算符将 int 转换为 Complex 对象，返回使用你在上一步中创建的构造函数构建的 Complex 类新实例。

- 3. 在 Complex 类中添加以下**加粗**所示的显式转换运算符。

点击此处查看代码图像
```csharp
class Complex
{
...
    public static explicit operator int(Complex from) => from.Real;
}
```

此运算符接收一个 Complex 对象并返回 Real 属性的值。此转换丢弃了复数的虚部。

- 4. 在代码和文本编辑器窗口中显示 Program.cs 文件。在 doWork 方法末尾添加以下**加粗**所示的代码：

点击此处查看代码图像
```csharp
static void doWork()
{
...
    Console.WriteLine("Current value of temp is ");
    if (temp == 2)
    {
        Console.WriteLine("Comparison after conversion: temp == 2");
    }
    else
    {
        Console.WriteLine("Comparison after conversion: temp != 2");
    }
    temp += 2;
    Console.WriteLine("Value after adding 2: temp = {0}");
}
```

这些语句测试了将 int 转换为 Complex 对象的隐式运算符。if 语句将 Complex 对象与 int 进行比较。编译器生成的代码将 int 先转换为 Complex 对象并调用 Complex 类的 == 运算符。为 temp 变量加 2 的语句将 int 值 2 转换为 Complex 对象，然后使用 Complex 类的 + 运算符。

```csharp
static void doWork()
{
    int tempInt = temp;
    Console.WriteLine("Int value after conversion: tempInt == {0}");
}
```

第一个语句尝试将 Complex 对象赋值给 int 变量。

- 5. 在生成（Build）菜单上，点击重新生成解决方案（Rebuild Solution）。
解决方案生成失败，编译器在错误列表窗口报告以下错误：
[点击查看代码图像]
无法隐式将 'ComplexNumbers.Complex' 转换为 'int'

- 6. 修改将 Complex 对象赋值给 int 变量的语句，使用强制转换：
```csharp
tempInt = (int)temp;
```
