
示例

```
public class Point {
    public int X { get; set; } // Automatically implemented
    public int Y { get; set; } // Automatically implemented
}
```

等价于以下声明：

```
public class Point {
    private int x;
    private int y;
    public int X { get { return x; } set { x = value; } }
    public int Y { get { return y; } set { y = value; } }
}
```

由于支持字段无法访问，即使在包含的类型内部，它也只能通过属性访问器进行读写。这意味着自动实现的只读或只写属性没有意义，因此不允许。可以为每个访问器设置不同的访问级别。因此，可以通过以下方式模拟具有私有支持字段的只读属性的效果：

```
public class ReadOnlyPoint {
    public int X { get; private set; }
    public int Y { get; private set; }
    public ReadOnlyPoint(int x, int y) { X = x; Y = y; }
}
```

> BILL WAGNER  虽然属性是只读的，但其底层的支持存储并不是。ReadOnlyPoint 内部的代码不必遵守不可变性的规则。

> JON SKEET  虽然这种行为对其他类型模拟了只读属性的效果，但它与属性（或确实是支持字段）真正只读并不相同。我希望能够指定只读属性，也许采用以下形式：
> 
> ```
> public int X { get; readonly set; }
> ```
> 
> 这段代码将产生一个只读字段；setter 的使用仅在构造函数内允许，在那里它将被编译为对支持字段的直接写入。遗憾的是，创建真正不可变类型的过程目前比创建可变类型更为冗长。

> PETER SESTOFT  自动实现的属性非常好，因为属性可以在对象初始值设定项中使用（§7.6.10.2）。对象初始值设定项对于坐标对和三元组、复数以及类似的项目——即结构体值——尤其有用。然而，通常我们更希望结构体具有不可变字段，因为它们在赋值和参数传递期间会被复制。因此，我完全支持 Jon 希望为具有自动实现访问器的只读字段提供简洁表示法的愿望，前提是 set 访问器可以在构造函数和对象初始值设定项中使用。

此限制还意味着，具有自动实现属性的结构类型的确定性赋值只能使用结构体的标准构造函数实现，因为对属性本身的赋值要求结构体已被确定性赋值。这意味着用户定义的构造函数必须调用默认构造函数。

## 10.7.4 可访问性

如果访问器具有访问器修饰符，则访问器的可访问性域（§3.5.2）使用访问器修饰符声明的可访问性确定。如果访问器没有访问器修饰符，则访问器的可访问性域由属性或索引器的声明可访问性确定。

访问器修饰符的存在永远不会影响成员查找（§7.3）或重载解析（§7.5.3）。无论访问的上下文如何，属性或索引器上的修饰符始终决定绑定到哪个属性或索引器。

一旦选择了特定的属性或索引器，就使用所涉及的特定访问器的可访问性域来确定该使用是否有效：

- 如果用作值（§7.1.1），则 get 访问器必须存在且可访问。
- 如果用作简单赋值（§7.17.1）的目标，则 set 访问器必须存在且可访问。
- 如果用作复合赋值（§7.17.2）的目标，或用作 ++ 或 -- 运算符（§7.5.9、§7.6.5）的目标，则 get 访问器和 set 访问器都必须存在且可访问。

在下面的示例中，属性 A.Text 被属性 B.Text 隐藏，即使在仅调用 set 访问器的上下文中也是如此。相比之下，属性 B.Count 对类 M 不可访问，因此改用可访问的属性 A.Count。

```
class A
{
    public string Text {
        get { return "hello"; }
        set { }
    }
    public int Count {
        get { return 5; }
        set { }
    }
}
class B : A
{
    private string text = "goodbye";
    private int count = 0;
    new public string Text {
        get { return text; }
        protected set { text = value; }
    }
    new protected int Count {
        get { return count; }
        set { count = value; }
    }
}
class M
{
    static void Main() {
        B b = new B();
        b.Count = 12;        // Calls A.Count set accessor
        int i = b.Count;     // Calls A.Count get accessor
        b.Text = "howdy";    // Error: B.Text set accessor is not accessible
        string s = b.Text;   // Calls B.Text get accessor
    }
}
```

用于实现接口的访问器不得具有访问器修饰符。如果仅使用一个访问器来实现接口，则另一个访问器可以用访问器修饰符声明：

```
public interface I
{
    string Prop { get; }
}
public class C : I
{
    public string Prop {
        get { return "April"; } // Must not have a modifier here
        internal set (...)    // Okay, because I.Prop has no set accessor
    }
}
```

## 10.7.5 虚拟、密封、重写和抽象访问器

虚拟属性声明指定属性的访问器是虚拟的。virtual 修饰符适用于读写属性的两个访问器——不可能让读写属性的仅一个访问器为虚拟。

抽象属性声明指定属性的访问器是虚拟的，但不提供访问器的实际实现。相反，非抽象派生类必须通过重写属性为访问器提供自己的实现。由于抽象属性声明的访问器不提供实际实现，其访问器体仅由一个分号组成。

包含 abstract 和 override 修饰符的属性声明指定该属性是抽象的并且重写了基属性。此类属性的访问器也是抽象的。

抽象属性声明仅允许在抽象类中（§10.1.1.1）。继承的虚拟属性的访问器可以通过包含指定 override 指令的属性声明在派生类中被重写。这称为重写属性声明。重写属性声明不会声明新属性。相反，它只是专门化现有虚拟属性的访问器的实现。

重写属性声明必须指定与继承属性完全相同的可访问性修饰符、类型和名称。如果继承的属性只有一个访问器（即继承的属性是只读或只写），则重写属性必须仅包含该访问器。如果继承的属性包含两个访问器（即继承的属性是读写），则重写属性可以包含单个访问器或两个访问器。

重写属性声明可以包含 sealed 修饰符。使用此修饰符可防止派生类进一步重写该属性。密封属性的访问器也是密封的。

除了声明和调用语法上的差异外，虚拟、密封、重写和抽象访问器的行为与虚拟、密封、重写和抽象方法完全相同。具体来说，§10.6.3、§10.6.4、§10.6.5 和 §10.6.6 中描述的规则适用于访问器作为相应形式的方法：

- get 访问器对应于一个无参数的方法，其返回值为属性类型，并且具有与包含属性相同的修饰符。
- set 访问器对应于一个具有属性类型单个值参数、void 返回类型并且具有与包含属性相同的修饰符的方法。
