

```csharp
theProfile.Bio = "New Bio for the Carmen account here";
theProfile.Save();
```

在接下来的练习中，你将把这些内容付诸实践，即显示创建特定照片相册的用户名称以及该用户的简介。

# 尝试一下：处理其他用户的配置文件

PhotoAlbums 文件夹下的 Default.aspx 页面显示特定照片相册中的图片。你无法看到是哪个用户创建了该照片相册，因此这将会是一个很棒的功能。为了进一步改进页面，你还可以显示用户的简介。在本次“尝试一下”中，你将看到如何实现这两个功能。

1. 从 PhotoAlbums 文件夹，以标记视图（Markup View）打开 Default.aspx 页面。向下滚动找到编辑之前添加的相册的 HyperLink 控件。在 HyperLink 控件之前，从工具箱拖入一个 `PlaceHolder` 控件并将其 ID 设置为 `PhotoAlbumDetails`。在 PlaceHolder 内部拖入两个 `Label` 控件，然后修改代码使其如下所示：

```asp
<asp:PlaceHolder ID="PhotoAlbumDetails" runat="server">
    <h2>Photo Album Details</h2>
    Created by: <asp:Label ID="UserNameLabel" runat="server" Text=""></asp:Label><br />
    About this user: <asp:Label ID="Bio" runat="server" Text=""></asp:Label>
</asp:PlaceHolder>
<br /><br />
<asp:HyperLink ID="EditLink" runat="server" Text="Edit Album" />
```

2. 切换到页面的后置代码（按 F7）并找到 ListView 控件的 `DataBound` 事件。在当用户没有权限时隐藏 HyperLink 控件的 `If` 语句之后，添加以下代码行以获取创建相册用户的配置文件，然后更新相关的标签：

```vbnet
EditLink.Visible = False

If Not String.IsNullOrEmpty(photoAlbumOwner) Then
    Dim ownerProfile As ProfileCommon = Profile.GetProfile(photoAlbumOwner)
    UserNameLabel.Text = photoAlbumOwner
    BioLabel.Text = ownerProfile.Bio
    PhotoAlbumDetails.Visible = True
Else
    PhotoAlbumDetails.Visible = False
End If
```

# C#

```csharp
EditLink.Visible = false;

if (!string.IsNullOrEmpty(photoAlbumOwner))
{
    ProfileCommon ownerProfile = Profile.GetProfile(photoAlbumOwner);
    UserNameLabel.Text = photoAlbumOwner;
    BioLabel.Text = ownerProfile.Bio;
    PhotoAlbumDetails.Visible = true;
}
else
{
    PhotoAlbumDetails.Visible = false;
}
```

3. 保存所有更改并在浏览器中打开该页面。

4. 从下拉菜单中选择你创建的照片相册，你应该能看到照片相册详情出现。如果你没有看到它们，请确保你已从列表中选择一个照片相册。如果你在较后阶段将 `UserName` 添加到数据库，则某些照片相册尚未与用户关联。“照片相册详情”部分将保持隐藏；创建一个新的照片相册并向其中再添加一张图片。这确保了你至少有一个带有 `UserName` 属性的相册。如果你从列表中选择照片相册，你应该会在分页控件下方看到照片相册详情，如图 17-9 所示。

![](img/9e033eb9560597824f822941d6dbb_696_0.png)

图 17-9

# 工作原理

此练习中的大部分代码之前已经讨论过。在照片相册页面中添加了几个 `Label` 控件后，你使用以下代码获取相册所有者的配置文件：

```vbnet
Dim ownerProfile As ProfileCommon = Profile.GetProfile(photoAlbumOwner)
```

```csharp
ProfileCommon ownerProfile = Profile.GetProfile(photoAlbumOwner);
```

此代码使用 `GetProfile` 获取现有配置文件的引用。返回的类是 `ProfileCommon`；Profile 的底层数据在 `Web.config` 文件中设置了如 `FirstName` 和 `LastName` 等属性。拥有引用后，对其进行操作与处理普通配置文件几乎相同。唯一的区别在于，正如你之前看到的，你必须调用 `Save` 将对配置进行的任何更改持久化到数据库中。

# 实用个性化提示

以下列表提供了一些个性化提示：

- 不要尝试在登录页面中访问当前用户的配置文件，因为此时尚未可用。配置文件在页面生命周期的早期就实例化了；当 Login 控件在登录页面中验证用户身份时，将该用户的配置文件与当前请求关联已经太晚了。请使用 `ProfileCommon` 的 `GetProfile` 方法或重定向到另一个页面。

- 仔细考虑存储在 Profile 中的内容以及哪些内容最好存储在你自己的数据库表中。虽然 ASP.NET 使用的单行结构来存储配置文件提供了一个简单方便的解决方案，但它不是最高效的，尤其是在处理大量数据时。不要尝试在 Profile 中存储完整的评论甚至照片相册，而应使用你自己的数据库表。

- Profile 目前的实现方式使得你从自己的查询中很难从 Profiles 表中查询数据。例如，很难回答诸如“给我看所有喜欢摇滚流派的用户”之类的查询，因为所有数据都存储在单列中。为了解决这些问题，请将数据存储在你自己的表中（例如使用 Entity Framework），或者从官方 ASP.NET 网站的 Sandbox 区域（www.asp.net/downloads/sandbox/）下载不同的 Profile Provider。

- 花些时间查看新的 ASP.NET Identity 系统。虽然它可以在高级场景中使用，但了解它提供了什么是有处的。

# 总结

在本章中，你学习了如何使用 ASP.NET 4.5 自带的 Profile 功能存储相关数据。你可以使用 Profile 来跟踪已验证用户和匿名用户。

设置配置文件是一个非常直接的操作。你需要在 `Web.config` 中配置 `<profile>` 元素并带有 `<properties>` 元素，然后使用 `<add>` 元素添加更多属性。为了对属性进行分组，可以使用 `<group>` 元素。

设置配置文件后，你通过页面的 `Profile` 属性访问它。这始终访问当前用户的配置文件。根据设计，配置文件属性仅对已登录用户可见。然而，你可以通过启用匿名身份轻松地更改这一点。

要访问与当前请求关联的用户的用户，可以使用 `GetProfile` 方法。对其进行的任何更改都不会自动保存，因此你必须调用 `Save` 将更改发送到数据库。

# 练习

1. 你之前创建的最喜主题功能是配置文件属性的绝佳候选。你需要在配置文件中添加哪些代码来实现这一目标？

2. 当你在 Web.config 中创建配置文件属性时，编译器仅为 Web Forms 后置代码类扩展了 `Profile` 属性。因此，为了在 BasePage 中设置最喜主题（或其他属性），你需要以特殊方式访问配置文件。不要访问页面类的 `Profile` 属性，而是通过 `HttpContext` 访问它：

```vbnet
Dim myProfile As ProfileCommon = CType(HttpContext.Current.Profile, ProfileCommon)
```

```csharp
ProfileCommon myProfile = (ProfileCommon) HttpContext.Current.Profile;
```

给定此代码，你如何重写 `Page_PreInit` 以便从配置文件而不是 Cookie 中获取偏好主题？

3. 你还需要哪些更改以最终完成将主题存储在配置文件而不是自定义 Cookie 中？

这些练习的答案可以在附录 A 中找到。