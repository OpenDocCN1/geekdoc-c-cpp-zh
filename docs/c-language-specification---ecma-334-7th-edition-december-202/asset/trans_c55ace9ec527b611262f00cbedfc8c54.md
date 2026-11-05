

```
public virtual int P
{
    get {...}
    protected set {...}
}

public class D: B
{
    public override int P
    {
        get {...}    // Must not have a modifier here
        protected set {...} // Must specify protected here
    }
}
```

*示例结束*

## 15.8 事件

### 15.8.1 概述

事件是一种成员，它使对象或类能够提供通知。客户端可以通过提供事件处理程序来为事件附加可执行代码。

事件使用 event_declarations 声明：

```
event_declaration
: attributes? event_modifier* 'event' type variable_declarators ';'
| attributes? event_modifier* 'event' type member_name
    '{' event_accessor_declarations '}'
;

event_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
| 'static'
| 'virtual'
| 'sealed'
| 'override'
| 'abstract'
| 'extern'
| unsafe_modifier  // 不安全代码支持
;

event_accessor_declarations
: add_accessor_declaration remove_accessor_declaration
| remove_accessor_declaration add_accessor_declaration
;

add_accessor_declaration
: attributes? 'add' block
;
remove_accessor_declaration
: attributes? 'remove' block
;
```

unsafe_modifier（§23.2）仅在不安全代码（§23）中可用。

event_declaration 可以包含一组特性（§22）以及任何允许的声明可访问性（§15.3.6）、new（§15.3.5）、static（§15.6.3、§15.8.4）、virtual（§15.6.4、§15.8.5）、override（§15.6.5、§15.8.5）、sealed（§15.6.6）、abstract（§15.6.7、§15.8.5）和 extern（§15.6.8）修饰符。

事件声明在修饰符的有效组合方面遵循与方法声明（§15.6）相同的规则。

事件声明的类型应为 delegate_type（§8.2.8），并且该 delegate_type 的可访问性至少应与事件本身相同（§7.5.5）。

事件声明可以包含 event_accessor_declarations。但是，如果未包含，则对于非 extern、非 abstract 的事件，编译器应自动提供这些访问器（§15.8.2）；对于 extern 事件，访问器由外部提供。

省略 event_accessor_declarations 的事件声明定义一个或多个事件——每个 variable_declarators 对应一个事件。特性和修饰符适用于此类 event_declaration 声明的所有成员。

如果 event_declaration 同时包含 abstract 修饰符和 event_accessor_declarations，则属于编译时错误。

当事件声明包含 extern 修饰符时，该事件称为外部事件。由于外部事件声明不提供实际实现，因此同时包含 extern 修饰符和 event_accessor_declarations 是错误的。

如果带有 abstract 或 external 修饰符的事件声明的 variable_initializer 包含变量初始化器，则属于编译时错误。

事件可以用作 `+=` 和 `-=` 运算符的左操作数。这些运算符分别用于向事件附加事件处理程序或从事件移除事件处理程序，事件的访问修饰符控制允许此类操作的上下文。

在声明事件的类型之外，代码对事件唯一允许的操作是 `+=` 和 `-=`。因此，虽然此类代码可以为事件添加和移除处理程序，但不能直接获取或修改底层的事件处理程序列表。

在形式为 `x += y` 或 `x -= y` 的操作中，当 x 是事件时，操作的结果类型为 void（§12.21.5）（而不是像非事件类型上定义的其它 `+=` 和 `-=` 运算符那样，具有 x 的类型以及赋值后 x 的值）。这可以防止外部代码间接检查事件的底层委托。

示例：以下示例展示了如何将事件处理程序附加到 Button 类的实例：

```
public delegate void EventHandler(object sender, EventArgs e);

public class Button : Control
{
    public event EventHandler Click;
}
```

```
public class LoginDialog : Form
{
    Button okButton;
    Button cancelButton;

    public LoginDialog()
    {
        okButton = new Button(...);
        okButton.Click += new EventHandler(OkButtonClick);
        cancelButton = new Button(...);
        cancelButton.Click += new EventHandler(CancelButtonClick);
    }

    void OkButtonClick(object sender, EventArgs e)
    {
        // 处理 okButton.Click 事件
    }

    void CancelButtonClick(object sender, EventArgs e)
    {
        // 处理 cancelButton.Click 事件
    }
}
```

此处，LoginDialog 实例构造函数创建了两个 Button 实例，并将事件处理程序附加到 Click 事件。

