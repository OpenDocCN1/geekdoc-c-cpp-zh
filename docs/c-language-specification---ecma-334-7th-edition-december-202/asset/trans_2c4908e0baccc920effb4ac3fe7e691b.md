

等同于以下声明：

```
public class Point
{
    private int x;
    private int y;

    public int X { get { return x; } set { x = value; } }
    public int Y { get { return y; } set { y = value; } }
}
```

示例结束

示例：在以下代码中

```
public class ReadOnlyPoint
{
    public int X { get; }
    public int Y { get; }

    public ReadOnlyPoint(int x, int y)
    {
        X = x;
        Y = y;
    }
}
```

等同于以下声明：

```
public class ReadOnlyPoint
{
    private readonly int __x;
    private readonly int __y;
    public int X { get { return __x; } }
    public int Y { get { return __y; } }

    public ReadOnlyPoint(int x, int y)
    {
        __x = x;
        __y = y;
    }
}
```

对只读字段的赋值是有效的，因为这些赋值发生在构造函数内。

示例结束

尽管后备字段是隐藏的，但可以通过自动实现属性的 property_declaration（§15.7.1）将面向字段的特性直接应用于该字段。

示例：以下代码

```
[Serializable]
public class Foo
{
    [field: NonSerialized]
    public string MySecret { get; set; }
}
```

会使字段目标特性 NonSerialized 应用于编译器生成的后备字段，就像代码编写如下所示：

```
[Serializable]
public class Foo
{
    [NonSerialized]
    private string _mySecretBackingField;
    public string MySecret
    {
        get { return _mySecretBackingField; }
        set { _mySecretBackingField = value; }
    }
}
```

*示例结束*

## 15.7.5 可访问性

如果访问器具有 accessor_modifier，则访问器的可访问域（§7.5.3）使用 accessor_modifier 的声明可访问性来确定。如果访问器没有 accessor_modifier，则访问器的可访问域根据属性或索引器的声明可访问性确定。

accessor_modifier 的存在绝不会影响成员查找（§12.5）或重载决策（§12.6.4）。属性或索引器上的修饰符始终决定绑定到哪个属性或索引器，而与访问的上下文无关。

一旦选定了特定的非 ref 值属性或非 ref 值索引器，就会使用所涉及的特定访问器的可访问域来确定该用法是否有效：

- 如果该用法是作为值（§12.2.2），则 get 访问器必须存在且可访问。
- 如果该用法是作为简单赋值（§12.21.2）的目标，则 set 访问器必须存在且可访问。
- 如果该用法是作为复合赋值（§12.21.4）的目标，或作为 ++ 或 -- 运算符（§12.8.15、§12.9.6）的目标，则 get 访问器和 set 访问器都必须存在且可访问。

*示例：*在以下示例中，属性 A.Text 被属性 B.Text 隐藏，即使在仅调用 set 访问器的上下文中也是如此。相反，类 M 无法访问属性 B.Count，因此改用可访问的属性 A.Count。

```
class A
{
    public string Text
    {
        get => "hello";
        set { }
    }

    public int Count
    {
        get => 5;
        set { }
    }
}
```

*示例结束*

## 15.7.6 虚拟、密封、重写和抽象访问器

*注意：*本条款适用于属性（§15.7）和索引器（§15.9）。本条款按属性来表述；当针对索引器阅读时，请将 property/properties 替换为 indexer/indexers，并查阅 §15.9.2 中给出的属性和索引器之间的差异列表。*注意结束*

虚拟属性声明指定该属性的访问器是虚拟的。virtual 修饰符适用于属性的所有非私有访问器。当虚拟属性的访问器具有 private accessor_modifier 时，该私有访问器隐式地不是虚拟的。

抽象属性声明指定该属性的访问器是虚拟的，但不提供访问器的实际实现。相反，非抽象派生类必须通过重写该属性来为访问器提供自己的实现。由于抽象属性声明的访问器不提供实际实现，其 accessor_body 仅由一个分号组成。抽象属性不得具有私有访问器。

同时包含 abstract 和 override 修饰符的属性声明指定该属性是抽象的，并重写基属性。此类属性的访问器也是抽象的。

抽象属性声明只允许在抽象类（§15.2.2.2）中。继承的虚拟属性的访问器可以在派生类中通过包含指定 override 指令的属性声明来重写。这称为重写属性声明。重写属性声明不声明新属性。相反，它只是特化现有虚拟属性的访问器实现。

override 声明和被重写的基属性必须具有相同的声明可访问性。换句话说，override 声明不得更改基属性的可访问性。但是，如果被重写的基属性是 protected internal，并且它声明在不同于包含 override 声明的程序集的程序集中，则 override 声明的声明可访问性应为 protected。如果继承的属性只有一个访问器（即，如果继承的属性是只读或只写的），则重写属性应仅包含该访问器。如果继承的属性包含两个访问器（即，如果继承的属性是读写的），则重写属性可以包含单个访问器或两个访问器。重写属性和继承属性的类型之间必须存在恒等转换。

重写属性声明可以包含 sealed 修饰符。使用此修饰符可防止派生类进一步重写该属性。密封属性的访问器也是密封的。

除了声明和调用语法上的差异外，virtual、sealed、override 和 abstract 访问器的行为与 virtual、sealed、override 和 abstract 方法完全相同。具体而言，§15.6.4、§15.6.5、§15.6.6 和 §15.6.7 中描述的规则适用，就像访问器是对应形式的方法一样：

- get 访问器对应于无参数方法，其返回值为属性类型，并具有与包含属性相同的修饰符。
- set 访问器对应于具有一个属性类型的值参数、void 返回类型以及与包含属性相同修饰符的方法。

*示例：*在以下代码中

```
abstract class A
{
    int y;

    public virtual int X
    {
        get => 0;
    }

    public virtual int Y
    {
        get => y;
        set => y = value;
    }

    public abstract int Z { get; set; }
}
```

X 是虚拟只读属性，Y 是虚拟读写属性，Z 是抽象读写属性。由于 Z 是抽象的，包含类 A 也必须声明为抽象。

下面展示了从 A 派生的类：

```
class B : A
{
    int z;

    public override int X
    {
        get => base.X + 1;
    }

    public override int Y
    {
        set => base.Y = value < 0 ? 0: value;
    }

    public override int Z
    {
        get => z;
        set => z = value;
    }
}
```

在此，X、Y 和 Z 的声明是重写属性声明。每个属性声明都完全匹配对应继承属性的可访问性修饰符、类型和名称。X 的 get 访问器和 Y 的 set 访问器使用 base 关键字访问继承的访问器。Z 的声明重写了两个抽象访问器——因此，B 中没有未实现的抽象函数成员，B 可以是非抽象类。

示例结束

当属性声明为 override 时，任何被重写的访问器都必须可由重写代码访问。此外，属性或索引器本身以及访问器的声明可访问性都必须与被重写成员和访问器的声明可访问性匹配。

示例：

```
public class B
{
```

