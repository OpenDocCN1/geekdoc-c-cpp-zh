
## 15. 委托

委托实现了其他语言（如 C++、Pascal 和 Modula）使用函数指针来处理的场景。然而，与 C++ 函数指针不同，委托是完全面向对象的，并且与 C++ 成员函数指针不同，委托同时封装了一个对象实例和方法。

委托声明定义了一个派生自类 System.Delegate 的类。委托实例封装了一个调用列表，它是一个包含一个或多个方法列表，每个方法被称为可调用实体。对于实例方法，可调用实体由一个实例及其上的方法组成。对于静态方法，可调用实体仅由一个方法组成。使用适当的一组参数调用委托实例会导致委托的每个可调用实体都使用给定的参数集被调用。

委托实例的一个有趣且有用的特性是它并不关心也不在乎其封装的方法的类；唯一重要的是这些方法与委托的类型兼容（§15.1）。这使得委托非常适合“匿名”调用。

### 15.1 委托声明

委托声明是一个类型声明（§9.6），它声明一个新的委托类型。

```
delegate-declaration:
    attributes_opt delegate-modifiers_opt delegate return-type
    identifier variant-type-parameter-list_opt
    ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt ;

delegate-modifiers:
    delegate-modifier
    delegate-modifier delegate-modifier

delegate-modifier:
    new
    public
    protected
    internal
    private
```

在委托声明中，相同的修饰符出现多次是编译时错误。

new 修饰符仅允许用于在另一个类型内声明的委托，在这种情况下它指定该委托隐藏了同名继承的成员，如 §10.3.4 所述。

public、protected、internal 和 private 修饰符控制委托类型的可访问性。根据委托声明出现的上下文，其中一些修饰符可能不被允许（§3.5.1）。

委托的类型名是 identifier。

可选的 formal-parameter-list 指定委托的参数，return-type 表示委托的返回类型。

可选的 variant-type-parameter-list（§13.1.3）指定委托本身的类型参数。

委托类型的返回类型必须是 void，或 output-safe（§13.1.3.1）。

委托类型的所有形式参数类型必须是 input-safe。此外，任何 out 或 ref 参数类型也必须是 output-safe。注意，即使是 out 参数也要求是 input-safe，这是由于底层执行平台的限制。

C# 中的委托类型按名称等价，而不是结构等价。具体来说，具有相同参数列表和返回类型的两个不同委托类型被视为不同的委托类型。然而，两个不同但结构等价的委托类型的实例可能比较相等（§7.9.8）。

例如：

```
delegate int D1(int i, double d);
class A
{
    public static int M1(int a, double b) {...}
}
class B
{
    delegate int D2(int c, double d);
    public static int M1(int f, double g) {...}
    public static void M2(int k, double l) {...}
    public static int M3(int g) {...}
    public static void M4(int g) {...}
}
```

委托类型 D1 和 D2 都与方法 A.M1 和 B.M1 兼容，因为它们具有相同的返回类型和参数列表；然而，这些委托类型是两种不同的类型，因此不可互换。委托类型 D1 和 D2 与方法 B.M2、B.M3 和 B.M4 不兼容，因为它们具有不同的返回类型或参数列表。

与其他泛型类型声明类似，必须给出类型参数才能创建构造的委托类型。通过为委托声明中的每个类型参数替换构造的委托类型的相应类型参数，来创建构造的委托类型的参数类型和返回类型。所得的返回类型和参数类型用于确定哪些方法与构造的委托类型兼容。例如：

```
delegate bool Predicate<T>(T value);
class X
{
    static bool F(int i) {...}
    static bool G(string s) {...}
}
```

委托类型 Predicate<int> 与方法 X.F 兼容，委托类型 Predicate<string> 与方法 X.G 兼容。

声明委托类型的唯一方式是通过委托声明。委托类型是从 System.Delegate 派生的类类型。委托类型是隐式密封的，因此不允许从委托类型派生任何类型。也不允许从 System.Delegate 派生非委托类类型。注意 System.Delegate 本身不是委托类型；它是一个类类型，所有委托类型都从它派生。

C# 为委托实例化和调用提供了特殊语法。除了实例化之外，可以应用于类或类实例的任何操作也可以分别应用于委托类或实例。特别是，可以通过通常的成员访问语法访问 System.Delegate 类型的成员。

委托实例封装的方法集称为调用列表。当委托实例由单个方法创建（§15.2）时，它封装该方法，其调用列表仅包含一个条目。然而，当两个非空委托实例组合时，它们的调用列表会按左操作数然后右操作数的顺序连接，以形成新的调用列表，其中包含两个或多个条目。

委托使用二元 +（§7.8.4）和 += 运算符（§7.17.2）组合。委托可以使用二元 -（§7.8.5）和 -= 运算符（§7.17.2）从委托组合中移除。委托可以进行相等比较（§7.10.8）。

以下示例展示了多个委托的实例化及其对应的调用列表：

```
delegate void D(int x);
class C
{
    public static void M1(int i) {...}
    public static void M2(int i) {...}
}
class Test
{
    static void Main() {
        D cd1 = new D(C.M1);      // M1
        D cd2 = new D(C.M2);      // M2
        D cd3 = cd1 + cd2;        // M1 + M2
        D cd4 = cd3 + cd1;        // M1 + M2 + M1
        D cd5 = cd4 + cd3;        // M1 + M2 + M1 + M1 + M2
    }
}
```

当 cd1 和 cd2 被实例化时，它们各自封装一个方法。当 cd3 被实例化时，它具有包含两个方法 M1 和 M2 的调用列表，按此顺序。cd4 的调用列表包含 M1、M2 和 M1，按此顺序。最后，cd5 的调用列表包含 M1、M2、M1、M1 和 M2，按此顺序。有关组合（以及移除）委托的更多示例，请参阅 §15.4。

### 15.2 委托兼容性

方法或委托 M 与委托类型 D *兼容* 当且仅当以下所有条件都为真时：

- D 和 M 具有相同数量的参数，并且 D 中的每个参数与 M 中对应参数具有相同的 `ref` 或 `out` 修饰符。
- 对于每个值参数（没有 `ref` 或 `out` 修饰符的参数），从 D 中的参数类型到 M 中对应参数类型存在恒等转换（§6.1.1）或隐式引用转换（§6.1.6）。
- 对于每个 `ref` 或 `out` 参数，D 中的参数类型与 M 中的参数类型相同。
- 从 M 的返回类型到 D 的返回类型存在恒等或隐式引用转换。

### 15.3 委托实例化

委托的实例由 *委托创建表达式*（§7.6.10.5）或转换为委托类型创建。新建的委托实例随后引用以下之一：

- *委托创建表达式* 中引用的静态方法，或
- *委托创建表达式* 中引用的目标对象（不能为 `null`）和实例方法，或
