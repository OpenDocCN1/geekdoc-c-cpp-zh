
Positional arguments passed to constructor:

Type=`System.Boolean`, Value=`True`

Named arguments set after construction: None

```
```

`System.STAThread`

Constructor called=`Void .ctor()`

Positional arguments passed to constructor:

Named arguments set after construction: None

```
Attributes applied to : None
```

## 属性类

随着时间的推移，对属性进行定义、应用和反射变得越来越容易。例如，在设计数据库时，可以定义列的数据类型为 32 位整数，映射到 Framework 中的 `Int32`。但数据库中的列可以指示该值是可空的。也就是说，行中没有值是允许的。使用 .NET Framework 处理数据库数据可能非常困难，因为在通用语言运行时 `CLR` 中，没有方法可以将 `Int32` 表示为空。为了解决这个问题，`CLR` 引入了可空值类型的概念。这是一个例子：

```csharp

using System;

using System.Diagnostics;

[Conditional("TEST")]

[Conditional("VERIFY")]

public sealed class Attribute {

    // ...

}

```

```csharp

[Serializable, StructLayout(LayoutKind.Sequential)]

public struct Nullable<T> where T : struct {

    // 两个 个字段表示状态

    private Boolean hasValue = false; // 假设为空

    internal T value = default(T); // 假设全为零

}

```

## 第 19 节 可空值类型

| 本节内容： |
| :--- |
| C# 对可空值类型的支持 | 459 |
| C# 的空合并运算符 | 462 |
| CLR 对可空值类型的特殊支持 | 463 |

如你所知，值类型的变量永远不会为 null；它始终包含值本身。事实上，在某些场景下，这是一个问题。例如，在设计数据库时，列可以指示该值是可空的。为了改进这一点，Microsoft 为 `CLR` 引入了空类型。

> 注意：`ADO.NET` 的表适配器不支持可空类型。遗憾的是，`System.Data.SqlTypes` 命名空间中的类型没有被可空类型取代，部分原因是类型之间没有一一对应的关系。例如，`SqlDecimal` 类型最多可达 38 位，而 `Decimal` 类型只能达到 29 位。此外，`SqlString` 类型支持它自己的本地化和比较选项，而普通的 `String` 类型则不支持这些选项。

这是另一个例子：在 Java 中，`java.util.Date` 类是一个引用类型，因此，该类型的变量可以设置为 null。然而，在 `CLR` 中，`System.DateTime` 是一个值类型，`DateTime` 变量可以为 null。

```csharp

public Nullable(T value) {

    this.value = value;

    this.hasValue = true;

}

```

```csharp

public Boolean HasValue { get { return returnValue; } }

```

```csharp

public T Value {

    get {

        if (!HasValue) {

            throw new InvalidOperationException(

                "Nullable object must have a value.");

        }

        return value;

    }

}

```

```csharp

public T GetValueOrDefault() { return value; }

```

```csharp

public T GetValueOrDefault(T defaultValue) {

    if (!HasValue) return defaultValue;

    return value;

}

```

```csharp

public override bool Equals(Object other) {

    if (!HasValue) return (other == null);

    if (other == null) return false;

    return value.Equals(other);

}

```

```csharp

public override int GetHashCode() {

    if (!HasValue) return 0;

    return value.GetHashCode();

}

```

```csharp

public override string ToString() {

    if (!HasValue) return "";

    return value.ToString();

}

```

```csharp

public static implicit operator Nullable<T>(T value) {

    return new Nullable<T>(value);

}

```

```csharp

public static explicit operator T(Nullable<T> value) {

    return value.Value;

}

```

如你所见，此类封装了可以为空的值类型概念。由于 `Nullable<T>` 本身是一个值类型，因此它的实例仍然相当轻量。也就是说，实例仍然可以位于栈上，且实例的大小等于原始值类型加上一个字段。注意，`Nullable` 的类型参数 `T` 被限制为 `struct`。这是因为引用类型变量已经可以为 null了。

# 第 19 章 可空值类型

现在，如果你想在代码中使用可空的 `Int32`，你可以写出类似下面的代码：
```csharp

Nullable<Int32> x = 5;

Nullable<Int32> y = null;

Console.WriteLine("x: HasValue={0}, Value={1}", x.HasValue, x.Value);

Console.WriteLine("y: HasValue={0}, Value={1}", y.HasValue, y.GetValueOrOrDefault());

```

当我编译并运行这段代码时，我得到了以下输出：

```
x: HasValue=True, Value=5
y: HasValue=False, Value=0
```

## C# 对可空值类型的支持

注意代码，C# 允许使用非常简单的语法来初始化两个 `Nullable<Int32>` 变量 `x` 和 `y`。事实上，C# 团队希望将可空值类型集成到 C# 语言中，使其成为一级公民。为此，C# 提供了（可以说是）更简洁的语法来处理可空值类型。C# 允许使用问号标记来编写初始化 `x` 和 `y` 变量的代码：

```csharp

Int32? x = 5;

Int32? y = null;

```

在 C# 中，`Int32` 是 `Nullable<Int32>` 的别名符号。但 C# 更进一步。C# 允许你对可空实例进行转换和强制类型转换。C# 还支持对可空实例应用运算符。以下代码展示了这些示例：

```csharp

private static void ConversionsAndCasting() {

    // 从不可空的 Int32 到 Nullable<Int32> 的隐式转换

    Int32? a = 5;

    // 从 'null' 到 Nullable<Int32> 的隐式转换

    Int32? b = null;

    // 从 Nullable<Int32> 到不可空 Int32 的显式转换

    Int32 c = (Int32) a;

    // 在可空原始类型之间进行强制类型转换

    Double? d = 5; // Int32->Double() (d 是 5.0 的 double)

    Double? e = b; // Int32->Double() (e 是 null)

}

```

