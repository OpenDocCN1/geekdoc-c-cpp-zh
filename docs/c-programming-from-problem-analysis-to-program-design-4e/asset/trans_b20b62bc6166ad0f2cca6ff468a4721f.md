

![](img/36e48639a06772bcb0fa1ea2525b33a3_1059_0.png)

示例 15-8 展示了 RadioButton 的 CheckedChanged() 事件的事件处理方法。

## 示例 15.8

```csharp
protected void radButtons_CheckedChanged(object sender, EventArgs e)
{
    if (radBtnFresSop.Checked)
    {
        lblClassif.Text = "Freshmen & Sophomores ";
    }
    else if (radBtnJrSr.Checked)
    {
        lblClassif.Text = "Junior & Seniors ";
    }
    else if (radBtnOther.Checked)
    {
        lblClassif.Text = "Special Students ";
    }
    lblClassif.Text += " Always Welcome!";
}
```

**Submit** 按钮的事件处理方法用于检索用户在 TextBox 字段中输入的值以及从 ListBox 对象中进行的选项。这些值用于填充 Label 控件，当页面为客户端重新加载时显示这些控件。示例 15-9 展示了 btnSubmit 事件处理方法。

## 示例 15.9

```csharp
protected void btnSubmit_Click(object sender, EventArgs e)
{
    lblSubmit.Text = "Thanks " + txtBxFname.Text +
        "! You will be contacted...";
    if (lstBxInterests.SelectedIndex > -1)
    {
        lblSubmit.Text += " to discuss joining" +
            " the \"" + lstBxInterests.SelectedItem.Text +
            "\" team.";
    }
}
```

在图 15-19 中，您可以看到所显示的 Web 应用程序中添加了另外两个控件：Calendar 和 GridView。此外，表单中还添加了一个验证控件。这些特殊控件将在下一节讨论。

## 验证、自定义和复合控件

如图 15-19 所示，左下角添加了一个 Calendar 控件，右下角添加了一个 GridView 控件，用于显示从 Microsoft Access 数据库中检索到的数据。这些是本节将讨论的特殊类型控件。另外，您没有看到，但还有一种类型的控件——验证控件被添加到表单中。首先讨论验证控件。

> **注意**
> 本示例中放置在 Web 窗体上的所有控件都使用了绝对定位。控件一被拖到窗体上，该控件即被选中，并从“格式”菜单中设置了“位置，绝对”。

### 验证控件

回顾图 15-17。注意有一个标记为“验证”的特殊选项卡。该选项卡的“工具箱”中列出了几种不同类型的验证控件。这些控件使输入可以由服务器进行验证或检查。表 15-2 按字母顺序列出了这些控件，并描述了它们的基本功能。

### 表 15-2 .NET 验证控件

| 控件类型 | 描述 |
|---|---|
| CompareValidator | 使用比较运算符将输入值与预设的常量值进行比较 |
| CustomValidator | 使用您自己编写的程序语句检查输入值 |
| RangeValidator | 比较输入值，看它是否在指定的上下边界之间（可以检查日期、数字或字母字符的范围） |
| RegularExpressionValidator | 将输入值与定义为正则表达式的模式进行匹配（用于电子邮件、电话号码和社会保险号等条目，以查看这些值是否与可预测的序列匹配） |
| RequiredFieldValidator | 检查输入项是否有值 |

### 验证控件属性

要使用这些控件之一，请将该控件拖到 Web 窗体页上，并将其放置在要验证的控件旁边。然后，您可以像对待任何其他控件一样对待验证控件对象。它具有可以设置的属性。使用 ControlToValidate 属性，您可以将验证控件绑定到特定的窗体控件对象，例如 TextBox 对象。ErrorMessage 属性可以设置为当输入控件未通过验证测试时要显示的消息，并且可以更改错误消息的颜色。

### 添加 RequiredFieldValidator 控件

图 15-21 演示了为名字添加一个 RequiredFieldValidator 控件。

![](img/36e48639a06772bcb0fa1ea2525b33a3_1062_0.png)

**图 15-21** 添加 RequiredFieldValidator 控件

注意，在图 15-21 中，txtBxFname 被设置为 ControlToValidate 属性的值。"Required!" 被设置为 ErrorMessage 值。ForeColor 选择了红色。EnableClientScript 被设置为 False。RequiredFieldValidator 控件被物理放置在其正在验证的 TextBox 对象的旁边（而不是顶部）。

> **注意**
> 将验证控件放置在您希望显示错误消息的位置；它不必放在被验证控件的旁边。有时由于空间限制，验证控件无法放置在其正在验证的控件旁边。与其他控件一样，要将其添加到窗体上，请从 **工具箱** 窗口中拖放它。

