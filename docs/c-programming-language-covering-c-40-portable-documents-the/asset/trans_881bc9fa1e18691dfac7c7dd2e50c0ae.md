
当需要为某个常量值使用符号名称，但该值的类型不允许在常量声明中使用，或者该值无法由常量表达式在编译时计算时，可以改用 readonly 字段（§10.5.2）。

声明多个常量的一个常量声明，等价于多个具有相同特性、修饰符和类型的单常量声明。例如，

```
class A
{
    public const double X = 1.0, Y = 2.0, Z = 3.0;
}
```

等价于

```
class A
{
    public const double X = 1.0;
    public const double Y = 2.0;
    public const double Z = 3.0;
}
```

> **克里斯·塞尔斯** 从可读性的角度来看，我认为在同一行中进行多个声明——无论是常量还是非常量、静态还是实例、字段还是局部变量——都难以解读。我倾向于每行只放一个声明，最好牢记引用的局部性。

只要依赖关系不是循环性质的，常量就允许依赖于同一程序内的其他常量。编译器会自动安排以适当的顺序计算常量声明。在示例

```
class A
{
    public const int X = B.Z + 1;
    public const int Y = 10;
}

class B
{
    public const int Z = A.Y + 1;
}
```

中，编译器首先计算 A.Y，然后计算 B.Z，最后计算 A.X，并按该顺序生成值 10、11 和 12。常量声明可以依赖于其他程序中的常量，但这种依赖只能在一个方向上进行。参考上面的示例，如果 A 和 B 声明在单独的程序中，则 A.X 可以依赖于 B.Z，但 B.Z 就不能同时依赖于 A.Y。

## 10.5 字段

字段是表示与对象或类关联的变量的成员。字段声明引入一个或多个给定类型的字段。

```
field-declaration:
    attributes_opt field-modifiers_opt type variable-declarators ;
```

```
field-modifiers:
    field-modifier
    field-modifiers field-modifier
```

```
field-modifier:
    new
    public
    protected
    internal
    private
    static
    readonly
    volatile
```

```
variable-declarators:
    variable-declarator
    variable-declarators , variable-declarator
```

```
variable-declarator:
    identifier
    identifier = variable-initializer
```

```
variable-initializer:
    expression
    array-initializer
```

字段声明可以包含一组特性（§17）、new 修饰符（§10.3.4）、四个访问修饰符的有效组合（§10.3.5）以及 static 修饰符（§10.5.1）。此外，字段声明可以包含 readonly 修饰符（§10.5.2）或 volatile 修饰符（§10.5.3），但不能同时包含两者。特性和修饰符应用于该字段声明所声明的所有成员。同一修饰符在字段声明中多次出现是错误的。

字段声明的类型指定该声明所引入成员的类型。类型后面是变量声明符列表，其中每个变量声明符引入一个新成员。变量声明符由一个为该成员命名的标识符组成，后面可选地跟一个“=”标记和一个变量初始值设定项（§10.5.5），后者给出该成员的初始值。

字段的类型必须至少与字段本身具有相同的可访问性（§3.5.4）。

在表达式中，字段的值通过简单名称（§7.6.2）或成员访问（§7.6.4）获取。非只读字段的值可以使用赋值（§7.17）修改。非只读字段的值既可以使用后缀递增和递减运算符（§7.6.9）获取和修改，也可以使用前缀递增和递减运算符（§7.7.5）获取和修改。

声明多个字段的一个字段声明，等价于多个具有相同特性、修饰符和类型的单字段声明。例如，

```
class A
{
    public static int X = 1, Y, Z = 100;
}
```

等价于

```
class A
{
    public static int X = 1;
    public static int Y;
    public static int Z = 100;
}
```

### 10.5.1 静态字段和实例字段

当字段声明包含 static 修饰符时，该声明引入的字段是静态字段。当不存在 static 修饰符时，该声明引入的字段是实例字段。静态字段和实例字段是 C# 支持的若干种变量（§5）中的两种。有时它们分别被称为静态变量和实例变量。

静态字段不属于特定实例；相反，它在封闭类型（§4.4.2）的所有实例之间共享。无论创建多少个封闭类类型的实例，对于关联的应用程序域，静态字段始终只有一个副本。

例如：

```
class C<T>
{
    static int count = 0;
    public C() {
        count++;
    }
    public static int Count {
        get { return count; }
    }
}
```

```
class Application
{
    static void Main() {
        C<int> x1 = new C<int>();
        Console.WriteLine(C<int>.Count);        // Prints 1
        C<double> x2 = new C<double>();
        Console.WriteLine(C<int>.Count);        // Prints 1
        C<int> x3 = new C<int>();
        Console.WriteLine(C<int>.Count);        // Prints 2
    }
}
```

实例字段属于实例。具体来说，类的每个实例都包含该类所有实例字段的单独一组。

当在形式为 E.M 的成员访问（§7.6.4）中引用字段时，如果 M 是静态字段，则 E 必须表示包含 M 的类型；如果 M 是实例字段，则 E 必须表示包含 M 的类型的实例。

静态成员和实例成员之间的差异将在 §10.3.7 中进一步讨论。

### 10.5.2 只读字段

当字段声明包含 readonly 修饰符时，该声明引入的字段是只读字段。对只读字段的直接赋值只能作为该声明的一部分，或在同一个类的实例构造函数或静态构造函数中进行。（在这些上下文中，可以对只读字段多次赋值。）具体来说，只允许在以下上下文中对只读字段进行直接赋值：

- 在引入该字段的变量声明符中（通过在声明中包含变量初始值设定项）。
- 对于实例字段，在包含该字段声明的类的实例构造函数中；对于静态字段，在包含该字段声明的类的静态构造函数中。这些也是唯一可以将只读字段作为 out 或 ref 参数传递的有效上下文。

在任何其他上下文中尝试对只读字段赋值或将其作为 out 或 ref 参数传递，都是编译时错误。

> **弗拉基米尔·列舍特尼科夫** 在实例构造函数中，只能对 this 对象的实例只读字段赋值，而不能对同一类型的任何其他对象的字段赋值：

```csharp
class A
{
    readonly int x;

    A(A a)
    {
        this.x = 1;    // Okay
        a.x = 1;       // Error CS0191: A read-only field
                       // cannot be assigned to
    }
}
```

此外，在匿名函数中不能对只读字段赋值（也不能将其作为 ref 或 out 参数传递），即使该函数位于构造函数内。

### 10.5.2.1 使用静态只读字段表示常量

当需要为某个常量值使用符号名称，但该值的类型不允许在 const 声明中使用，或者该值无法在编译时计算时，静态只读字段很有用。在示例

```
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);

    private byte red, green, blue;

    public Color(byte r, byte g, byte b) {
        red = r;
        green = g;
        blue = b;
    }
}
```

中，Black、White、Red、Green 和 Blue 成员不能声明为 const 成员，因为它们的值无法在编译时计算。改为将它们声明为 static readonly 具有大致相同的效果。

### 10.5.2.2 常量和静态只读字段的版本管理

常量和只读字段具有不同的二进制版本管理语义。当表达式引用常量时，常量的值在编译时获取，但当
