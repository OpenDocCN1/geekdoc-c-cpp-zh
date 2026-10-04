
2. 在此阶段，VS 已在“标记视图”（Markup View）中为 GridView 创建了列。要删除项并定义您自己的项，请使用 GridView 的智能任务（Smart Tasks）面板并点击“编辑列”（Edit Columns）。这将弹出“字段”（Fields）对话框。如果“已选字段”（Selected Fields）中包含项，请使用删除按钮（带有大 X 符号）清除第一个。

3. 在“可用字段”（Available）列表中，选择 `BoundField`（不是 CheckField 下方的那个）并点击“添加”（Add）按钮将其添加到“已选字段”列表中。对 `CreateTime` 字段重复此步骤。您的对话框现在看起来类似于图 13-12。

![](img/9e033e3b9560597824f8b22941d6d8bb_499_0.png)

图 13-12

4. 在屏幕顶部的“可用字段”中，选择 `HyperLinkField`，然后点击“添加”按钮将其添加到“已选字段”列表中。点击带有向上箭头的按钮将 `HyperLinkField` 移动到列表顶部。然后，使用右侧的“属性网”（Properties Grid）对 `HyperLinkField` 设置以下属性：

| 属性 (PROPERTY) | 设置值为 |
| --- | --- |
| HeaderText | Title |
| DataNavigateUrlFields | Id |
| DataNavigateUrlFormatString | AddEditReview.aspx?Id={0} |
| DataTextField | Title |

5. 在“可用字段”列表中，选择 `CommandField` 并再次点击“添加”按钮。然后，使用“属性网”将您插入的项的 `HeaderText` 设置为 `Delete`，并将 `ShowdeleteButton` 设置为 `True`。这允许您使用 GridView 从数据库中删除评论。“字段”对话框现在看起来类似于图 13-13。

![](img/9e033e3b9560597824f8b22941d6d8bb_500_0.png)

图 13-13

6. 点击“已选字段”列表中的 `Authorized` 列，然后点击图 13-1 对话框右下角的“将字段转换为模板字段”（Convert Field into a TemplateField）链接。

7. 点击左侧的 `CreateDateTime` 列，并将其 `DataFormatString` 属性设置为 `{0:g}`。

8. 点击“确定”将更改应用于源代码。

9. 切换到“标记视图”并移除 `Authorized` 字段的 `<EditTemplate>`。GridView 仅以只读模式显示，因此您不需要此模板。

10. 修改 `Authorized` 字段 `ItemTemplate` 中的 `Label` 控件，使其如下所示：

```
<asp:Label Id="AuthorizedLabel" run="server"
Text="<% GetBooleanText(Eval("Authorized")) />"
```

11. 按 F7 切换到页面的后台代码（Code Behind），并在类文件顶部添加以下函数——该函数根据您传递的值返回文本 "Yes" 或 "No"——位于 VB.NET 的 `Inherits` 行之后，以及 C# 的左大括号 `{` 之后：

# VB.NET

```
Inherits System.Web.UI.Page
Protected Function GetBooleanText(booleanValue As Object) As String
Dim authorized As Boolean = CType(booleanValue, Boolean)
If authorized Then
    Return "Yes"
Else
    Return "No"
End If
```

# C#

```sharp
public partial class Management_Reviews : System.Web.UI.Page

protected string GetBooleanText(object booleanValue)
{
    bool authorized = (bool)booleanValue;
    if (authorized)
    {
        return "Yes";
    }
    else
    {
        return "No";
    }
}
```

保存所有更改（按 `Ctrl+Shift+S`）并打开 Reviews。从下拉列表中选择一种类型，您将看到评论列表出现。`Authorized` 列显示 "Yes" 或 "No"。`CreateDateTime` 列显示短格式的日期和时间。图 13-14 显示了这种结果。

![](img/9e033e3b9560597824f8b22941d6d8bb_500_0.png)

图 13-14

## 自定义控件外观

注意 GridView 的第一列链接到页面，该页面取决于您传递的值：`https://example.org/AddEditReview.aspx?Id=1`。如果需要，可以去掉 `.aspx` 后缀，因为配置了友好 URL 会解决此问题。

## 工作原理

通过修改 `SqlDataSource` 的 `SelectCommand`，不再使用 `SELECT *` 而是选择特定的字段，这提高了页面加载速度：

```asp
<SqlDataSource ID="DataSource2"
ConnectionString="{ConnectionStrings:PlanetWorkConnectionString1}"
SelectCommand="SELECT [ID], [Title], [Authorized], [CreateDateTime]
FROM [Review] WHERE ([GenId] = @GenId)"
```
