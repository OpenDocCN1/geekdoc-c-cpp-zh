
```
property_body
: '{' accessor_declarations '}' property_initializer?
| '=>' expression ';'
;
```

```
property_initializer
: '=' variable_initializer ';'
;
```

unsafe_modifier（§22.2）仅在 unsafe 代码（§22）中可用。

property_declaration 可以包含一组特性（§21）以及四个访问修饰符（§14.3.6）与 new（§14.3.5）、static（§14.7.2）、virtual（§14.6.4、§14.7.6）、override（§14.6.5、§14.7.6）、sealed（§14.6.6）、abstract（§14.6.7、§14.7.6）和 extern（§14.6.8）修饰符的有效组合。

就修饰符的有效组合而言，属性声明遵循与方法声明（§14.6）相同的规则。

属性声明的类型指定该声明所引入属性的类型，而 member_name（§14.6.1）指定属性的名称。除非该属性是显式接口成员实现，否则 member_name 就是一个标识符。对于显式接口成员实现（§17.6.2），member_name 由一个 interface_type、后跟一个“.”和一个标识符组成。

属性的类型应至少与属性本身具有相同的可访问性（§7.5.5）。

property_body 可以由访问器体或表达式体组成。在访问器体中，accessor_declarations（应包含在“{”和“}”标记中）声明属性的访问器（§14.7.3）。访问器指定与读取和写入该属性关联的可执行语句。

由 => 后跟表达式 E 和一个分号组成的表达式体，完全等价于语句体 { get { return E; } }，因此只能用于指定只读属性，其中 get 访问器的结果由单个表达式给出。

只能为自动实现的属性（§14.7.4）提供 property_initializer，它使此类属性的基础字段用表达式给定的值进行初始化。

尽管访问属性的语法与访问字段的语法相同，但属性不被归类为变量。因此，不能将属性作为 ref 或 out 实参传递。

当属性声明包含 extern 修饰符时，该属性称为外部属性。由于外部属性声明不提供实际实现，其每个 accessor_declarations 都由一个分号组成。

## 14.7.2 静态属性和实例属性

当属性声明包含 static 修饰符时，该属性称为静态属性。当不存在 static 修饰符时，该属性称为实例属性。

静态属性不与特定实例关联，在静态属性的访问器中引用 this 会导致编译时错误。

实例属性与类的给定实例关联，并且可以在该属性的访问器中通过 this（§11.7.12）访问该实例。

静态成员和实例成员之间的差异在 §14.3.8 中进一步讨论。

## 14.7.3 访问器

属性的 accessor_declarations 指定与读取和写入该属性关联的可执行语句。

```
accessor_declarations
  : get_accessor_declaration set_accessor_declaration?
  | set_accessor_declaration get_accessor_declaration?
  ;

get_accessor_declaration
  : attributes? accessor_modifier? 'get' accessor_body
  ;

set_accessor_declaration
  : attributes? accessor_modifier? 'set' accessor_body
  ;

accessor_modifier
  : 'protected'
  | 'internal'
  | 'private'
  | 'protected' 'internal'
  | 'internal' 'protected'
  ;

accessor_body
  : block
  | ';'
  ;
```

访问器声明由一个 get_accessor_declaration、一个 set_accessor_declaration 或二者组成。每个访问器声明由可选特性、可选 accessor_modifier、标记 get 或 set，以及后跟的 accessor_body 组成。

accessor_modifier 的使用受以下限制约束：

- accessor_modifier 不得在接口或显式接口成员实现中使用。
- 对于没有 override 修饰符的属性或索引器，仅当该属性或索引器同时具有 get 和 set 访问器时，才允许使用 accessor_modifier，并且只允许在其中一访问器上使用。
- 对于包含 override 修饰符的属性或索引器，访问器应匹配被重写访问器的 accessor_modifier（如果有）。
- accessor_modifier 声明的可访问性应严格比属性或索引器本身声明的可访问性更具限制性。具体而言：
  - 如果属性或索引器的声明可访问性为 public，则 accessor_modifier 可以是 protected internal、internal、protected 或 private。
  - 如果属性或索引器的声明可访问性为 protected internal，则 accessor_modifier 可以是 internal、protected 或 private。

```
    }
    }
    Repaint();
    }
}

public override void Paint(Graphics g, Rectangle r)
{
    // Painting code goes here
}
```

Button 控件声明一个公共的 Caption 属性。Caption 属性的 get 访问器返回存储在私有 caption 字段中的字符串。set 访问器检查新值是否与当前值不同，如果不同，则存储新值并重绘控件。属性通常遵循上面所示的模式：get 访问器只返回存储在私有字段中的值，而 set 访问器修改该私有字段，然后执行完全更新对象状态所需的任何附加操作。给定上面的 Button 类，以下是对 Caption 属性的使用示例：

```
Button okButton = new Button();
okButton.Caption = "OK"; // Invokes set accessor
string s = okButton.Caption; // Invokes get accessor
```

这里，通过向属性赋值来调用 set 访问器，而通过在表达式中引用属性来调用 get 访问器。

*示例结束*

属性的 get 和 set 访问器不是不同的成员，并且无法单独声明属性的访问器。

示例：下面的示例

```
class A
{
    private string name;

    // Error, duplicate member name
    public string Name
    {
        get => name;
    }

    // Error, duplicate member name
    public string Name
    {
        set => name = value;
    }
}
```

并未声明单个读写属性。相反，它声明了两个同名属性，一个只读，一个只写。由于同一个类中声明的两个成员不能具有相同名称，该示例会导致编译时错误发生。

*示例结束*

当派生类声明与继承属性同名的属性时，派生属性在读取和写入两方面都会隐藏继承属性。

示例：在以下代码中

```
class A
{
    public int P
    {
        set {...}
    }
}

class B : A
{
    public new int P
    {
        get {...}
    }
}
```

B 中的 P 属性在读取和写入两方面都会隐藏 A 中的 P 属性。因此，在以下语句中

```
B b = new B();
b.P = 1;    // Error, B.P is read-only
((A)b).P = 1;  // Ok, reference to A.P
```

对 b.P 的赋值会导致报告编译时错误，因为 B 中的只读 P 属性隐藏了 A 中的只写 P 属性。但请注意，可以使用强制转换来访问被隐藏的 P 属性。

示例结束

与公共字段不同，属性在对象的内部状态与其公共接口之间提供分离。

示例：考虑以下代码，它使用 Point 结构表示位置：

```
class Label
{
    private int x, y;
    private string caption;

    public Label(int x, int y, string caption)
    {
        this.x = x;
        this.y = y;
        this.caption = caption;
    }

    public int X => x;
    public int Y => y;
    public Point Location => new Point(x, y);
    public string Caption => caption;
}
```

这里，Label 类使用两个 int 字段 x 和 y 来存储其位置。该位置通过 X 和 Y 属性以及 Point 类型的 Location 属性公开。如果在 Label 的未来版本中，在内部将位置存储为 Point 变得更方便，则可以在不影响类公共接口的情况下进行更改：
