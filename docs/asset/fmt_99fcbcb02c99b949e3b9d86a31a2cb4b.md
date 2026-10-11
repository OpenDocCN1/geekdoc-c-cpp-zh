
- 接口必须由结果类型实现，而不是由该部分单独实现。不同的部分可以出不同的基接口。结果类型的基接口列表是各个部分接口的并集（去重）。

- 如果部分声明泛型类型（第 26 节），所有部分必须具有相同的类型参数。所有具有类型约束（第 26.4 节）的部分必须具有相同的约束，顺序任意；这些是泛型类型的类型约束。

- 部分上的属性（第 32 节）适用于整个类型，不仅仅是该部分。结果类型的属性列表是各个部分属性的拼接，顺序任意且可能重复。

# 示例 250 局部类型声明，第一部分

此示例包含接口 `I` 的部分声明和类 `C` 的部分声明，而类 `C` 又包含结构体 `S` 的部分声明。剩余的局部类型声明将在 251 中给出。这两个示例文件必须同时编译，命令如下：

```bash
csc Example250.cs Example251.cs
```

这会创建一个可执行文件 `Example250.exe`，它包含入口点 `Main`。类 `C` 声明的任何单一部分单独都不是一个有效的声明：`C` 的每个部分都使用了在其他部分声明的成员；结构体 `S` 也是如此。

`S` 声明的所有部分都具有相同的访问修饰符（`public`）。虽然类 `C` 只有一个部分具有 `sealed` 修饰符，一个部分具有 `public` 修饰符，但这些修饰符也适用于其他部分，生成的类型 `C` 是一个密封的公共类。同样，尽管类 `C` 只有一部分表示它实现了接口 `I`，但 `C` 的所有部分都对实现 `I` 做出了贡献。

```csharp
partial interface I {
    void M2(C s);
}
sealed partial class C : I {
    public void M1(S s) {
        if (s.x > 0)
            M2(s.Decr());
    }
    public partial struct S {
        public S(int x) { this.x = x; }
    }
    public static void Main() {
        C c = new C();
        c.M1(new S(5));
    }
}
```

# 示例 251 局部类型声明，第二部分

```csharp
partial interface I {
    void M1(C s);
}
public partial class C {
    public partial struct S {
        public int x;
        public S Decr() { x--; return this; }
    }
}
```

```csharp
public void M2(S n) {
    Console.WriteLine("n.x={0}", n.x);
    M1(n);
}
```

# 31 断言与 Debug.Assert 方法

`System.Diagnostics.Debug` 类定义了 `Assert` 方法的几个重载版本：

```csharp
static void Assert(bool chk)
static void Assert(bool chk, String msg)
```

在程序的普通执行下，对 `Assert(expression)` 的调用没有任何影响；参数表达式不会被求值。然而，可以通过在编译时使用选项 `/d:DEBUG` 使用以下命令行之一（第 1.1 节）来启用断言：

```bash
csc /d:DEBUG Prog.cs
mcs -define:DEBUG Prog.cs
```

要在编译单元的部分选择性启用断言，可以在该部分之前插入预处理器指令 `#define DEBUG`，并在之后插入预处理器指令 `#undef DEBUG`。

当启用断言时，调用 `Assert` 将求值参数。如果第一个表达式的结果为真，程序继续正常执行。如果结果为假，则断言失败。这意味着将出现对话框，或者通过 `TraceListener` 记录消息，或者启动 `CLR` 调试器；在任何情况下，都会给出一个关于错误的提示消息。如果存在字符串表达式，消息将包含该表达式的结果。这简化了故障程序的故障排除工作。

断言失败应该表示程序中某个基本假设的失败。

`Assert` 可以起到两个作用：记录程序员对程序某点状态的假设，以及在运行时检查该假设是否成立（前提是程序在编译时启用了断言）。

- 可以在特别复杂的代码之后放置一个 `Assert`，以检查它是否实现了预期的功能（示例 252）。

- 在具有数据表示不变性的类中，可以在该类的每个方法的结束处对该不变性进行断言（示例 253）。

- 不应使用 `Assert` 调用来检查用户输入、公共方法或构造函数的有效性，因为该检查只有在编译时启用了断言时才会执行。相反，请使用 `if` 语句并在发生错误时抛出异常。

# 断言与 Debug.Assert 方法 215

示例 252 使用 `Assert` 指定并检查算法结果

`x ≥ 0` 的整数平方根是一个整数 `y`，满足 `y ≤ x` 且 `(y+1) > x`。先决条件 `x ≥ 0` 始终通过语句进行检查。对 `y` 的后置条件通过调用 `Assert` 指定，并在运行时启用了断言时会进行检查，这令人感到放心，因为算法的正确性绝不是显而易见的。该断言使用了调用来避免算术溢出。

```csharp
static int Sqrt(int x) { // 算法来自 Borgerding, Hsieh
  if (x < 0)
    throw new ArgumentOutOfRangeException("Sqrt: negative argument");
  int temp, y = 0, b = 0x8000, bshift = 15, v = x;
  do {
    if (v >= (y << bshift))
      y += b; v -= bshift;
  } while ((b >>= 1) > 0);
  Debug.Assert((long)y <= x && (long)(y+1) > x);
  return y;
}
```

