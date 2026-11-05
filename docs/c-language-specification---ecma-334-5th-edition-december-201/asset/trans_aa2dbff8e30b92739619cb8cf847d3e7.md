
```csharp
class Test
{
    static void F(params object[] args) {
        foreach (object o in args) {
            Console.Write(o.GetType().FullName);
            Console.Write(" ");
        }
        Console.WriteLine();
    }
    static void Main() {
        object[] a = {1,"Hello", 123.456};
        object o = a;
        F(a);
        F((object)a);
        F(o);
        F((object[])o);
    }
}
```

产生输出

System.Int32 System.String System.Double
System.Object[]
System.Object[]
System.Int32 System.String System.Double

在对 F 的第一次和最后一次调用中，F 的正常形式适用，因为参数类型到参数类型的隐式转换存在（两者都是 object[] 类型）。因此，重载解析选择 F 的正常形式，并且参数作为常规值参数传递。在第二次和第三次调用中，F 的正常形式不适用，因为参数类型到参数类型的隐式转换不存在（object 类型不能隐式转换为 object[] 类型）。然而，F 的扩展形式适用，因此被重载解析选中。结果，调用创建了一个包含一个元素的 object[]，并且数组的单个元素被初始化为给定的参数值（它本身是对 object[] 的引用）。结束示例

## 15.6.3 静态方法和实例方法

当方法声明包含 static 修饰符时，该方法称为静态方法。当没有 static 修饰符时，该方法称为实例方法。

静态方法不操作特定实例，并且在静态方法中引用 this 是编译时错误。

实例方法操作类的给定实例，并且该实例可以作为 this 访问（§12.7.8）。

静态成员和实例成员之间的差异在 §15.3.8 中进一步讨论。

## 15.6.4 虚拟方法

当实例方法声明包含 virtual 修饰符时，该方法称为虚拟方法。当没有 virtual 修饰符时，该方法称为非虚拟方法。

非虚拟方法的实现是不变的：无论方法是在声明它的类实例上调用，还是在派生类实例上调用，实现都相同。相比之下，虚拟方法的实现可以被派生类取代。将继承的虚拟方法的实现取代的过程称为重写该方法（§15.6.5）。

在虚拟方法调用中，进行该调用的实例的运行时类型决定了要调用的实际方法实现。在非虚拟方法调用中，实例的编译时类型是决定因素。精确地说，当在具有编译时类型 C 和运行时类型 R（其中 R 是 C 或派生自 C 的类）的实例上使用参数列表 A 调用名为 N 的方法时，调用按如下方式处理：

- 在绑定时，对 C、N 和 A 应用重载解析，以从声明于 C 中并由 C 继承的方法集合中选择特定方法 M。这在 §12.7.6.2 中描述。
- 然后在运行时：
  - 如果 M 是非虚拟方法，则调用 M。
  - 否则，M 是虚拟方法，并且相对于 R 调用 M 的最派生实现。

对于每个在类中声明或继承的虚拟方法，相对于该类都存在该方法的最派生实现。相对于类 R 的虚拟方法 M 的最派生实现按如下方式确定：

- 如果 R 包含 M 的引入虚拟声明，则这是相对于 R 的 M 的最派生实现。
- 否则，如果 R 包含 M 的重写，则这是相对于 R 的 M 的最派生实现。
- 否则，相对于 R 的 M 的最派生实现与相对于 R 的直接基类的 M 的最派生实现相同。

[示例：以下示例说明虚拟方法和非虚拟方法之间的差异：

```
using System;
class A
{
    public void F() { Console.WriteLine("A.F"); }
    public virtual void G() { Console.WriteLine("A.G"); }
}
class B: A
{
    new public void F() { Console.WriteLine("B.F"); };
    public override void G() { Console.WriteLine("B.G"); }
}
class Test
{
    static void Main() {
        B b = new B();
        A a = b;
        a.F();
        b.F();
        a.G();
        b.G();
    }
}
```

在示例中，A 引入了一个非虚拟方法 F 和一个虚拟方法 G。类 B 引入了一个新的非虚拟方法 F，从而隐藏了继承的 F，并且还重写了继承的方法 G。示例产生输出：

A.F
B.F
B.G
B.G

请注意，语句 a.G() 调用的是 B.G，而不是 A.G。这是因为实例的运行时类型（即 B），而不是实例的编译时类型（即 A），决定了要调用的实际方法实现。结束示例]

