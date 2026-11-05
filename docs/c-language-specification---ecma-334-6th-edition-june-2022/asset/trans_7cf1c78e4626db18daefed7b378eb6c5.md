
- 如果数组创建表达式包含数组初始化器，则数组初始化器中的每个表达式都会被求值并赋给其对应的数组元素。求值和赋值按照数组初始化器中表达式的书写顺序执行——换句话说，元素按递增的索引顺序初始化，最右边的维度最先递增。如果某个表达式的求值或随后对其对应数组元素的赋值导致异常，则不会再初始化后续元素（因此剩余元素将具有其默认值）。

数组创建表达式允许实例化元素类型为数组类型的数组，但此类数组的元素必须手动初始化。

*示例：* 语句

```
int[][] a = new int[100][];
```

创建一个具有 100 个类型为 int[] 元素的单维数组。每个元素的初始值为 null。同一数组创建表达式无法同时实例化子数组，并且语句

```
int[][] a = new int[100][5]; // Error
```

会导致编译时错误。子数组的实例化可以改为手动执行，如下所示

```
int[][] a = new int[100][];
for (int i = 0; i < 100; i++)
{
    a[i] = new int[5];
}
```

*结束示例*

*注意：* 当数组的数组具有“矩形”形状时，即当子数组都具有相同的长度时，使用多维数组更高效。在上面的示例中，数组的数组的实例化创建了 101 个对象——一个外部数组和 100 个子数组。相比之下，

```
int[,] a = new int[100, 5];
```

仅创建一个对象，即二维数组，并在单个语句中完成分配。

*结束注释*

*示例：* 以下是对隐式类型数组创建表达式的示例：

```
var a = new[] { 1, 10, 100, 1000 };          // int[]
var b = new[] { 1.5, 2, 2.5 };               // double[]
var c = new[] { { "hello", null }, { "world", "!" } }; // string[,]
var d = new[] { 1, "one", 2, "two" };        // Error
```

最后一个表达式会导致编译时错误，因为 int 和 string 彼此都不是隐式可转换的，因此没有最佳公共类型。在这种情况下必须使用显式类型数组创建表达式，例如指定类型为 object[]。或者，可以将其中一个元素强制转换为公共基类型，这将成为推断的元素类型。

*结束示例*

隐式类型数组创建表达式可以与匿名对象初始化器 (§11.7.15.7) 结合使用，以创建匿名类型的数据结构。

*示例：*

```
var contacts = new[]
{
    new
    {
        Name = "Chris Smith",
        PhoneNumbers = new[] { "206-555-0101", "425-882-8080" }
    },
    new
    {
        Name = "Bob Harris",
        PhoneNumbers = new[] { "650-555-0199" }
    }
};
```

*结束示例*

## 11.7.15.6 委托创建表达式

A *委托创建表达式* 用于获取 *委托类型* 的实例。

```
delegate_creation_expression
    : 'new' delegate_type '(' expression ')'
    ;
```

委托创建表达式的参数应为方法组、匿名函数，或编译时类型为 *动态* 或 *委托类型* 的值。如果参数是方法组，则它标识该方法，以及对于实例方法，创建委托的对象。如果参数是匿名函数，则它直接定义委托目标的参数和方法体。如果参数是值，则它标识要创建副本的委托实例。

如果 *表达式* 的编译时类型为 *动态*，则 *委托创建表达式* 动态绑定 (§11.7.15.6)，并且以下规则使用 *表达式* 的运行时类型在运行时应用。否则，规则在编译时应用。

形式为 new D(E) 的 *委托创建表达式* 的绑定时处理，其中 D 是 *委托类型* 且 E 是 *表达式*，包括以下步骤：

- 如果 E 是方法组，则委托创建表达式的处理方式与方法组转换 (§10.8) 从 E 到 D 相同。
- 如果 E 是匿名函数，则委托创建表达式的处理方式与匿名函数转换 (§10.7) 从 E 到 D 相同。
- 如果 E 是值，则 E 必须与 D 兼容 (§19.2)，结果是对新创建的委托的引用，该委托具有单入口调用列表以调用 E。