示例 253 使用 `Assert` 指定并检查不变性

单词列表将被格式化为一行文本。其长度是格式化单词和间所需的所需的字符数，即单词长度加上单词数减 1。

```csharp
class WordList {
    private Queue<string> words = new Queue<string>();
    private int length = 0;

    public string Next() {
        if (words.Count == 0) return null;
        string s = words.Dequeue();
        length -= s.Length + 1;
        return s;
    }

    public void Add(string s) {
        words.Enqueue(s);
        length += s.Length + 1;
        Debug.Assert(length >= 0);
    }

    public void CheckInvariant() {
        // 不变性是列表长度为负数。
        Debug.Assert(length >= 0);
    }
}
```

# 属性 217

## 示例 254 使用序列化属性

`SC` 和 `SO` 类具有 `Serializable` 属性，因此可以被序列化和反序列化。

`SO` 类的字段 `s` 具有 `NonSerialized` 属性，因此不会与类的其他字段一起被序列化和反序列化。此示例使用了命名空间 `System.Runtime.Serialization` 和 `System.Runtime.Serialization.Formatters.Soap` 或 `System.Runtime.Serialization.Formatters.Binary`。

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

`C#` 类似于 `Java` 编程语言，但具有许多额外特性：

- 所有成员的名称必须是唯一的：方法和字段不能具有相同的名称。

- 矩形 `C` 风格多维数组，以及 `Java` 风格的数组数组（第 9.2 节）。

- 看起来像虚实例方法的非虚方法调用（第 10.7 节）。

- 属性（`Properties`）：看起来像字段访问和赋值的 `get-set` 方法调用（第 10.15 节）。

- 索引器（`Indexers`）：看起来像数组索引的 `get-set` 方法调用（第 10.16 节）。

- 大多数运算符可以重载，就像 `C++` 语言（第 10.17 节）。

- 用户定义的自定义类型的隐式和显式转换（第 10.18 节）。

- 像 `Pascal`、`Ada` 和 `C++` 那样的方法按引用传递（第 12.17.2 节）。

- 用于方便定义枚举枚举的 `yield`，在 `Java` 中称为迭代器（第 13.12 节）。

- 用户定义的值类型，最著名的结构体（`structs`）（第 14 节）。值位于评估栈中或在对象或其他另一个结构体内联，与对象不同，对象存储在堆中的独立实体中（第 5.1, 14 和 16 节）。

- 可空类型（`Nullable types`）：对缺失值的统一处理，也适用于值类型（第 19 节）。

- 委托（`Delegates`）：作为值的方法，也称为闭包（第 17 节）。

- 匿名方法（第 12.22 节）和 `lambda` 表达式（第 12.23 节）。

- 与 `Java` 不同，泛型和方法中的类型参数可以使用简单类型实例化。这避免了装箱和拆箱的时间空间开销，并允许精确的运行时类型和类型安全的数组赋值。

- 与 `Java` 包不同，命名空间（`namespaces`）不考虑源文件组织问题（第 29 节）。

- 使用不安全代码、指针等的可能性。这在常规编程中是不被鼓励的。

- 与 `Java` 不同，在另一个类或结构体内声明的类是静态成员类。没有内部类（非静态成员类）或本地匿名类（方法内部）。

- 与 `Java` 不同，没有方法声明或限制方法可以的内容。

- 与 `Java` 不同，没有方法声明本地变量或参数为只读。

- `C#` 有条件编译指令，如 `#define` 和 `#if`（本书中未描述）。

- 可选方法参数（第 10.10 节）和命名方法参数（第 12.17.6 节）。

- 对象初始化器（第 12.10 节）和集合初始化器（第 12.11 节）。

- 使用 `var` 关键字对局部变量进行编译时类型推断（第 6.3 节）。

- 使用 `dynamic` 类型解析方法调用和重载（第 6 和 18 节）。

- 匿名对象表达式（第 12.24 节）。

- 泛型接口和委托类型上的变体声明（第 26.12 节）。

- 扩展方法（第 10.9 节）。

- 用于可枚举、数据库等的语言集成查询 (`Linq`) 运算符（第 28 节）。

## 示例 256 Java 中不具备的 C# 特性

此示例使用泛型 `LinkedList<T>`（示例 200）来突出一些非 `Java` 特性：属性、索引器、`yield` 关键字、显式接口实现、泛型上的精确运行时类型、显式转换、重载运算符 (`+`)、委托参数的方法，以及编译时类型推断 (`var`)。

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

与 `Java` 的某些区别：集合初始化器 (1)、属性和索引器 (2,3)、显式转换 (4)、重载运算符 (5)、委托 (6)、`lambda` 表达式 (7) 以及动态 类型 (9)：

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

- `C# 4.0` 编程语言由 `Anders Heielsberg`, `Mads Torgensen`, `Scott Wollamuth`, `Peter Golde` 在《The C# Programming Language, 4th ed. Addison-Wesley, 2010》中详细描述。`ISBN 978-032174179`。
