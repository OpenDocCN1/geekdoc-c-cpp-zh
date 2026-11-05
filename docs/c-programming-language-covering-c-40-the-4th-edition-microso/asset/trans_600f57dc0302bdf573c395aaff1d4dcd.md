

## 10.6.3 虚方法

当实例方法声明包含 `virtual` 修饰符时，该方法称为虚方法。当不存在 `virtual` 修饰符时，该方法称为非虚方法。

> **BILL WAGNER** 即使在非泛型类中，也可以创建泛型虚方法。这样做时，任何重写也必须是泛型的。不能重写某个特定的实例化版本。

> **JON SKEET** 私有方法不能是虚方法，尽管存在一种边界情况，在这种情况下允许私有方法为虚方法是有意义的：从其自身容器类派生的嵌套类可以重写它（使用另一个私有方法）。规范禁止这种可能性虽然略显不够优雅，但这意味着那些意外声明为私有且为虚方法的方法可以被视为错误——而这种情况要常见得多。

非虚方法的实现是不变的：无论该方法是在声明它的类的实例上调用，还是在派生类的实例上调用，其实现都相同。相比之下，虚方法的实现可以被派生类取代。取代继承的虚方法的实现的过程称为重写该方法（§10.6.4）。

在虚方法调用中，调用所针对的实例的运行时类型决定实际要调用的方法实现。在非虚方法调用中，实例的编译时类型起决定作用。更精确地说，当在编译时类型为 C、运行时类型为 R 的实例上使用参数列表 A 调用名为 N 的方法时（其中 R 要么是 C，要么是从 C 派生的类），该调用按以下方式处理：

- 首先，对 C、N 和 A 应用重载解析，从 C 声明或继承的方法集合中选择一个特定的方法 M。相关内容请参见 §7.6.5.1。
- 然后，如果 M 是非虚方法，则调用 M。
- 否则，M 是虚方法，并调用相对于 R 的 M 的最派生实现。

对于类声明或继承的每个虚方法，相对于该类都存在一个该方法的最派生实现。相对于类 R 的虚方法 M 的最派生实现按以下方式确定：

- 如果 R 包含 M 的引入虚声明，则该声明就是 M 的最派生实现。
- 否则，如果 R 包含 M 的重写，则该重写就是 M 的最派生实现。
- 否则，相对于 R 的 M 的最派生实现，与相对于 R 的直接基类的 M 的最派生实现相同。

以下示例说明了虚方法和非虚方法之间的差异：

```
using System;
class A
{
    public void F() { Console.WriteLine("A.F"); }
    public virtual void G() { Console.WriteLine("A.G"); }
}
class B : A
{
    new public void F() { Console.WriteLine("B.F"); }
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

在此示例中，A 引入了一个非虚方法 F 和一个虚方法 G。类 B 引入了一个新的非虚方法 F，从而隐藏继承的 F，同时还重写了继承的方法 G。该示例产生以下输出：

A.F
B.F
B.G
B.G

请注意，语句 `a.G()` 调用的是 B.G，而不是 A.G。出现这种结果是因为决定实际要调用的方法实现的是实例的运行时类型（即 B），而不是实例的编译时类型（即 A）。

由于允许方法隐藏继承的方法，因此一个类可能包含多个具有相同签名的虚方法。这不会造成歧义问题，因为除了最派生的方法之外，其他方法都会被隐藏。在以下示例中：

```
using System;
class A
{
    public virtual void F() { Console.WriteLine("A.F"); }
}
class B : A
{
    public override void F() { Console.WriteLine("B.F"); }
}
class C : B
{
    new public virtual void F() { Console.WriteLine("C.F"); }
}
class D : C
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

C 类和 D 类包含两个具有相同签名的虚方法：一个由 A 引入，另一个由 C 引入。C 引入的方法隐藏了从 A 继承的方法。因此，D 中的重写声明重写的是 C 引入的方法，而 D 不可能重写 A 引入的方法。该示例产生以下输出：

```
B.F
B.F
D.F
D.F
```

请注意，可以通过一个派生程度较低且该方法未被隐藏的类型来访问 D 的实例，从而调用被隐藏的虚方法。

## 10.6.4 重写方法

当实例方法声明包含 `override` 修饰符时，该方法称为重写方法。重写方法会重写具有相同签名的继承虚方法。虚方法声明会引入一个新方法，而重写方法声明则通过提供该方法的新实现，来专门化一个现有的继承虚方法。

被重写声明重写的方法称为被重写的基方法。对于类 C 中声明的重写方法 M，被重写的基方法通过检查 C 的每个基类类型来确定：从 C 的直接基类类型开始，依次检查后续的每个直接基类类型，直到在某个基类类型中找到至少一个可访问的方法，该方法在替换类型参数后与 M 具有相同的签名。为了定位被重写的基方法，如果方法是公共的、受保护的、受保护的内部方法，或者是内部方法且与 C 在同一程序中声明，则该方法被视为可访问。

除非重写声明满足以下所有条件，否则会发生编译时错误：

- 可以按照上述方式找到被重写的基方法。
- 恰好存在一个这样的被重写基方法。仅当基类类型是构造类型，并且类型参数的替换使两个方法具有相同签名时，此限制才会生效。
- 被重写的基方法是虚方法、抽象方法或重写方法。换句话说，被重写的基方法不能是静态方法或非虚方法。
- 被重写的基方法不是密封方法。
- 重写方法与被重写的基方法具有相同的返回类型。
- 重写声明与被重写的基方法具有相同的声明可访问性。换句话说，重写声明不能更改虚方法的可访问性。但是，如果被重写的基方法是受保护的内部方法，并且它声明在不同于包含重写方法的程序集的另一个程序集中，则重写方法的声明可访问性必须是受保护的。
- 重写声明不指定类型参数约束子句。相反，约束从被重写的基方法继承。请注意，被重写方法中的类型参数约束可能会在继承的约束中被类型实参替换。这可能导致一些在显式指定时不合法的约束，例如值类型或密封类型。

以下示例演示了泛型类中重写规则的工作方式：

```
abstract class C<T>
{
    public virtual T F() {...}
    public virtual C<T> G() {...}
    public virtual void H(C<T> x) {...}
}
class D: C<string>
{
    public override string F() {...}        // Okay
    public override C<string> G() {...}    // Okay
    public override void H(C<T> x) {...}   // Error: should be C<string>
}
class E<T,U>: C<U>
{
    public override U F() {...}            // Okay
    public override C<U> G() {...}         // Okay
    public override void H(C<T> x) {...}   // Error: should be C<U>
}
```

重写声明可以使用 *基访问*（§7.6.8）访问被重写的基方法。在以下示例中：

```
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
    public override void PrintFields() {
        base.PrintFields();
        Console.WriteLine("y = {0}", y);
    }
}
```

B 中的 `base.PrintFields()` 调用调用的是 A 中声明的 `PrintFields` 方法。*基访问*会禁用虚调用机制，并将基方法简单地视为非虚方法。如果 B 中的调用写成 `((A)this).PrintFields()`，它