形式为 new D(E) 的 *委托创建表达式* 的运行时处理，其中 D 是 *委托类型* 且 E 是 *表达式*，包括以下步骤：

- 如果 E 是方法组，则委托创建表达式被评估为方法组转换 (§10.8) 从 E 到 D。
- 如果 E 是匿名函数，则委托创建被评估为匿名函数转换从 E 到 D (§10.7)。
- 如果 E 是 *委托类型* 的值：
  - E 被求值。如果此求值导致异常，则不再执行后续步骤。
  - 如果 E 的值为 null，则抛出 `System.NullReferenceException` 且不再执行后续步骤。
  - 分配委托类型 D 的新实例。如果没有足够的内存分配新实例，则抛出 `System.OutOfMemoryException` 且不再执行后续步骤。
  - 新的委托实例使用单入口调用列表初始化以调用 E。

委托的调用列表在委托实例化时确定，然后在委托整个生命周期内保持不变。换句话说，一旦委托被创建，就不可能更改其目标可调用实体。

*注意：* 请记住，当两个委托组合在一起或从另一个委托中移除一个委托时，会产生一个新的委托；现有委托的内容不会被更改。 *结束注释*

无法创建引用属性、索引器、用户定义运算符、实例构造函数、终结器或静态构造函数的委托。

*示例：* 如上所述，当从方法组创建委托时，委托的形式参数列表和返回类型决定选择哪个重载方法。在示例中

```
delegate double DoubleFunc(double x);

class A
{
    DoubleFunc f = new DoubleFunc(Square);

    static float Square(float x) => x * x;
    static double Square(double x) => x * x;
}
```

A.f 字段被初始化为引用第二个 Square 方法的委托，因为该方法与 DoubleFunc 的形式参数列表和返回类型完全匹配。如果没有第二个 Square 方法，则会发生编译时错误。

*结束示例*

## 11.7.15.7 匿名对象创建表达式

匿名对象创建表达式 用于创建匿名类型的对象。

```
anonymous_object_creation_expression
: 'new' anonymous_object_initializer
;

anonymous_object_initializer
: '{' member_declarator_list? '}'
| '{' member_declarator_list ',' '}'
;

member_declarator_list
: member_declarator (',' member_declarator)*
;
```

```
member_declarator
: simple_name
| member_access
| null_conditional_projection_initializer
| base_access
| identifier '=' expression
;
```

匿名对象初始化器声明一个匿名类型并返回该类型的实例。匿名类型是直接继承自 object 的无名类类型。匿名类型的成员是从用于创建类型实例的匿名对象初始化器推断出来的一系列只读属性。具体来说，形式为

```
new { p1 = e1 , p2 = e2 , ... pn = en }
```

的匿名对象初始化器声明形式为

```
class __Anonymous1
{
    private readonly «T1» «f1»;
    private readonly «T2» «f2»;
    ...
    private readonly «Tn» «fn»;

    public __Anonymous1(«T1» «a1», «T2» «a2»,..., «Tn» «an»)
    {
        «f1» = «a1»;
        «f2» = «a2»;
        ...
        «fn» = «an»;
    }

    public «T1» «p1» { get { return «f1»; } }
    public «T2» «p2» { get { return «f2»; } }
    ...
    public «Tn» «pn» { get { return «fn»; } }
    public override bool Equals(object __o) { ... }
    public override int GetHashCode() { ... }
}
```

的匿名类型，其中每个 «Tx» 是对应表达式 «ex» 的类型。member_declarator 中使用的表达式必须具有类型。因此，member_declarator 中的表达式为 null 或匿名函数是编译时错误。表达式具有指针类型 (§22.3) 也同样是编译时错误。

匿名类型的名称及其 Equals 方法的参数由编译器自动生成，不能在程序文本中引用。

在同一程序中，指定相同名称和编译时类型的属性序列且顺序相同的两个匿名对象初始化器将生成同一匿名类型的实例。

示例： 在示例中

```
var p1 = new { Name = "Lawnmower", Price = 495.00 };
var p2 = new { Name = "Shovel", Price = 26.95 };
p1 = p2;
```
