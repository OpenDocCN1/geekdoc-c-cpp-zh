

## 使用查询进行筛选

你可能希望让一个窗体控件控制另一个控件。或者你可能希望记录集根据用户输入的临时条件显示选定的数据。例如，每次运行报表时，都会显示一个对话框，用户输入一组日期或选择产品或客户。实现此目的的一种方法是使用参数查询。

## 创建参数查询

参数查询是指任何查询的准则引用变量、函数或窗体上的控件。通常，你在准则输入区域输入 SMITH、26 或 6/15/18 等值。但你也可以输入变量（也称为提示），例如 [Enter the Last Name] 或引用窗体上的控件，例如 Forms!frmProducts![cboQuickFind]。

ON THE WEB
Chapter29.accdb 数据库包含一个名为 qryProductParameterQuery 的参数查询。

创建参数查询最简单的方法是创建一个选择查询，指定查询的准则，并运行查询以确保其正常工作。然后将准则更改为以下内容：

- Like [<some prompt>] & "*"
- OR:
- Like "*" & [<some prompt>] & "*"

其中 <some prompt> 是你希望向用户提出的问题。图 29.7 显示了一个参数查询，每次运行查询时都会提示用户输入产品类别。

### FIGURE 29.7

Creating a simple parameter query.

![](img/1e45673ab6eca9d20e67635ff5b9b318_990_0.png)

## Part VII: Advanced Access Programming Techniques

无论查询如何运行，即使它用作窗体或报表的记录源，或列表或组合框的行来源，参数对话框都会显示——并且根据输入的内容，查询准则会筛选查询结果。图 29.8 显示了参数对话框打开，提示输入查询所需产品类别值。

### FIGURE 29.8

Running the parameter query.

![](img/1e45673ab6eca9d20e67635ff5b9b318_991_0.png)

你可能记得学习过 Like 运算符允许使用通配符搜索。例如，如果你想筛选查询记录为任何以 "car"（或 "CAR"）开头的产品类别，你在参数对话框中输入 CAR。如果没有参数，你必须在查询的准则区域输入 Like "CAR*"。此外，由于通配符 (*) 已作为参数的一部分包含在内，用户在响应参数对话框时无需包含通配符。

### Tip

你可以在任何查询或 SQL 字符串中使用通配符 *（此位置及之后的所有内容）和 ?（此位置的一个字符）与 Like 运算符一起使用。

### NOTE

如果选择了 SQL Server 兼容语法（ANSI 92）（选择 File → Options，然后选择 Object Designers 选项卡）或如果使用 ADO 运行 SQL 语句，则通配符为 %（此位置及之后的所有内容）和 _（此位置的一个字符）。

添加星号到参数的一个后果是，如果用户未输入参数值，则准则会计算为 "LIKE *" ，查询将返回除空值外的所有记录。如果在准则表达式中省略星号，则如果用户未能提供产品类别，则不会返回任何记录。

图 29.9 显示了查询参数对话框（通过右键单击查询的上部区域并从快捷菜单中选择 Parameters 打开）。你使用查询参数对话框来指定需要特别考虑的参数，例如日期/时间输入或特殊格式的数字。已在查询参数对话框中输入一个文本条目以显示其工作原理。你输入参数文本并选择参数的数据类型。

### FIGURE 29.9

The Query Parameters dialog box.

![](img/1e45673ab6eca9d20e67635ff5b9b318_992_0.png)

> TIP
> 如果你想添加更复杂的参数，例如日期范围，请在日期字段中使用 Between [Enter the Start Date] and [Enter the End Date] 等表达式作为准则。这将显示两个单独的参数对话框，然后相应地筛选日期值。

不幸的是，Access 参数查询不提供为参数提供默认值的方法。你最好的选择是始终在准则表达式中包含星号，这样如果用户在未输入值的情况下关闭参数对话框，查询将返回所有记录，因为准则表达式将解析为 Like "*"。

## 创建交互式筛选对话框

> **CAUTION**
> 你只能对文本字段使用 like "*" 。对于数字字段，你可以将准则设置为 [My Prompt] OR [My Prompt] IS NULL。只需确保 My Prompt 的两个出现都完全相同地输入。（复制和粘贴是个好主意。）如果你想返回包括空值在内的所有记录，也可以使用此技术与文本字段一起使用。

