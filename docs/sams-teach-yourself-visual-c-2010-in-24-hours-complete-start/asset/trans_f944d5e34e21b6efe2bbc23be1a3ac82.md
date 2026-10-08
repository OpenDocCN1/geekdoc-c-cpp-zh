

➤ **CustomValidator（自定义验证器）**——允许你定义自己的自定义验证逻辑。

每个验证控件仅执行单一且定义明确的验证，但你可以组合多个验证控件以执行更复杂的验证。当验证控件确定某个控件包含无效数据时，它会在该控件旁边显示提供的错误消息。

你还可以使用 ValidationSummary（验证摘要）控件，以便以列表、项目符号列表或单个段落的格式汇总页面上所有验证控件的错误消息。

验证控件的常用属性如表 19.3 所示。

### 表 19.3 常见验证控件属性

| 名称 | 描述 |
| :--- | :--- |
| **ControlToValidate** | 验证控件将对其求值的输入控件的 ID。 |
| **Display** | 验证控件的显示行为。可接受的值为：<br>➤ None（无）——验证控件从不显示（最常与 ValidationSummary 控件组合使用）。<br>➤ Static（静态）——如果验证失败，验证控件显示错误消息，即使控件通过验证，也为错误消息分配了空间。<br>➤ Dynamic（动态）——如果验证失败，验证控件显示错误消息，且仅当控件通过验证时，才为错误消息分配空间。 |
| **ErrorMessage** | 如果验证失败，在 ValidationSummary 控件中显示的消息。如果未同时设置 Text 属性，当验证失败时，此文本也会在验证控件中显示。 |
| **Text** | 当验证失败时，在验证控件中显示的消息。如果未设置此项，则使用 ErrorMessage 的值。 |

清单 19.9 展示了一个使用部分验证控件的简单 ASPX 页面。

### 清单 19.9 使用验证控件

```html
<%@ Page Language="C#" AutoEventWireup="True" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html>
  <head>
    <title>Validation Controls</title>
  </head>
  <body>
    <form id="Form1" runat="server">
      <h3>Validator Example</h3>
      Enter a number from 1 to 30:
      <asp:TextBox ID="TextBox1" runat="server" /><br />
      <asp:RequiredFieldValidator
          ID="RequiredFieldValidator1"
          ControlToValidate="TextBox1"
          Display="None" ErrorMessage="You must enter a value."
          runat="server" />
      <asp:RegularExpressionValidator
          ID="RegularExpressionValidator1"
          ControlToValidate="TextBox1"
          Display="None" ValidationExpression="\d+"
          ErrorMessage="You must enter a numeric value."
          runat="server" />
      <asp:RangeValidator
          ID="Range1"
          ControlToValidate="TextBox1"
          Display="None"
          MinimumValue="1"
          MaximumValue="30"
          Type="Integer"
          ErrorMessage="The value must be from 1 to 30"
          runat="server" />
      <p />
      <asp:ValidationSummary runat="server" />
      <p />
      <asp:Button ID="Button1" Text="Submit" runat="server" />
    </form>
  </body>
</html>
```

图 19.11 展示了输入无效数据后的这个简单验证器示例。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_443_0.png)

**图 19.11**
验证器示例

# 摘要

在本节中，你学习了如何构建 Web 应用程序，包括如何应用样式、数据绑定和验证。正如你所见，虽然构建 Web 应用程序与构建 WPF 桌面应用程序有许多相似之处，但也有许多不同之处。虽然许多开发者熟悉这两类应用程序，但大多数人往往倾向于专精于其中一类。

# 问答

**问.** *什么是 Web 窗体？*

**答.** Web 窗体是一个 ASPX 页面，它使用 HTML 描述用户界面标记，通常还包含一个代码后置文件。

**问.** *Global.asax 文件用于什么？*

**答.** Global.asax 文件为 Web 应用程序提供应用程序级别的事件和代码，这与 App.xaml 文件在 WPF 应用程序中的作用非常相似。

**问.** *如何为 Web 应用程序应用样式？*

**答.** 可以使用层叠样式表（CSS）为 Web 应用程序应用样式。

