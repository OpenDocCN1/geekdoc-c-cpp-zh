

如果你想查看工作中的其他事件，只需重复上一个练习的第 7 和第 10 步，为各种事件设置处理程序。要查看视图状态（View State）的效果，可以尝试在控件级别（例如针对 GridView）或页面级别禁用它。在第 18 章中，你将学习到一种名为“跟踪”（tracing）的技术，它可以让你获取页面中所有控件的信息，包括执行各种事件所需的时间。

虽然上一个练习在实际应用中并没什么用，但它能帮助你理解控件事件及其触发顺序。你可以使用相同的原理来挂钩页面并对页面本身或页面上的任何控件进行修改。在下一个练习中，你将看到如何根据正在显示的数据更改数据源行的外观。

# ASP.NET 页面生命周期与数据控件中的事件

如所述，GridView 会为其其添加到输出中的每行抛出 `RowCreated` 和 `RowDataBound` 事件。这些事件非常适合用于监视数据，并根据这些数据采取适当的操作。例如，你可以使用这些事件来验证评论是否已授权显示。如果不是（意味着它不在前端视图中），你可以更改评论的外观以引起注意。另一个使用事件的示例是，当界面中的控件显示或激活状态没有意义时，隐藏或禁用这些控件。你将在下一个练习中看到如何删除 GridView 中的链接。

> 尝试一下：挂钩 RowDataBound

在本次尝试中，你为管理部分（Management section）中 Genres 页面的 `RowDataBound` 事件编写一个事件处理程序。在此事件中，你可以诊断绑定到 GridView 行的数据项，让你查看该类型是否关联了评论。如果该类型与评论关联，你将使用某些代码禁用链接，以便用户不会意外删除它。

- 1. 从管理视图（Management View）打开 `Genres.aspx` 页面并找到 `SqlDataSource` 控件。找到 `SelectCommand` 并修改 SQL 语句使其如下：

```
SELECT Review.Id, Genre.Name, Genre.SortOrder
COUNT(Review.Id) AS NumberOfReviews FROM Genre LEFT OUTER JOIN Review
ON Genre.Id = Review.GenreId GROUP BY Genre.Id, Genre.Name, Genre.SortOrder
```

你可以将编辑后的 SQL 语句写在一行，也可以像我在这里这样将其拆分成多行。

- 2. 切换到设计视图（Design View）并打开 GridView 控件的智能任务（Smart Tasks）面板。点击“刷新架构”（Refresh Schema）面板，对关于重新生成字段回答“否”，并保持控件当前的布局。

点击智能任务面板上的“编辑列”（Edit Columns）打开字段对话框。在“所选字段”（Selected Fields）列表中点击 `CommandField` ，然后点击对话框右下角的链接将字段转换为模板字段（TemplateField）。这样，列就会扩展为模板，从而更方便地访问其中包含的控件（例如删除 链接）。点击“确定”关闭字段对话框。

- 3. 在标记视图（Markup View）中，找到删除 链接（`CommandName` 设置为 `Delete` 的那个），并将其 ID 更改为 `DeleteLink`：

```
<asp:LinkButton ID="DeleteLink" runat="server" CausesValidation="False" CommandName="Delete" Text="Delete"></asp:LinkButton>
```

- 4. 切换到设计视图，打开 GridView 的属性网格，并切换到事件（Events）选项卡。为 `RowDataBound` 事件设置事件处理程序。

- 5. 在 Web 表单的后代码（Code Behind）顶部添加以下代码：

```VB.NET
Imports System.Data;
```
```csharp
using System.Data;
```

- 6. 在 VS 为你创建的事件处理器内部添加以下代码：

```VB.NET
Protected Sub GridView1_RowDataBound(sender As Object, e As GridViewRowEventArgs) Handles GridView1.RowDataBound
Select Case e.Row.RowType
 Case DataControl.RowType.Data:
 Dim myRow As DataView = CType(e.Row.DataItem, DataView)
 If Convert.ToInt32(myRow("NumberOfReviews")) > 0 Then
 Dim deletelink As LinkButton =
 TryCast(e.Row.FindControl("DeleteLink"), LinkButton)
 If deletelink Is Not Nothing Then
 deletelink.Enabled = False
 End If
 End If
End Select
End Sub
```

```csharp
protected void GridView1_RowDataBound(object sender, GridViewRowEventArgs e)
{
    if (e.Row.RowType == DataControl.RowType.Data)
    {
        DataView myDataView = (DataView)e.Row.DataItem;
        if (Convert.ToInt32(myDataView["NumberOfReviews"]) > 0)
        {
            LinkButton deleteLink = e.Row.FindControl("DeleteLink") as LinkButton;
            if (deleteLink != null)
            {
                deleteLink.Enabled = false;
            }
        }
    }
}
```

- 7. 保存更改打开所有文件，然后在浏览器中请求 `Genres.aspx`。注意对于关联了评论的类型，删除 链接已禁用，如图 15-8 所示。

# 工作原理

虽然很短，但这个练习演示了挂钩控件不同事件并更改底层控件呈现的强大方法。要查看它的工作原理，首先查看修改后的 SQL 代码：

```
SELECT
Genre.Id, Genre.Name, Genre.SortOrder, COUNT(Review.Id) As NumberOfReviews
FROM
Genre LEFT OUTER JOIN
Review ON Genre.Id = Review.GenreId
GROUP BY
Genre.Id, Genre.Name, Genre.SortOrder
```

| Edit | Name | SortOrder |
|---|---|---|
| Delete | Rap and Hip-Hop | 14 |
| Delete | Pop | 12 |
| Delete | Jazz | 8 |
| Delete | Hard Rock | 3 |
| Delete | Indie Rock | 7 |
| Delete | Punk | 1 |
| Delete | Rock | 2 |
| Delete | Grunge | 4 |
| Delete | Alternative Rock | 9 |
| Delete | Reggae | 11 |

图 15-8

此修改后的 SQL 语句获取了 `Genre` 表的所有列，但引入了一个新列 `NumberReviews`，它包含与每个类型关联的评论数量。这是通过对 `Review` 表的 `Id` 列执行 SQL `COUNT` 函数来实现的。该语句使用 `GROUP BY` 通过合并非唯一行将选定行分组一组摘要行。

