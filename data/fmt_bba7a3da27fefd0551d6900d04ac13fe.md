
| Label14 | Cost |

| Label15 | Amount |

| Button1 | Calculate Bill |

同样，设置 TextBox 和 Button 控件的 ID 属性，如表 18.4 所示。

| 表 18.4 设置控件的 ID 属性 |

| 控件 | ID |

| --- | --- |

| TextBox1 | txtProductName |

| TextBox2 | txtQuantity |

| TextBox3 | txtCost |

| TextBox4 | txtAmount |

| Button1 | btnCalculate |

在你设置控件的 Text 和 ID 属性后，Default.aspx Web 表单看起来就像图 18.5 所示。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_580_0.png)

图 18.5 Default.aspx Web 表单中的控件。

经 Microsoft 许可使用。

在 Default.aspx Web 表单中放置上述控件并设置它们的 Text 和 ID 属性后，会出现生成的代码，如列表 18.1 所示。代码代表了控件、它们在 Web 表单上的位置以及 Size、Font、Text、ID 等其他属性。

### 18.1 Default.aspx 文件中的程序代码

```aspx
<@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs"
Inherits=".Default" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
</</div>
<asp:Label ID="Label1" runat="server" Font-Bold="True" Font-Size="X-Large"
Text="Online Store"></asp:Label>
<br />
<br />
<asp:Label ID="Label2" runat="server" Text="Product Name"></asp:Label>
<asp:TextBox ID="txtProductName" runat="server"></asp:TextBox>
<br />
<asp:Label ID="Label3" runat="server" Text="Quantity"></asp:Label>
<asp:TextBox ID="txtQuantity" runat="server"></asp:TextBox>
<br />
<asp:Label ID="Label4" runat="server" Text="Cost"></asp:Label>
<asp:TextBox ID="txtCost" runat="server"></asp:TextBox>
<br />
<asp:Label ID="Label5" runat="server" Text="Amount"></asp:Label>
<asp:TextBox ID="txtAmount" runat="server"></asp:TextBox>
<br />
<asp:Button ID="Button1" runat="server" Text="Calculate Bill" />
</form>
</body>
</html>
```

# 构建你的第一个 Web 应用程序

并将文本转换为整数格式后将其赋值给变量 `q`。`Convert.ToInt32()` 函数将文本转换为整数。同样，输入到 `txtCost` 中的产品成本在将 Text 数据转换为单一类型（单精度浮点数）后，被检索到变量 `r` 中。然后将变量 `q` 和 `r` 中的值相乘，结果赋值给变量 `a`。变量 `a` 中的金额赋值给控件 `txtAmount` 的 `Text` 属性。变量 `a` 中的浮点值在赋值给 `txtAmount` 的 `Text` 属性之前，会被转换为字符串。

代码列表 18.2 中的 `btnCalculate_Click()` 方法是一个事件处理方法，包含了你在 Button 控件上发生点击事件时想要执行的代码。表 18.5 显示了事件列表及其关联的控件。

### 18.5 控件及其常用事件列表

| 事件 | 属性 | 控件 |

| --- | --- | --- |

| Click | OnClick | Button, ImageButton, LinkButton, ImageMap |

| Command | OnCommand | Button, ImageButton, LinkButton |

| TextChanged | OnTextChanged | TextBox |

| SelectedIndexChanged | OnSelectedIndexChanged | DropDownList, ListBox, RadioButtonList, CheckListBox |

| Changed | OnCheckedChanged | CheckBox, RadioButton |

列表 18.2 中另一个需要解释的内容是 `Page_Load` 方法。当服务器请求页面时，会发生两个事件：`Init` 和 `Load`。在这两个事件中，`Init` 事件首先发生并触发以便恢复页面及其控件的状态。在所有控件初始化后，会调用 `Page_Load` 事件来执行表单控件的初始化、定义 `SqlConnection`（如果有）、检索某些数据等。因此，每当页面加载进行处理时，都会调用 `Page_Load` 方法。以下是 `Page_Load` 的语法：

```
protected void Page_Load(object sender, System.EventArgs e)
```

# 第 18 章 ■ .NET Web 应用程序开发

