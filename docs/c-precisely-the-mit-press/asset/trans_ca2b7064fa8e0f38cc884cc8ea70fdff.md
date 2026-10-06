

# 属性 217

## 示例 254 使用序列化属性
SC 和 SO 类具有 `Serializable` 属性，因此可以被序列化和反序列化。
SO 类的字段 s 具有 `NonSerialized` 属性，因此不会与类的其他字段一起被序列化和反序列化。此示例使用了命名空间 `System.Runtime.Serialization` 和 `System.Runtime.Serialization.Formatters.Soap` 或 `System.Runtime.Serialization.Formatters.Binary`。

```csharp
[Serializable()]
class SC {
    public int ci;
}
[Serializable()]
class SO {
    public int i;
    public SC c;
    [NonSerialized()] public String s;
    public SO(int i, SC c) { this.i = i; this.c = c; s = i.ToString(); }
}

Formatter fmtr = new SoapFormatter(); // 或 new BinaryFormatter();
// 将 o1 和 o2 序列化到文件 "objects"
sc = new SC();
so1 = new SO(1, sc), o2 = new SO(2, c);
Stream stream = File.Open("Objects", FileMode.Create);
fmtr.Serialize(stream, o1);
// 从文件反序列化 o1 和 o2；c 的共享性丢失了
stream = File.Open("Objects", FileMode.Open);
so1 = (SO)fmtr.Deserialize(stream), o2 = (SO)fmtr.Deserialize(stream);
```

## 示例 255 声明和使用自定义属性
`AuthorAttribute` 是一个自定义属性，包含作者名称和月份（`Month` 类型：参见示例 15）。它的合法目标是类和方法，并且可以在每个目标上多次使用。

```csharp
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, AllowMultiple = true)]
class AuthorAttribute : Attribute {
    public readonly String Name;
    public readonly Month Month;
    public AuthorAttribute(String name, Month month) { }
    public override String ToString() { }
}
class TestAttributes {
    [Author("Donald", Month.May)]
    public void MyMethod1() { }

    [Author("Andrzej", Month.Jul)]
    [Author("Andreas", Month.Mar)]
    public void MyMethod2() { }
}

```

* 注意

# 33 C# 与 Java 的 33 区别

C# 类似于 Java 编程语言，但具有许多额外特性：

- 所有成员的名称必须是唯一的：方法和字段不能具有相同的名称。
- 矩形 C 风格多维数组，以及 Java 风格的数组数组（第 9.2 节）。
- 看起来像虚实例方法的非虚方法调用（第 10.7 节）。
- 属性（Properties）：看起来像字段访问和赋值的 get-set 方法调用（第 10.15 节）。
- 索引器（Indexers）：看起来像数组索引的 get-set 方法调用（第 10.16 节）。
- 大多数运算符可以重载，就像 C++ 语言（第 10.17 节）。
- 用户定义的自定义类型的隐式和显式转换（第 10.18 节）。
- 像 Pascal、Ada 和 C++ 那样的方法按引用传递（第 12.17.2 节）。
- 用于方便定义枚举枚举的 `yield`，在 Java 中称为迭代器（第 13.12 节）。
- 用户定义的值类型，最著名的结构体（structs）（第 14 节）。值位于评估栈中或在对象或其他另一个结构体内联，与对象不同，对象存储在堆中的独立实体中（第 5.1, 14 和 16 节）。
- 可空类型（Nullable types）：对缺失值的统一处理，也适用于值类型（第 19 节）。
- 委托（Delegates）：作为值的方法，也称为闭包（第 17 节）。
- 匿名方法（第 12.22 节）和 lambda 表达式（第 12.23 节）。
- 与 Java 不同，泛型和方法中的类型参数可以使用简单类型实例化。这避免了装箱和拆箱的时间空间开销，并允许精确的运行时类型和类型安全的数组赋值。
- 与 Java 包不同，命名空间（namespaces）不考虑源文件组织问题（第 29 节）。
- 使用不安全代码、指针等的可能性。这在常规编程中是不被鼓励的。
- 与 Java 不同，在另一个类或结构体内声明的类是静态成员类。没有内部类（非静态成员类）或本地匿名类（方法内部）。
- 与 Java 不同，没有方法声明或限制方法可以的内容。
- 与 Java 不同，没有方法声明本地变量或参数为只读。
- C# 有条件编译指令，如 `#define` 和 `#if`（本书中未描述）。
- 可选方法参数（第 10.10 节）和命名方法参数（第 12.17.6 节）。
- 对象初始化器（第 12.10 节）和集合初始化器（第 12.11 节）。
- 使用 `var` 关键字对局部变量进行编译时类型推断（第 6.3 节）。
- 使用 `dynamic` 类型解析方法调用和重载（第 6 和 18 节）。
- 匿名对象表达式（第 12.24 节）。
- 泛型接口和委托类型上的变体声明（第 26.12 节）。
- 扩展方法（第 10.9 节）。
- 用于可枚举、数据库等的语言集成查询 (Linq) 运算符（第 28 节）。

