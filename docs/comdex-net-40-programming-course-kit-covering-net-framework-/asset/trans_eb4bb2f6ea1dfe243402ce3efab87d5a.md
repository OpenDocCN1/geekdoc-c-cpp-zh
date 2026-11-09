
在单个 ASP.NET 4.0 应用程序中使用不同语言。你可以通过将 Web 应用程序配置为把 App_Code 文件夹的子文件夹视为单独的可编译单元，从而在单个 ASP.NET 4.0 应用程序中使用不同语言。Web.config 文件中 `compilation` 元素的 `codeSubDirectories` 元素可帮助你实现多语言支持功能，其中每个文件夹可以包含不同编程语言的源代码。例如，你可以通过在 Web.config 文件中使用以下代码片段，将名为 VB 和 CS 的子文件夹配置为编译到单独的程序集中：

```xml
<compilation debug="false">
    <codeSubDirectories>
        <add directoryName="VB" />
        <add directoryName="CS" />
    </codeSubDirectories>
</compilation>
```

在前面的代码片段中，引用 VB 和 CS 子文件夹不需要有关编程语言的任何信息。

# 优化动态编译

如你所知，如果对动态编译的 ASP.NET 文件做任何更改，它会自动使该文件缓存的已编译程序集失效，并触发所有受影响资源（如 .dll 文件）的重新编译。然而，对于大型应用程序，此重新编译过程可能会使应用程序在很长时间内不可用，即使更改很小。

你可以通过在 Web.config 文件中将 `optimizeCompilations` 属性设置为 True 来避免这种情况。这意味着，在将此属性设置为 True 后，当你实施任何更改时，只会重新编译发生更改的文件。

# 描述动态编译的缺点

ASP.NET 应用程序中动态编译的缺点如下：

- 用户响应时间慢，因为 ASP.NET 页面和代码必须在首次请求时编译
- 在用户访问网站之前，无法识别任何编译时 Bug
- 无法创建可在没有源代码的情况下部署到生产服务器上的网站编译版本

# 总结

在本章中，你学习了 ASP.NET 及其各种版本。本章还描述了使用 ASP.NET 而不是早期编程语言开发 Web 应用程序的优势。此外，还介绍了 ASP.NET 4.0 的新功能，例如它对 ASP.NET AJAX 的支持，以及动态控件的添加。本章还重点介绍了编码模型和提供程序模型。接下来，你学习了开发 Web 应用程序所需的代码共享和编译概念。

在下一章中，你将学习在 ASP.NET 4.0 中使用标准控件。

# 标准控件

## 第 2 章

## 本章内容：

- *介绍 WebControl 类*
- *使用 Label 控件*
- *使用 TextBox 控件*
- *使用 Button 控件*
- *使用 ImageButton 控件*
- *使用 ListBox 控件*
- *使用 RadioButton 控件*
- *使用 CheckBox 控件*
- *使用 Table 控件*
- *使用 Wizard 控件*
- *使用 Calendar 控件*
- *使用 AdRotator 控件*

**WebControl** 类值得注意的方法列于表 2.2：

**表 2.2：WebControl 类值得注意的方法**

| **方法** | **描述** |
|---|---|
| `ApplyStyle` | 将指定样式的任何非空元素复制到 Web 控件。它还会覆盖控件的任何现有样式元素。 |
| `MergeStyle` | 将指定样式的任何非空元素复制到 Web 控件，但不会覆盖控件的任何现有样式元素。 |
| `RenderBeginTag` | 将指定标记元素的开始标记写入输出流。 |
| `RenderEndTag` | 将标记元素的结束标记写入输出流。 |

讨论完 **WebControl** 类后，现在让我们了解 **Label** 控件。

## 使用 Label 控件

Label 控件用于在 Web 窗体上显示不可编辑的文本。你可以通过在设计时或运行时设置 Label 控件的 Text 属性来设置该控件上的文本。Label 控件作为输出控件工作，可显示动态文本和静态文本。你还可以通过设置其各种属性（如 ForeColor 和 BackColor）来更改此控件的外观。

表 2.3 列出了 Label 控件值得注意的属性：

**表 2.3：Label 类值得注意的属性**

