

## 数据源与数据绑定控件协同工作 | 47

有一些值得研究的有趣点。首先，注意 `ConnectionString` 和 `ProviderName` 属性指向在 `Web.config` 文件中定义的连接字符串。你将在下一节中看到更多此类内容，包括对属性使用的 `<% %>` 语法的解释。

然后你会看到四个命令，每个命令都是一个 SQL 语句，用于 CRUD 缩写的四个操作之一。`INSERT`、`UPDATE` 和 `DELETE` 命令包含参数，由符号 `@` 标识。在运行时，当控件被要求执行相关操作时，这些参数会被值替换。`SqlDataSource` 在 `Parameters` 集合中跟踪相关参数。例如，`<DeleteParameters>` 包含一个用于 `Id`（主键）的单个参数：

```xml
<DeleteParameters>
<asp:Parameter Name="Id" Type="Int32" />
</DeleteParameters>
```

注意参数名称减去符号 `@` 后的部分与 SQL 语句中的参数匹配：

```sql
DELETE FROM [Genre] WHERE [Id] = @Id
```

注意 VS 如何将列名和表名封装在方括号 `[]` 中。如果你的列名或表名包含特殊字符（如空格）或匹配保留字，你通常需要这些。VS 非常谨慎，为所有列和表添加了它们。如果你编写自己的 SQL 语句，可以保留它们。`SqlDataSource` 本身无法控制在此阶段发生的情况。数据绑定控件告诉它执行哪些操作。在本次练习中，数据绑定控件是用此代码定义的 `GridView`：

```xml
<GridView ID="GridView" runat="server" AllowPaging="True" AllowSorting="True" AutoGenerateColumns="False" DataKeyNames="Id" DataSourceID="SqlDataSource" EmptyData="There are no records to display.">
<Columns>
<asp:CommandField ShowSelectButton="True" ShowEditButton="True" ShowDeleteButton="True" />
<asp:BoundField DataField="Id" HeaderText="Id" ReadOnly="True" SortExpression="Id" />
<asp:BoundField DataField="Name" HeaderText="Name" SortExpression="Name" />
<asp:BoundField DataField="SortOrder" HeaderText="SortOrder" SortExpression="SortOrder" />
</Columns>
</GridView>
```

`GridView` 包含几个重要的属性。首先，`DataKeyNames` 属性告诉 `GridView` 数据的主键是什么。这唯一标识了 `GridView` 中的行。`DataSourceID` 属性指向你之前看到的 `SqlDataSource` 控件。`AllowPaging` 和 `AllowSorting` 启用了 `GridView` 上关联的功能。

## 第 13 章显示和更新数据

在 `<Columns>` 元素下你可以看到 `CommandField`。`CommandField` 是 `GridView` 中的一列，允许用户对行执行一个或多个操作。它在浏览器中显示为一个或多个文本链接或按钮。在本示例中，`ShowDeleteButton`、`ShowEditButton` 和 `ShowSelectButton` 都被设置为 True。这为网格提供了图 15-3 所示的功能。当你点击由 `CommandField` 创建的链接之一时，它们将在服务器端触发命令。例如，点击 Edit 链接会将 `GridView` 置于编辑模式，你可以编辑选中的行。注意 Select 链接似乎完全没有改变 `GridView`。在第 15 章中，你将看到如何为 `GridView` 创建样式，以便你可以从其他行中彻底改变选中行的外观。

如果你想让 `GridView` 渲染而不是链接，需要将 `ButtonType` 设置为 True：

```xml
<asp:CommandField ShowDeleteButton="True" ShowEditButton="True" ShowSelectButton="True" ButtonType="Button" /></asp:CommandField>
```

另外三个字段是绑定字段（bound-fields），它们通过 `DataField` 属性直接映射到数据库中的列，因此 `GridView` 知道要显示什么数据。

`GridView` 和 `SqlDataSource` 控件密切配合，以检索和修改底层数据源中的数据。为了让你了解其工作原理，这里是你在浏览器中请求页面并编辑单个类型时发生的事件概述：

1. `GridView` 知道它被配置为检索和显示数据，因为它有一个指向 `SqlDataSource` 控件的 `DataSourceID` 属性。这把数据源连接到数据库并向其请求数据。`SqlDataSource` 然后连接到数据库并触发其 `SelectCommand`，即从数据库的 `Genre` 表中选择 `Id`、`Name` 和 `SortOrder` 的 SQL 语句：
```sql
SelectCommand="SELECT [Id], [Name], [SortOrder] FROM Genre"
```
2. 当 `SqlDataSource` 从数据库接收请求的行时，它将它们交给 `GridView`，`GridView` 使用在 `<Columns>` 元素中设置的绑定字段创建 HTML 表格。`GridView` 通过将其存储在 View State 中跟踪页面显示的每行的唯一 ID。
3. 当你点击 Edit 链接时，页面回传（post back）。`GridView` 可以通过查看关联的 `DataKeys` 并从 View State 中检索行的 `Id` 来查明你点击了什么。它通过再次要求 `SqlDataSource` 触发其 `SelectCommand` 获取最新结果，最后将选中的行进行编辑，以便你更改检索到的详情。当你点击 Update 链接时，`GridView` 从 `TextBox` 控件收集新值，然后再次联系 `SqlDataSource`。
4. 对于 `SqlDataSource` 中 `<UpdateParameters>` 元素中的每个参数，`GridView` 都会提供一个值。它从选中行检索类型的 `Id`，然后从页面中的 `TextBox` 控件中检索 `Name` 和 `SortOrder` 值。
5. 凭借了 `Id`、`Name` 和 `SortOrder` 的相关数据，`SqlDataSource` 在数据库上执行其 `UpdateCommand`：
```sql
UpdateCommand="UPDATE [Genre] SET Name = @Name, SortOrder = @SortOrder WHERE Id = @Id"
```
6. 最后，`GridView` 在要求 `SqlDataSource` 触发其 `SelectCommand` 后刷新页面。`GridView` 现在显示了你所做的更新。

