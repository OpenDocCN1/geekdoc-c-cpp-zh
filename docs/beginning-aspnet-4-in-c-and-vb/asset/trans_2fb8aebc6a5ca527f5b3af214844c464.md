
这里最有趣的地方在于如何访问你之前创建的连接字符串，使用以下语法：

```
ConfigurationManager.ConnectionStrings["MRBConnectionString"].ConnectionString
```

ConfigurationManager 类（需要导入 System.Configuration 命名空间）可让你访问所有各种配置信息，这些信息都存储在 Web 应用程序的 Web.config 配置文件中。你将在本章后面更详细地了解这一点。

创建 SQL 命令后，你可以使用它来插入新事件：

```
conn.Open();
int queryResult = insertCommand.ExecuteNonQuery();
conn.Close();
```

ExecuteNonQuery() 返回一个整数，表示查询影响了多少行表。如果它等于 1，则插入成功。如果是这样，就在 resultLabel 中放置成功消息，清除 EventData 因为它现在已过时，并将日历选择更改为新的空闲日期。因为 GetFreeDate() 涉及使用 EventData，而 EventData 属性如果没有数据会自动刷新自身，所以存储的事件数据将被刷新：

```
if (queryResult == 1)
{
    resultLabel.Text = "Event Added.";
    EventData = null;
    calendar.SelectedDate =
    GetFreeDate(calendar.SelectedDate.AddDays(1));
}
```

如果 ExecuteNonQuery() 返回的不是 1 的数字，你就知道出现了问题。本示例中的代码如果返回的不是 1 的数字就会抛出异常。此异常会被数据库访问代码的通用 catch 块捕获。

此 catch 块只是在 resultLabel 中显示一个一般的失败通知：

```
else
{
    throw new System.Data.DataException("Unknown data error.");
}
catch
{
    resultLabel.Text = "Event not added due to DB access "
        + "problem.";
}
```

这完成了你的事件预订应用程序的数据感知版本。

## 关于数据绑定的更多内容

如本章前面所述，可用的 Web 服务器控件中包含多个处理数据显示的控件（GridView、DataList、DetailsView、FormView 和 Repeater）。当输出数据到网页时，它们都非常有用，因为它们会自动执行许多任务，否则需要相当多的编码。

首先，你将通过在 PCSWebSite3 显示的底部添加事件列表显示，来看看使用这些控件有多容易。

从工具箱拖动一个 GridView 控件到 Default.aspx 的底部，并为其选择你之前添加的 MRSEventData 数据源，如图 40-12 所示。

接下来，单击 Refresh Schema，就这样，你只需这样做即可在表单下显示事件列表——现在尝试查看网站，你应该能看到事件，如图 40-13 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1237_0.png)

图 40-12

| ID | 名称 | 房间 | 参会者列表 | 事件日期 |
|---|---|---|---|---|
| 1 | My Birthday | 4 | Iggy Pop (5), Sean Connery (7), Albert Einstein (10), George Clooney (14), Jules Verne (18), Robin Hood (20), and Kurt Watson | 17/09/2010 00:00:00 |
| 2 | Dinner | 1 | Bill Gates (1), Monika Lewinsky (2), and Bruce Lee | 15/06/2010 00:00:00 |
| 3 | Discussion of darkness | 6 | Vlad the Impaler (4), Moya Hindley (13), and Bedelbud | 29/10/2010 00:00:00 |
| 4 | Christmas with P... | 9 | Dr Frank N Parter (11), Bobby Davro (15), John F Kennedy (16), Stephen Kang (19), and Karth Watson | 25/12/2010 00:00:00 |
| 5 | Escape | 17 | Monika Lewinsky (2), Stephen King (19), and Spartacus | 10/05/2010 00:00:00 |
| 6 | Planetary Conquest | 14 | RB Gates (1), Albert Einstein (10), Dr Frank N Parter (11), Bobby Davro (15), and Darth Vader | 15/06/2010 00:00:00 |
| 7 | Homecoming Celebration | 7 | William Shakespeare (6), Christopher Columbus (12), Robin Hood (20), and Ulysses | 22/06/2010 00:00:00 |
| 8 | Dalek Reunion Ball | 12 | Roger Moore (8), George Clooney (14), Bobby Davro (15), and Davros | 12/06/2010 00:00:00 |
| 9 | Romantic meal for two | 13 | George Clooney (14), and Donna Watson | 29/09/2010 00:00:00 |

