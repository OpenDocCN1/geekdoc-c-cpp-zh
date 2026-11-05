
## 论文标题

这是论文摘要部分，描述了研究的主要内容和结论。摘要通常简明扼要地概括全文。

关键词: 文档提取; 图像识别; JSON

### 引言

引言部分介绍了研究背景、目的和意义。

- 列表项 1
- 列表项 2
- 列表项 3

| 列1 | 列2 | 列3 |
| --- | --- | --- |
| A1 | B1 | C1 |
| A2 | B2 | C2 |
| A3 | B3 | C3 |

### 结论

总结部分给出研究的结论和未来展望。

> 这是一段引用文字。

![](img/541c03e86b4ea7cc5306c6c5cd0d4b48_387_0.png)

在执行重载解析时会被考虑，因此第一次和第三次方法调用从而选择常规方法。当一个类声明了一个带参数数组的方法时，同时包含一些展开形式作为常规方法并不罕见。通过这样做，可以避免在调用带参数数组的方法的展开形式时发生的数组实例分配。

*示例结束*

数组是引用类型，因此为参数数组传递的值可以为 null。

示例：示例：

```
using System;

class Test
{
    void F(params string[] array) => Console.WriteLine(array == null);

    static void Main()
    {
        F(null);
        F((string) null);
    }
}
```

输出如下：

True
False

第二次调用产生 False，因为它等价于 F(new string[] { null })，并传递一个包含单个 null 引用的数组。

*示例结束*

当参数数组的类型为 object[] 时，方法常规形式与单个 object 参数的展开形式之间会产生潜在的歧义。产生歧义的原因是 object[] 本身可以隐式转换为 object 类型。然而，这种歧义并不会造成问题，因为如果需要，可以通过插入强制转换来解决。

示例：示例

```
using System;

class Test
{
    static void F(params object[] args)
    {
        foreach (object o in args)
        {
            Console.Write(o.GetType().FullName);
            Console.Write(" ");
        }
        Console.WriteLine();
    }

    static void Main()
    {
object[] a = {1, "Hello", 123.456};
object o = a;
F(a);
F((object)a);
F(o);
F(((object[])o));
}
```

输出如下

```
System.Int32 System.String System.Double
System.Object[]
System.Object[]
System.Int32 System.String System.Double
```

在 F 的第一次和最后一次调用中，F 的常规形式适用，因为参数类型到参数类型的隐式转换存在（两者均为 object[] 类型）。因此，重载解析选择 F 的常规形式，并且参数作为常规值参数传递。在第二次和第三次调用中，F 的常规形式不适用，因为参数类型到参数类型的隐式转换不存在（object 类型无法隐式转换为 object[] 类型）。然而，F 的展开形式适用，因此被重载解析选中。结果是，调用时创建了一个包含一个元素的 object[]，并且数组的单个元素被初始化为给定的参数值（它本身是对 object[] 的引用）。

*示例结束*

## 14.6.3 静态方法和实例方法

当方法声明包含 static 修饰符时，该方法被称为静态方法。当没有 static 修饰符时，该方法被称为实例方法。

静态方法不操作特定实例，并且在静态方法中引用 this 会导致编译时错误。

实例方法操作类的给定实例，并且该实例可以作为 this（§11.7.12）访问。

静态成员和实例成员之间的差异在 §14.3.8 中进一步讨论。

## 14.6.4 虚拟方法

- 在绑定时，对 C、N 和 A 应用重载解析，以从 C 中声明并继承的方法集中选择特定的方法 M。这在 §11.7.8.2 中描述。
- 然后在运行时：
  - 如果 M 是非虚拟方法，则调用 M。
  - 否则，M 是虚拟方法，并且相对于 R 的 M 的最派生实现被调用。

对于在类中声明或继承的每个虚拟方法，相对于该类都存在该方法的 **最派生实现**。相对于类 R 的虚拟方法 M 的 **最派生实现** 如下确定：

- 如果 R 包含 M 的引入虚拟声明，则这是相对于 R 的 M 的最派生实现。
- 否则，如果 R 包含 M 的重写，则这是相对于 R 的 M 的最派生实现。
- 否则，相对于 R 的 M 的最派生实现与相对于 R 的直接基类的 M 的最派生实现相同。

