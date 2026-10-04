

# 用户控件介绍

通过这段代码，Label 控件的 `Text` 属性将包含 `Banner1_VerticalPanel`，这是 `Panel` 的客户端 ID。在下一章节中，你将看到使用 `ClientID` 的更实用的示例。

使用显式 ID，可以更容易地预测客户端 HTML 元素的最终 `id`，这反过来也使得在 JavaScript 或 CSS 中引用这些元素变得更加容易。

> 注意：由于 ASP.NET 运行时可能会更改 HTML 元素的客户端 ID 属性，你使用 CSS ID 选择器引用元素时可能会遇到困难。解决此问题最简单的方法是使用 Class 选择器而不是 ID 选择器。或者，在使用嵌入式样式时，可以使用控件的 `ClientID`。

ASP.NET 4 引入了一个影响客户端 ID 的新选项：`ClientIDMode`。

# 介绍 ClientIDMode

从 ASP.NET 4 开始，每个 Web 控件都有一个 `ClientIDMode` 属性，允许你决定客户端 ID 的生成方式。你可以将 `ClientIDMode` 设置为以下四个值之一：

| 值 | 描述 |
| :--- | :--- |
| AutoID | 按照以前 ASP.NET 版本的方式生成 ID。 |
| Inher | 使用此设置，控件将从父控件继承其 `ClientIDMode` 值。 |
| Predictable | 此值主要用于数据绑定控件（在第 13 节及以后讨论），并允许你为重复元素创建可预测的客户端 ID。控件的客户端 ID 是通过拼接父控件的客户端 ID 和控件自身的服务器 ID 生成的。可以使用 `ClientIDRowSuffix` 为每个元素可选地扩展唯一值。 |
| Static | 使用此值，客户端 ID 将与你设置的服务器 ID 完全相同。这允许你显式设置客户端 ID，从而获得更大的控制权。但它并不能防止分配两次相同的值，这可能导致客户端 HTML 中出现重复 ID。请谨慎使用！ |

`Page` 类的 `ClientIDMode` 默认值为 `Predictable`，控件的默认值为 `Inherit`。这意味着控件的 ID 生成模式实际上是 `Predictable`，因为它们从 `Page` 继承了设置。如果你使用 Visual Studio 将项目从早期版本转换为 ASP.NET 4.5.1，Visual Studio 会自动在 `Web.config` 文件的 `<pages>` 元素中将默认值设置为 `AutoID`：

```xml
<pages controlRenderingCompatibilityVersion="3.5" clientIDMode="AutoID"/>
```

目前，Planet Wrox 网站从更改任何现有控件的客户端 ID 中获益不多，因此目前不需要更改任何内容。但在随后的章节中，请使用 `ClientIDMode` 属性创建更简洁的客户端 ID。

虽然当前的横幅控件可以方便地在网站各个位置显示横幅，但它并不智能。它能做的只是显示一张链接图片，仅此而已。为了提高可用性，你可以为控件添加行为，使其在网站的不同页面上表现出不同的行为。

# 为你的控件添加逻辑

虽然使用控件处理重复内容非常有用，但当你向它们添加自定义逻辑时，它们会变得更有用。通过向用户控件添加公共属性或方法，你可以影响其运行时的行为。当你向用户控件添加属性时，它将自动出现在 IntelliSense 和你正在操作的控件的属性网（Properties Grid）中，从而易于从页面等其他文件更改行为。

要向用户控件添加属性或方法，你需将它们添加到控件的后台代码（Code Behind）中。在最简单的形式中，属性看起来与你在第 5 节看到的属性完全相同。对于更高级的场景，你需要添加 View State 属性，它们能够在回传（postbacks）之间维护状态。在接下来的两个练习中，你将看到如何创建此类属性。

# 为属性创建自定义数据类型

为了让横幅控件更有用，你可以为它添加第二张图片显示水平横幅。你还可以给控件添加一个属性，来决定显示垂直图像还是水平图像。你可以通过创建一个 `System.Byte` 类型的数值属性来实现这一点。例如，0 代表垂直，1 代表水平。然而，这使得很难记住每个数字代表什么。你可以通过创建一个接受 `Horizontal` 和 `Vertical` 值的 String 属性让它变得简单一点。但是，字符串无法在编译时进行检查，因此你可能会出错，导致错误或显示错误的横幅。.NET Framework 提供了一种很好的方法来解决这个问题，它允许你以枚举（enumeration）的形式创建自己的数据类型。通过枚举（简称为 `enum`），你将数字分配给人类可读的字符串。开发者使用这些可读的文本，而在底层则使用数值。以下代码段显示了枚举的一个基本示例（注意 VB 示例没有使用逗号，而在 C# 中是必须的)：

```vb.net
Public Enum Direction
    Horizontal
    Vertical
End Enum
```

```csharp
public enum Direction
{
    Horizontal,
    Vertical
}
```

通过这些枚举，编译器会自动为 `Horizontal` 和 `Vertical` 成员分配数值值，从 0 开始递增。如果你需要，也可以显式地定义数值：

# VB.NET

```vb.net
Public Enum Direction
    Horizontal
    Vertical
End Enum
```

# C#
```csharp
public enum Direction
{
    Horizontal,
    Vertical
}
```

通过这些枚举，编译器会自动为 `Horizontal` 和 `Vertical` 成员分配数值值，从 0 开始递增。如果你需要，也可以显式地定义数值：

枚举的酷之处在于，你可以在代码、属性网甚至编辑器中获得 IntelliSense。图 8-6 显示了它在 VB.NET 中的工作方式。图 8-7 显示了 C# 的情况。图 8-8 显示了该属性的使用。枚举非常适合简单短的列表。它们可以帮助你避免像 0 或 1 这样的“魔法数字”，而允许你使用人类可读的文本。

#尝试创建更智能的用户控件

在此练习中，你为用户控件添加一个横幅。此横幅在其自己的面板内显示水平图像。为了避免横幅同时显示，你添加了一个属性来确定显示哪个横幅。使用控件的页面就可以定义正确的横幅。

- 1. 首先创建一个包含两个方向成员的枚举：垂直和水平。要此操作，右键点击 `AppCode` 文件夹并选择“新建项”。选择你的编程语言并添加一个名为 `Direction` 的类。
- 2. 打开文件后，清除其内容并将以下代码添加到其中：

```vb.net
Public Enum Direction
    Horizontal
    Vertical
End Enum
```

```csharp
public enum Direction
{
    Horizontal,
    Vertical
}
```

- 3. 保存并关闭文件。
- 4. 打开用户控件 `Banner.ascx` 的后台代码并添加以下属性。为了帮助你创建属性，VS 提供了一个实用的代码片段。要在 C# 中激活该代码片段，输入 `prop` 然后按 Tab 键。VS 会为你添加自动属性的代码结构。对于 VB.NET，你可以输入 `Property` 然后按 Tab 键。但这将创建一个完整属性而不是自动属性（本练习使用的），在这种情况下你最好手动输入代码。在插入代码后，你可以按 Tab 键在字段之间移动，每次输入正确的数据类型或属性名称。完成代码，使其看起来所示：

```vb.net
Public Property DisplayDirection As Direction
csharp
public Direction DisplayDirection { get; set; }
```

注意属性名称为 `DisplayDirection`，其数据类型为 `Direction`，即你之前定义的枚举。

