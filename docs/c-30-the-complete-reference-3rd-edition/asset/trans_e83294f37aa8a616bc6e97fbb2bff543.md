
## 静态类

从 C# 2.0 开始，你可以声明一个类为静态。静态类有两个关键特性。首先，不能创建静态类的对象。其次，静态类必须只包含静态成员。静态类是通过使用关键字 static 修改类声明创建的，如下所示。

```csharp
static class class-name { // ... }
```

在类内部，所有成员都必须显式指定为 static。使类变为静态并不会自动使其成员变为静态。

静态类主要有两种用途。首先，在创建扩展方法时需要静态类，而扩展方法是 C# 3.0 中添加的新功能。扩展方法主要与 LINQ 相关，扩展方法的讨论见第 19 章。其次，静态类用于包含一组相关的静态方法。这里演示了第二种用法。

以下示例使用名为 NumericFn 的静态类来保存一组对数值进行操作的静态方法。由于 NumericFn 的所有成员都被声明为 static，因此该类也可以声明为 static，从而防止其被实例化。因此，NumericFn 起到组织作用，提供了一种逻辑分组相关方法的好方法。

```csharp
// Demonstrate a static class.

using System;

static class NumericFn {
    // Return the reciprocal of a value.
    static public double Reciprocal(double num) {
        return 1/num;
    }

    // Return the fractional part of a value.
    static public double FracPart(double num) {
        return num - (int) num;
    }

    // Return true if num is even.
    static public bool IsEven(double num) {
        return (num % 2) == 0 ? true : false;
    }

    // Return true if num is odd.
    static public bool IsOdd(double num) {
        return !IsEven(num);
    }
}

class StaticClassDemo {
    static void Main() {
        Console.WriteLine("Reciprocal of 5 is " + 
            NumericFn.Reciprocal(5.0));
    }
}
```

## 运算符重载

C# 允许你为自己创建的类定义运算符的含义。此过程称为运算符重载。通过重载运算符，你可以将其实用范围扩展到你的类。运算符的效果完全由你控制，并且可能因类而异。例如，定义链表的类可能会使用 + 运算符将对象添加到列表中。实现栈的类可能会使用 + 将对象压入栈中。另一个类可能会以完全不同的方式使用 + 运算符。

当运算符被重载时，其原始含义不会丢失。只是相对于特定类添加了一个新的操作。因此，例如将 + 重载以处理链表，并不会改变其相对于整数（即加法）的含义。

运算符重载的主要优点是它允许你将新类类型无缝集成到编程环境中。这种类型可扩展性是 C# 等面向对象语言强大功能的重要组成部分。一旦为类定义了运算符，你就可以使用正常的 C# 表达式语法对该类的对象进行操作。你甚至可以在涉及其他类型数据的表达式中使用对象。运算符重载是 C# 最强大的功能之一。

### 运算符重载基础

运算符重载与方法重载密切相关。要重载运算符，请使用 operator 关键字定义运算符方法，该方法定义运算符相对于其类的行为。

运算符方法有两种形式：一种用于一元运算符，一种用于二元运算符。每种的一般形式如下所示：

```csharp
// General form for overloading a unary operator
public static ret-type operator op(param-type operand)
{
    // operations
}
```

```csharp
// General form for overloading a binary operator
public static ret-type operator op(param-type1 operand1, param-type2 operand2)
{
    // operations
}
```

这里，将你要重载的运算符（如 + 或 /）替换为 op。ret-type 指定指定操作返回的值的类型。虽然它可以是你选择的任何类型，但返回值通常与正在为其重载运算符的类相同。这种关联便于在表达式中使用重载的运算符。对于一元运算符，操作数通过 operand 传入。对于二元运算符，操作数通过 operand1 和 operand2 传入。请注意，运算符方法必须同时是 public 和 static。

对于一元运算符，操作数必须与为其定义运算符的类相同类型。对于二元运算符，至少一个操作数必须与其实类相同类型。因此，你不能为未创建的对象重载任何 C# 运算符。例如，你不能为 int 或 string 重新定义 +。