图 40-13

你还可以在 submitButton_Click() 中做进一步的修改，以确保在添加新记录时更新此数据：

```
if (queryResult == 1)
{
    resultLabel.Text = "Event Added.";
    EventData = null;
    calendar.SelectedDate =
    GetFreeDate(calendar.SelectedDate.AddDays(1));
    GridView1.DataBind();
}
```

所有可数据绑定的控件都支持此方法，如果你调用顶级（this）DataBind() 方法，表单通常会调用它。

你可能在图 40-13 中注意到 EventDate 字段的日期/时间显示有点混乱。因为你只查看日期，所以时间始终为 00:00:00 AM——这不是真正需要显示的信息。在下一节中，你将看到如何在 ListView 控件的上下文中以更用户友好的方式显示此日期信息。正如你所预期的那样，DataGrid 控件包含许多可用于格式化显示数据的属性，但我把这些留给你去发现。

## 使用模板进行数据展示

许多数据显示控件允许你使用模板来格式化显示数据。在 ASP.NET 的意义上，模板是 HTML 的参数化部分，用于某些控件的输出元素。它们使你能够自定义数据输出到浏览器的确切方式，并且可以在不费太多努力的情况下实现专业外观的显示。

有多个模板可用于自定义列表行为的各个方面。其中最重要的模板之一是 <ItemTemplate>，它用于 Repeater、DataList 和 ListView 控件的列表中每个数据项的显示。你在控件声明内部声明此模板（以及所有其他模板）。例如：

```
<asp:DataList Runat="server" ... >
<ItemTemplate>
</ItemTemplate>
</asp:DataList>
```

在模板声明中，你通常希望输出 HTML 部分以及绑定到控件的数据的参数。你可以使用特殊语法输出此类参数：

```
<%# expression %>
```

表达式占位符可能只是将参数绑定到页面或控件属性的表达式，但更可能由 Eval() 或 Bind() 表达式组成。这些函数可通过指定列来输出绑定到控件的表中的数据。Eval() 使用以下语法：

```
<%# Eval("ColumnName") %>
```

可选的第二个参数允许你格式化返回的数据，其语法与别处使用的字符串格式化表达式相同。例如，这可用于将日期字符串格式化为更易读的格式——这是前面示例所缺乏的。

Bind() 表达式是相同的，但允许你将数据插入服务器控件的属性中。例如：

```
<asp:Label Runat="server" ID="ColumnDisplay" Text='<%# Bind("ColumnName") %>' />
```

请注意，因为 Bind() 参数中使用了双引号，所以需要使用单引号来包含属性值。

下表提供了可用模板的列表以及它们的使用时机。

| 模板 | 应用于 | 描述 |
|---|---|---|
| `<ItemTemplate>` | DataList, Repeater, ListView | 用于列表项 |
| `<HeaderTemplate>` | DataList, DetailsView, FormView, Repeater | 用于在项目之前输出 |
| `<FooterTemplate>` | DataList, DetailsView, FormView, Repeater | 用于在项目之后输出 |
| `<LayoutTemplate>` | ListView | 用于指定包围项目的输出 |
| `<SeparatorTemplate>` | DataList, Repeater | 用于列表中项目之间 |
| `<ItemSeparatorTemplate>` | ListView | 用于列表中项目之间 |
| `<AlternatingItemTemplate>` | DataList, ListView | 用于交替项目；可提高可见性 |
| `<SelectedItemTemplate>` | DataList, ListView | 用于列表中选中的项目 |
| `<EditItemTemplate>` | DataList, FormView, ListView | 用于正在编辑的项目 |
| `<InsertItemTemplate>` | FormView, ListView | 用于正在插入的项目 |