*示例：* 下面的示例说明了虚拟方法与非虚拟方法之间的差异：

```csharp
using System;

class A
{
    public void F() => Console.WriteLine("A.F");
    public virtual void G() => Console.WriteLine("A.G");
}

class B : A
{
    public new void F() => Console.WriteLine("B.F");
    public override void G() => Console.WriteLine("B.G");
}

class Test
{
    static void Main()
    {
        B b = new B();
        A a = b;
        a.F();
        b.F();
        a.G();
        b.G();
    }
}
```

在示例中，A 引入了一个非虚拟方法 F 和一个虚拟方法 G。类 B 引入了一个新的非虚拟方法 F，从而隐藏了继承的 F，并且还重写了继承的方法 G。示例产生的输出为：

- A.F
- B.F
- B.G
- B.G

请注意，语句 a.G() 调用的是 B.G，而不是 A.G。这是因为实例的运行时类型（即 B），而不是实例的编译时类型（即 A），决定了要调用的实际方法实现。

示例结束

因为方法允许隐藏继承的方法，所以一个类可能包含多个具有相同签名的虚拟方法。这不会产生歧义问题，因为除最派生方法之外的所有方法都被隐藏。

示例：在下面的代码中

```
using System;

class A
{
    public virtual void F() => Console.WriteLine("A.F");
}

class B : A
{
    public override void F() => Console.WriteLine("B.F");
}

class C : B
{
    public new virtual void F() => Console.WriteLine("C.F");
}

class D : C
{
    public override void F() => Console.WriteLine("D.F");
}

class Test
{
    static void Main()
    {
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

C 和 D 类包含两个具有相同签名的虚拟方法：一个由 A 引入，一个由 C 引入。C 引入的方法隐藏了从 A 继承的方法。因此，

D 中的重写声明重写了 C 引入的方法，并且 D 不可能重写 A 引入的方法。示例产生的输出为：

B.F
B.F
D.F
D.F

请注意，可以通过通过方法未被隐藏的较少派生类型访问 D 的实例来调用隐藏的虚拟方法。

示例结束

## 14.6.5 重写方法

当实例方法声明包含 override 修饰符时，该方法被称为重写方法。重写方法重写具有相同签名的继承虚拟方法。虚拟方法声明引入了新方法，而重写方法声明通过提供该方法的新实现来特化已存在的继承虚拟方法。

被重写声明重写的方法称为被重写的基方法。对于在类 C 中声明的重写方法 M，被重写的基方法是通过检查 C 的每个基类来确定的，从 C 的直接基类开始，继续每个后续直接基类，直到在给定的基类类型中至少定位到一个在类型参数替换后具有与 M 相同签名的可访问方法为止。为了定位被重写的基方法，如果方法是 public、protected、protected internal，或者是 internal 且在与 C 相同的程序中声明，则认为该方法是可访问的。

除非以下所有条件都为重写声明为真，否则会发生编译时错误：

- 可以按照上述描述定位被重写的基方法。
- 只有一个这样的被重写的基方法。此限制仅在基类类型为构造类型时才有效，其中类型参数的替换使两个方法的签名相同。
- 被重写的基方法是一个虚拟、抽象或重写方法。换句话说，被重写的基方法不能是静态或非虚拟的。
- 被重写的基方法不是密封方法。
- 被重写基方法的返回类型与重写方法之间存在恒等转换。
- 重写声明和被重写的基方法具有相同的声明可访问性。换句话说，重写声明不能更改虚拟方法的可访问性。然而，如果被重写的基方法是 protected internal 并且在与包含重写声明的程序集不同的程序集中声明，则重写声明的声明可访问性应为 protected。
- 重写声明不指定任何 type_parameter_constraints_clauses。相反，约束从被重写的基方法继承。被重写方法中的类型参数约束可能被继承约束中的类型参数替换。这可能导致在显式指定时无效的约束，例如值类型或密封类型。

示例：下面演示了泛型类的重写规则的工作方式：