另外一点：运算符参数不得使用 ref 或 out 修饰符。

### 重载二元运算符

为了了解运算符重载的工作原理，让我们从一个重载两个二元运算符 + 和 - 的示例开始。以下程序创建了一个名为 ThreeD 的类，该类维护三维空间中对象的坐标。重载的 + 将一个 ThreeD 对象的各个坐标加到另一个对象上。重载的 - 将一个对象的坐标从另一个对象中减去。

```csharp
// An example of operator overloading.

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

        /* This adds together the coordinates of the two points
           and returns the result. */
        result.x = op1.x + op2.x; // These are integer additions
        result.y = op1.y + op2.y; // and the + retains its original
        result.z = op1.z + op2.z; // meaning relative to them.

        return result;
    }

    // Overload binary -.
    public static ThreeD operator -(ThreeD op1, ThreeD op2)
    {
        ThreeD result = new ThreeD();

        /* Notice the order of the operands. op1 is the left
           operand and op2 is the right. */
        result.x = op1.x - op2.x; // these are integer subtractions
        result.y = op1.y - op2.y;
        result.z = op1.z - op2.z;

        return result;
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
        ThreeD c;

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

        c = a + b + c; // add a, b, and c together
        Console.Write("Result of a + b + c: ");
        c.Show();
        Console.WriteLine();

        c = c - a; // subtract a
        Console.Write("Result of c - a: ");
        c.Show();
        Console.WriteLine();

        c = c - b; // subtract b
        Console.Write("Result of c - b: ");
        c.Show();
        Console.WriteLine();
    }
}
```

该程序产生以下输出：

```text
Here is a: 1, 2, 3

Here is b: 10, 10, 10

Result of a + b: 11, 12, 13
Result of a + b + c: 22, 24, 26
Result of c - a: 21, 22, 23
Result of c - b: 11, 12, 13
```

让我们仔细检查前面的程序，从重载的运算符 + 开始。当两个 ThreeD 类型的对象由 + 运算符操作时，它们的各自坐标的幅度会被相加，如 operator+() 所示。然而，请注意，此方法不会修改任一操作数的值。相反，由该方法返回一个包含操作结果的 ThreeD 类型的新对象。为了理解为什么 + 操作不会改变任一对象的内容，请考虑像这样应用的标准算术 + 操作：10 + 12。此操作的結果是 22，但 10 和 12 都不会因此而改变。虽然没有规则禁止重载的运算符更改其操作数之一的值，但最好使重载运算符的行为与其通常含义一致。

请注意，operator+() 返回一个 ThreeD 类型的对象。虽然该方法可以返回任何有效的 C# 类型，但它返回 ThreeD 对象这一事实允许 + 运算符在复合表达式中使用，例如 a+b+c。这里，a+b 生成的结果是 ThreeD 类型。此值然后可以加到 c 上。如果 a+b 生成了任何其他类型的值，则此类表达式将无法工作。

这里还有一点很重要：在 operator+() 内部，当坐标相加时，各个坐标的相加结果为整数相加。这是因为各个坐标 x、y 和 z 都是整数量。+ 运算符为 ThreeD 类型对象重载这一事实对 + 运算符应用于整数值没有任何影响。

现在，来看 operator-()。- 运算符的工作方式与 + 运算符完全相同，只是参数的顺序很重要。请记住，加法是可交换的，但减法不是。（也就是说，A - B 不等于 B - A！）对于所有二元运算符，运算符方法的第一个参数将包含左操作数。第二个参数将包含右操作数。在实现非交换运算符的重载版本时，你必须记住哪个操作数在左边，哪个在右边。

### 重载一元运算符

一元运算符的重载方式与二元运算符相同。当然，主要区别在于只有一个操作数。例如，这里有一个为 ThreeD 类重载一元负号的方法：

```csharp
// Overload unary -.
public static ThreeD operator -(ThreeD op)
{
    ThreeD result = new ThreeD();
    result.x = -op.x;
    result.y = -op.y;
    result.z = -op.z;
    return result;
}
```