## 示例 256 Java 中不具备的 C# 特性
此示例使用泛型 `LinkedList<T>`（示例 200）来突出一些非 Java 特性：属性、索引器、`yield` 关键字、显式接口实现、泛型上的精确运行时类型、显式转换、重载运算符 (`+`)、委托参数的方法，以及编译时类型推断 (`var`)。

```csharp
public class LinkedList<T> : IEnumerable<T> {
    public int Count { get; set; }
    public T this[int i] {
        get { return item; }
        set { item = value; }
    }
    public void Add(T item) { ... }
    public IEnumerator<T> GetEnumerator() {
        for (Node curr=first; curr!=null; curr=curr.next)
            yield return curr;
    }

    IEnumerator GetEnumerator() { ... }
    public override bool Equals(object obj) {
        return this as LinkedList<T>;
    }
    public bool Equals(LinkedList<T> other) { ... }
    public static LinkedList<T> operator +(LinkedList<T> arr, LinkedList<T> xs2) { ... }
    public LinkedList<D> Map(Func<T, D> f) {
        var res = new LinkedList<D>();
    }
    public void Apply(Action<T> act) { ... }
    public static LinkedList<T> Tabulate(Func<int, T> f, int from, int to) { ... }
}
```

与 Java 的某些区别：集合初始化器 (1)、属性和索引器 (2,3)、显式转换 (4)、重载运算符 (5)、委托 (6)、lambda 表达式 (7) 以及动态 类型 (9)：

```csharp
LinkedList<int> xs = new LinkedList<int>(0, 2, 4, 6, 8);
Console.WriteLine(xs.Count + " " + xs[2]);
int xs2 = 10;
LinkedList<int> ys = new LinkedList<int>(new int[]{1, 2, 3, 4, 5});
LinkedList<int> zs = xs + ys;
zs.Apply((int x) => Console.WriteLine(x + " " + x));
var vs = LinkedList<double>Tabulate(x => 1.0, 1, 5);
foreach (var g in zs) select new {(1): (2), g.Key+10, g.Count};
LinkedList<dynamic> ds = new LinkedList<dynamic>();
ds.Add(5); ds.Add(0.25); ds.Add("true"); ds.Add("foo");
double d = ds[1];
Console.WriteLine(ds[2] ? ds[3].Length : false);
```

# 34 资源

- C# 4.0 编程语言由 Anders Heielsberg, Mads Torgensen, Scott Wollamuth, Peter Golde 在《The C# Programming Language, 4th ed. Addison-Wesley, 2010》中详细描述。ISBN 978-032174179。
- C# 2.0 编程语言包括泛型类型和方法、匿名方法、可空类型等，由 Ecma International 于 2006 年 6 月标准化。在编写本文时，C# 3.0 或 C# 4.0 尚未标准化。可以下载采用 Ecma 标准 ECMA-334 第 4 版的《C# (2.0) 语言规范》。
- Microsoft .Net Framework 可从 http://msdn.microsoft.com/framework/ 获取。
- 用于 C# 及其他许多语言的 Visual Studio 开发环境可以在 http://msdn.microsoft.com/studio/ 购买。
- 用于 C# 的 Microsoft Visual 环境适用于许多项目，可以在 http://msdn.microsoft.com/express/ 免费获取。
- Microsoft .Net Framework 类参考文档可以在 http://msdn.microsoft.com/library/ 获取。
- 第 23 节对异步编程的描述基于 Mads Torgensen 的《Asynchronous Functions in C#》和《Asynchronous Programming in C# and Visual Basic》，均于 2010 年出版；以及 Microsoft 在 2010 年 11 月发布的异步 CTP 软件。
- Unicode 编码 (<http://www.unicode.org>) 对应通用字符集 (UCS)，它是国际标准 ISO 10646-1:2000。UTF-8 是 UCS 的变长编码，其中 7 位 ASCII 字符被编码为它们。它在上述标准的附录 R 中描述。
- 浮点运算由 ANSI/IEEE 二进制浮点运算标准 (IEEE Std 754-2008) 描述。http://en.wikipedia.org/wiki/IEEE_754-2008 有描述。
- C# 的集合类库由 C5 库提供，可在 http://www.itu.dk/research/c5/ 根据宽松许可获取。
- 示例 252 中的整数平方根算法源于 Mark Borgerding, Paul Hsieh 和 Jim Ulery，见 http://www.azillionmonkeys.com/qsd/sqroot.html。