参数查询的问题在于它们只适用于简单的参数。用户必须确切知道要在参数对话框中输入什么内容，如果他们输入参数不正确，就不会看到预期的结果。此外，使用参数查询输入复杂准则相当困难。

更好的技术是创建一个简单的窗体，在窗体上放置控件，并从查询中引用控件作为参数。换句话说，查询使用窗体的控件获取其参数值。这对用户来说是一个巨大的优势，因为控件可以通过呈现可接受参数值的列表或下拉菜单来帮助用户选择准则。此外，可以向每个控件的 AfterUpdate 事件添加代码以验证用户输入，以确保查询确实可以运行。组合框或列表框等控件的内容可以是动态的，并包含来自底层表中的实际值。这意味着准则控件可能只包含已下过订单的客户名称，或数据库中当前实际存在的产品类别。

图 29.10 显示了 frmFilterProducts 在设计视图中。cboCategory 用 qryCategories 中的数据填充，该查询按字母顺序对 tblCategories 中的记录进行排序。

### FIGURE 29.10

Creating a dialog box for selecting records.

![](img/1e45673ab6eca9d20e67635ff5b9b318_993_0.png)

cboCategory 的 Default Value 属性设置为 Cars，因为这是 Products 窗体最常用的准则。在这种情况下，Limit To List 设置为 Yes，因为我们希望强制用户仅从 tblCategories 中实际存在的类别中选择。

图 29.11 显示了 qryProducts_FormParameter。此查询根据从 frmFilterProducts 上的 cboCategory 检索到的类别选择 tblProducts 中的所有字段。请注意 Criteria 列中的准则表达式。

```
= [Forms]![frmFilterProducts]![cboCategory]
```

查询运行时，它会自动从 cboCategory 检索准则值。组合框返回 Cars，除非用户选择了不同的类别。

### FIGURE 29.11

Creating a query that references a form control.

![](img/1e45673ab6eca9d20e67635ff5b9b318_994_0.png)

在正常操作中，用户从 frmFilterProducts 中选择产品类别并单击 OK。按钮后面的代码打开 frmProductsExample4，该窗体绑定到 qryProducts_FormParameter。qryProducts_FormParameter 中 Category 字段的准则查找 frmFilterProducts 上 cboCategory 中选择的 value，然后神奇地 frmProductsExample4 打开，仅加载所选产品类别。

开发人员在使用这种紧密集成的数据库对象时面临的唯一问题是（在本例中为 frmFilterProducts、qryProducts_FormParameter 和 frmProductsExample4），可能并不明显这些对象协同工作。删除或修改这些对象中的任何一个都可能破坏工作流程或给用户带来问题。

你可能会选择使用一种命名约定来暗示两个窗体和查询之间的关系，例如为每个项目赋予相同的名称，但使用不同的

## Linking the dialog box to another form

前缀。或者，你可以使用导航窗格中的自定义组并将对象添加到单个组。非常经常对你来说显而易见的事情——原始设计师和开发人员——可能对其他人来说并不那么清楚，因此利用有助于记录应用程序的简单技术是值得的。

> **CAUTION**
> 
> 当 frmFilterProducts 未打开时运行 qryProducts_FormParameter 将导致查询提示用户输入值。当 frmFilterProducts 未打开时，Access 无法弄清楚准则 `[Forms]![frmFilterProducts]![cboCategory]` 的含义，因为没有名为 frmFilterProducts 的窗体加载。在这种情况下，Access 假定参数是提示并显示输入框。

frmFilterProducts 对话框（参见图 29.10）不仅仅是创建可从查询引用的值。它还包含用于打开 frmProductsExample4 的代码。

图 29.12 显示了 frmFilterProducts 上 Cancel 和 OK 按钮后面的 cmdCancel_Click 和 cmdOK_Click 事件过程。

![](img/1e45673ab6eca9d20e67635ff5b9b318_995_0.png)

cmdOK_Click 事件过程代码打开 frmProductsExample4，将焦点设置在其上，然后重新查询窗体以确保使用最新的选择。SetFocus 方法对于将焦点移动到打开的窗体是必要的。Requery

