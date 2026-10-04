

![](img/9e033e3b9560597824f8b22941d6d8bb_495_0.png)

图 13-10

出于某种原因，你的每个控件可能会在 Control ID 下拉列表中显示两次。无论你选择 DropDownList:i 选项中的哪一个都没有关系。

- 点击 Add 按钮将选择项添加到屏幕底部的 WHERE 子句列表中，并点击 OK。

- 回到配置数据源（Configure Data Source）向导，点击 Next。要测试查询，请点击 Test Query 按钮。如果你正确设置了参数，将弹出一个对话框允许你输入值。在 Genre 表中输入一个你已知的数字（例如 2）并点击 OK。如果 Review 表中存在对应所选流类型的行，它们将显示在 Test Query 窗口中。最后，点击 Finish 完成向导。如果弹出关于刷新参数的对话框，请点击 Yes 让系统自动为你更新 Markup View 中的代码。

- 保存你的更改，并在浏览器中打开 Reviews.aspx。

> 常见错误：如果你收到错误提示“输入字符串格式不是正确的格式”，请确保你像前一个练习所示，将下拉列表中静态 ListItem 的 Value 设置为空字符串（""）。

- 在下拉列表中选择一个新项目。页面将刷新，现在会显示属于所选流类型的评论。如果页面没有刷新，请确保你在上一个练习中将 AutoPostBack 设置为 True。在此阶段，页面看起来相当杂乱，因为 GridView 包含许多列，但在下一个“尝试一试”（Try It Out）中，你将看到如何修复这个问题。

# 自定义数据控件的外观

## 工作原理

在大多数情况下，这个练习与之前显示可用流类型列表的练习类似。这次的不同之处在于 SqlDataSource 如何根据你在 DataList 中所做的选择来过滤 Review 表。查看 SqlDataSource 的代码以了解其工作原理：

```asp
<asp:SqlDataSource Id="SqlDataSource2" runat="server"
    ConnectionString="<%= ConnectionStrings.MyConnectionString1 %>"
    SelectCommand="SELECT * FROM Review WHERE [GenreId] = @GenreId">
    <SelectParameters>
        <ControlParameter ControlID="DropDownList1" Name="GenreId"
            PropertyName="SelectedValue" Type="Int32" />
    </SelectParameters>
</asp:SqlDataSource>
```

SelectCommand 的 SQL 语句包含一个用于 Select 语句变量 GenreId 参数。这意味着 SQL 语句仅从 Review 表返回特定流类型的数据。在运行时，该参数的值从 ControlParameter 元素中定义的控件中获取。在此示例中，代码被配置为从 DropDownList 获取值，并访问其 SelectedValue 属性，因此添加了 PropertyName；如果你需要不同的属性，只需在 ControlParameter 的声明中更改它即可。

通过这种设置，GridView 使用 SqlDataSource 获取数据。该数据源从用户在列表中选择的 DropList 获取项。此值被插入到 SQL 语句中，从数据库返回的结果将通过数据源传回给 GridView，GridView 使用这些数据在浏览器中创建 HTML 表格。

当你从下拉列表中选择一个 Selection（选择）时，你会得到一个没有任何行的空白页面。在这种情况下，DropDownList 返回一个空字符串作为其值（在 Value 属性中定义），该值会被转换为 null（数据库中等同于“无”）。这会导致查询从 Review 表中返回行。

现在你已经依靠 VS 的代码生成工具设置了 GridView 和 DetailsView。默认情况下，VS 会为数据源中找到的每一列创建一个列（对于 GridView）或一个字段（对于 DetailsView）。它足够智能识别数据库中的某些底层数据类型，因此对于数据库中的布尔（bit）字段，你会获得一个 CheckBoxField，仅此而已。若要进一步自定义这些控件的外观和感受，你需要自定义我们的 Columns 和 Fields 集合。

# **自定义数据控件的外观**

默认情况下，GridView 和 DetailsView 会根据它们接收的数据自动渲染列或行。或者，当你将控件附加到数据源时，你也可以为你创建许多字段或列。但大多数情况下，你想要更改你在屏幕上看到的内容，无论是更少的列、不同的列标题，还是用于显示数据的不同控件。坦率地说，使用 VS 中的 Fields 编辑器来实现这些操作非常简单。在下一节中，你将看到如何使用此编辑器来创建和修改不同类型的内置列和字段。在随后的章节中，你将看到即使使用用户定义模板也可以如何自定义字段。

# 配置数据绑定控件的列和字段

在 GridView 和 DetailsView 的 `<columns>` 或 `<Fields>` 元素内部，你可以添加下表所示的字段类型。

| 字段类型 | 说明 |
| :--- | :--- |
| BoundField | 大多数数据类型的默认字段。在只读模式下显示为文本，在编辑模式下显示为 TextBox。 |
| ButtonField | 用于在服务器上执行命令。 |
| CheckBoxField | 在只读模式下显示为选择框，在编辑模式下显示为可编辑的选框。 |
| CommandField | 允许设置各种命令，包括编辑和删除。 |
| HyperLinkField | 显示为链接（<a>）。你可以设置 DataNavigateUrl、DataFormatString 和 DataTextField 来影响链接的行为。在下一个练习中看到更多。 |
| ImageField | 在浏览器中显示为 <img> 元素。 |
| TemplateField | 允许为各种模板定义自己的外观，例如 ItemTemplate、InsertTemplate 和 EditItemTemplate。 |

显然，每个字段类型都有独特的用途，因此你可以选择最符合你要求的。将在下一个练习中更详细地查看这些字段。

# 尝试一试：自定义 GridView 列

在本次练习中，你将看到如何在 Reviews.aspx 中执行以下操作：

- 使用 Fields 编辑器自定义 GridView 的字段。
- 使用 HyperLink 列创建指向详情页的链接。
- 格式化 BoundField 列的输出。
- 使用后台自定义函数对 TemplateField 的输出进行完全控制。

后面的练习将向你如何创建详情页以插入新评论并编辑现有评论。

1. 在 Reviews.aspx 中，在设计视图打开 SqlDataSource2 控件的智能面板并点击 Configure Data Source。点击 Next 跳过连接字符串，按照图 13-11 所示完成屏幕，选择 Review 表中的 Id、Title、Authorized 和 CreateDateTime 列。确保 SQL 语句也包含之前设置的 WHERE 过滤器。你可能需要按照上一个练习的步骤再次设置，因为 VS 有时会丢失这些信息。

![](img/9e033e3b9560597824f8b22941d6d8bb_498_0.png)

图 13-11

点击 Advanced 按钮，勾选第一项让 VS 生成 INSERT、UPDATE 和 DELETE 语句的命令。你可以保留乐观并发复选框——它用于检测自上次从数据源加载以来行的更改。点击 OK 关闭高级 SQL 生成选项对话框，然后点击 Next 和 Finally 更新页面源的 SQL 语句。当询问是否要刷新 GridView 的字段和键时，点击 Yes。

> 如果高级 SQL 生成选项对话框中的两个选项都呈灰色，请使用 SQL Server Management Studio 检查数据库中的表。确保你已如上一一章所述，将 Review 表的 Id 列设为主键和标识列。

