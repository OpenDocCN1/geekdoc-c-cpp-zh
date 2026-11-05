

抽象属性声明仅允许出现在抽象类中（§15.2.2.2）。在派生类中，可以通过包含指定 override 指令的属性声明来重写继承的虚拟属性的访问器。这称为重写属性声明。重写属性声明不会声明新属性，而只是对现有虚拟属性的访问器实现进行特化。

重写属性声明应指定与继承属性完全相同的可访问性修饰符和名称，并且重写属性的类型与继承属性的类型之间应存在标识转换。如果继承属性只有一个访问器（即继承属性是只读或只写的），则重写属性只能包含该访问器。如果继承属性包含两个访问器（即继承属性是读写的），则重写属性可以包含单个访问器，也可以同时包含两个访问器。

重写属性声明可以包含 sealed 修饰符。使用该修饰符可防止派生类进一步重写该属性。sealed 属性的访问器也是 sealed 的。

除了声明和调用语法上的差异之外，virtual、sealed、override 和 abstract 访问器的行为与 virtual、sealed、override 和 abstract 方法完全相同。具体来说，§15.6.4、§15.6.5、§15.6.6 和 §15.6.7 中描述的规则同样适用，就好像访问器是相应形式的方法一样：

-   get 访问器对应于一个无参数方法，返回值为属性类型，并具有与所属属性相同的修饰符。
-   set 访问器对应于一个具有单个属性类型值参数、void 返回类型，并具有与所属属性相同的修饰符的方法。

[示例：在以下代码中

```
abstract class A
{
    int y;
    public virtual int X {
        get { return 0; }
    }
    public virtual int Y {
        get { return y; }
        set { y = value; }
    }
    public abstract int Z { get; set; }
}
```

X 是虚拟只读属性，Y 是虚拟读写属性，Z 是抽象读写属性。由于 Z 是抽象的，包含类 A 也必须声明为抽象。

下面显示了从 A 派生的类：

```
class B: A
{
    int z;
    public override int X {
        get { return base.X + 1; }
    }
    public override int Y {
        set { base.Y = value < 0 ? 0 : value; }
    }
    public override int Z {
        get { return z; }
        set { z = value; }
    }
}
```

这里，X、Y 和 Z 的声明都是重写属性声明。每个属性声明都与相应继承属性的可访问性修饰符、类型和名称完全匹配。X 的 get 访问器和 Y 的 set 访问器使用 base 关键字来访问继承的访问器。Z 的声明重写了两个抽象访问器——因此，B 中没有未实现的抽象函数成员，B 允许是非抽象类。示例结束]

当属性被声明为 override 时，任何被重写的访问器都应能被重写代码访问。此外，属性或索引器本身以及访问器的声明可访问性，都必须与被重写的成员和访问器的声明可访问性匹配。

[示例：

```
public class B
{
    public virtual int P {
        protected set {...}
        get {...}
    }
}
public class D: B
{
    public override int P {
        protected set {...}    // Must specify protected here
        get {...}              // Must not have a modifier here
    }
}
```

示例结束]

## 15.8 事件

### 15.8.1 概述

事件是一种成员，它使对象或类能够提供通知。客户端可以通过提供事件处理程序来为事件附加可执行代码。

事件使用事件声明（event-declarations）声明：

```
event-declaration:
    attributesopt event-modifiersopt event type variable-declarators ;
    attributesopt event-modifiersopt event type member-name
    { event-accessor-declarations }

event-modifiers:
    event-modifier
    event-modifiers event-modifier

event-modifier:
    new
    public
    protected
    internal
    private
    static
    virtual
    sealed
    override
    abstract
    extern

event-accessor-declarations:
    add-accessor-declaration remove-accessor-declaration
    remove-accessor-declaration add-accessor-declaration

add-accessor-declaration:
    attributesopt add block

remove-accessor-declaration:
    attributesopt remove block
```

事件声明可以包含一组特性（§22）以及四个访问修饰符（§15.3.6）、new（§15.3.5）、static（§15.6.3, §15.8.4）、virtual（§15.6.4, §15.8.5）、override（§15.6.5, §15.8.5）、sealed（§15.6.6）、abstract（§15.6.7, §15.8.5）和 extern（§15.6.8）修饰符的有效组合。

