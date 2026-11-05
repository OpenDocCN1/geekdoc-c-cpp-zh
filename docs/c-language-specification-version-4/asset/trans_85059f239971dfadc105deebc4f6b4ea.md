
## 10.7.1 静态属性和实例属性

当属性声明包含 static 修饰符时，该属性称为静态属性。当不存在 static 修饰符时，该属性称为实例属性。

静态属性不与特定实例关联，在静态属性的访问器中引用 this 会导致编译时错误。

实例属性与类的给定实例关联，并且在该属性的访问器中可以通过 this（§7.6.7）访问该实例。

当在形式为 E.M 的成员访问（§7.6.4）中引用属性时，如果 M 是静态属性，则 E 必须表示包含 M 的类型；如果 M 是实例属性，则 E 必须表示包含 M 的类型的实例。

静态成员和实例成员之间的差异将在 §10.3.7 中进一步讨论。

## 10.7.2 访问器

属性的访问器声明指定与读取和写入该属性相关联的可执行语句。

```
accessor-declarations:
    get-accessor-declaration  set-accessor-declaration_opt
    set-accessor-declaration  get-accessor-declaration_opt

get-accessor-declaration:
    attributes_opt accessor-modifier_opt get accessor-body

set-accessor-declaration:
    attributes_opt accessor-modifier_opt set accessor-body

accessor-modifier:
    protected
    internal
    private
    protected internal
    internal protected

accessor-body:
    block
    ;
```

访问器声明由 get 访问器声明、set 访问器声明或两者组成。每个访问器声明由标记 get 或 set 后跟可选的访问器修饰符和访问器体组成。

访问器修饰符的使用受以下限制约束：

- 访问器修饰符不得用于接口或显式接口成员实现中。
- 对于没有 override 修饰符的属性或索引器，仅当该属性或索引器同时具有 get 和 set 访问器时才允许使用访问器修饰符，并且只能用于其中一个访问器。
- 对于包含 override 修饰符的属性或索引器，访问器必须与被重写访问器的访问器修饰符（如果有）匹配。
- 访问器修饰符声明的可访问性必须严格比属性或索引器本身声明的可访问性限制更严格。具体而言：
  - 如果属性或索引器声明的可访问性为 public，则访问器修饰符可以为 protected internal、internal、protected 或 private。
  - 如果属性或索引器声明的可访问性为 `protected internal`，则 *访问器修饰符* 可以为 `internal`、`protected` 或 `private`。
  - 如果属性或索引器声明的可访问性为 `internal` 或 `protected`，则 *访问器修饰符* 必须为 `private`。
  - 如果属性或索引器声明的可访问性为 `private`，则不得使用 *访问器修饰符*。

对于抽象属性和 extern 属性，所指定的每个访问器的 *访问器体* 只是一个分号。非抽象、非 extern 属性可以是 *自动实现的属性*，在这种情况下必须同时提供 get 和 set 访问器，且两者的体均为分号（§10.7.3）。对于任何其他非抽象、非 extern 属性的访问器，*访问器体* 是一个 *块*，它指定在调用相应访问器时要执行的语句。

get 访问器对应于一个无参数方法，其返回值为属性类型。除非作为赋值目标，否则当在表达式中引用属性时，会调用该属性的 get 访问器来计算属性值（§7.1.1）。get 访问器的主体必须符合 §10.6.10 中所述的值返回方法规则。特别是，get 访问器主体中的所有 return 语句都必须指定一个可隐式转换为属性类型的表达式。此外，get 访问器的端点必须不可到达。

set 访问器对应于一个方法，该方法具有一个属性类型的值参数和 void 返回类型。set 访问器的隐式参数始终名为 value。当属性作为赋值目标（§7.17）或作为 ++ 或 -- 的操作数（§7.6.9、§7.7.5）被引用时，会使用一个提供新值的参数（其值为赋值右侧的值或 ++ 或 -- 运算符的操作数）调用 set 访问器（§7.17.1）。set 访问器的主体必须符合 §10.6.10 中所述的 void 方法规则。特别是，set 访问器主体中的 return 语句不得指定表达式。由于 set 访问器隐式具有名为 value 的参数，因此 set 访问器中的局部变量或常量声明使用该名称会导致编译时错误。

根据是否存在 get 和 set 访问器，属性分类如下：

- 同时包含 get 访问器和 set 访问器的属性称为 *读写* 属性。
- 只有 get 访问器的属性称为 *只读* 属性。只读属性作为赋值目标会导致编译时错误。
- 只有 set 访问器的属性称为 *只写* 属性。除非作为赋值目标，否则在表达式中引用只写属性会导致编译时错误。

在以下示例中

```
public class Button: Control
{
    private string caption;
    public string Caption {
        get {
            return caption;
        }
        set {
            if (caption != value) {
                caption = value;
                Repaint();
            }
        }
    }
    public override void Paint(Graphics g, Rectangle r) { // Painting code goes here
    }
}
```

Button 控件声明了一个 public 的 Caption 属性。Caption 属性的 get 访问器返回存储在私有 caption 字段中的字符串。set 访问器检查新值是否不同于当前值，如果不同，则存储新值并重新绘制控件。属性通常遵循上面所示的模式：get 访问器仅返回存储在私有字段中的值，set 访问器修改该私有字段，然后执行完全更新对象状态所需的任何附加操作。

给定上面的 Button 类，以下是对 Caption 属性的使用示例：

```
Button okButton = new Button(); // Invokes set accessor
okButton.Caption = "OK"; // Invokes set accessor
string s = okButton.Caption; // Invokes get accessor
```

这里，通过向属性赋值来调用 set 访问器，通过在表达式中引用属性来调用 get 访问器。

属性的 get 和 set 访问器不是不同的成员，并且不可能单独声明属性的访问器。因此，读写属性的两个访问器不可能具有不同的可访问性。示例

```
class A
{
    private string name;
    public string Name {
        get { return name; } // Error, duplicate member name
    }
    public string Name {
        set { name = value; } // Error, duplicate member name
    }
}
```

并未声明单个读写属性。相反，它声明了两个同名属性，一个只读，一个只写。由于在同一类中声明的两个成员不能同名，因此该示例会导致编译时错误。

当派生类声明与继承属性同名的属性时，派生属性在读取和写入两方面都会隐藏继承属性。在示例

```
class A
{
    public int P {
        set {...}
    }
}
class B: A
{
    new public int P {
        get {...}
    }
}
```

中，B 中的 P 属性在读取和写入两方面隐藏了 A 中的 P 属性。因此，在以下语句中

```
B b = new B(); // Error, B.P is read-only
((A)b).P = 1; // Ok, reference to A.P
```