## 练习

### 小测验

1. 什么是母版页？
2. Web 窗体是否总是需要与母版页关联？
3. 如何在 Web 窗体中指定数据绑定表达式？

### 答案

1. 你可以将母版页背后的概念视为类似于许多文字处理应用程序中的邮件合并功能。子页面使用映射到母版页中定义占位符的 `ContentPlaceholder` 控件，而母版页定义了页面的其余部分。当发起请求时，ASP.NET 将子页面的输出与母版页的输出合并，并将合并后的内容发送给用户。
2. 不，可以创建不与母版页关联的 Web 窗体。
3. 数据绑定表达式包含在 `<%#` 和 `%>` 分隔符之间，并使用 `Eval`（单向）或 `Bind`（双向）函数。当调用控件或 Page 类的 `DataBind` 方法时，这些表达式会被解析。

## 演练

本章没有演练题目。

# 第五部分

# 深入探索

- 第 20 小时：使用特性进行编程 427
- 第 21 小时：动态类型与语言互操作性 439
- 第 22 小时：内存组织与垃圾回收 451
- 第 23 小时：理解线程、并发性与并行性 461
- 第 24 小时：下一步：Silverlight、PowerShell 和实体框架 479

*此页故意留白*

# 第 20 小时

# 使用特性进行编程

## 本小时你将学到什么：

- 理解特性
- 使用常见特性
- 使用自定义特性
- 在运行时访问特性

在第 1 小时“.NET 框架和 C#”中，你了解到 C# 支持面向组件的编程，它允许你创建自包含、自文档化、可再分发的代码单元，即程序集。元数据指定了类型、属性、事件、方法及其他代码元素之间的关系。特性使你能向程序集添加额外的元数据，提供了一种将声明式信息与代码关联的方式。特性会被编译并存储在生成的 CLI 中，并可以在运行时访问。

.NET 框架提供并使用了特性来实现许多不同的目的。在第 5 小时“创建枚举类型和结构”中，你看到了特性的一个例子，当时你学习了标志枚举。特性还用于描述安全性、描述如何序列化数据、限制 JIT 编译器的优化、以及控制应用程序开发期间属性和方法的可见性等，其中包含许多其他用途。要添加自己的自定义元数据，你需要使用自己创建的自定义特性。

在本小时中，你将更多地了解特性——如何使用它们、创建自己的自定义特性，以及在运行时访问它们。

# 理解特性

虽然特性几乎可以添加到任何代码声明（包括程序集、类、方法、属性和字段）中，但许多特性仅适用于特定的代码声明。例如，有些特性仅适用于方法，而另一些则仅适用于类型声明。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_448_0.png)

### **特性名称**

虽然最佳实践建议所有特性名称都以“Attribute”一词结尾，以便可以轻松地将它们与其他类型区分开来，但在代码中使用它们时无需指定“Attribute”后缀。例如，`[Flags]` 等同于 `[FlagsAttribute]`。特性的实际类名是 FlagsAttribute。

要在代码声明上放置特性，需将该特性的名称用方括号 ([ ] ) 括起来，并直接放在应用该特性的声明之前。例如，清单 20.1 中显示的 `System.IO.FileShare` 枚举应用了 `FlagsAttribute`。

### **清单 20.1** 使用 FlagsAttribute

```csharp
[Flags]
public enum FileShare
{
    None = 0, Read = 0x001,
    Write = 0x002, ReadWrite = 0x003,
    Delete = 0x004, Inheritable = 0x010,
}
```

代码声明可以拥有多个特性，并且对于同一个声明，某些特性可以指定多次，如清单 20.2 所示。

### **清单 20.2** 特性的其他用法

```csharp
[Conditional("DEBUG"), Conditional("EXAMPLE")]
void Method() { }

void TestMethod([In][Out] string value) { }
void TestMethod2([In, Out] string value) { }
```

当你将特性应用于代码声明时，实际上你是在调用特性类的一个构造函数。这意味着你可以向特性提供参数，如清单 20.2 中的 `ConditionalAttribute` 所示。