- `protected` 访问修饰符指定了只有相同类中的程序可以使用此方法。
- `void` 关键字意味着该事件处理方法不会返回值。
- 括号中的参数 `(object sender, System.EventArgs)` 是 ASP.NET 传递给事件方法的变量。`sender` 是触发事件的对象；第二个参数 `e` 包含了事件处理方法可能需要的额外信息。

运行网站后，你将得到图 18.6 所示的输出。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_584_0.png)

**图 18.6** CalculateBillApp 网站的输出。

经微软许可使用。

在你输入产品名称、数量、成本和金额后，点击“Calculate Bill”（计算账单），将调用 `btnCalculate_Click` 方法并显示金额。

现在你将为你的网站 CalculateBillApp 添加一个功能：计算销售产品总额的折扣。为了计算折扣，你将在 Default.aspx Web 表单中再添加两个 `Label` 和 `TextBox` 控件。将 `Label6` 和 `Label7` 的 `Text` 属性分别改为“Discount”（折扣）和“Net Amount”（净额）。将 `TextBox5` 和 `TextBox6` 控件的 `ID` 设置为 `txtDiscount` 和 `txtNetAmount`。在你添加这些控件并设置属性后，你的 Default.aspx Web 表单如图 18.7 所示。

# 构建你的第一个 Web 应用程序

![](img/3ca47f8f6f5560f07650d3563e2f2c05_585_0.png)

### 图 18.7

设置了两个 Label 和 TextBox 控件的 Text 属性后的 Web 表单。

经微软许可使用。

在你点击“Calculate Bill”按钮后，你希望根据这里给出的公式计算金额、折扣和净额：

Amount=Quantity * Cost

Discount=10% of Amount

Net Amount=Amount-Discount

由于你希望在点击“Calculate Bill”按钮后计算并显示这些内容，你需要在 Button 控件的点击事件处理方法中编写代码。双击“Calculate Bill”按钮并按如下所示编写代码：

```
protected void btnCalculate_Click(object sender, EventArgs e)
{
    int q;
    float d, n, r, a;
    q = Convert.ToInt32(txtQuantity.Text);
    r = Convert.ToSingle(txtCost.Text);
    a = q * r;
    d = (float)a * 10 / 100;
    n = a - d;
    txtAmount.Text = a.ToString();
    txtDiscount.Text = d.ToString();
    txtNetAmount.Text = n.ToString();
}
```

你包含了两个浮点变量：`d` 和 `n`（分别用于存储折扣和净额的值）。用户在 `txtQuantity` 控件中输入的数量在文本转换为整数后被检索并存储在变量 `q` 中。同样，输入到 `txtCost` 中的成本在将 Text 类型转换为 `Single`（单精度浮点数）后被检索并存储在变量 `r` 中。然后将 `q` 和 `r` 相乘以计算总额，并存储在变量 `a` 中。之后，计算出总额 10% 的折扣，并赋值给变量 `d`。通过从总额 `a` 中减去折扣 `d` 可以很容易地计算出净额。变量 `a` 中的浮点值在赋值给 `txtAmount` 之前，会被转换为字符串。同样，折扣和净额分别赋值给 `txtDiscount` 和 `txtNetAmount`。运行网站后，你将得到图 18.8 所示的输出。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_586_0.png)

（注：此处原文路径似乎不完整，已原样保留）

到为止，你已经学会了如何使用 Label、TextBox 和 Button 控件。现在你将学习如何通过 DropList 控件显示不同的选项。

# 使用 DropList 控件

`DropDownList` 控件提供了用户可以选择的任何选项。`DropDownList` 中显示的选项可以从表格、数组列表或其他数据源检索。当选择 `DropDownList` 中的任何项时，你可以通过 `SelectedIndex` 属性获取选中项的索引。你可以通过 `SelectedItem` 属性访问 `DropDownList` 控件的选中项名称。初始情况下，`DropDownList` 控件的 `SelectedIndex` 属性为0，这意味着默认选择了控件的第一项。

为了实际理解如何使用 `DropDownList`，你将将其应用于之前创建的 CalculateBillApp。你将通过 `DropDownList` 控件显示三种类型的客户。不再使用固定的10%折扣，而是根据客户所属的类别计算折扣。你将通过 `DropDownList` 显示的三个类别是“Individual”（个人）、“Non Profit Organization”（非组织）和“Corporate”（企业）。个人、非组织和企业客户的折扣分别为10%、20%和15%。

