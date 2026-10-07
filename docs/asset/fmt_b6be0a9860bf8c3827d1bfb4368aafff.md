
```csharp
m_byteArray[bitPos / 8] |= (1 << (bitPos % 8));
} else {
// 将索引位关闭
m_byteArray[bitPos / 8] &= ~(1 << (bitPos % 8));
}
}
}
```

## 第 10 章 属性 255

- 托管程序集元数据中的属性定义，它总是会被发射。这里没有特殊的参数化属性元数据表，因为由于 CLR 的存在，参数化属性仅仅就是属性。

早期显示的 `BitArray` 类，编译器按照原始源代码编写的方式编译索引器，如下：

```csharp
public sealed class BitArray {
// 这是索引器的访问器方法。
public Boolean get_Item(Int32 bitPos) { /* ... */ }
// 这是索引器的访问器方法。
public void set_Item(Int32 bitPos, Boolean value) { /* ... */ }
}
```

编译器通过在索引器名称前加上 `get_` 和 `set_` 来自动为这些方法生成名称。由于 C# 的索引器语法不允许开发者指定索引器名称，C# 编译器团队必须选择一个默认名称用于访问器方法；因此，编译器命名的方法为 `get_Item` 和 `set_Item`。

在查看 .NET Framework 参考文档时，你可以通过寻找名为 `Item` 的属性来判断一个类型是否提供了索引器。例如，`System.Collections.Generic.List` 类型提供了一个名为 `Item` 的公共实例属性；该属性就是 `List` 的索引。

当你用 C# 编程时，你使用 `Item` 的名称，所以你通常不在乎编译器为你选择了这个名称。如果你正在为可以使用其他编程语言编写的类型设计索引器，你可能想要更改赋予索引器 `get` 和 `set` 访问器方法的默认名称 `Item`。C# 允许你通过对索引器应用 `System.Runtime.CompilerServices.IndexerNameAttribute` 自定义特性来重命名它们。以下代码演示了如何这样做：

```csharp
using System;
using System.Runtime.CompilerServices;
public sealed class BitArray {
[IndexerName("Bit")]
public Boolean get_Item(Int32 bitPos) {
// 这里定义了一个访问器方法
}
}
```

编译器将发射名为 `get_Bit` 和 `set_Bit` 的方法代替 `get_Item` 和 `set_Item`。在编译时，C# 编译器看到 `IndexerName` 特性，这告诉编译器如何命名方法和属性元数据；该特性本身不会被发射到程序集的元数据中。

# 第二部分 设计类型

以下是一些 Visual Basic 代码，演示了如何访问此 C# 索引器：

```vb
'构造一个 BitArray 类型的实例。
Dim ba as New BitArray(10)
```

```vb
'Visual Basic 使用 () 而不是 [] 来指定数组元素。
Console.WriteLine(ba(2)) '显示 True 或 False
```

```vb
'Visual Basic 也允许你通过名称访问索引器。
Console.WriteLine(ba.Bit(2)) '显示与上一行相同'
```

在 C# 中，单个类型可以定义多个索引，只要这些索引器采用的是不同的参数集。在编程语言中，`IndexerName` 允许你定义具有相同签名的多个索引，因为每个索引可以有不同的名称。C# 不允许你这样做的原因是它的语法并不通过名称来引用索引器；编译器将不知道你正在引用的是哪一个索引器。尝试编译以下 C# 源代码会导致编译器生成以下消息：
"error CS011: 类型 'SomeType' 已定义了具有相同参数类型的名为 'this' 的成员。"

```csharp
using System;
using System.Runtime.CompilerServices;
public sealed class SomeType {
// 定义一个 get_item 访问方法。
public Int32(Boolean b) {
get { return 0; }
}
// 定义一个 get_jeff 访问方法。
[IndexerName("Jeff")]
public String this[Boolean b] {
get { return null; }
}
}
```

你可以清楚地看到 C# 将索引器视为重载 `[]` 运算符的方式，而该运算符无法用于区分具有不同名称但相同参数集的参数化属性。`String` 类型是一个更改了索引器名称的示例。`String` 的索引器名称是 `Chars`。这种只读属性允许你获取单个字符。对于不使用 `[]` 语法访问此属性的编程语言，`Chars` 被决定为 C# 的一个更有意义的名称。

> ² 出于此原因，`IndexerAttribute` 类并不是 CLI 标准的一部分。

## 选择参数化属性

这两个问题的答案是，类型必须通过在类本身上应用 `System.Reflection.DefaultMemberAttribute` 实例，从参数化属性名称中选择一个作为默认属性。`DefaultMemberAttribute` 可以应用于类、结构体或接口。在 C# 中，当你编译一个定义参数化属性的类型时，编译器会自动在定义类型上应用 `DefaultMember` 特性，并在你使用 `IndexerName` 特性时考虑到它。该特性的构造函数指定了用于类型默认参数化属性的名称。