C# 还允许对可空实例使用运算符。以下代码展示了这些示例：

```csharp

private static void Operators() {

    Int32? a = 5;

    Int32? b = null;

    // 一元运算符 (+ + - ! ~)

    a++; // // a = 6

    b = -b; // // b = null

    // 二元运算符 (+ - / % & ^ << >>)

    a = a + 3; // a = 9

    b = b * 3; // b = null;

    // 等于运算符 (== !=)

    if (a == null) { /* 无 * */ } else { /* 是 / */ }

    if (b == null) { /* 是 * */ } else { /* 无 / */ }

    if (a != b) { /* 是 * */ } else { /* 无 / */ }

    // 比较运算符 (< <= >= >)

    if (a < b) { /* 无 * */ } else { /* 是 / */ }

}

```

以下是 C# 如何解释运算符：`+, -, !, ~`。如果操作数为 null，结果则为 **null**。

- **二元运算符 (+, -, *, /, &, ^, << >>)** 如果任一操作数为 **null**，结果即为 **null**。然而，当 `&` 或 `|` 运算符为 **Boolean?** 时会有例外，这样这两个运算符的行为就与 SQL 的三值逻辑一致。对于这些运算符，如果两个操作数都不是 null，运算符按预期执行；如果两个操作数均为 null，结果则为 null。下表列出了这些运算符在 **true**、**false** 和 **null** 所有组合下的结果：

| 操作数1 \ 操作数2 | true | false | null |
| :--- | :--- | :--- | :--- |
| true | false | null |
| false | false | null |
| null | null | null |

- **等于运算符 (==, !=)** 如果两个操作数均为 null，则它们相等。否则比较它们的值。

- **关系运算符 (<, >, >=)** 如果任一操作数为 null，结果即为 **false**。如果两个操作数都不是 null，处理可空实例会生成大量代码。请看以下方法：

```csharp

private static Nullable<Int32> NullableSize(Int32 a, Int32 b) {

  return a + b

```

当我编译这个方法时，存在大量的中间语言 `IL` 代码，这使得对可空类型的操作比对不可空类型慢。以下是编译器生成的 IL 的 C# 等效代码：

```csharp

private static Nullable<Int32> nullableSize(Nullable<Int32> a, Nullable<Int32> b) {

    Nullable<Int32> nullable1 = a;

    Nullable<Int32> nullable2 = b;

    if (!nullable1.HasValue || !nullable2.HasValue) {

        return new Nullable<Int32>();

    }

    return new Nullable<Int32>(nullable1.GetValueOrDefault() + nullable2.GetValueOrDefault());

}

```

最后，让我指出你可以定义重载上述运算符的自定义类型。我在第 8 章的“运算符”部分讨论过这一点。如果你使用自定义类型的可空实例，编译器会调用你重载的运算符。例如，假设有一个重载了 `==` 和 `!=` 运算符的 Point 类型：

```csharp

using System;

internal struct Point {

    private Int32 m_x, m_y;

    public Point(Int32 x, Int32 y) { m_x = x; m_y = y; }

    public static Boolean operator ==(Point p1, Point p2) {

        return (p1.m_x == p2.m_x) && (p1.m_y == p2.m_y);

    }

    public static Boolean operator !=(Point p1, Point p2) {

        return !(p1 == p2);

    }

}

```

此时，你可以使用 Point 类型的可空实例：

```csharp

internal static class Program {

    public static void Main() {

        Point p1 = new Point(1, 1);

        Point p2 = new Point(2, 2);

        Console.WriteLine("Are points equal? " + (p1 == p2).ToString());

        Console.WriteLine("Are points not equal? " + (p1 != p2).ToString());

    }

}

```

当我构建并运行上述代码时，得到了如下输出：

Are points equal? False
Are points not equal? True

## C# 的合并运算符

C# 有一个称为合并运算符 `??`，接收两个操作数。如果左侧的操作数不是 null，则返回该操作数的值。如果左侧的操作数为 null，则返回右侧操作数的值。合并运算符提供了一种设置变量默认值的非常方便的方法。

合并运算符的一个酷特性是它既可以用于引用类型，也可以用于可空类型。以下是使用合并运算符的代码：

```csharp

private static void NullCoalescingOperator() {

    Int32 b = null;

    // 下面行等于：

    // x = (b.HasValue) ? b.Value : 123

    Int32 x = b ?? 123;

    Console.WriteLine(x); // "123"

    // 下面行等于：

    // String temp = GetFileName();

    // filename = (temp != null) ? temp : "Untitled";

    String filename = GetFileName() ?? "Untitled";

}

```

有些人认为合并运算符仅仅是 `?:` 运算符的语法糖，C# 编译器不应该在语言中添加这个运算符。然而，合并运算符提供了两个重要的语法改进。第一是 `??` 运算符在表达式中工作得更好：

```csharp

Func<String> f = () => SomeMethod() ?? "Untitled";

```

这段代码比下面这一行更容易阅读和理解，后者需要变量赋值和多个语句：

```csharp

Func<String> f = () => {

    var temp = SomeMethod();

    return temp != null ? temp : "Untitled";

}

```

第二个改进是 `??` 在组合场景下工作得更好。例如，单行代码

```csharp

String s = SomeMethod1() ?? SomeMethod2() ?? "Untitled"

```

比这段代码块更容易阅读和理解：

```csharp

String s;

var sm1 = SomeMethod1();

if (sm1 != null) s = sm1;

else {

    var sm2 = SomeMethod2();

    if (sm2 != null) s = sm2;

    else s = "Untitled"

}
```
