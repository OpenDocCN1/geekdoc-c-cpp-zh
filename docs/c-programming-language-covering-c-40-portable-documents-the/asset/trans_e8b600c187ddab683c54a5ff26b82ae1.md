

```
class Test
{
    static void Main()
    {
        Console.WriteLine(StringFromColor(Color.Red));
        Console.WriteLine(StringFromColor(Color.Green));
        Console.WriteLine(StringFromColor(Color.Blue));
    }

    static string StringFromColor(Color c)
    {
        switch (c)
        {
            case Color.Red:
                return String.Format("Red = {0}", (int)c);
            case Color.Green:
                return String.Format("Green = {0}", (int)c);
            case Color.Blue:
                return String.Format("Blue = {0}", (int)c);
            default:
                return "Invalid color";
        }
    }
}
```

会打印出枚举成员名称及其关联值。输出为

Red = 0
Green = 10
Blue = 11

原因如下：

- 枚举成员 Red 被自动赋予值零（因为它没有初始值设定项，并且是第一个枚举成员）。
- 枚举成员 Green 被显式赋予值 10。
- 枚举成员 Blue 被自动赋予比在文本上位于它之前的成员大 1 的值。

枚举成员的关联值不得直接或间接使用其自身关联枚举成员的值。除了这一循环性限制外，枚举成员初始值设定项可以自由引用其他枚举成员初始值设定项，而不论它们在文本中的位置如何。在枚举成员初始值设定项内，其他枚举成员的值始终被视为具有其基础类型，因此在引用其他枚举成员时不需要强制转换。

示例

```
enum Circular
{
    A = B,
    B
}
```

会导致编译时错误，因为 A 和 B 的声明是循环的。A 显式依赖于 B，而 B 隐式依赖于 A。

枚举成员的命名和作用域方式与类中的字段完全类似。枚举成员的作用域是其包含枚举类型的正文。在该作用域内，枚举成员可以通过其简单名称来引用。在所有其他代码中，枚举成员的名称必须用其枚举类型的名称限定。枚举成员没有任何声明的可访问性——如果其包含枚举类型可访问，则该枚举成员可访问。

## 14.4 System.Enum 类型

System.Enum 类型是所有枚举类型的抽象基类（这与枚举类型的基础类型不同且有所区别），并且从 System.Enum 继承的成员在任何枚举类型中都可用。存在从任何枚举类型到 System.Enum 的装箱转换（§4.3.1），以及从 System.Enum 到任何枚举类型的拆箱转换（§4.3.2）。

注意，System.Enum 本身不是枚举类型。相反，它是所有枚举类型派生自的类类型。System.Enum 类型继承自 System.ValueType 类型（§4.1.1），后者又继承自 object 类型。在运行时，System.Enum 类型的值可以为 null，也可以是对任何枚举类型的装箱值的引用。

## 14.5 枚举值与操作

每个枚举类型都定义一种不同的类型；在枚举类型与整型之间，或在两个枚举类型之间进行转换，需要显式枚举转换（§6.2.2）。枚举类型可以采用的值的集合不受其枚举成员限制。特别是，枚举的基础类型的任何值都可以强制转换为该枚举类型，并且是该枚举类型的一个不同的有效值。

枚举成员具有其包含枚举类型的类型（其他枚举成员初始值设定项内除外；参见 §14.3）。在枚举类型 E 中声明的关联值为 v 的枚举成员，其值为 (E)v。

以下运算符可用于枚举类型的值：==、!=、<、>、<=、>=（§7.10.5）、二元 +（§7.8.4）、二元 -（§7.8.5）、^、&、|（§7.11.2）、~（§7.7.4），以及 ++ 和 --（§7.6.9 和 §7.7.5）。

> > **JON SKEET** 其中一些运算符实际上只对用 [Flags] 修饰的枚举有意义，但语言在任何意义上都不强制执行这一限制。

每个枚举类型都自动派生自类 System.Enum（后者又派生自 System.ValueType 和 object）。因此，该类继承的方法和属性可用于枚举类型的值。

