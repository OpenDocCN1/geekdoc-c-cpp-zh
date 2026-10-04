

当应用程序初始化时，我们只实例化一个 MailManager——随后应用程序就可以实例化任意数量的 Fax 和 Pager 类型。图 11-1 显示了应用程序如何初始化，以及当有新邮件消息到达时会发生什么。

![](img/0ce3b788d061e3d3095fa554b1a34adf_275_0.png)

- 1. Fax 对象中的一个方法向 MailManager 的事件注册兴趣。
- 2. Pager 对象中的一个方法向 MailManager 的事件注册了兴趣。
- 3. 一封新邮件消息到达 MailManager。
- 4. MailManager 对象向所有注册的方法发送通知，这些方法根据需要处理邮件消息。

**图 11-1** 针对事件的应用程序架构。

以下是图 11-1 所示应用程序的工作原理：应用程序通过构造 MailManager 实例来完成初始化。Manager 提供了一个 NewMail 事件。当 Fax 和 Pager 对象被构造时，它们会向 MailManager 的 NewMail 事件注册一个实例方法，MailManager 知道在有新邮件消息到达时通知 Fax 和 Pager 对象。现在，当 MailManager 接收到新邮件（有时是在未来）时，它将触发 NewMail 事件，让所有注册的方法有机会以任何方式处理新消息。

## 设计一个暴露事件的类型

为了定义一个暴露一个或多个成员的类型，开发者必须采取许多步骤。在本节中，我将介绍每一个必要的步骤。MailManager 示例应用程序（可以从 http://wintlect.com/Books 资源 Books 部分下载）显示了 MailManager 类型、Fax 类型和 Pager 类型的所有源代码。你会发现 Pager 类型与 Fax 类型几乎完全相同。

## 步骤 #1：定义一个类型，用于持有任何应发送给事件通知接收者的额外信息

当事件被触发时，触发事件的对象可能希望向接收事件通知的对象传递一些额外信息。这些额外信息需要被封装在它自己的类中，该类通常包含一组字段以及一些用于暴露这些字段的只读属性。根据约定，持有要传递给事件处理程序的事件信息的类应该派生自 System.EventArgs，且类名应以 EventArgs 结尾。在示例中，NewMailEventArgs 类具有以下字段：用于识别消息发送者 (m_from)、消息接收者 (m_to) 以及消息的主题。

```
// 步骤 #1：定义一个持有任何额外信息的类型
// 这些信息应发送给事件通知接收者
internal class NewMailEventArgs {

    private readonly String m_from, m_to, m_subject;

    public NewMailEventArgs(String from, String to, String subject) {
        m_from = from; m_to = to; m_subject = subject;
    }

    public String From { get { return m_from; } }
    public String To { get { return m_to; } }
    public String Subject { get { return m_subject; }}
}
```

> 注意：EventArgs 类定义在 Microsoft .NET Framework 类库 (FCL) 中，其实现如下。

```
[Visible(true), Serializable]
public class EventArgs {
    public static readonly EventArgs Empty = new EventArgs();
    public EventArgs() {
}}
```

如你所见，这个类型并没有特别之处。它仅仅作为一个基类型，其他类型可以从其上派生。许多事件并没有额外的信息要传递。例如，当按钮 通知其注册的接收者它已被点击时，只需调用回调方法就是足够的信息了。当你定义一个没有额外数据要传递的事件时，只需使用 EventArgs.Empty 而不是构造一个新的 EventArgs 对象。

## 步骤 #2：定义事件成员

事件使用 C# 关键字 `event` 来定义。每个事件成员都被赋予了访问访问符（几乎总是是 public，以便其他代码可以访问该事件成员）、一个指示将调用的方法（方法）原型的委托类型以及一个名称（可以是任何有效标识符）。以下是我们的 MailManager 类中事件成员的样式。

```
internal class MailManager {
    // 步骤 #2：定义事件成员
    public event EventHandler<NewMailEventArgs> NewMail;
    ...
}
```

NewMail 是事件的名称。事件成员的类型是 `EventHandler<NewMailEventArgs>`，这意味着所有事件通知的接收者都必须提供一个回调方法，其原型必须与 `EventHandler<NewMailEventArgs>` 委托类型匹配。由于如下定义的泛型 System.EventHandler 委托：

```
public delegate void EventHandler<TEventArgs>(Object sender, TEventArgs);
```

方法原型必须看起来如下所示。

```
void MethodName(Object sender, NewMailEventArgs e);
```

> 许多人奇怪为什么该模式要求 `sender` 参数的类型为 `Object`。毕竟，由于 MailManager 将是唯一触发带有 NewMailEventArgs 对象的事件的类型，将回调方法原型设计成如下更符合逻辑：
void MethodName(MailManager sender, NewMailEventArgs e);

该模式要求 `sender` 参数为 `Object` 类型主要是由于继承。如果 MailManager 被用作 SmtpMailManager 的基类怎么办？在这种情况下，回调方法的 `sender` 参数原型应该是应该是SmtpMailManager` 而不是 `MailManager`，但这是不可能发生的，因为 SmtpMailManager 继承了 NewMail 事件。将 `sender` 参数使用 `Object` 的另一个比为了灵活性。它允许委托被多个类型使用。例如，即使该类没有派自 MailManager，PopMailManager 类也可以使用该委托。

事件模式还要求委托定义和回调方法将 EventArgs 派生的参数命名为 `e`。其唯一目的是增加模式的一致性，让开发者更容易学习和实现该模式。生成源代码的工具（如 Microsoft Visual Studio）也知道返回类型为 `void`。这是必要的，因为事件模式要求所有事件处理程序返回 `void`。触发事件可能会调用回调方法，并且无法获取它们的返回值。使用 `void` 类型允许回调在之后返回值。遗憾的是，FCL 中的某些事件处理程序（如 `ResolveEventHandler`）没有遵循微软规定的模式，因为它返回一个 `Assembly` 类型的对象。

## 步骤 #3：定义一个负责触发以以注册对象事件已发生的方法

根据约定，类应该定义一个受保护的虚方法，在事件被触发时由类内部及其派生类调用。该方法接受一个参数，即一个 `NewMailEventArgs` 对象，它包含了传递给接收通知的信息。该方法的默认实现只是检查是否有对象对该事件注册了兴趣，如果是，则将触发事件，通知注册的方法事件已发生。以下是我们的 MailManager 中的方法样式。

```
internal class MailManager {
    ...
    // 步骤 #3：定义一个负责触发事件
    // 以通知注册对象事件已发生的方法
    // 如果类是密封的，请将此方法设为私有非虚
    protected virtual void OnMail(NewMailEventArgs args) {

        // 将委托字段的引用复制到临时字段中以线程安全
        EventHandler<NewMailEventArgs> temp = Volatile.Read(ref NewMail);

        // 如果有方法注册了我们的事件，则通知它们
        if (temp != null) temp(this, args);
    }
    ...
}
```

