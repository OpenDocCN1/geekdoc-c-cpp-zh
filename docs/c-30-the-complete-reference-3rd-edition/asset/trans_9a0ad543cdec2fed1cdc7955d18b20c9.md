

```
if(a || c) Console.WriteLine("a || c is true.");
```

true 运算符首先应用于 a。由于在这种情况下 a 为 true，因此无需使用 | 运算符方法。然而，如果语句重写为如下形式：

```
if(c || a) Console.WriteLine("c || a is true.");
```

那么 true 运算符将首先应用于 c，而在此情况下 c 为 false。因此，将调用 | 运算符方法来判断 a 是否为 true（在此情况下确实为 true）。

尽管一开始您可能会觉得，启用短路运算符所用的技术有些复杂，但稍微思考一下就会明白它是合理的。通过为类重载 true 和 false，您可以让编译器使用短路运算符，而无需显式重载其中任何一个。此外，您还获得了在条件表达式中使用对象的能力。一般来说，除非您需要非常狭窄地实现 & 和 |，否则最好创建完整的实现。

## 转换运算符

在某些情况下，您会希望在涉及其他数据类型的表达式中使用某个类的对象。有时，重载一个或多个运算符可以提供实现这一目的的手段。然而，在其他情况下，您想要的是从类类型到目标类型的简单类型转换。为了处理这些情况，C# 允许您创建一种特殊类型的运算符方法，称为转换运算符。转换运算符将您的类的对象转换为另一种类型。转换运算符允许类的对象与其他数据类型自由混合（只要定义了到这些其他类型的转换），从而帮助将类类型完全集成到 C# 编程环境中。

转换运算符有两种形式：隐式和显式。每种形式的一般形式如下所示：

```
public static implicit operator target-type(source-type v) { return value; }
public static explicit operator target-type(source-type v) { return value; }
```

这里，target-type 是您要转换到的目标类型；source-type 是您要从中转换的源类型；value 是转换后类的值。转换运算符返回 target-type 类型的数据，并且不允许其他返回类型说明符。

如果转换运算符指定为 implicit，则转换会自动调用，例如当对象与目标类型一起用于表达式时。当转换运算符指定为 explicit 时，转换在使用强制转换时调用。不能为相同的目标类型和源类型同时定义隐式和显式转换运算符。

为了说明转换运算符，我们将为 ThreeD 类创建一个转换运算符。假设您想将 ThreeD 类型的对象转换为整数，以便它可以在整数表达式中使用。此外，转换将通过使用三个维度的乘积来进行。为此，您将使用如下所示的隐式转换运算符：

```
public static implicit operator int(ThreeD op1)
{
    return op1.x * op1.y * op1.z;
}
```

下面是一个说明此转换运算符的程序：

```
// An example that uses an implicit conversion operator.
using System;

// A three-dimensional coordinate class.
class ThreeD {
    int x, y, z; // 3-D coordinates

    public ThreeD() { x = y = z = 0; }
    public ThreeD(int i, int j, int k) { x = i; y = j; z = k; }

    // Overload binary +.
    public static ThreeD operator +(ThreeD op1, ThreeD op2)
    {
        ThreeD result = new ThreeD();

        result.x = op1.x + op2.x;
        result.y = op1.y + op2.y;
        result.z = op1.z + op2.z;

        return result;
    }

    // An implicit conversion from ThreeD to int.
    public static implicit operator int(ThreeD op1)
    {
        return op1.x * op1.y * op1.z;
    }

    // Show X, Y, Z coordinates.
    public void Show()
    {
        Console.WriteLine(x + ", " + y + ", " + z);
    }
}

class ThreeDDemo {
    static void Main() {
        ThreeD a = new ThreeD(1, 2, 3);
        ThreeD b = new ThreeD(10, 10, 10);
        ThreeD c = new ThreeD();
        int i;

        Console.Write("Here is a: ");
        a.Show();
        Console.WriteLine();
        Console.Write("Here is b: ");
        b.Show();
        Console.WriteLine();

        c = a + b; // add a and b together
        Console.Write("Result of a + b: ");
```
```
c.Show();
Console.WriteLine();

i = a; // convert to int
Console.WriteLine("Result of i = a: " + i);
Console.WriteLine();

i = a * 2 - b; // convert to int
Console.WriteLine("result of a * 2 - b: " + i);
}
```

该程序显示以下输出：

```
Here is a: 1, 2, 3

Here is b: 10, 10, 10

Result of a + b: 11, 12, 13

Result of i = a: 6

result of a * 2 - b: -988
```