## 14. 枚举

## 15. 委托

委托支持其他语言（如 C++、Pascal 和 Modula）用函数指针解决的场景。然而，与 C++ 函数指针不同，委托是完全面向对象的。另外，与 C++ 指向成员函数的指针不同，委托同时封装对象实例和方法。

> > **BILL WAGNER** 读到语言规范中的这一小章时，我体验到一种奇怪的惊叹感。自 1.0 版本发布以来，委托就一直是 C# 的一部分。当时，大多数 C# 社区成员（包括我）都把委托看作围绕事件的一点点额外仪式。十年后，我无法想象没有委托的 C# 语言。它们是我们大多数人每天在 LINQ 查询、函数组合、闭包等中使用的东西。委托以及将代码视为数据的概念，是现代 .NET 生态系统中如此多部分不可或缺的组成部分，以至于我无法想象用一种不允许我将函数（和操作）的概念表达为数据的语言来编程。

委托声明定义一个派生自 System.Delegate 类的类。委托实例封装一个调用列表，该列表由一个或多个方法组成，其中每个方法称为可调用实体。对于实例方法，可调用实体由实例和该实例上的方法组成。对于静态方法，可调用实体仅由一个方法组成。用适当的一组参数调用委托实例，会导致该委托的每个可调用实体都用给定的一组参数被调用。

委托实例的一个有趣且有用的属性是，它不知道也不关心它所封装的方法的类；唯一重要的是那些方法与委托类型兼容（§15.1）。这使得委托非常适合“匿名”调用。

> ERIC LIPPERT 开发人员第一次遇到委托时，通常相当困惑。我喜欢把委托类型看作类似于一个恰好有一个方法的接口；委托类型的实例是实现该方法的对象。

### 15.1 委托声明

委托声明是一种类型声明（§9.6），它声明一个新的委托类型。

```
delegate-declaration:
    attributes_opt delegate-modifiers_opt delegate return-type
    identifier variant-type-parameter-list_opt
    ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt ;
```

```
delegate-modifiers:
    delegate-modifier
    delegate-modifiers delegate-modifier
```

delegate-modifier:
- new
- public
- protected
- internal
- private

同一修饰符在委托声明中出现多次是编译时错误。

new 修饰符只允许用于在另一个类型内声明的委托，在这种情况下，它指定此类委托隐藏同名的继承成员，如 §10.3.4 所述。

public、protected、internal 和 private 修饰符控制委托类型的可访问性。根据委托声明发生的上下文，其中一些修饰符可能不被允许（§3.5.1）。

委托的类型名是 identifier。可选的 formal-parameter-list 指定委托的参数，return-type 指示委托的返回类型。

可选的 variant-type-parameter-list（§13.1.3）指定委托自身的类型参数。

委托类型的返回类型必须是 void 或输出安全的（§13.1.3.1）。

委托类型的所有形参类型必须是输入安全的。此外，任何 out 或 ref 参数类型必须是输出安全的。注意，由于底层执行平台的限制，甚至 out 参数也要求是输入安全的。

> > **ERIC LIPPERT** 这里提到的限制是，out 参数在幕后实际上被实现为 ref 参数：你可以读取和写入 out 参数。编译器强制执行的规则是，out 参数必须先写入再读取，但这是 C# 语言的规则，而不是运行时的规则。如果 out 参数真正是“只写”的，并且这一限制由运行时强制执行，那么从理论上讲，它们就可以被做成协变的。下次设计新的类型系统时，请记住这一点。

C# 中的委托类型是名称等价的，而不是结构等价的。具体来说，具有相同参数列表和返回类型的两个不同委托类型被视为不同的委托类型。然而，两个不同但结构等价的委托类型的实例可以比较为相等（§7.9.8）。

例如：

```csharp
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

委托类型 D1 和 D2 都与方法 A.M1 和 B.M1 兼容，因为它们具有相同的返回类型和参数列表；但是，这些委托类型是两个不同的类型，因此它们不能互换。委托类型 D1 和 D2 是

