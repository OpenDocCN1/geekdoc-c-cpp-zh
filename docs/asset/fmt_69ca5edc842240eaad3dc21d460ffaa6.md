
正如图中的代码示例所示，你使用 `DataSourceID` 属性来指定 `DetailsView` 控件应绑定到的數據源。然后，`Fields` 元素包含一组子元素，用于定义 `DetailsView` 控件要显示的各个字段。这与 `GridView` 控件的 `Columns` 元素的工作方式类似。

`DetailsView` 控件可以以三种模式之一显示。在 `ReadOnly` 模式下，当前数据源行的數據会显示但不能修改。在 `Edit` 模式下，用户可以修改当前行的數據。而在 `Insert` 模式下，用户可以输入将作为新行插入到数据源中的數據。

## 显示所选产品的 DetailsView 控件

![](img/c024ccf88e28c30c07dd410d4342288f_504_0.png)

## 上述所示 DetailsView 控件的 aspx 代码

```
<asp:DetailsView ID="DetailsView1" runat="server" AutoGenerateRows="False" DataKeyNames="ProductID" DataSourceID="SqlDataSource2" Width="450px">
    <Fields>
        <asp:BoundField DataField="ProductID" HeaderText="Product ID:" ReadOnly="True">
            <HeaderStyle Width="125px" />
            <ItemStyle Width="325px" />
        </asp:BoundField>
        <asp:BoundField DataField="Name" HeaderText="Name:" />
        <asp:BoundField DataField="ShortDescription" HeaderText="Short Description:" />
        <asp:BoundField DataField="LongDescription" HeaderText="Long Description:" />
        <asp:BoundField DataField="CategoryID" HeaderText="Category ID:" />
        <asp:BoundField DataField="ImageFile" HeaderText="Image File:" />
        <asp:BoundField DataField="UnitPrice" HeaderText="Unit Price:" />
        <asp:BoundField DataField="OnHand" HeaderText="On Hand:" />
    </Fields>
</asp:DetailsView>
```

## DetailsView 控件的三种模式

| Mode | Description |
|------|-------------|
| ReadOnly | 用于从数据源显示一项。 |
| Edit | 用于编辑数据源中的一项。 |
| Insert | 用于向数据源中插入新项。 |

## 描述

- `DetailsView` 控件显示数据源中单行的數據。它通常与用于选择要显示的项的下拉列表或 `GridView` 控件结合使用。
- `DetailsView` 元素包含一个 `Fields` 元素，其中包含从数据源检索的每个字段的 `BoundField` 元素。
- 你可以通过从 `DetailsView` 控件的智能标记菜单中选择 `Edit Fields` 来编辑字段集合。

## DetailsView 控件的属性和子元素

图 15-2 中的表格列出了用于声明 `DetailsView` 控件的属性和子元素。第一个表格列出了你最有可能为此控件使用的属性。你可以使用 `DataKeyNames` 属性列出数据源的主键字段的名称。并且，如果你希望 `DetailsView` 控件自动生成数据字段，可以将 `AutoGenerateRows` 属性设置为 `True`。然后，你需要删除在创建 `DetailsView` 控件时添加的 `Fields` 元素。

顺便说一下，你可以在 `DetailsView` 元素上使用许多其他属性来指定控件的布局和格式。例如，你可以包含 `Height`、`Width`、`BackColor` 和 `ForeColor` 等属性。要查看所有可用属性，可以使用 HTML 编辑器的 IntelliSense 功能。

此图中的第二个表格列出了 `DetailsView` 元素的开始和结束标签之间可使用的子元素。这些元素中的大多数提供了样式和模板，用于控制 `DetailsView` 控件不同部分的格式。与 `DataList` 和 `GridView` 控件一样，`DetailsView` 控件以表格形式呈现。因此，最好使用样式元素来格式化控件，而不是使用 CSS。

`Fields` 元素可以包含此图第三个表格中列出的任何子元素。这些元素描述了 `DetailsView` 控件显示的各个字段。虽然此图未显示，但这些子元素本身可以包含子元素来指定格式信息。例如，你可以在 `BoundField` 元素的子元素中包含 `HeaderStyle` 和 `ItemStyle`，以控制绑定字段的标题和项部分的格式。同样，你可以使用 HTML 编辑器的 IntelliSense 功能查看有哪些子元素可用以及它们支持哪些属性。

## 如何在 DetailsView 控件中定义字段

就像创建 `GridView` 控件时一样，在创建 `DetailsView` 控件时，会为数据源中的每一列创建一个 `BoundField` 元素。然后，你可以使用第 14 章图 14-2 中看到的 `Fields` 对话框来处理这些字段或创建附加字段。要显示此对话框，请从控件的智能标记菜单中选择 `Edit Fields` 命令。你也可以使用 HTML 编辑器手动创建这些字段。或者，你可以使用本章后面描述的 `Add Field` 对话框。

为 `DetailsView` 控件创建的每个 `BoundField` 元素都包含一个 `SortExpression` 属性。然而，这些排序表达式只有在为控件启用分页时才有意义。因此，如果你不使用分页，可以安全地删除这些属性。

