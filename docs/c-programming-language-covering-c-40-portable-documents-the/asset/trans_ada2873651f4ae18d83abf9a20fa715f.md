

由于方法可以隐藏继承的方法，因此一个类可能包含多个具有相同签名的虚方法。这不会造成歧义问题，因为除最派生的方法外，其他方法都会被隐藏。在下面的示例中：

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

C 类和 D 类包含两个具有相同签名的虚方法：一个由 A 引入，另一个由 C 引入。C 引入的方法隐藏了从 A 继承的方法。因此，D 中的重写声明重写的是 C 引入的方法，而 D 无法重写 A 引入的方法。该示例产生以下输出：

```
B.F
B.F
D.F
D.F
```

请注意，可以通过以一个方法未被隐藏的较低派生类型访问 D 的实例，从而调用被隐藏的虚方法。

## 10.6.4 重写方法

当实例方法声明包含 `override` 修饰符时，该方法称为重写方法。重写方法重写具有相同签名的继承虚方法。虚方法声明会引入一个新方法，而重写方法声明则通过提供该方法的新实现来特化现有的继承虚方法。

被重写声明重写的方法称为被重写的基方法。对于在类 C 中声明的重写方法 M，被重写的基方法通过检查 C 的每个基类类型来确定：从 C 的直接基类类型开始，依次检查每个后续的直接基类类型，直到在某个基类类型中找到至少一个可访问的方法。该方法在替换类型参数后，必须与 M 具有相同的签名。为了定位被重写的基方法，如果某个方法是公共方法、受保护方法、受保护内部方法，或者是与 C 在同一程序中声明的内部方法，则认为该方法是可访问的。

除非重写声明满足以下所有条件，否则会发生编译时错误：

- 可以按照上述说明找到被重写的基方法。
- 恰好存在一个这样的被重写基方法。仅当基类类型是构造类型，并且类型参数的替换使两个方法具有相同签名时，此限制才有效。
- 被重写的基方法是虚方法、抽象方法或重写方法。换言之，被重写的基方法不能是静态方法或非虚方法。
- 被重写的基方法不是密封方法。
- 重写方法与被重写的基方法具有相同的返回类型。
- 重写声明与被重写的基方法具有相同的声明可访问性。换言之，重写声明不能更改虚方法的可访问性。但是，如果被重写的基方法是受保护内部方法，且它声明所在的程序集不同于包含重写方法的程序集，则重写方法的声明可访问性必须是受保护。
- 重写声明不指定类型参数约束子句。相反，约束会从被重写的基方法继承。在被重写的方法中作为类型参数的约束，可能会在继承的约束中被类型实参替换。这可能导致出现显式指定时不合法的约束，例如值类型或密封类型。

以下示例演示了泛型类中的重写规则：

```
abstract class C<T>
{
    public virtual T F() {...}
    public virtual C<T> G() {...}
    public virtual void H(C<T> x) {...}
}

class D: C<string>
{
    public override string F() {...}      // 正确
    public override C<string> G() {...}   // 正确
    public override void H(C<T> x) {...}  // 错误：应为 C<string>
}

class E<T,U>: C<U>
{
    public override U F() {...}           // 正确
    public override C<U> G() {...}        // 正确
    public override void H(C<T> x) {...}  // 错误：应为 C<U>
}
```

重写声明可以使用基访问（§7.6.8）访问被重写的基方法。在下面的示例中：

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

B 中的 `base.PrintFields()` 调用会调用 A 中声明的 PrintFields 方法。基访问会禁用虚调用机制，并将基方法简单地视为非虚方法。如果 B 中的调用写成 `((A)this).PrintFields()`，则它会递归调用 B 中声明的 PrintFields 方法，而不是 A 中声明的方法，因为 PrintFields 是虚方法，并且 `((A)this)` 的运行时类型是 B。

只有包含 `override` 修饰符的方法才能重写另一个方法。在其他所有情况下，与继承方法具有相同签名的方法只会隐藏继承的方法。在下面的示例中：

```
class A
{
    public virtual void F() {}
}
class B: A
{
    public virtual void F() {}    // 警告：隐藏了继承的 F()
}
```

B 中的 F 方法不包含 `override` 修饰符，因此不会重写 A 中的 F 方法。相反，B 中的 F 方法会隐藏 A 中的方法，并且由于该声明不包含 `new` 修饰符，因此会报告警告。

在下面的示例中：

```
class A
{
    public virtual void F() {}
}
class B: A
{
    new private void F() {}    // 在 B 的主体中隐藏 A.F
}
class C: B
{
    public override void F() {}    // 正确：重写 A.F
}
```

B 中的 F 方法隐藏了从 A 继承的虚 F 方法。由于 B 中新的 F 具有私有访问权限，因此其作用域仅包括 B 的类主体，并不会扩展到 C。因此，C 中的 F 声明可以重写从 A 继承的 F。

## 10.6.5 密封方法

当实例方法声明包含 `sealed` 修饰符时，该方法称为密封方法。如果实例方法声明包含 `sealed` 修饰符，则它还必须包含 `override` 修饰符。使用 `sealed` 修饰符可以防止派生类进一步重写该方法。

在下面的示例中：

```
using System;
class A
{
    public virtual void F() {
        Console.WriteLine("A.F");
    }

    public virtual void G() {
        Console.WriteLine("A.G");
    }
}
class B: A
{
    sealed override public void F() {
        Console.WriteLine("B.F");
    }

    override public void G() {
        Console.WriteLine("B.G");
    }
}
class C: B
{
    override public void G() {
        Console.WriteLine("C.G");
    }
}
```

B 类提供了两个重写方法：一个带有 `sealed` 修饰符的 F 方法，以及一个不带该修饰符的 G 方法。B 类使用 `sealed` 修饰符，阻止了 C 类进一步重写 F。

> **CHRIS SELLS** 当我想从一个类派生时，如果该类是密封的，或者其中某个方法是密封的，就会让我非常抓狂，因为这些限制会限制我使用该类的方式。
>
> 当我想构建一个基类时，我希望它尽可能受到限制，这样我就可以测试自己希望支持的各种派生场景。我不想被迫支持某些客户做出的、而我从未打算支持的疯狂用法。
>
> 与软件设计中的所有事情一样，使用 `sealed` 修饰符需要权衡。我通常会避免使用 `sealed` 关键字，除非确实必须使用它。如果客户做出疯狂的事情，那也正是让一切变得有趣的地方。

