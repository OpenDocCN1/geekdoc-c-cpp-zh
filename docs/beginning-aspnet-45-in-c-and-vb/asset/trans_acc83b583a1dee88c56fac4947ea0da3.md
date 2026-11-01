

请注意，VS 已将列名和表名用方括号（[]）括起来。通常，只有列名或表名包含特殊字符（如空格）或名称与保留字匹配时，才需要这样做。VS 只是比较谨慎，对所有列和表都加上了括号。你可以保留它们，但如果你自己编写 SQL 语句，则不必包含这些括号（当然，如果你愿意，也可以加上）。

在此阶段，SqlDataSource 控件本身还不能做太多事情。它需要一个数据绑定控件来告诉它要执行哪些数据操作。在本练习中，数据绑定控件是使用以下代码定义的 GridView：

```
<asp:GridView ID="GridView1" runat="server" AllowPaging="True" AllowSorting="True" AutoGenerateColumns="False" DataKeyNames="Id" DataSourceID="SqlDataSource1" EmptyDataText="There are no data records to display.">
    <Columns>
        <asp:CommandField ShowDeleteButton="True" ShowEditButton="True" ShowSelectButton="True" />
        <asp:BoundField DataField="Id" HeaderText="Id" ReadOnly="True" SortExpression="Id" />
        <asp:BoundField DataField="Name" HeaderText="Name" SortExpression="Name" />
        <asp:BoundField DataField="SortOrder" HeaderText="SortOrder" SortExpression="SortOrder" />
    </Columns>
</asp:GridView>
```

GridView 包含几个重要的属性。首先，`DataKeyNames` 属性告诉 GridView 数据库中行的主键是什么。它需要这个属性来唯一标识网格中的行。

`DataSourceID` 属性指向之前看到的 SqlDataSource 控件，而 `AllowPaging` 和 `AllowSorting` 则在 GridView 上启用关联的功能。

在 `<Columns>` 元素下，你可以看到设置了许多字段。首先，你看到一个 `CommandField`。`CommandField` 是 GridView 中的一列，允许用户对 `CommandField` 所应用的行执行一个或多个操作。它在浏览器中最终显示为一个或多个文本链接或按钮。在此示例中，`ShowDeleteButton`、`ShowEditButton` 和 `ShowSelectButton` 都已设置为 `True`。这为网格提供了你在图 13-5 中看到的功能。当你单击 `CommandField` 创建的某个链接时，它们会在服务器端触发一条命令。例如，单击“Edit”链接会使 GridView 进入编辑模式，这样你就可以编辑所选行。请注意，单击“Select”链接似乎根本不会改变 GridView。在第 15 章中，你将看到如何为 GridView 创建样式，从而可以彻底改变该控件的外观，包括在视觉上区分所选行与其他行。

如果你希望 GridView 渲染按钮而不是链接，则需要将 `ButtonType` 设置为 `Button`：

```
<asp:CommandField ShowDeleteButton="True" ShowEditButton="True" ShowSelectButton="True" ButtonType="Button"></asp:CommandField>
```

其他三个字段是所谓的绑定字段，通过其 `DataField` 属性直接映射到数据库中 Genre 表的列，这样 GridView 就知道在何处显示什么数据。GridView 和 SqlDataSource 控件紧密协作，以检索和修改底层数据源中的数据。为了让你了解其工作原理，下面概述了你在浏览器中请求 Genres 页面然后编辑单个流派时所发生的事件：

1. 你在浏览器中请求该页面，页面开始其页面生命周期。
2. GridView 知道它被设置为检索并显示数据，因为它有一个指向 SqlDataSource 控件的 `DataSourceID` 属性。它会联系此数据源控件并请求数据。SqlDataSource 连接到数据库，并触发其 `SelectCommand`，即从数据库的 Genre 表中选择 `Id`、`Name` 和 `SortOrder` 的 SQL 语句：
3. 当 SqlDataSource 从数据库接收到请求的行时，它会将这些行交给 GridView，GridView 使用在 `<Columns>` 元素中设置的绑定字段，用这些行生成一个 HTML 表格。GridView 通过将每行的唯一 ID 存储在 View State 中来跟踪页面中显示的行。
4. 一旦你单击“Edit”链接，页面就会回发。GridView 通过查看关联的 `DataKeyNames` 并从 View State 中检索该行的 ID，来识别你单击了哪一行。然后，它通过再次要求 SqlDataSource 触发其 `SelectCommand` 来从数据库获取最新结果，最后将所选行置于编辑模式，以便你可以修改相关详细信息。当你单击“Update”链接时，GridView 会从 TextBox 控件中收集新值，然后再次联系 SqlDataSource。
5. 对于 SqlDataSource 的 `<UpdateParameters>` 元素中的每个参数，GridView 都会提供一个值。它从所选行中检索流派的 `Id`，然后从页面中的 TextBox 控件中检索新的 `Name` 和 `SortOrder` 值。
6. 有了 `Id`、`Name` 和 `SortOrder` 的相关数据后，SqlDataSource 随后对数据库执行其 `UpdateCommand`：
   每个以 at 符号（@）为前缀的参数都会被填充为 GridView 提供的值。发送到数据库的 SQL 语句最终看起来类似于以下内容：
