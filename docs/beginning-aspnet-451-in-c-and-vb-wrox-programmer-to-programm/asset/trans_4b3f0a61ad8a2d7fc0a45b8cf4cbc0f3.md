

```xml
</asp:HyperLink><br />
</ItemTemplate>
</asp:Repeater>
</ItemTemplate>
</asp:Repeater>
<asp:PlaceHolder ID="NoRecords" runat="server" Visible="False">
<p>抱歉，没有找到任何评论。您可能没有设置喜喜欢的类型，或者您可能需要先登录。</p>
</asp:PlaceHolder>
<p>您可以在<a href="~/MyProfile" runat="server">这里</a>更改您的类型偏好。</p>
```

您可以通过编写必要的代码来手动创建 Repeater 控件，也可以从工具箱的 Data 类别中将它们拖放。。内部 Repeater 包含一个 HyperLink 控件，该控件指向您在第 15 章中创建的 ViewDetails.aspx 页面。注意，内部 Repeater 通过设置其 `ItemType` 为 `Review` 实现了强类型支持（因为它显示的是 Review 实例）。您无法对外部 Repeater 这样做，因为它的数据源是一个匿名对象集合，如下所示，是在后台代码的 `Page_Load` 中设置的。

- 3. 在设计视图中双击页面以设置加载处理程序。在 VS 为您创建的处理程序中添加以下代码：

# VB.NET

```vb
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    Using myEntities As PlanetWroxEntities = New PlanetWroxEntities()
        If Profile.FavoriteGenres.Count > 0 Then
            Dim favGenres = From genre In myEntities.Genres.Include("Reviews")
                            Order By genre.Name
                            Where Profile.FavoriteGenres.Contains(genre.Id)
                            Select New With {genre.Name, genre.Reviews}

            GenreRepeater.DataSource = favGenres.ToList()
            GenreRepeater.DataBind()
        End If

        GenreRepeater.Visible = GenreRepeater.Items.Count > 0
        NoRecords.Visible = Not GenreRepeater.Visible
    End Using
End Sub
```

# C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    using (PlanetWroxEntities myEntities = new PlanetWroxEntities())
    {
        if (Profile.FavoriteGenres.Count > 0)
        {
            var favGenres = from genre in myEntities.Genres.Include("Reviews")
                            orderby genre.Name
                            where Profile.FavoriteGenres.Contains(genre.Id)
                            select new { genre.Name, genre.Reviews };

            GenreRepeater.DataSource = favGenres.ToList();
            GenreRepeater.DataBind();
        }
        GenreRepeater.Visible = GenreRepeater.Items.Count > 0;
        NoRecords.Visible = !GenreRepeater.Visible;
    }
}
```

- 4. 保存所有更改并在浏览器中请求该页面。如果您之前在 Profile 页面中选择了一个或多个类型，并且这些类型有评论，您应该会看到类似于图 17-6 的列表。

![](img/9e033e3b9560597824f8b22941d6d8bb_685_0.png)

# 图 17-6

如果您没有设置任何偏好类型，或者尚未登录，将看到如图 17-7 所示的消息。

![](img/9e033e3b9560597824f8b22941d6d8bb_685_1.png)

# 图 17-7

通过点击消息中的链接，您将被带到 My Profile 页面，以便可以在那里设置或更改您的偏好类型。未经授权的用户在访问 Profile 页面之前需要登录或注册账户。

# 工作原理

后台代码中的代码执行了一个 LINQ to Entities 查询，检索所有属于用户喜好类型的评论。对于匿名用户，喜好类型列表将为空，因此他们始终会看到关于在 Profile 页面中设置偏好的消息。为了避免不必要的数据库调用，查询只有在检查 `FavoriteGenres` 列表的 `Count` 属性并确认用户至少选择了一个偏好类型时才会执行。

由于您添加到 Default.aspx 页面上的嵌套 Repeater 的数据源是 Review 实例集合，通过设置其 `ItemType` 并使用 `Item` 属性而不是使用 `Eval`，它已经实现了强类型。正如您之前学到的，这更容易编写代码并更早地发现错误。

嵌套 Repeater 看起来与 AllByGenre.aspx 页面的代码有点像，该页面包含一个带有 BulletedList 控件的 Repeater。与在该页面中一样，嵌套 Repeater 通过 `DataSource` 属性从外部 Repeater 获取数据：

```xml
<asp:Repeater ID="ReviewRepeater" runat="server" ItemType="Review"
    DataSource='<%# Eval("Reviews") %>'>
    ...
</asp:Repeater>
```

随后，嵌套 Repeater 使用 Reviews 列表构建跳转到详情页的超链接：

```xml
<asp:HyperLink ID="HyperLink1" runat="server" Text='<%# Item.Title %>'
    NavigateUrl='<%# "ViewDetails?ReviewId=" + Item.Id.ToString() %>'>
</asp:HyperLink>
```

HyperLink 控件从其绑定的 Review 实例中获取 `Text`，并使用其 `Id` 构建 `NavigateUrl`。

