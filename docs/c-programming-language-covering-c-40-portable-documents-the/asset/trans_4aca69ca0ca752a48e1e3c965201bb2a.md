
在下面的示例中

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

X 是虚只读属性，Y 是虚读写属性，Z 是抽象读写属性。由于 Z 是抽象的，包含它的类 A 也必须声明为抽象类。

从 A 派生的类如下所示：

```
class B : A
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

这里，X、Y 和 Z 的声明是重写属性声明。每个属性声明都与其对应继承属性的可访问性修饰符、类型和名称完全匹配。X 的 get 访问器和 Y 的 set 访问器使用 base 关键字来访问继承的访问器。Z 的声明重写了两个抽象访问器——因此 B 中不再有未实现的抽象函数成员，B 可以是非抽象类。

当属性声明为 override 时，任何被重写的访问器都必须可由重写代码访问。此外，属性或索引器本身以及各访问器的声明可访问性，必须与被重写成员和访问器的声明可访问性匹配。例如：

```csharp
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
        protected set {...}      // Must specify protected here
        get {...}                // Must not have a modifier here
    }
}
```

## 10.8 事件

*事件*是一种成员，它使对象或类能够提供通知。客户端可以通过提供*事件处理程序*来为事件附加可执行代码。

事件使用*事件声明*来声明：

```
event-declaration:
    attributes_opt event-modifiers_opt event type variable-declarators ;
    attributes_opt event-modifiers_opt event type member-name
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
```

```
event-accessor-declarations:
add-accessor-declaration remove-accessor-declaration
remove-accessor-declaration add-accessor-declaration
```

```
add-accessor-declaration:
attributes_opt add block
```

```
remove-accessor-declaration:
attributes_opt remove block
```

事件声明可以包含一组特性（§17）、四个访问修饰符的合法组合（§10.3.5），以及 new（§10.3.4）、static（§10.6.2）、virtual（§10.6.3）、override（§10.6.4）、sealed（§10.6.5）、abstract（§10.6.6）和 extern（§10.6.7）修饰符。

在修饰符的合法组合方面，事件声明遵循与方法声明（§10.6）相同的规则。

事件声明的类型必须是委托类型（§4.2），并且该委托类型的可访问性必须至少与事件本身相同（§3.5.4）。

事件声明可以包含事件访问器声明。但是，如果事件声明不包含它们，那么对于非 extern、非 abstract 事件，编译器会自动提供这些访问器（§10.8.1）；对于 extern 事件，访问器由外部提供。

省略事件访问器声明的事件声明会定义一个或多个事件——每个变量声明符对应一个事件。特性和修饰符适用于此类事件声明所声明的所有成员。

事件声明同时包含 abstract 修饰符和用大括号分隔的事件访问器声明，是编译时错误。

当事件声明包含 extern 修饰符时，该事件称为外部事件。由于外部事件声明不提供实际实现，因此它同时包含 extern 修饰符和事件访问器声明是错误的。

事件可以用作 += 和 -= 运算符（§7.17.3）的左操作数。这两个运算符分别用于将事件处理程序附加到事件或从事件中移除事件处理程序，而事件的访问修饰符控制允许执行此类操作的上下文。

由于 += 和 -= 是声明事件的类型之外唯一允许对事件执行的操作，外部代码可以为事件添加和移除处理程序，但不能以任何其他方式获取或修改底层的事件处理程序列表。

在 x += y 或 x -= y 形式的操作中，当 x 是事件且该引用发生在包含 x 声明的类型之外时，操作的结果具有 void 类型（而不是具有 x 的类型并携带赋值后 x 的值）。此规则禁止外部代码间接检查事件的底层委托。

下面的示例展示了如何将事件处理程序附加到 Button 类的实例：

```csharp
public delegate void EventHandler(object sender, EventArgs e);
public class Button: Control
{
    public event EventHandler Click;
}
public class LoginDialog: Form
{
    Button OkButton;
    Button CancelButton;
    public LoginDialog() {
        OkButton = new Button(...);
        OkButton.Click += new EventHandler(OkButtonClick);
        CancelButton = new Button(...);
        CancelButton.Click += new EventHandler(CancelButtonClick);
    }
    void OkButtonClick(object sender, EventArgs e) {
        // Handle OkButton.Click event
    }
    void CancelButtonClick(object sender, EventArgs e) {
        // Handle CancelButton.Click event
    }
}
```

这里，LoginDialog 实例构造函数创建两个 Button 实例，并将事件处理程序附加到 Click 事件。

> > **CHRISTIAN NAGEL** 内存泄漏常常源于错误使用事件。如果客户端对象订阅了事件但不取消订阅，并且对该客户端对象的引用不再使用，那么由于发布者仍保留引用，该客户端对象仍然无法被垃圾回收器回收。可以通过以下方式避免：(1) 当客户端对象不再使用时取消事件订阅；(2) 使用持有委托的 WeakReference 类自定义实现 add 和 remove 访问器；或 (3) 使用 WPF 中配合 IWeakEventListener 接口的弱事件模式。

> > **JON SKEET**  我倾向于把事件看作（并向别人解释成）类似于属性。它们是一对方法（add 和 remove），编译器知道如何用简写（`+=` 和 `-=`）调用它们。事件比属性限制更多，因为其类型必须是委托类型，而且必须始终同时有 add 和 remove 方法；不存在“只读属性”那样的“只添加”事件。除了这些点之外，相似性很强——然而属性通常被理解得很好，而事件却会造成大量混淆。我推测，字段式事件是这一问题的根源。

### 10.8.1 字段式事件

在包含事件声明的类或结构的程序文本中，某些事件可以像字段一样使用。要以这种方式使用，事件不能是 abstract 或 extern，并且不能显式包含事件访问器声明。此类事件可用于任何允许字段的上下文。该字段包含一个委托（§15），它引用已添加到该事件的事件处理程序列表。如果尚未添加任何事件处理程序，则该字段包含 null。

> > **JON SKEET**  如果自动实现属性从一开始就存在于 C# 中，我认为把字段式事件称为“自动实现事件”并采用如下语法会更有意义：
> >
> > ```csharp
> > public event EventHandler Click { add; remove; }
> > ```
> >
> > 这也许能减少人们对事件究竟是什么的困惑。

```
public event EventHandler Click { add; remove; }
```

在下面的示例中

```
public delegate void EventHandler(object sender, EventArgs e);
public class Button: Control
{
    public event EventHandler Click;
    protected void OnClick(EventArgs e) {
        if (Click != null) Click(this, e);
    }

    public void Reset() {
        Click = null;
    }
}
```