# 第 11 章 事件

在本章中，将介绍：
设计暴露事件的类型 ........................................................ 260
编译器如何实现事件 ................................................................... 266
设计监听事件的类型 ............................................................... 269
显式实现事件 ................................................................................. 271

在本章中，我将介绍关于类型可以定义的最后一种成员类型：事件。一个类型定义的事件成员允许该类型（或该类型的实例）通知其他对象某些事情已经发生了了。例如，`Button` 类提供了一个名为 `Click` 的事件。当 `Button` 被点击时，应用程序中的一个或多个对象可能希望接收有关此事件的通知，以便执行某些操作。事件是允许这种交互作用的类型成员。具体来说，定义一个事件成员意味着该类型提供了以下功能：

- 方法可以注册其对事件的关注。
- 方法可以取消其对事件的关注注册。
- 当事件发生时，已注册的方法将收到通知。

类型在定义事件时可以使用此功能，因为它们维护了一个已注册方法的列表。当事件发生时s，该类型会通知集合中的所有已注册方法。

通用语言运行时（CLR）的事件模型基于委托（delegates）。委托是一种调用回调方法的类型安全方式。回调方法是对象接收其订阅的通知的手段。在本章中，我将使用委托，但在进入第 17 章“委托”之前，我不会详细解释它们的细节。

为了帮助你完全理解事件在 CLR 中如何工作，我将从一个事件很有用的场景开始。假设你想设计一个电子邮件应用程序。当新邮件到达时，用户可能希望将消息转发到传真机或寻寻器。在构建此应用程序时，假设你首先设计一个名为 `MailManager` 的类型，用于接收传入的电子邮件。`MailManager` 将暴露一个名为 `NewMail` 的事件。其他类型（如 `Fax` 和 `Pager`）可能会对此事件注册感兴趣。当 `MailManager` 接收到新电子邮件时，它将引发事件，导致消息分发给每个注册的对象。每个对象都可以以其所需的方式处理消息。

当应用程序初始化时，让我们只实例化一个 `MailManager` ——应用程序可以实例化任意数量的 `Fax` 和 `Pager` 类型。图 11-1 显示了应用程序如何初始化以及当新邮件到达时会发生什么。

![](img/47eccf75186e2a4895549653d7520b0a_277_0.png)

- 1. `Fax` 对象中的方法向 `MailManager` 的事件注册关注。
- 2. `Pager` 对象中的方法向 `MailManager` 的事件注册关注。
- 3. 一封新邮件到达 `MailManager`。
- 4. `MailManager` 对象向所有注册的方法发送通知，这些方法根据需要处理邮件。

图 11-1 使用事件构建应用程序架构

图 11-1 所示的应用程序工作原理如下：应用程序通过构造 `MailManager` 实例来初始化。`MailManager` 提供一个 `NewMail` 事件。当 `Fax` 和 `Pager` 对象被构造时，它们会向 `MailManager` 的 `NewMail` 事件注册一个实例方法，这样 `MailManager` 就知道在有新邮件到达时通知 `Fax` 和 `Pager` 对象。

# 设计暴露事件的类型

开发者为了定义暴露一个或多个事件成员的类型，必须采取许多步骤。在本节中，我将介绍每一个必要的步骤。`MailManager` 示例应用程序（可以从 http://wintellect.com 下载）显示了 `MailManager` 类型、`Fax` 类型和 `Pager` 类型的所有源代码。你会发现 `Pager` 类型与 `Fax` 类型几乎完全相同。

# 步骤 #1：定义一个类型，用以持有任何应发送给事件通知接收者的额外信息

当事件被引发时，引发事件的对象可能希望向接收通知的对象传递一些额外信息。这些额外信息需要被封装到它自己的类中，该类通常包含许多私有字段，以及一些用于暴露这些字段的只读公有属性。按照惯例，持有传递给事件处理程序的事件信息的类应该派生自 `System.EventArgs`，且类名应以 `EventArgs` 为后缀。在示例中，`NewMailEventArgs` 类具有标识谁发送了消息（`m_from`）、谁接收了消息（`m_to`）以及消息的主题（`m_subject`）的字段。

```csharp
// 步骤 #1：定义一个类型，用以持有任何应发送给事件通知接收者的额外信息
internal class NewMailEventArgs : EventArgs {
private readonly String m_from, m_to, m_subject;
public NewMailEventArgs(String from, String to, String subject) {
m_from = from; m_to = to; m_subject = subject;
}
public String From { get { return m_from; }}
public String To { get { return m_to; }}
public String Subject { get { return m_subject; } }
}
```

