

## 如何启用排序

GridView 控件内置了让用户根据控件显示的任意一列或所有列对行进行排序的能力。如图 14-4 所示，要启用排序，你只需将 AllowSorting 属性设置为 True，并为你想要允许排序的每一列提供 SortExpression 属性。当为某列启用排序时，用户可以通过单击列标题对数据进行排序。第一次单击时，数据将按升序排序。第二次单击时，数据将按降序排序。以此类推。

请注意，SortExpression 属性会自动为默认包含的每个 BoundField 列或你使用 Fields 对话框创建的列生成。因此，与其为你想要允许排序的列添加 SortExpression 属性，不如删除你不想要允许排序的列的 SortExpression 属性。你可以通过在 Fields 对话框中清除 SortExpression 属性来做到这一点。或者，你也可以使用 HTML 编辑器删除 SortExpression 属性。

本图中的代码示例允许对 GridView 控件显示的五个字段中的三个字段进行排序。对于前两个字段，SortExpression 属性只是简单地重复字段绑定的数据源列的名称。例如，如果用户单击 ProductID 列的标题，数据将按 ProductID 字段排序。

不过，在某些情况下，你可能希望排序表达式基于两列或更多列。要做到这一点，你只需用逗号分隔排序字段名称即可。在此示例中，Category ID 列的排序表达式为“CategoryID, Name”。这样，任何具有相同 Category ID 的行都将按 Name 列排序。请注意，第一次单击 Category ID 列标题时，行将按 CategoryID 列的升序在 Name 列中按升序排序。如果再次单击 Category ID 列标题，类别 ID 将保持升序，但名称将按降序排序。

需要特别注意的是，GridView 控件本身并不实际执行排序。相反，它依赖于底层数据源对数据进行排序。因此，排序只有在数据源提供排序功能时才有效。对于 SqlDataSource 或 AccessDataSource，这意味着你需要使用默认的 DataSet 模式。

## 如何启用分页

分页是指 GridView 控件能够一次显示一页绑定数据，并显示分页控件让用户选择要显示的下一页数据。如图 14-5 所示，GridView 控件允许你通过将 AllowPaging 属性设置为 True 来启用分页。

启用分页时，GridView 控件底部会额外显示一行来显示分页控件。如果需要，你可以提供一个 PagerStyle 元素来控制此行的格式。在本图中的示例中，PagerStyle 元素指定分页行的背景颜色应为浅灰色，且分页控件应水平居中。

与排序不同，GridView 控件不会将分页功能委托给底层数据源。但是，与排序一样，分页仅适用于处于 DataSet 模式的数据源。

### 启用分页的 GridView 控件

| ID | Name | Category | Unit Price | On Hand |
|---|---|---|---|---|
| arm01 | Freddie Arm | props | $20.95 | 200 |
| bats01 | Flying Bats | props | $69.99 | 25 |
| bl01 | Black Light | fx | $19.99 | 200 |
| cat01 | Deranged Cat | props | $19.99 | 45 |
| fog01 | Fog Machine | fx | $34.99 | 100 |
| fogj01 | Fog Juice (1qt) | fx | $9.99 | 500 |
| frankc01 | Frankenstein | costumes | $39.99 | 100 |
| fred01 | Freddie | masks | $29.99 | 50 |
| head01 | Michael Head | props | $29.99 | 100 |
| head02 | Saw Head | props | $29.99 | 100 |
|  |  |  |  |  |
|  |  |  | 1 2 3 |  |

### 上述控件的 aspx 代码

```
<asp:GridView ID="GridView1" runat="server" AllowPaging="True"
    AutoGenerateColumns="False" DataKeyNames="ProductID"
    DataSourceID="SqlDataSource1">
    <Columns>
        <asp:BoundField DataField="ProductID" HeaderText="ID"
            ReadOnly="True">
            <HeaderStyle HorizontalAlign="Left" />
            <ItemStyle Width="75px" />
        </asp:BoundField>
        <asp:BoundField DataField="Name" HeaderText="Name">
            <HeaderStyle HorizontalAlign="Left" />
            <ItemStyle Width="200px" />
        </asp:BoundField>
        <asp:BoundField DataField="CategoryID" HeaderText="Category" />
        <asp:BoundField DataField="UnitPrice" DataFormatString="{0:c}"
            HeaderText="Unit Price">
            <ItemStyle Width="85px" HorizontalAlign="Right" />
            <HeaderStyle HorizontalAlign="Right" />
        </asp:BoundField>
        <asp:BoundField DataField="OnHand" HeaderText="On Hand">
            <ItemStyle Width="85px" HorizontalAlign="Right" />
            <HeaderStyle HorizontalAlign="Right" />
        </asp:BoundField>
    </Columns>
    <HeaderStyle BackColor="LightGray" />
    <PagerStyle BackColor="LightGray" HorizontalAlign="Center" />
</asp:GridView>
```

