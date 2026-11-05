
数组创建表达式允许实例化一个元素类型为数组类型的数组，但此类数组的元素必须手动初始化。例如，该语句

```
int[][] a = new int[100][];
```

创建一个具有 100 个类型为 int[] 的元素的一维数组。每个元素的初始值为 null。相同的数组创建表达式不可能同时实例化子数组，并且该语句

```
int[][] a = new int[100][5];    // Error
```

会导致编译时错误。子数组的实例化必须改为手动执行，如下所示

```
int[][] a = new int[100][];
for (int i = 0; i < 100; i++) a[i] = new int[5];
```

> BILL WAGNER 下面的注释违反了 FxCop 规则，但确实解释了在什么条件下应该违反该规则。

当数组的数组具有“矩形”形状时——也就是说，当子数组都具有相同的长度时——使用多维数组更高效。在上面的示例中，数组的数组的实例化创建了 101 个对象——一个外部数组和 100 个子数组。相比之下，

```
int[,] a = new int[100, 5];
```

只创建单个对象——即二维数组——并在一个语句中完成分配。

> PETER SESTOFT 在语言规范中包含关于效率的陈述有些可疑，因为效率是与实现相关的问题，而不是语义。事实上，虽然分配（随后管理）单个包含 500 个整数的块可能比分配 100 个包含 5 个整数的块更快，但作用于“慢速”数组-数组表示的矩阵乘法算法可能比作用于“高效”矩形数组表示的算法更快——这可能得益于 JIT 编译器技巧和现代 CPU 架构的结合。

以下是对隐式类型数组创建表达式的示例：

```
var a = new[] { 1, 10, 100, 1000 };          // int[]
var b = new[] { 1, 1.5, 2, 2.5 };            // double[]
var c = new[,] { { "hello", null }, { "world", "!" } }; // string[,]
var d = new[] { 1, "one", 2, "two" };        // Error
```

最后一个表达式导致编译时错误，因为 int 和 string 都不能隐式相互转换，因此没有最佳公共类型。在这种情况下必须使用显式类型数组创建表达式——例如，指定类型为 object[]。或者，可以将其中一个元素强制转换为公共基类型，这将成为推断的元素类型。

隐式类型数组创建表达式可以与匿名对象初始化器 (§7.6.10.6) 结合使用以创建匿名类型的数据结构。例如：

```
var contacts = new[] {
    new {
        Name = "Chris Smith",
        PhoneNumbers = new[] { "206-555-0181", "425-882-8088" }
    },
    new {
        Name = "Bob Harris",
        PhoneNumbers = new[] { "650-555-0199" }
    }
};
```

## 7.6.10.5 委托创建表达式

delegate-creation-expression 用于创建 delegate-type 的新实例。

```
delegate-creation-expression:
    new delegate-type ( expression )
```

委托创建表达式的参数必须是方法组、匿名函数，或编译时类型为 dynamic 或 delegate-type 的值。如果参数是方法组，则它标识该方法，并且对于实例方法，标识为其创建委托的对象。如果参数是匿名函数，则它直接定义委托目标的参数和方法体。如果参数是值，则它标识要创建副本的委托实例。

如果表达式具有编译时类型 dynamic，则 delegate-creation-expression 动态绑定 (§7.2.2)，并且以下规则使用表达式的运行时类型在运行时应用。否则，规则在编译时应用。

形式为 new D(E) 的 delegate-creation-expression 的绑定时处理，其中 D 是 delegate-type，E 是表达式，包括以下步骤：

- 如果 E 是方法组，则委托创建表达式的处理方式与从 E 到 D 的方法组转换 (§6.6) 相同。
- 如果 E 是匿名函数，则委托创建表达式的处理方式与从 E 到 D 的匿名函数转换 (§6.5) 相同。

如果 E 是值，则 E 必须与 D 兼容 (§15.1)，并且结果是对新创建的类型为 D 的委托的引用，该委托引用与 E 相同的调用列表。如果 E 与 D 不兼容，则会发生编译时错误。

形式为 new D(E) 的 delegate-creation-expression 的运行时处理，其中 D 是 delegate-type，E 是表达式，包括以下步骤：