如程序所示，当 **ThreeD** 对象用于整数表达式（例如 `i = a`）时，转换会应用于该对象。在这种特定情况下，转换返回 *值* 6，即存储在 `a` 中的坐标的乘积。然而，当表达式不需要转换为 `int` 时，不会调用转换运算符。这就是为什么 `c = a + b` *不*会调用 `operator int()`。

请记住，您可以创建不同的转换运算符来满足不同的需求。例如，您可以定义第二个转换运算符，将 **ThreeD** 转换为 **double**。每种转换都会自动且独立地应用。

隐式转换运算符会在以下情况下自动应用：表达式中需要转换时、将对象传递给方法时、赋值时，以及使用到目标类型的显式强制转换时。或者，您可以创建显式转换运算符，它仅在显式强制转换时被调用。显式转换运算符不会自动调用。例如，下面是修改后的前述程序，它使用到 `int` 的显式转换：

```
// Use an explicit conversion.

using System;

// A three-dimensional coordinate class.
class ThreeD {
  int x, y, z; // 3-D coordinates

  public ThreeD() { x = y = z = 0; }
  public ThreeD(int i, int j, int k) { x = i; y = j; z = k; }

  // Overload binary +.
  public static ThreeD operator +(ThreeD op1, ThreeD op2)
  {
```
```
ThreeD result = new ThreeD();

result.x = op1.x + op2.x;
result.y = op1.y + op2.y;
result.z = op1.z + op2.z;

return result;
}

// This is now explicit.
public static explicit operator int(ThreeD op1)
{
    return op1.x * op1.y * op1.z;
}

// Show X, Y, Z coordinates.
public void Show()
{
    Console.WriteLine(x + ", " + y + ", " + z);
}
}

class ThreeDDemo {
    static void Main() {
        ThreeD a = new ThreeD(1, 2, 3);
        ThreeD b = new ThreeD(10, 10, 10);
        ThreeD c = new ThreeD();
        int i;

        Console.Write("Here is a: ");
        a.Show();
        Console.WriteLine();
        Console.Write("Here is b: ");
        b.Show();
        Console.WriteLine();

        c = a + b; // add a and b together
        Console.Write("Result of a + b: ");
        c.Show();
        Console.WriteLine();

        i = (int) a; // explicitly convert to int -- cast required
        Console.WriteLine("Result of i = a: " + i);
        Console.WriteLine();

        i = (int)a * 2 - (int)b; // casts required
        Console.WriteLine("result of a * 2 - b: " + i);

    }
}
```

由于转换运算符现在标记为 explicit，因此转换为 int 时必须显式强制转换。例如，在下面这一行中：

```
i = (int) a; // explicitly convert to int -- cast required
```

如果移除强制转换，程序将无法编译。

转换运算符有一些限制：

- 转换的目标类型或源类型必须是声明该转换的类。例如，您不能重新定义从 double 到 int 的转换。
- 不能定义到 object 或从 object 的转换。
- 不能为相同的源类型和目标类型同时定义隐式转换和显式转换。
- 不能定义从基类到派生类的转换。（有关基类和派生类的讨论，请参见第 11 章。）
- 不能定义到接口或从接口的转换。（有关接口的讨论，请参见第 12 章。）

除了这些规则之外，在选择隐式转换运算符和显式转换运算符时，通常还应遵循一些建议。隐式转换虽然方便，但只应在转换本身不会出错的情况下使用。为确保这一点，只有在满足以下两个条件时才应创建隐式转换：第一，不发生信息丢失，例如截断、溢出或符号丢失。第二，转换不会导致异常。如果转换不能满足这两个要求，则应使用显式转换。

## 运算符重载提示与限制

重载运算符应用于其定义所在的类时，其行为不必与该运算符应用于 C# 内置类型时的默认用法有任何关系。然而，出于代码结构和可读性的考虑，重载运算符应尽可能体现该运算符原始用法的精神。例如，相对于 ThreeD 的 + 在概念上类似于相对于整数类型的 +。例如，以更符合您对 / 运算符预期行为的方式来定义相对于某个类的 + 运算符，几乎没有什么好处。核心概念是：虽然您可以赋予重载运算符任何您喜欢的含义，但为了清晰起见，最好使其新含义与原始含义相关。

重载运算符有一些限制。不能更改任何运算符的优先级。不能更改运算符所需操作数的数量，尽管您的运算符方法可以选择忽略某个操作数。有一些运算符不能重载。也许最重要的是，不能重载任何赋值运算符，包括复合赋值运算符，例如 +=。以下是其他不能重载的运算符。（此列表包括本书后面讨论的几个运算符。）

| && | () | . | ? |
|---|---|---|---|
| ?? | [ ] | || | = |
| => | -> | as | checked |
| default | is | new | sizeof |
| typeof | unchecked |  |  |