在添加 RequiredFieldValidator 控件并将其绑定到 txtBxFname 对象后，如果表单加载并提交到服务器时 txtBxFname 控件中没有输入任何值，则会以红色显示 "Required!"。显示 "Required!" 是因为 ErrorMessage 属性值被设置为 "Required!"。这只是在设计期间键入的一个值。

使用验证控件可用的 Text 属性，您还可以自定义向用户显示的错误信息。一种常见做法是将验证控件的 Text 属性设置为红色星号（星号），并将其放置在要验证的输入框旁边。如果这样做，当控件未通过验证时，运行时将显示一个星号。

> **注意**
> 请注意，Text 属性和 ErrorMessage 属性都用于设置验证失败时打印的消息。如果同时设置了这两者，Text 属性会覆盖 ErrorMessage 属性。

### 页面验证

默认情况下，当单击窗体上任意按钮时都会发生页面验证。之所以称为页面验证，是因为页面上每一个关联了验证控件的控件字段都会被检查，看它是否通过验证规则。如果您不希望一个或多个 Button 对象引发页面验证，可以在 Button 上设置一个名为 CausesValidation 的属性。默认情况下，每个 Button 对象的 CausesValidation 属性都被设置为 true。

> **注意**
> 在设计解决方案时，请仔细考虑哪些按钮应导致输入控件的页面验证。对所有其他 Button 对象，将 CausesValidation 设置为 false。

在名字文本框键入值之前单击 Submit Info 按钮，会导致验证错误消息 "Required!" 以红色显示，如图 15-22 所示。

![](img/36e48639a06772bcb0fa1ea2525b33a3_1063_0.png)

**图 15-22** RequiredFieldValidator 控件产生的错误消息

回顾表 15-2 中的预定义验证控件列表。列出的另一个验证控件是 RangeValidator。使用 RangeValidator，您可以确保用户输入的值落在预定的值集之间。该控件可用于测试有效日期，以确保输入的日期落在特定范围内，或者测试数值，以确保它们落在设计期间指定的范围内。您可以使用 RegularExpressionValidator 控件进行模式匹配。使用 RegularExpressionValidator 控件对电子邮件地址进行检查，以确保包含 @ 符号。一个输入对象可以关联多个验证控件。建议您进行实验并查阅 MSDN 文档。

在运行时，您可以使用 `Page.IsValid` 属性来检查页面上的所有验证控件当前是否都有效。该属性可以放在选择语句中，根据其布尔结果执行相应操作。

## 页面生命周期

Web 编程的性质与 Windows 应用程序开发不同，原因在于页面生命周期。Web 页面上有许多事件会自动且按顺序触发。它们包括 Page_PreInit()、LoadViewState()、LoadPostBackData()、Page_Load() 以及最终的 Page_Unload() 等方法。事件的顺序有些复杂。前面已经指出，当您创建新的 Web 窗体页时，会自动添加一个 Page_Load() 方法。您无需做任何额外或特殊的事情来注册它。只要您在名称中包含了 "Page" 一词，它与其他页面方法一样，会在页面加载时被触发。Page_Load() 和其他方法的方法体包含在代码隐藏文件中。您不必为所有这些方法都提供方法体；许多 ASP.NET 应用程序确实包含一个 Page_Load() 事件处理程序。Page_Load() 方法是 .aspx 文件的服务端应用程序代码中最常用的方法。

最后处理的方法是 Page_Unload()。在此方法期间，可以释放数据以释放服务器上的资源供其他进程使用。此方法完成后，HTML 会被发送到浏览器进行客户端处理。

回想一下，Windows 应用程序的加载事件 Form_Load() 只执行一次——在应用程序最初运行时执行。Web 窗体的 Page_Load() 事件不仅在应用程序最初加载时触发，而且会执行多次。每次单击按钮以及每次加载页面时都会执行。有时需要确定这是否是页面第一次被加载，还是回发、第二次或后续加载。ASP.NET 提供了一个特殊属性 IsPostBack，它返回一个布尔值，指示页面是否是第一次被加载。

如果您只想在页面第一次被加载时执行 Page_Load() 方法中的代码，可以使用 Page.IsPostBack 属性。如果 Page.IsPostBack 属性返回 false，则页面是第一次被加载。如果返回 true，则页面被回发到服务器，例如当单击表单上的按钮时会发生这种情况。

如前所述，Web 基本上是无状态的。每个页面请求都被视为新请求。默认情况下，一个请求中的信息不会提供给下一个请求，这意味着每次单击按钮时，您都会丢失上一次页面加载时的值。对于 Web 页面，每个请求都会实例化 Page 类

