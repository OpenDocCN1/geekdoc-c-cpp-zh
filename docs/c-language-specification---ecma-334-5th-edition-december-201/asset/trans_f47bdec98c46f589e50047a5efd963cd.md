
All the formal parameter types of a delegate type shall be input-safe. In addition, any out or ref parameter types shall also be output-safe. [Note: 即使是 out 参数也要求是输入安全的，这是由于常见的实现限制。end note]

C# 中的委托类型按名称等价，而不是按结构等价。

示例：

```csharp
delegate int D1(int i, double d);
delegate int D2(int c, double d);
```

委托类型 D1 和 D2 是两种不同的类型，因此即使它们的签名相同，也不可互换。结束示例

与其它泛型类型声明类似，需要提供类型参数来创建构造的委托类型。构造的委托类型的参数类型和返回类型是通过为委托声明中的每个类型参数替换构造的委托类型的相应类型参数而创建的。

声明委托类型的唯一方式是通过委托声明。每个委托类型都是派生自 System.Delegate 的引用类型。每个委托类型所需成员的细节在 §20.3 中说明。委托类型是隐式密封的，因此不允许从委托类型派生任何类型。也不允许声明派生自 System.Delegate 的非委托类类型。System.Delegate 本身不是委托类型；它是一个类类型，所有委托类型都派生自它。

### 20.3 委托成员

每个委托类型都继承自 Delegate 类的成员，如 §15.3.4 所描述。此外，每个委托类型必须提供一个非泛型的 Invoke 方法，其参数列表与委托声明中的形式参数列表匹配，其返回类型与委托声明中的返回类型匹配。Invoke 方法的可访问性至少应与包含的委托类型相同。在委托类型上调用 Invoke 方法在语义上等同于使用委托调用语法 (§20.6)。

实现可以在委托类型中定义额外的成员。

除实例化外，可以应用于类或类实例的任何操作也可以分别应用于委托类或实例。特别是，可以通过通常的成员访问语法访问 System.Delegate 类型的成员。

### 20.4 委托兼容性

方法或委托类型 M 与委托类型 D 兼容的条件是以下所有条件都为真：

- D 和 M 具有相同数量的参数，并且 D 中的每个参数都具有与 M 中对应参数相同的 ref 或 out 修饰符。
- 对于每个值参数（没有 ref 或 out 修饰符的参数），从 D 中的参数类型到 M 中对应参数类型存在恒等转换 (§11.2.2) 或隐式引用转换 (§11.2.7)。
- 对于每个 ref 或 out 参数，D 中的参数类型与 M 中的参数类型相同。
- 从 M 的返回类型到 D 的返回类型存在恒等转换或隐式引用转换。

此一致性定义允许返回类型的协变和参数类型的逆变。

示例：

```csharp
delegate int D1(int i, double d);
delegate int D2(int c, double d);
delegate object D3(string s);

class A
{
    public static int M1(int a, double b) {...}
}
class B
{
    public static int M1(int f, double g) {...}
    public static void M2(int k, double l) {...}
    public static int M3(int g) {...}
    public static void M4(int g) {...}
    public static object M5(string s) {...}
    public static int[] M6(object o) {...}
}
```

方法 A.M1 和 B.M1 都与委托类型 D1 和 D2 兼容，因为它们具有相同的返回类型和参数列表。方法 B.M2、B.M3 和 B.M4 与委托类型 D1 和 D2 不兼容，因为它们具有不同的返回类型或参数列表。方法 B.M5 和 B.M6 都与委托类型 D3 兼容。结束示例]

示例：

```csharp
delegate bool Predicate<T>(T value);

class X
{
    static bool F(int i) {...}
    static bool G(string s) {...}
}
```

方法 X.F 与委托类型 Predicate<int> 兼容，方法 X.G 与委托类型 Predicate<string> 兼容。结束示例]

[Note: 委托兼容性的直观含义是，如果每次委托的调用都可以用该方法调用替换而不违反类型安全，则该方法与委托类型兼容，将可选参数和参数数组视为显式参数。例如，在以下代码中：

```csharp
delegate void Action<T>(T arg);
class Test {
    static void Print(object value) {
        Console.WriteLine(value);
    }
    static void Main() {
        Action<string> log = Print;
        log("text");
    }
}
```

Print 方法与 Action<string> 委托类型兼容，因为任何 Action<string> 委托的调用也都是 Print 方法的有效调用。

如果将上述 Print 方法的签名改为例如 Print(object value, bool prependTimestamp = false)，则根据本条款的规则，Print 方法将不再与 Action<string> 兼容。end note]

### 20.5 委托实例化

委托的实例由 *委托创建表达式* (§12.7.11.6)、转换为委托类型、委托组合或委托移除创建。新建的委托实例随后引用以下一项或多项：

- *委托创建表达式* 中引用的静态方法，或
- 目标对象（不能为 *空*）和 *委托创建表达式* 中引用的实例方法，或
- 另一个委托 (§12.7.11.6)。

示例：