## DetailsView 控件属性

| Attribute | Description |
|---|---|
| ID | 此控件的 ID。 |
| Runat | 必须指定 "server"。 |
| DataSourceID | 要将 `DetailsView` 控件绑定到的數據源的 ID。 |
| DataKeyNames | 构成数据源主键的字段名称列表。 |
| AutoGenerateRows | 如果为 `True`，则为数据源中的每个字段自动生成一行。如果为 `False`，则必须在 `Fields` 元素中定义行。 |
| DefaultMode | 设置 `DetailsView` 控件的初始模式。有效选项为 `Edit`、`Insert` 或 `ReadOnly`。 |
| AllowPaging | 设置为 `True` 以允许分页。 |

## DetailsView 子元素

| Element | Description |
|---|---|
| Fields | `DetailsView` 控件显示的字段。 |
| RowStyle | `ReadOnly` 模式下数据行的样式。 |
| AlternatingRowStyle | 交替行的样式。 |
| EditRowStyle | `Edit` 模式下数据行的样式。 |
| InsertRowStyle | `Insert` 模式下数据行的样式。 |
| CommandRowStyle | 命令行的样式。 |
| EmptyDataRowStyle | 数据源为空时数据行的样式。 |
| EmptyDataTemplate | 数据源为空时使用的模板。 |
| HeaderStyle | 标题行的样式。 |
| HeaderTemplate | 标题行使用的模板。 |
| FooterStyle | 页脚行的样式。 |
| FooterTemplate | 页脚行使用的模板。 |
| PagerSettings | 用于控制分页行的设置。 |
| PagerStyle | 分页行的样式。 |
| PagerTemplate | 分页行使用的模板。 |

## Fields 子元素

| Element | Description |
|---|---|
| asp:BoundField | 绑定到数据源列的字段。 |
| asp:ButtonField | 显示按钮的字段。 |
| asp:CheckBoxField | 显示复选框的字段。 |
| asp:CommandField | 包含命令按钮的字段。 |
| asp:HyperlinkField | 显示超链接的字段。 |
| asp:ImageField | 显示图像的字段。 |
| asp:TemplateField | 具有自定义内容的列。 |

Figure 15-2 Attributes and child elements for the DetailsView control

## 如何启用分页

与 `GridView` 控件一样，`DetailsView` 控件也支持分页。如图 15-3 所示，当你将 `AllowPaging` 属性设置为 `True` 时，`DetailsView` 控件的底部会显示一行分页控件。然后，你可以通过包含 `PagerSettings` 元素来指定分页模式，还可以包含 `PagerStyle` 和 `PagerTemplate` 元素来指定分页控件的外观。

请注意，如果数据源包含的项目超过几十个，分页并不是一种实用的导航方式。因此，在大多数情况下，`DetailsView` 控件会与一个用于选择要显示项目的列表控件关联使用。你将在下一幅图中学习如何创建以这种方式工作的页面。

## 如何创建主/从页面

如图 15-4 所示，主/从页面是一种显示数据源中的数据项列表以及从列表中选择的某一项详细信息的页面。项目列表可以由任何允许用户选择项目的控件显示，包括下拉列表或 `GridView` 控件。然后，你可以使用 `DetailsView` 控件来显示所选项目的详细信息。图 15-1 中显示的页面就是一个主/从页面的示例，其中主列表以下拉列表的形式显示，`DetailsView` 控件用于显示所选项目的详细信息。

主/从页面通常使用两个数据源。第一个数据源检索包含数据项列表的控件要显示的项目。为了提高效率，该数据源应只检索显示列表所需的数据列。例如，图 15-1 中下拉列表的数据源只需要从 Halloween 数据库的 Products 表中检索 `ProductName` 和 `ProductID` 列。

第二个数据源为所选项目提供数据。它通常使用一个参数来指定应从数据库中检索哪一行。在本图的示例中，数据源使用一个绑定到下拉列表的参数。这样，该数据源就会自动检索下拉列表所选产品的数据。

## 主/从页面通常包含：

- 一个允许用户选择要显示项目的控件，例如下拉列表或 `GridView` 控件。
- 一个检索列表中要显示的所有项目的数据源。包含数据项列表的控件应绑定到该数据源。
- 一个显示用户所选项目数据的 `DetailsView` 控件。
- 一个检索用户所选项目数据的数据源。`DetailsView` 控件应绑定到该数据源。为了检索所选项目，该数据源可以使用一个绑定到包含数据项列表控件的 `SelectedValue` 属性的参数。

## 一个带有绑定到下拉列表的参数的 SqlDataSource 控件

```
<asp:SqlDataSource ID="SqlDataSource2" runat="server"
    ConnectionString="<%$ ConnectionStrings:HalloweenConnection %>"
    SelectCommand="SELECT [ProductID], [Name], [ShortDescription], [LongDescription], [CategoryID], [ImageFile], [UnitPrice], [OnHand] FROM [Products] WHERE ([ProductID] = @ProductID)">
    <SelectParameters>
        <asp:ControlParameter ControlID="ddlProducts" Name="ProductID" PropertyName="SelectedValue" Type="String" />
    </SelectParameters>
</asp:SqlDataSource>
```