### 描述

- 要启用分页，将 AllowPaging 属性设置为 True。然后，添加一个 PagerStyle 元素来定义分页控件的外观。你还可以添加一个 PagerSettings 元素，如下一图所示来自定义分页的工作方式。
- 要使分页工作正常，数据源的 DataSourceMode 属性必须设置为 DataSet 模式。

## 如何自定义分页

图 14-6 显示了如何自定义 GridView 控件的分页工作方式。首先，第一张表中的两个属性可让你启用分页并指定每页将显示的数据行数。第二个属性的默认设置是 10。

你还可以通过在 GridView 控件的开始和结束标签之间包含一个 PagerSettings 元素来自定义分页区域的外观。然后，你可以使用第二张表中的属性进行自定义。其中最重要的属性是 Mode，它决定分页区域中显示哪些按钮。例如，如果你将模式设置为 NextPrevious，则只会显示 Next 和 Previous 按钮。

如果你为 Mode 属性指定 Numeric 或 NumericFirstLast，则分页区域中会显示单独的页码，以便用户可以直接转到任意列出的页面。然后，你可以使用 PageButtonCount 属性指定在分页区域中应显示多少个这些页码。请注意，如果你指定 NumericFirstLast，则只有当总页数超过你为 PageButtonCount 属性指定的值且未显示第一页或最后一页时，才会显示第一个和最后一个按钮。

此表中的其余属性可让你控制各种按钮显示的文本或图像。默认情况下，First、Previous、Next 和 Last 按钮的值使用小于号和大于号，但示例显示了如何更改这些按钮的文本。

### 影响分页的 GridView 控件属性

| Attribute | Description |
|---|---|
| AllowPaging | 设置为 True 以启用分页。 |
| PageSize | 指定每页显示的行数。默认值为 10。 |

### PagerSettings 元素属性

| Attribute | Description |
|---|---|
| Mode | 控制分页区域中显示哪些按钮。你可以指定 NextPrevious、NextPreviousFirstLast、Numeric 或 NumericFirstLast。 |
| FirstPageText | 用于第一页按钮的显示文本。默认值为 &lt;&lt;，显示为 <<。 |
| FirstPageImageUrl | 用于显示第一页按钮的图像文件的 URL。 |
| PreviousPageText | 用于上一页按钮的显示文本。默认值为 &lt;，显示为 <。 |
| PreviousPageImageUrl | 用于显示上一页按钮的图像文件的 URL。 |
| NextPageText | 用于下一页按钮的显示文本。默认值为 &gt;，显示为 >。 |
| NextPageImageUrl | 用于显示下一页按钮的图像文件的 URL。 |
| LastPageText | 用于最后一页按钮的显示文本。默认值为 &gt;&gt;，显示为 >>。 |
| LastPageImageUrl | 用于显示最后一页按钮的图像文件的 URL。 |
| PageButtonCount | 如果 Mode 设置为 Numeric 或 NumericFirstLast，则要显示的页按钮数。 |
| Position | 分页区域的位置。你可以指定 Top、Bottom 或 TopAndBottom。 |
| Visible | 设置为 False 以隐藏分页控件。 |

### 示例

### 一个 PagerSettings 元素

```
<PagerSettings Mode="NextPreviousFirstLast"
    NextPageText="Next" PreviousPageText="Prev"
    FirstPageText="First" LastPageText="Last" />
```

### 生成的分页区域

![](img/c024ccf88e28c30c07dd410d4342288f_474_0.png)

### 描述

- 你可以使用 GridView 元素的 PageSize 属性指定每页显示的行数。
- 你还可以添加一个 PagerSettings 元素来控制分页区域的外观。

