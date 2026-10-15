
表 14.3：Control 类值得关注的公共事件

| 事件 | 描述 |
|-------|-------------|
| PreRender | 在服务器控件即将呈现到其包含的 Page 对象时发生。 |
| Unload | 在服务器控件从内存中卸载时发生。 |

在讨论了 Control 类的主要属性、方法和事件之后，让我们继续讨论 WebControl 类，因为它是所有控件直接依赖的类。

## WebControl 类

所有 Web 服务器控件都存在于 System.Web.UI.WebControls.WebControl 命名空间中，并且可以在任何 Web 窗体上使用。WebControl 类的层次结构如下：

```
System.Object
  System.Web.UI.Control
    System.Web.UI.WebControls.WebControl
```

WebControl 类值得关注的公共属性列于表 14.4：

表 14.4：WebControl 类值得关注的公共属性

| 属性 | 描述 |
|----------|-------------|
| AccessKey | 获取允许您快速导航到 Web 服务器控件的访问键。 |
| Attributes | 获取与服务器控件属性不对应的任意属性集合（仅用于呈现）。 |
| BackColor | 获取 Web 服务器控件的背景色。 |
| BorderColor | 获取 Web 服务器控件的边框颜色。 |
| BorderStyle | 获取 Web 服务器控件的边框样式。 |
| BorderWidth | 获取 Web 服务器控件的边框宽度。 |
| ControlStyle | 获取 Web 服务器控件的样式。 |
| ControlStyleCreated | 获取一个值，该值指示是否已为 ControlStyle 属性创建 Style 对象。此属性主要用于控件开发人员。 |
| CssClass | 获取 Web 服务器控件在客户端呈现的级联样式表 (CSS) 类。 |
| Enabled | 获取一个值，该值指示 Web 服务器控件是否已启用。 |
| EnableTheming | 获取一个值，该值指示主题是否应用于 Web 服务器控件。 |
| Font | 获取与 Web 服务器控件关联的字体属性。 |
| ForeColor | 获取 Web 服务器控件的前景色（通常是文本颜色）。 |
| HasAttributes | 指定一个值，该值指示是否为 Web 服务器控件设置了属性。 |
| Height | 获取 Web 服务器控件的高度。 |
| SkinID | 获取要应用于 Web 服务器控件的样式。 |
| Style | 获取文本属性集合，这些属性将在 Web 服务器控件的外部标记上呈现为 style 属性。 |
| TabIndex | 获取 Web 服务器控件的 Tab 索引。 |
| ToolTip | 获取当鼠标指针悬停在 Web 服务器控件上时显示的文本。 |
| Width | 获取 Web 服务器控件的宽度。 |

表 14.5 列出了 WebControl 类值得关注的公共方法：

表 14.5：WebControl 类值得关注的公共方法

| 方法 | 描述 |
|---|---|
| ApplyStyle | 将指定样式的任何非空白元素复制到 Web 控件。它还会覆盖控件的任何现有样式元素。 |
| CopyBaseAttributes | 将未由 Style 对象封装的属性从指定的 Web 服务器控件复制到调用此方法的 Web 服务器控件。此方法主要用于控件开发人员。 |
| MergeStyle | 将指定样式的任何非空白元素复制到 Web 控件，但不会覆盖控件的任何现有样式元素。此方法主要用于控件开发人员。 |
| RenderBeginTag | 将指定标记元素的开始标记写入输出流。 |
| RenderEndTag | 将标记元素的结束标记写入输出流。 |

WebControl 类中包含的一些基本标准控件如下：

- Button 控件
- TextBox 控件
- Label 控件
- HyperLink 控件
- HiddenField 控件
- FileUpload 控件
- CheckBox 控件
- CheckBoxList 控件
- RadioButton 控件
- RadioButtonList 控件
- ListBox 控件
- DropDownList 控件
- Image 控件
- Calendar 控件

让我们详细讨论这些控件。

## Button 控件

Button 控件用于创建向 Web 页面发送请求的按钮。该控件存在于 System.Web.UI.WebControls 命名空间中。单击时，它会将数据发布到服务器。

Button 类的类层次结构如下：

```
System.Object
  System.Web.UI.Control
    System.Web.UI.WebControls.WebControl
      System.Web.UI.WebControls.Button
```

表 14.6 列出了 Button 类值得关注的公共属性：

表 14.6：Button 类值得关注的公共属性

| 属性 | 描述 |
|---|---|
| CausesValidation | 获取或设置一个值，该值指示单击 Button 控件时是否执行验证。 |
| CommandArgument | 获取或设置一个可选参数，该参数与关联的 CommandName 属性一起传递给 Command 事件。 |
| CommandName | 获取或设置与 Button 控件关联的命令名称，该名称传递给 Command 事件。 |
| OnClientClick | 获取或设置当引发 Button 控件的 Click 事件时执行的客户端脚本。 |
| PostBackUrl | 获取或设置单击 Button 控件时要发布到的页面的 URL。 |
| Text | 获取或设置要在 Button 控件上显示的文本。 |
| UseSubmitBehavior | 获取或设置一个值，该值指示 Button 控件是使用客户端浏览器的提交机制还是使用 ASP.NET 回发机制向服务器提交数据。 |
| ValidationGroup | 获取或设置控件组，Button 控件在向服务器回发时会对该控件组执行验证。 |

Button 类值得关注的公共事件列于表 14.7：

表 14.7：Button 类值得关注的公共事件

| 事件 | 描述 |
|---|---|
| Click | 单击 Button 控件时发生。 |
| Command | 单击 Button 控件时发生。此事件帮助您在 Web 页面上创建多个 Button 控件，然后以编程方式确定单击了哪个 Button 控件。 |

Button 控件还用于在 Web 页面上创建下压按钮。下压按钮可以是提交按钮或命令按钮。默认情况下，Button 控件是提交按钮。提交按钮没有与 Button 控件关联的命令名称元素，您需要使用 CommandName 属性来指定该元素。您可以为 Click 事件提供事件处理程序，以编程方式控制在单击 Submit 按钮时执行的操作。

命令按钮具有与按钮关联的命令名称，您需要使用 CommandName 属性（例如 Sort）来指定该名称。这使您可以在 Web 页面上创建多个 Button 控件，并以编程方式找出单击了哪个 Button 控件。您可以为 Command 事件提供事件处理程序，以编程方式控制在单击 Command 按钮时执行的操作。

## TextBox 控件

TextBox 控件是一个输入控件，允许您输入文本。它位于 System.Web.UI.WebControls 命名空间中。此类的类层次结构如下：

```
System.Object
  System.Web.UI.Control
    System.Web.UI.WebControls.WebControl
      System.Web.UI.WebControls.TextBox
```

您可以使用 TextMode 属性设置 TextBox 控件的样式。默认情况下，TextMode 属性设置为 SingleLine 以创建单行 HTML 文本字段，但也可以设置为 MultiLine 以创建多行文本框。

您可以将 TextBox 控件的模式转换为 Password 控件，在这种模式下，您键入的文本会被特殊符号（如星号 (*)）屏蔽。

文本框的显示宽度通过其 Columns 属性设置，如果是多行文本框，则显示高度通过 Rows 属性设置。表 14.8 列出了 TextBox 类值得关注的公共属性：