```csharp
delegate void D(int x);
class C
{
    public static void M1(int i) {...}
    public void M2(int i) {...}
}
class Test
{
    static void Main() {
        D cd1 = new D(C.M1);    // static method
        C t = new C();
        D cd2 = new D(t.M2);    // instance method
        D cd3 = new D(cd2);     // another delegate
    }
}
```

结束示例

由委托实例封装的方法集合称为 *调用列表*。当委托实例由单个方法创建时，它封装该方法，其调用列表仅包含一个条目。然而，当两个非 *空* 委托实例组合时，它们的调用列表会按左操作数然后右操作数的顺序连接，形成一个新的调用列表，其中包含两个或更多条目。

当从单个委托创建新委托时，结果的调用列表只有一个条目，即源委托 (§12.7.11.6)。

委托使用二元 + (§12.9.5) 和 += 运算符 (§12.18.3) 进行组合。委托可以使用二元 - (§12.9.6) 和 -= 运算符 (§12.18.3) 从委托组合中移除。委托可以进行相等比较 (§12.11.9)。

示例：以下示例展示了多个委托的实例化及其对应的调用列表：

```csharp
delegate void D(int x);
class C
{
    public static void M1(int i) {...}
    public static void M2(int i) {...}
}
class Test
{
    static void Main() {
        D cd1 = new D(C.M1);    // M1 - one entry in invocation list
        D cd2 = new D(C.M2);    // M2 - one entry
        D cd3 = cd1 + cd2;      // M1 + M2 - two entries
        D cd4 = cd3 + cd1;      // M1 + M2 + M1 - three entries
        D cd5 = cd4 + cd3;      // M1 + M2 + M1 + M1 + M2 - five entries
        D td3 = new D(cd3);     // [M1 + M2] - ONE entry in invocation
                                // list, which is itself a list of two methods.
        D td4 = td3 + cd1;      // [M1 + M2] + M1 - two entries
        D cd6 = cd4 - cd2;      // M1 + M1 - two entries in invocation list
        D td6 = td4 - cd2;      // [M1 + M2] + M1 - two entries in
                                // invocation list, but still three methods called, M2 not removed.
    }
}
```

当 cd1 和 cd2 被实例化时，它们各自封装一个方法。当 cd3 被实例化时，它具有两个方法的调用列表，分别为 M1 和 M2，按此顺序。cd4 的调用列表包含 M1、M2 和 M1，按此顺序。对于 cd5，调用列表包含 M1、M2、M1、M1 和 M2，按此顺序。

使用委托创建表达式从另一个委托创建委托时，结果的调用列表与原始列表结构不同，但会导致以相同顺序调用相同的方法。当 td3 由 cd3 创建时，其调用列表只有一个成员，但该成员是方法 M1 和 M2 的列表，并且这些方法由 td3 调用的顺序与由 cd3 调用的顺序相同。类似地，当 td4 被实例化时，其调用列表只有两个条目，但它按 M1、M2 和 M1 的顺序调用三个方法，就像 cd4 一样。

方法列表的结构会影响委托减法。委托 cd6 由从 cd4（调用 M1、M2 和 M1）中减去 cd2（调用 M2）创建，调用 M1 和 M1。然而委托 td6 由从 td4（调用 M1、M2 和 M1）中减去 cd2（调用 M2）创建，仍然按顺序调用 M1、M2 和 M1，因为 M2 不是列表中的单个条目，而是嵌套列表的成员。

有关组合（以及移除）委托的更多示例，请参阅 §20.6。结束示例

一旦实例化，委托实例始终引用相同的调用列表。[Note: 请记住，当两个委托组合或一个从另一个中移除时，会产生一个具有自己调用列表的新委托；被组合或移除的委托的调用列表保持不变。end note]

### 20.6 委托调用

C# 提供了用于调用委托的特殊语法。当调用调用列表包含一个条目的非空委托实例时，它使用相同的参数调用该方法，并返回被引用方法相同的返回值。（有关委托调用的详细信息，请参阅 §12.7.6.4。）如果在调用此类委托期间发生异常，并且该异常未在被调用的方法内捕获，则异常捕获子句的搜索将继续在调用委托的方法中，就好像该方法直接调用了该委托引用的方法一样。

调用列表包含多个条目的委托实例的调用会按顺序同步调用调用列表中的每个方法。每个被调用的方法都传递与委托实例相同的参数集。如果此类委托调用包含引用参数 (§15.6.2.3)，则每次方法调用都将使用对同一变量的引用；调用列表中一个方法对该变量的更改将对调用列表中后面的方法可见。如果委托调用包含输出参数或返回值，则其最终值来自列表中最后一个委托的调用。如果在处理此类委托的调用期间发生异常，并且该异常未在被调用的方法内捕获，则异常捕获子句的搜索将继续在调用委托的方法中，并且调用列表中后面的任何方法都不会被调用。

尝试调用值为 null 的委托实例会引发 System.NullReferenceException 类型的异常。

示例：以下示例展示了如何实例化、组合、移除和调用委托：

```csharp
using System;
```