7. 最后，GridView 再次要求 SqlDataSource 执行其 `SelectCommand` 来刷新页面上的数据。这样，GridView 现在显示的就是你进行更新后的最新数据。

```
SelectCommand="SELECT [Id], [Name], [SortOrder] FROM [Genre]"
```

```
UpdateCommand="UPDATE [Genre] SET [Name] = @Name, [SortOrder] = @SortOrder WHERE [Id] = @Id"
```

```
UPDATE [Genre] SET [Name] = 'New Name', [SortOrder] = 1 WHERE [Id] = 1
```

其他命令以类似的方式工作，并向数据库发送自己的 SQL 命令。

在练习结束时，你向 Management 文件夹添加了一个新的 Web.config 文件，以重置应用于 Management 部分所有页面的主题。移除主题后，更容易关注 Management 部分的功能，而不是被布局问题分散注意力。在第 15 章中，你将专门为 Management 文件夹创建第三个主题，并在 Management 文件夹的 Web.config 文件中应用该主题。这样，你的管理页面将具有与前端页面不同的外观和感觉。

6. 保存对页面的更改，然后按 Ctrl+F5 在浏览器中打开它。现在，你应该会在 GridView 下方看到允许你插入新流派的控件，如图 13-6 所示。

7. 插入一个新流派，例如 Disco 或 Dance。确保同时输入名称和排序顺序（一个数字），然后点击“Insert”链接。你可能需要点击屏幕底部 Pager 栏中的某个数字翻到 GridView 的最后一页，才能看到新行。

![](img/eadab2ccd79b253c01a3fdff2321202d_509_0.png)

## 工作原理

与其他数据绑定控件相同，你通过设置 `DataSourceID` 属性将 DetailsView 连接到数据源控件。由于页面上已经有一个可用的 SqlDataSource 控件，你可以直接重用它。DetailsView 提供了不同的视图，分别用于只读、插入和编辑模式。通过将 `DefaultMode` 设置为 `Insert`，你强制该控件切换到插入模式，这意味着你会自动获得一个用于输入流派详细信息的 UI，以及“Insert”和“Cancel”链接。DetailsView 控件实际上相当智能。当你将其指向 SqlDataSource 控件时，它能够自动推断出 `DataKeyNames` 属性，该属性被设置为 `Id`。

```
<asp:DetailsView ID="DetailsView1" runat="server" AutoGenerateRows="False" DataKeyNames="Id" DataSourceID="SqlDataSource1" ...>
```

它还能理解 `Id` 列在数据库中是标识列，因此通过将 `InsertVisible` 设置为 `False`，在插入屏幕（如图 13-6 所示）中将其隐藏。由于数据库会自动生成此 ID，因此让用户为其输入值是没有意义的。

当你输入一些值并单击“Insert”链接时，会执行一个类似于使用 GridView 进行更新的过程。DetailsView 从页面控件中收集相关信息（`Name` 和 `SortOrder`），并将其转发给 SqlDataSource。该控件随后将新值推送到 INSERT 语句的参数中，然后向数据库发送该命令，数据库会在 Genre 表中插入新行。如果你在没有输入名称或排序顺序的情况下单击“Insert”链接，则会收到错误。在本章及后续章节中，你将看到如何修改数据绑定控件以包含验证功能。

在本章前面，当你将 Genre 表拖放到 Genres.aspx 页面上时，VS 不仅为你创建了一堆控件，还将有关数据库的信息存储在你的 Web.config 文件中。下一节将解释其工作原理以及为什么这很重要。

## 在 Web.config 中存储连接字符串

当你在页面上首次查看 Genre 表时，VS 为你创建了一个 SqlDataSource 控件。为了告诉该控件要访问哪个数据库，VS 还在连接字符串中创建了