## 说明

- 主/从页面是一种显示数据库中的项目列表以及列表中某一项详细信息的页面。`DetailsView` 控件通常用于显示主/从页面的详细信息部分。
- 主/从页面的列表部分可以由任何包含数据项列表的控件显示，包括下拉列表或 `GridView` 控件。
- 主/从页面通常包含两个数据源，一个用于主列表，另一个用于 `DetailsView` 控件。

## 如何更新 DetailsView 数据

除了显示数据源中特定项目的数据外，你还可以使用 `DetailsView` 控件来编辑、插入和删除项目。你将在以下主题中学习如何执行这些操作。

## 命令按钮简介

与 `GridView` 控件非常相似，`DetailsView` 控件使用命令按钮来让用户编辑和删除数据。因此，`DetailsView` 控件提供了“编辑”、“删除”、“更新”和“取消”按钮。此外，`DetailsView` 控件还允许用户插入数据，因此它还提供了两个按钮。“新建”按钮使 `DetailsView` 控件进入插入模式，“插入”按钮则接受用户输入的数据并将其写入数据源。这些命令按钮在图 15-5 中进行了总结。

有两种方法可以为 `DetailsView` 控件提供命令按钮。最简单的方法是使用 `AutoGeneratexxxButton` 属性，这些属性在第二个表格中列出，并在代码示例中进行了说明。但是，当你使用这些属性时，你无法控制按钮的外观。为此，你必须使用命令字段，如下一幅图所述。

## 一个带有自动生成命令按钮的 DetailsView 控件

| 产品 ID： | pow01 |
| 名称： | Austin Powers |
| 简短说明： | Austin Powers 服装 |
| 详细说明： | 成为今年派对上最酷炫的客人，宝贝。 |
| 类别 ID： | costumes |
| 图片文件： | powers1.jpg |
| 单价： | 79.9900 |
| 库存量： | 25 |
|  | 编辑 删除 新建 |

## 命令按钮

| 按钮 | 说明 |
| 编辑 | 将 `DetailsView` 控件置于编辑模式。 |
| 删除 | 删除当前项目，并将 `DetailsView` 控件保持在只读模式。 |
| 新建 | 将 `DetailsView` 控件置于插入模式。 |
| 更新 | 仅在编辑模式下显示。更新数据源，然后返回只读模式。 |
| 插入 | 仅在插入模式下显示。插入数据，然后返回只读模式。 |
| 取消 | 在编辑或插入模式下显示。取消操作并返回只读模式。 |

## 生成命令按钮的属性

| 属性 | 说明 |
| AutoGenerateDeleteButton | 生成“删除”按钮。 |
| AutoGenerateEditButton | 生成“编辑”按钮。 |
| AutoGenerateInsertButton | 生成“新建”按钮。 |

## 一个自动生成命令按钮的 DetailsView 元素

```
<asp:DetailsView ID="DetailsView1" runat="server"
    DataSourceID="SqlDataSource2" DataKeyNames="ProductID"
    AutoGenerateRows="False"
    AutoGenerateDeleteButton="True"
    AutoGenerateEditButton="True"
    AutoGenerateInsertButton="True">
</asp:DetailsView>
```

## 说明

- `DetailsView` 控件支持六种不同的命令按钮。
- 你可以使用 `AutoGenerateDeleteButton`、`AutoGenerateEditButton` 和 `AutoGenerateInsertButton` 属性来自动生成命令按钮。
- 要自定义命令按钮的外观，请使用命令字段而不是自动生成的按钮，如下一幅图所述。

## 如何添加命令按钮

与 `GridView` 控件一样，`DetailsView` 控件允许你使用 `CommandField` 元素来指定控件应显示的命令按钮。其中一种方法是使用图 15-6 中显示的“添加字段”对话框向 `DetailsView` 控件添加命令字段。当然，你也可以使用“编辑字段”对话框来添加命令字段，或者使用 HTML 编辑器手动编写 `CommandField` 元素。

要使用“添加字段”对话框创建命令按钮，请选择 `CommandField` 作为字段类型。此时会出现四个复选框，让你选择要在命令字段中显示哪些命令按钮。此外，还有一个下拉列表，让你选择命令按钮应显示为按钮还是超链接。

当你首次为命令字段显示“添加字段”对话框时，你会注意到“显示取消按钮”复选框被禁用。这是因为该按钮只能与“新建/插入”和“编辑/更新”按钮结合使用。当你选择其中一个按钮时，“显示取消按钮”复选框就会启用并默认选中。这很合理，因为你通常希望允许用户取消插入或编辑操作。

请注意，`CommandField` 元素包含一些属性，用于指定要显示的文本或图像，以及按钮是否触发验证。有关使用这些属性的更多信息，请参阅第 14 章。

在继续之前，你应该认识到，你可以使用“添加字段”对话框来创建图 15-2 中第三个表格所示的任何元素。要做到这一点，只需从对话框顶部的下拉列表中选择要创建的字段类型即可。然后，该字段类型的相应选项就会显示出来。如果你尝试一下，应该不会有什么困难就能弄清楚它的工作原理。