- 如果 E 是方法组，则委托创建表达式被评估为从 E 到 D 的方法组转换 (§6.6)。
- 如果 E 是匿名函数，则委托创建被评估为从 E 到 D 的匿名函数转换 (§6.5)。
- 如果 E 是 delegate-type 的值：
  - 对 E 进行求值。如果此求值导致异常，则不执行后续步骤。
  - 如果 E 的值为 null，则抛出 System.NullReferenceException 并且不执行后续步骤。
  - 分配委托类型 D 的新实例。如果没有足够的内存来分配新实例，则抛出 System.OutOfMemoryException 并且不执行后续步骤。
  - 新的委托实例使用由 E 给出的委托实例相同的调用列表进行初始化。

委托的调用列表在委托实例化时确定，然后在委托的整个生命周期内保持不变。换句话说，一旦委托被创建，就不可能更改其目标可调用实体。当两个委托组合在一起或一个从另一个中移除时 (§15.1)，会产生新的委托；现有委托的内容不会被更改。

不可能创建引用属性、索引器、用户定义运算符、实例构造函数、析构函数或静态构造函数的委托。

如上所述，当从方法组创建委托时，委托的形式参数列表和返回类型决定选择哪个重载方法。在示例中

```
delegate double DoubleFunc(double x);
class A
{
    DoubleFunc f = new DoubleFunc(Square);
    static float Square(float x) {
        return x * x;
    }
}
static double Square(double x) {
    return x * x;
}
```

a.f 字段被初始化为引用第二个 Square 方法的委托，因为该方法与 DoubleFunc 的形式参数列表和返回类型完全匹配。如果没有第二个 Square 方法，则会发生编译时错误。

## 7.6.10.6 匿名对象创建表达式

anonymous-object-creation-expression 用于创建匿名类型对象。

```
anonymous-object-creation-expression:
    new anonymous-object-initializer

anonymous-object-initializer:
    { member-declarator-list_opt }
    { member-declarator-list , }

member-declarator-list:
    member-declarator
    member-declarator-list , member-declarator

member-declarator:
    simple-name
    member-access
    base-access
    identifier = expression
```

> VLADIMIR RESHETNIKOV base-access 只有在形式为 base.identifier 时才能是 member-declarator；也就是说，这里不允许使用 base 索引器访问。

匿名对象初始化器声明一个匿名类型并返回该类型的实例。匿名类型是一个无名的类类型，直接继承自 object。匿名类型的成员是从用于创建该类型实例的匿名对象初始化器推断的一系列只读属性。具体来说，形式为

```
new { p1 = e1 , p2 = e2 , ... pn = en }
```

的匿名对象初始化器声明形式为的匿名类型

```
class __Anonymous1
{
    private readonly T1 f1;
    private readonly T2 f2;
    ...
    private readonly Tn fn;
    public __Anonymous1(T1 a1, T2 a2, ..., Tn an) {
        f1 = a1;
        f2 = a2;
        ...
        fn = an;
    }
    public T1 p1 { get { return f1; } }
    public T2 p2 { get { return f2; } }
    ...
    public Tn pn { get { return fn; } }
    public override bool Equals(object o) { ... }
    public override int GetHashCode() { ... }
}
```

其中每个 Ti 是对应表达式 ei 的类型。member-declarator 中使用的表达式必须具有类型。因此，member-declarator 中的表达式为 null 或匿名函数是编译时错误。表达式具有不安全类型也是编译时错误。

> ERIC LIPPERT 微软实现为匿名类型生成的实际代码比本讨论所暗示的更为复杂，因为希望（后面提到）结构上等价的匿名类型在整个程序中由同一类型表示。由于字段类型可能是受保护的嵌套类型，因此很难确定在何处生成匿名类以便在不同派生类型之间有效共享。出于这个原因，微软的实现实际上生成一个泛型类，然后用适当的类型参数构造它。

匿名类型的名称由编译器自动生成，不能在程序文本中引用。

> JON SKEET 听起来自相矛盾，但我非常希望看到命名匿名类型：类，其表达方式与匿名类型一样简单，并且具有不可变性、自然相等性以及属性的类型和名称安全性——但带有名称。尽管许多工具可以将匿名类型“展开”为等效的普通类，但此时类型的简洁表达就丢失了。