启动 Visual Studio 并打开 CalculateBillApp。在 Default.aspx 表单上拖入一个 `Label` 和 `DropDownList` 控件。将 `Label` 控件的 `Text` 属性设置为“Category”（类别），如图 18.9 所示。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_587_0.png)

**图 18.9**

CalculateBillApp 网站 Default.aspx 上添加的 Label 和 DropList 控件。

经微软许可使用。

将 `DropDownList` 控件的 `ID` 属性设置为 `drpdnCategory`。为了通过 `DropDownList` 控件显示三个选项，请在后代码文件 Default.aspx.cs 中添加以下代码：

```
protected String[] category = { "Individual", "Non Profit Organization", "Corporate" };
protected void Page_Load(object sender, EventArgs e)
```

```csharp
if (!IsPostBack)
{
    drdpnCategory.DataSource = category;
    drdpnCategory.DataBind();
}
```

如前所述，你可以通过 DropList 控件显示三个字符串选项：个人（Individual）、非营利组织（Non Profit Organization）和企业（Corporate）。为了实现，你需要使用字符串数组 `category`（用于指定客户类型），并将三个选项作为数组元素存储在 `category` 数组中。之后，将 DropList 控件绑定到字符串数组 `category`。通过使用 `DataBind` 方法，`DataSource`（category 数组）的内容会被分配给 DropList 控件。上述代码中使用的 `IsPostBack` 方法需要解释。

当点击按钮时，会触发 `Page_Load` 事件。这意味着当 Web 表单首次加载以及 Web 表单上的任何控件发生事件时，都会触发 `Page_Load` 事件。但有时你可能希望特定的代码只执行一次。例如，在 `Page_Load` 方法中初始化的变量，你不希望在事件发生时重新初始化。在这种情况下，你可以在下面的 `if` 块中编写代码：

```csharp
if (!IsPostBack)
{
    ------------------
}
```

`IsPostBack` 用于标识页面是否已回传（posted）。如果页面是首次加载，`IsPostBack` 返回 `false`；如果页面已经加载，`IsPostBack` 返回 `true`。当你在上述 `if` 块中编写语句集时，这些语句只会执行一次（在 `IsPostBack` 返回 `false` 时——即页面加载时）。当表单上的任何控件发生事件时，这些语句不会执行。

当你移动到另一个页面时，`IsPostBack` 会重置。

## 构建你的第一个 Web 应用程序

除了 `IsPostBack` 方法外，还有另一种处理页面回传的方法：使用 `AutoPostBack` 属性。

## 理解 AutoPostBack 属性

对于非回传控件，`AutoPostBack` 属性设置为 `false`。回传控件会导致表单立即回传或提交到服务器。例如，`Button` 是一个回传控件；它有一个回传事件 `Button.Click`，当点击事件发生时，它会导致表单立即回传或提交到服务器。非回传控件（如 `CheckBox` 和 `DropDownList`）具有非回传事件，这意味着当事件发生时，表单不会立即回传，而是缓存起来直到下一次回传发生。通过将这些非回传控件的 `AutoPostBack` 属性设置为 `true`，你可以确保在发生非回传事件时，表单也会立即提交。

以下是回传控件：

- Button
- Calendar
- DataGrid
- DataList
- FileUpload
- GridView
- ImageButton
- ImageMap
- LinkButton
- Menu
- Repeater

以下是非回传控件：

- BulletedList
- CheckListBox
- DropList
- ListBox
- RadioButtonList
- RadioButton
- TextBox

假设客户属于个人、企业或非营利组织，并根据以下规则计算折扣：

- 个人（Individual）类别提供 10% 折扣
- 企业（Corporate）类别提供 15% 折扣
- 非营利组织（Non Profit Organization）类别提供 20% 折扣

要通过 `DropDownList` 控件显示选项并根据从 `DropDownList` 控件选择的类别计算折扣，请修改后台代码文件 `Default.aspx.cs`，使其如列表 18.3 所示。

## 列表 18.3 Default.aspx.cs 文件中的代码