由于允许方法隐藏继承的方法，因此一个类可能包含多个具有相同签名的虚拟方法。这不会产生歧义问题，因为除最派生方法之外的所有方法都被隐藏。[示例：在以下代码中

```
using System;
class A
{
    public virtual void F() { Console.WriteLine("A.F"); }
}
class B: A
{
    public override void F() { Console.WriteLine("B.F"); }
}
class C: B
{
    new public virtual void F() { Console.WriteLine("C.F"); }
}
class D: C
{
    public override void F() { Console.WriteLine("D.F"); }
}
class Test
{
    static void Main() {
        D d = new D();
        A a = d;
        B b = d;
        C c = d;
        a.F();
        b.F();
        c.F();
        d.F();
    }
}
```

C 和 D 类包含两个具有相同签名的虚拟方法：一个由 A 引入，一个由 C 引入。C 引入的方法隐藏了从 A 继承的方法。因此，D 中的重写声明重写了 C 引入的方法，并且 D 不可能重写 A 引入的方法。示例产生输出：

B.F
B.F
D.F
D.F

请注意，可以通过通过未隐藏该方法的较少派生类型访问 D 的实例来调用隐藏的虚拟方法。结束示例]

## 15.6.5 重写方法

当实例方法声明包含 override 修饰符时，该方法称为重写方法。重写方法重写具有相同签名的继承的虚拟方法。虚拟方法声明引入新方法，而重写方法声明通过提供该方法的新实现来特化现有的继承虚拟方法。

由重写声明重写的方法称为被重写的基方法。对于在类 C 中声明的重写方法 M，被重写的基方法是通过检查 C 的每个基类来确定的，从 C 的直接基类开始，继续每个后续直接基类，直到在给定的基类类型中至少找到一个可访问的方法，该方法在替换类型参数后具有与 M 相同的签名。为了定位被重写的基方法，如果方法是 public、protected、protected internal，或者是 internal 且在与 C 相同的程序中声明，则认为该方法是可访问的。

除非重写声明满足以下所有条件，否则会发生编译时错误：

- 可以按照上述描述找到被重写的基方法。
- 恰好存在这样一个被重写的基方法。此限制仅在基类类型为构造类型且类型参数的替换使两个方法的签名相同的情况下才有效。
- 被重写的基方法是 virtual、abstract 或 override 方法。换句话说，被重写的基方法不能是 static 或非虚拟的。
- 被重写的基方法不是 sealed 方法。
- 被重写的基方法的返回类型与重写方法之间存在恒等转换。
- 重写声明和被重写的基方法具有相同的声明可访问性。换句话说，重写声明不能更改虚拟方法的可访问性。然而，如果被重写的基方法是 protected internal 并且它声明在与包含重写声明的程序集不同的程序集中，则重写声明的声明可访问性应为 protected。
- 重写声明不指定类型参数约束子句。相反，约束从被重写的基方法继承。被重写方法中为类型参数的约束可能被继承约束中的类型参数替换。这可能导致在显式指定时无效的约束，例如值类型或密封类型。

[示例：以下演示了泛型类的重写规则如何工作：

```csharp
abstract class C<T>
{
    public virtual T F() {...}
    public virtual C<T> G() {...}
    public virtual void H(C<T> x) {...}
}
class D: C<string>
{
    public override string F() {...}       // ok
    public override C<string> G() {...}    // ok
    public override void H(C<T> x) {...}   // Error, should be C<string>
}
class E<T,U>: C<U>
{
    public override U F() {...}            // ok
    public override C<U> G() {...}         // ok
    public override void H(C<T> x) {...}   // Error, should be C<U>
}
```

结束示例]

重写声明可以使用 *基访问*（§12.7.9）访问被重写的基方法。[示例：在以下代码中

```csharp
class A
{
    int x;
    public virtual void PrintFields() {
        Console.WriteLine("x = {0}", x);
    }
}
class B: A
{
    int y;
```