> 注意 `EventArgs` 类定义在 .NET 框架类库 (FCL) 中，其实现方式如下：
[Visible(true)]
public class EventArgs {
public static readonly EventArgs Empty = new EventArgs();
public EventArgs() {}
}

如你所见，这个类型没什么好写的。它仅仅作为其他类型可以派生的基类型。许多事件并没有额外数据需要传递。例如，当 `Button` 通知其注册者它被点击时，调用回调方法就足够了。

# 步骤 #2：定义事件成员

事件成员使用 C# 的 `event` 关键字定义。每个事件成员被赋予了访问级别（通常是公有的，以便其他代码可以访问）、一个指示要调用的方法原型的委托类型，以及一个名称（可以是任何有效标识符）。以下是 `MailManager` 中事件成员的内容：

```csharp
internal class MailManager {
// 步骤 #2：定义事件成员
public event EventHandler<NewMailEventArgs> NewMail;
}
```

`NewMail` 是此事件的名称。事件成员的类型是 `EventHandler<NewMailEventArgs>`，这意味着事件的所有接收者必须提供一个原型与 `EventHandler<NewMailEventArgs>` 委托匹配的回调方法。由于泛型 `System.EventHandler` 委托定义如下：

```csharp
public delegate void EventHandler<TEventArgs>(Object sender, TEventArgs) where TEventArgs : EventArgs;
```

方法的原型看起来：

```csharp
void MethodName(Object sender, NewMailEventArgs);
```

> 注意 有人疑惑为什么事件模式要求发送者为 `Object`。毕竟，由于 `MailManager` 将是引发带有 `NewMailEventArgs` 对象事件的唯一类型，回调原型采用如下形式更为合理：

MethodName(MailManager sender, NewMailEventArgs e);

由于继承的原因，模式要求发送者参数为 `Object` 类型。如果 `MailManager` 被用作 `SmtMailManager` 的基类呢？在这种情况下，回调的发送者参数原型应该是 `SmtMailManager` 而不是 `MailManager`，但这不会发生，因为 `SmtMailManager` 继承了 `NewMail` 事件。因此，期望 `SmtMailManager` 引发事件的代码仍然必须将发送者转换为 `SmtMailManager`。换句话说，转换仍然是，所以发送者参数完全可以类型为 `Object`。

发送者参数类型为 `Object` 的另一个原因是灵活性。它允许多个提供传递 `NewMailEventArgs` 对象事件的类型使用该委托。例如，如果该类没有派自 `MailManager`，那么 `PopMailManager` 就可以使用该委托。

# 第 11 章 事件 263

事件模式还需要委托定义、回调方法名以及派生自 `EventArgs` 的参数 `e`。此设计的唯一目的是为该模式增加额外的一致性，让开发者更容易学习和实现该模式。分析代码的工具（如 Microsoft Visual Studio）也知道调用参数 `e`。

最后，事件模式要求所有事件处理程序都返回 `void` 类型。这是必要的，因为引发事件可能会调用多个回调方法，而无法获取它们所有方法的返回值。使用 `void` 返回类型不允许回调返回任何值。遗憾的是，FCL（框架类库）中的某些事件处理程序（例如 `EventHandler`）并没有遵循微软自己的模式，因为它返回的是一个类型为 `Assembly` 的对象。

## 第 3 步：定义一个负责引发事件的方法，以通知已注册的对象事件已经发生

按照惯例，类应该定义一个受保护的、虚拟的方法，该方法在需要引发事件时，由该类内部及其派生类的代码调用。该方法接受一个参数，即 `NewMailEventArgs` 对象，它包含了传递给接收通知对象的各种。该方法的默认实现只是检查是否有对象对该事件注册了兴趣，如果是，则引发事件，从而通知已注册的方法事件已经发生。以下是我们的 `MailManager` 类中方法的写法：

```csharp
internal class MailManager {
...
// 第 3 步：定义一个负责引发事件的方法
// 以通知已注册的对象事件已经发生
// 如果此类是密封的，请将此方法改为私有且非虚拟
protected virtual void OnNewMail(NewMailEventArgs e) {
// 现在将委托字段的引用复制到临时字段以确保线程安全
EventHandler<EventArgs> temp =
Interlocked.CompareExchange(ref NewMail, null, null);
// 如果有方法对我们的事件注册了兴趣，则通知它们
if (temp != null) temp(this, e);
}
...
}
```

# 以线程安全的方式引发事件

当 .NET 框架首次发布时，推荐开发者引发事件的方法是使用类似于下面的代码：

```csharp
// 版本 1
protected virtual void OnNewMail(NewMailEventArgs e) {
if (NewMail != null) NewMail(this, e);
}
```