| **属性** | **描述** |
|---|---|
| `BackColor` | 指定 Label 控件的背景色 |
| `BorderColor` | 指定 Label 控件的边框颜色 |
| `BorderStyle` | 指定 Label 控件的边框样式 |
| `BorderWidth` | 指定 Label 控件的边框宽度 |
| `Font` | 指定字体属性 |
| `ForeColor` | 指定文本颜色 |
| `Height` | 指定 Label 控件的高度 |
| `Text` | 获取或设置要在 Label 控件中显示的文本 |
| `Width` | 指定 Label 控件的宽度 |

现在，让我们按照以下步骤学习在 Web 应用程序中使用 Label 控件：

- 1. *打开 Visual Studio 2010。*
- 2. 从菜单栏中*选择* **文件 → 新建 → 网站**。将打开 **新建网站** 对话框。
- 3. 在“新建网站”对话框的“已安装的模板”窗格中*选择* **Visual C#**。
- 4. 在 **新建网站** 对话框的右窗格中*选择* **ASP.NET 网站**。
- 5. 在 Web 位置组合框中指定应用程序的位置和名称。在此例中，我们提供的名称为 **Label Example**。
- 6. 单击 **确定** 按钮保存所有设置。将创建 **LabelExample** 应用程序（CD 中也提供）（图 ASP-2.1）。
- 7. 单击 **设计** 选项卡查看 **Default.aspx** 页面的设计（图 ASP-2.1）。
- 8. 从 **工具箱** 中在 Web 窗体上*添加*一个 **Label** 控件，如图 ASP-2.1 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_483_0.png)

图 ASP-2.1

一旦将 Label 控件放到 Web 窗体上，以下代码片段就会添加到 Web 页面的源代码中：

```aspx
<asp:Label ID="Label1" runat="server" Text="Label"></asp:Label>
```

- 9. *右击* Web 窗体上的 **Label1** 控件，并从上下文菜单中选择 **属性** 选项（图 ASP-2.2）。
- 10. 将 **Label** 控件的 **Text** 属性设置为 **欢迎使用 Visual Studio 2010**，如图 ASP-2.3 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_483_1.png)

图 ASP-2.2

![](img/9862a98a1a2d3bb14334137965a1ec60_483_2.png)

图 ASP-2.3

![](img/9862a98a1a2d3bb14334137965a1ec60_483_3.png)

> 你也可以按 F4 键打开控件的“属性”窗口。

- 11. *按* F5 键在浏览器中查看输出，如图 ASP-2.4 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_484_0.png)

接下来，让我们了解 TextBox 控件。

## 使用 TextBox 控件

TextBox 控件是一个输入控件，允许你输入文本。默认情况下，TextBox 控件只接受一行文本。你可以通过修改 TextBox 控件的相应属性，使 TextBox 控件接受多行文本、以密码形式显示文本，以及禁用 TextBox 控件中的文本编辑。TextBox 控件主要作为输入控件工作；不过，它也可以作为输出控件，在运行时向用户显示文本。TextBox 类存在于 System.Web.UI.WebControls 命名空间中。

TextBox 控件值得注意的属性列于表 2.4：

**表 2.4：TextBox 控件值得注意的属性**

| **属性** | **描述** |
|---|---|
| `AutoCompleteType` | 获取或设置一个值，该值指示 TextBox 控件的自动完成行为 |
| `AutoPostBack` | 获取或设置一个值，该值指示当 TextBox 控件失去焦点时是否自动回发到服务器 |
| `Columns` | 获取或设置文本框的显示宽度（以字符为单位） |
| `MaxLength` | 获取或设置文本框中允许的最大字符数 |
| `ReadOnly` | 获取或设置一个值，该值指示 TextBox 控件的内容是否可以更改 |
| `Rows` | 获取或设置多行文本框中显示的行数 |
| `Text` | 获取或设置 TextBox 控件的文本内容 |
| `TextMode` | 获取或设置 TextBox 控件的行为模式（单行、多行或密码） |
| `ValidationGroup` | 获取或设置一组控件，当 TextBox 控件回发到服务器时，将对这些控件进行验证 |
| `Wrap` | 获取或设置一个值，该值指示文本内容是否在多行文本框内换行 |