*示例结束*

### 15.8.2 类字段事件

在包含事件声明的类或结构的程序文本中，某些事件可以像字段一样使用。要以这种方式使用，事件不得是 abstract 或 extern，并且不得显式包含 event_accessor_declarations。此类事件可以在允许字段的任何上下文中使用。该字段包含一个委托（§20），该委托引用已添加到事件中的事件处理程序列表。如果尚未添加任何事件处理程序，则该字段包含 null。

示例：在以下代码中

```
public delegate void EventHandler(object sender, EventArgs e);

public class Button : Control
{
    public event EventHandler Click;

    protected void OnClick(EventArgs e)
    {
        EventHandler handler = Click;
        if (handler != null)
        {
            handler(this, e);
        }
    }
}
```

```
public void Reset() => Click = null;
}
```

在 Button 类中，Click 被用作字段。如示例所示，该字段可以被检查、修改，并用于委托调用表达式。Button 类中的 OnClick 方法“触发”Click 事件。触发事件的概念与调用事件所表示的委托完全相同——因此，没有专门的语言结构用于触发事件。请注意，委托调用之前会进行检查以确保委托非 null，并且该检查在局部副本上进行以确保线程安全。

在 Button 类声明之外，Click 成员只能用在 `+=` 和 `-=` 运算符的左侧，例如

```
b.Click += new EventHandler(...);
```

该操作将一个委托追加到 Click 事件的调用列表中，以及

```
Click -= new EventHandler(...);
```

该操作从 Click 事件的调用列表中移除一个委托。

示例结束

在编译类字段事件时，编译器会自动创建存储来保存委托，并为事件创建访问器，以向委托字段添加或移除事件处理程序。添加和移除操作是线程安全的，并且可以（但不是必须）在持有包含对象的锁（§13.13）（对于实例事件）或 System.Type 对象（§12.8.17）（对于静态事件）的情况下进行。

注意：因此，形式为：

```
class X
{
    public event D Ev;
}
```

的实例事件声明应编译为等效于：

### 15.8.3 事件访问器

注意：事件声明通常省略 event_accessor_declarations，如上面的 Button 示例所示。例如，如果为每个事件提供一个字段的存储成本不可接受，则可能包含这些访问器。在这种情况下，类可以包含 event_accessor_declarations 并使用私有机制来存储事件处理程序列表。注意结束

事件的 event_accessor_declarations 指定与添加和移除事件处理程序关联的可执行语句。

访问器声明由 add_accessor_declaration 和 remove_accessor_declaration 组成。每个访问器声明由 token `add` 或 `remove` 后跟一个 block 组成。与 add_accessor_declaration 关联的 block 指定添加事件处理程序时要执行的语句，与 remove_accessor_declaration 关联的 block 指定移除事件处理程序时要执行的语句。

每个 add_accessor_declaration 和 remove_accessor_declaration 对应一个方法，该方法具有事件类型的一个值参数和 void 返回类型。事件访问器的隐式参数名为 value。当事件用于事件赋值时，会使用相应的事件访问器。具体来说，如果赋值运算符是 `+=`，则使用 add 访问器；如果赋值运算符是 `-=`，则使用 remove 访问器。在这两种情况下，赋值运算符的右操作数都用作事件访问器的参数。add_accessor_declaration 或 remove_accessor_declaration 的 block 应符合 §15.6.9 中描述的 void 方法规则。特别是，此类 block 中的 return 语句不允许指定表达式。

由于事件访问器隐式具有名为 value 的参数，因此在事件访问器中声明的局部变量或常量不能使用该名称，否则属于编译时错误。

示例：在以下代码中

```
class Control : Component
{
    // 事件的唯一键
    static readonly object mouseDownEventKey = new object();
    static readonly object mouseUpEventKey = new object();

    // 返回与键关联的事件处理程序
    protected Delegate GetEventHandler(object key) {...}

    // 添加与键关联的事件处理程序
    protected void AddEventHandler(object key, Delegate handler) {...}

    // 移除与键关联的事件处理程序
    protected void RemoveEventHandler(object key, Delegate handler) {...}

    // MouseDown 事件
    public event MouseEventHandler MouseDown
    {
        add { AddEventHandler(mouseDownEventKey, value); }
        remove { RemoveEventHandler(mouseDownEventKey, value); }
    }

    // MouseUp 事件
    public event MouseEventHandler MouseUp
```