在修饰符的有效组合方面，事件声明遵循与方法声明（§15.6）相同的规则。

事件声明的类型应为委托类型（§9.2.8），并且该委托类型的可访问性应至少与事件本身（§8.5.5）相同。

事件声明可以包含事件访问器声明（event-accessor-declarations）。但是，如果未包含，对于非 extern、非 abstract 事件，编译器应自动提供它们（§15.8.2）；对于 extern 事件，访问器由外部提供。

省略 event-accessor-declarations 的事件声明会定义一个或多个事件——每个变量声明符（variable-declarator）对应一个事件。特性和修饰符适用于此类事件声明所声明的所有成员。

事件声明同时包含 abstract 修饰符和 event-accessor-declarations 是编译时错误。

当事件声明包含 extern 修饰符时，该事件称为外部事件。由于外部事件声明不提供实际实现，因此它同时包含 extern 修饰符和 event-accessor-declarations 是错误的。

带有 abstract 或 extern 修饰符的事件声明的变量声明符包含变量初始化器是编译时错误。

事件可以用作 += 和 -= 运算符的左操作数。这两个运算符分别用于向事件附加事件处理程序或从事件移除事件处理程序，并且事件的访问修饰符控制允许此类操作的上下文。

对于声明该事件的类型之外的代码，允许对事件执行的操作只有 += 和 -=。因此，此类代码虽然可以为事件添加和移除处理程序，但不能直接获取或修改底层的事件处理程序列表。

在 x += y 或 x -= y 形式的操作中，当 x 是事件时，操作结果的类型为 void（§12.18.4）（而不是像对非事件类型定义的其他 += 和 -= 运算符那样，具有 x 的类型，并返回赋值后 x 的值）。这可以防止外部代码间接检查事件的底层委托。

[示例：以下示例演示如何将事件处理程序附加到 Button 类的实例：]

```
public delegate void EventHandler(object sender, EventArgs e);
public class Button: Control
{
    public event EventHandler Click;
}
public class LoginDialog: Form
{
    Button okButton;
    Button cancelButton;

    public LoginDialog() {
        okButton = new Button(...);
        okButton.Click += new EventHandler(OkButtonClick);
        cancelButton = new Button(...);
        cancelButton.Click += new EventHandler(CancelButtonClick);
    }
    void OkButtonClick(object sender, EventArgs e) {
        // Handle okButton.Click event
    }
    void CancelButtonClick(object sender, EventArgs e) {
        // Handle cancelButton.Click event
    }
}
```

这里，LoginDialog 实例构造函数创建了两个 Button 实例，并将事件处理程序附加到 Click 事件。示例结束

### 15.8.2 类似字段的事件

在包含事件声明的类或结构体的程序文本中，某些事件可以像字段一样使用。要以这种方式使用，事件不得是 abstract 或 extern，也不得显式包含 event-accessor-declarations。此类事件可以在任何允许字段的上下文中使用。该字段包含一个委托（§20），该委托引用已添加到事件的事件处理程序列表。如果未添加任何事件处理程序，该字段包含 null。

[示例：在以下代码中

```
public delegate void EventHandler(object sender, EventArgs e);
public class Button: Control
{
    public event EventHandler Click;
    protected void OnClick(EventArgs e) {
        EventHandler handler = Click;
        if (handler != null)
            handler(this, e);
    }
    public void Reset() {
        Click = null;
    }
}
```

在 Button 类中，Click 被用作字段。如示例所示，该字段可以被检查、修改，并用于委托调用表达式。Button 类中的 OnClick 方法“引发”Click 事件。引发事件的概念与调用事件所表示的委托完全等价——因此，没有用于引发事件的特殊语言构造。请注意，委托调用之前会进行一项检查以确保委托非 null，并且该检查是在局部副本上进行的，以确保线程安全。

在 Button 类声明之外，Click 成员只能用在 += 和 -= 运算符的左侧，例如 `b.Click += new EventHandler(...);` 会将委托追加到 Click 事件的调用列表，而 `b.Click -= new EventHandler(...);` 会将委托从 Click 事件的调用列表中移除。示例结束

在编译类似字段的事件时，编译器会自动创建用于保存委托的存储，并为事件创建访问器，以便向委托字段添加或移除事件处理程序。添加和移除操作是线程安全的，并且可以（但不是必须）在持有锁的情况下执行。

