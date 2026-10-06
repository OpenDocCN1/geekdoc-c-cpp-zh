

# 示例 57 System.DateTime 上的周数

当此扩展方法的声明在作用范围内时，可以通过调用 `dt.IsoWeek()` 从 System.DateTime 结构体 `dt` 获取 ISO 周数。

```csharp
public static class DateTimeExtensions {
    public static int IsoWeek(this DateTime dt) { }
}
```

# 示例 58 使用扩展方法拼接字符串

扩展方法可以添加到特定的数组类型（如 `String[]`）或泛型类型的特定实例。如果 `ss` 的类型为 `String[]`，则可以通过 `ss.Concat(", ")` 将数组元素格式化为逗号分隔的值。

```csharp
public static class StringArrayExtensions {
    public static StringBuilder Concat(this[] arr, string sep) {
        StringBuilder sb = new StringBuilder();
        if (arr.Length > 0) {
            sb.Append(arr[0]);
            for (int i = 1; i < arr.Length; i++) {
                sb.Append(sep).Append(arr[i]);
            }
        }
        return sb.ToString();
    }
}
```

# 示例 59 带类型约束的扩展方法

扩展方法可以添加到泛型类型的特定实例上，并受类型约束的限制。此扩展方法只能对实现了 `IComparable<T>` 的类型实例 `IEnumerable<T>` 调用，例如 `IEnumerable<int>`、`IList<int>`、`int[]` 或 `List<String>`。

```csharp
public static bool IsSorted<T>(this IEnumerable<T> xs) where T : IComparable<T> {
    var etor = xs.GetEnumerator();
    if (etor.MoveNext()) {
        T prev = etor.Current;
        while (etor.MoveNext()) {
            if (prev.CompareTo(etor.Current) > 0)
                return false;
            } else {
                prev = etor.Current;
            }
        }
    }
    return true;
}
```

# 示例 60 可选参数

由于 `Convert` 方法参数 `radix` 提供了默认值，因此调用 `Convert("123")` 的含义与 `Convert("123", 10)` 相同。

```csharp
static uint Convert(String s, uint radix = 10) { ... }
```

# 10.11 构造函数声明

类 `C` 中的实例构造函数的目的是初始化该类的一个新对象（实例）。类 `C` 中的构造函数声明具有如下形式：

```
constructor-modifier (formal-list)
constructor-body
```

`constructor-modifier` 是成员访问修饰符之一（第 10.3 节），`formal-list` 的形式同方法（第 10.7 节）。构造函数不能是抽象的（abstract）或密封的（sealed）。对于静态构造函数，请参见 10.12。构造函数没有返回值。

实例构造函数可以以与方法相同的方式进行重载：构造函数签名（`formal-list` 中的参数列表）用于区分同类中的构造函数。构造函数可以使用以下语法调用同类中的另一个重载构造函数：

```
constructor-modifier (formal-list) : this(actual-list)
constructor-body
```

但构造函数不能直接或间接地自调用自己。`actual-list` 中的参数表达式是静态代码，不能使用对象引用 `this` 或类 `C` 的任何实例成员，但可以使用 `formal-list` 中的参数。

`constructor-body` 是一个语句块（第 13.2 节），可以包含带有变量声明的语句。`constructor-body` 可以包含 `return` 语句，但任何 `return` 语句不能接受参数表达式。

未显式声明构造函数的类会隐式声明一个公共默认构造函数，其唯一操作是调用基类构造函数（第 10.4 节）：

```csharp
public C() : base() {
```

当 `new` 在计算机存储器中创建一个新对象时（第 12.9 节），会调用构造函数来初始化类的字段。对象的实例字段的首次初始化器将按照它们在类声明中出现的顺序执行执行。然后，会调用同类中的构造函数 `this(...)` 或基类构造函数 `base(...)`（显式或隐式地；参见示例 62 和 98）。最后，执行构造函数的体（示例 63）。

对基类构造函数的调用将导致其基类中构造函数的调用，并执行其实例初始化器，依此类推，直到构造函数 `Object()`。

# 10.12 静态字段初始化与静态构造函数

对象的静态字段可以通过静态字段初始化器（第 10.5 节）或无参数的静态构造函数进行初始化，声明如下：

```
static C()
block-statement
```

参见示例 56。当类加载时，所有的静态初始化器都会按照它们在类声明中出现的顺序执行。然后执行静态构造函数的体（如果有）。如果执行静态字段初始化器或静态构造函数抛出异常（第 20 节），则会抛出 `TypeInitializationException`，且类不会加载。

# 类 49

示例 61 构造函数重载：调用另一个构造函数
向 `Point` 类（示例 43）中添加新的构造函数会重载其构造函数。旧的构造函数签名是 `Point(int, int)`，新的签名为 `Point()` 和 `Point(Point)`。后者通过使用 `: this(p.x, p.y)` 语法调用旧构造函数来创建点 `p` 的副本。

```csharp
public class Point {
    protected internal int x, y;
    public Point(int x, int y) { }
    public Point() : this(0, 0) { }
    public Point(Point p) : this(p.x, p.y) { }
}
```
（注：上述代码的 OCR 文本存在碎片；已根据标准 C# 模式和提供的上下文重新调整了逻辑）

示例 63 初始化器与构造函数体的执行顺序
评估 `new C()` 将执行类 `C` 中的实例初始化器、执行类 `B` 中的实例初始化器、执行 `B()` 构造函数的体、执行 `C(int)` 构造函数的体，最后执行 `C()` 的体。这意味着它将打印 1 2 3 4 5 6 7。

```csharp
class B {
    public readonly int fb1 = Print(3);
    public B(int k) { Print(5); }
    public readonly int fb2 = Print(4);
    public static int Print(int i) { Console.Write(i + " "); return i; }
}

class C : B {
    public readonly int fc1 = Print(1);
    public C() : this(0) { Print(7); }
    public C(int k) : base(k) { Print(6); }
    public readonly int fc2 = Print(2);
}
```

# 10.13 成员类或嵌套类

嵌套类声明在另一个类或结构体内部。嵌套类的代码可以引用闭包类或结构体的所有静态成员（即使是私有的），但无法通过对闭包类或结构体的实例来引用其成员。与 Java 不同，C# 没有内部类（inner class）的概念，其实例不会包含对闭包类实例的引用。

嵌套类中的成员表示声明该名称的最内层闭包类的成员。也就是说，如果类 `C` 有基类 `B` 并嵌套在类 `E` 中，那么 `C` 中的名称解析将优先考虑 `C` 声明的成员或继承自基类 `B` 的非私有成员，而不是闭包类 `E` 的成员（示例 90）。

嵌套类可以有静态成员，也可以有实例成员。

# 10.14 类访问修饰符

类修饰符（第 10.1 节）可以包含访问修饰符来控制类的访问性。对于声明在编译单元顶层或命名空间顶层（第 29 节）的类，访问修饰符可以是 `public` 或省略（意味着 `internal`）。公共顶层类在所有程序集中均可见；内部顶层类仅在其所属的程序集（第 1.1 节）可见。

对于声明在类或结构体内部的类，访问修饰符可以是成员访问修饰符之一（第 10.3 节）。

