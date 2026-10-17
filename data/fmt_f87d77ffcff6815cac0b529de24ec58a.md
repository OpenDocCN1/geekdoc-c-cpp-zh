
这与创建新相册的代码几乎相同。这里的区别是另一个 `QueryString` 属性，它填充了相册的 ID。你在本章稍早之前启用的 Entity Framework，“Include Key Columns”选项在 `Picture` 类上为你提供了一个 `PhotoAlbumId` 属性，该属性允许你直接设置相册的 ID（你从查询字符串中获取的 ID）。这反过来将数据库中的图片与 `PhotoAlbum` 表中的特定相册关联起来。如果你没有启用该选项，该属性将不会存在，你将根据根据 ID 从数据库查询相册，并将 `PhotoAlbum` 实例分配给图片的 `PhotoAlbum` 属性。使用外键列让这个过程变得简单得多，因为你只需要分配你想要添加此图片的相册 ID 即可。

当你点击图片的删除按钮时，ListView 会找到如下所示的 `DeleteMethod`：

```vb.net
Public Sub ListView_DeleteItem(ByVal id As Integer)
    Using myWeb As New PlanetWroxEntities()
        Dim picture = (From p in myWeb.Pictures
                       Where p.Id = id
                       Select p).Single()
        myEntities.Pictures.Remove(picture)
        myEntities.SaveChanges()
    End Using
End Sub
```

```csharp
public void ListView_DeleteItem(int id)
{
    using (var entities = new PlanetWroxEntities())
    {
        var picture = (from p in entities.Pictures
                        where p.Id == id
                        select p).Single();
        entities.Pictures.Remove(picture);
        entities.SaveChanges();
    }
}
```

此方法创建了一个新的 `PlanetWroxEntities` 实例，然后使用 LINQ 查询找到正确的图片。然后它调用 `Pictures` 集合上的 `Remove` 方法并将其推取，然后调用 `SaveChanges`。但 ListView 如何知道如何填充此方法的 `ID` 参数呢？答案定义在 ListView 上的 `DataKeyNames` 属性中：

```asp
<asp:ListView ID="ListView1" runat="server" DataKeyNames="ID" ...
```

ListView 在 `ViewState` 中存储每个单独项的 ID。然后当你点击删除按钮时，它会提取你想要删除的图片的正确 ID，然后将其发送到后台代码（Code Behind）中的 `DeleteItem` 方法。

此练习的最后一部分是你需要查看你添加到主题 CSS 文件中的 CSS 代码，以便以组织化的方式显示项目。通过将 `<ul>` 控件的 `class` 属性设置为该列表：

```css
.ItemContainer
{
  width: 600px;
  list-style-type: none;
  clear: both;
}
```

第一个属性将整个列表的宽度设置为 600 像素，第二个声明删除了列表项目中的项目符号。列表中的每个项目随后显示在 `<li>` 元素中，并应用以下 CSS：

```css
.ItemContainer li
{
  height: 300px;
  width: 200px;
  float: left;
}
```

每个项目都强制获得 200 像素的宽度。`float` 属性告诉 `<li>` 元素相互浮动。在 600 像素的父级区域内，你可以容纳三个 200 像素的 `<li>` 元素，导致第四个及后续元素被放置在自己的行上。这是使用 HTML 表格呈现数据的极佳替代方案，因为网格通常需要大量的标记才能实现相同的效果。

最后，`<li>` 元素内的每张图像都强制获得 180 像素的宽度，并且上下有 10 像素的外边距，右侧 20 像素（以便在图片之间留出空间），左侧为零：

```css
.ItemContainer img
{
  width: 180px;
  margin: 10px 20px 10px 0px;
}
```

在深灰色中，`ItemContainer` 的宽度设置为 400 像素。这种方式可以并排显示图片。ASP.NET 4.5 引入了新方法来设置这些绑定。查看如何使用这些绑定。

# 使用强类型控件

当你向 ListView 添加代码时，使用了如下的 `Bind` 和 `Eval` 语句：

```asp
<asp:TextBox ID="ToolTip" runat="server" Text='<%# Bind("ToolTip") %>' />
...
Text='<%# Eval("ToolTip") %>'
```

正如你在“工作原理”部分中所学到的，`Bind` 用于双向绑定（用于插入和编辑场景），而 `Eval` 用于只读场景。注意属性名称是放在引号之间的。使用字面量会让代码更容易出错。首先，字符串无法在开发时进行检查，你只有查看页面时才会发现错误。

幸运有一个解决方案。数据绑定控件（如 ListView、Repeater、GridView、DetailsView 和 FormView）扩展了一个 `ItemType` 属性，你可以将其指向分配的对象类型。在示例中，该类型将 `Picture`。一旦设置了此属性，数据绑定控件就有两个新属性 `Item` 和 `BindItem`，它们的类型为你分配的类型。第一个作为 `Eval` 的替代品，第二个替换 `Bind`。当你漏掉属性名称或重命名它时，你会在错误列表中收到错误，从而获得修复问题的机会。

尽管这是一个帮助你编写更好代码的极佳功能，但你只有在处理强类型对象（例如来自 EF 模型的 `Picture` 或你或第三方创建的其他类）时才能使用该解决方案。它不支持以下情况：

- 使用 `DataSource` 控件。该控件下的对象没有映射到列的强类型属性（例如 `ToolTip` 和 `Description`），因此无法通过 `Item` 和 `BindItem` 属性访问这些列或属性。
- 使用匿名对象。由于匿名对象没有名称，你无法将其名称分配给 `ItemType` 属性。

# 尝试使用强类型数据绑定控件

在本次练习中，你把 `ManagePhotoAlbum.aspx` 中的 ListView 控件改为强类型。你看到如何设置 `ItemType` 属性以及如何将 `Bind` 和 `Eval` 替换为它们的强类型对应项。当你运行页面时，页面的工作与之前完全相同，但未来将更容易维护。

# 第 14 章 LINQ 与 ADO.NET 框架

## 练习步骤

- 1. 首先，在 VS 的标记视图中打开 `ManagePhotoAlbum.aspx`。
- 2. 找到 ListView 标签并添加 `ItemType` 属性，将其值设为 `Picture`。注意 IntelliSense 如何通过显示所有可以作为 `ItemType` 的类型列表来帮助你找到正确的项，如图 14-13 所示。
- 3. 在 ListView 的 `InsertItemTemplate` 模板内部，为 Description TextBox 绑定语句，将其从 `Bind("Description")` 更改为 `Bind(BindItem.Description)`。注意 IntelliSense 如何帮助你输入 `description` 属性。你最终得到的结果应该是这样的：

```asp
<asp:TextBox ID="Description" runat="server" Text='<%# Bind(BindItem.Description) %>' />
```

- 4. 对 ToolTip TextBox 重复上述步骤。`ImageUrl` 在本章稍后会进行特殊处理，因此现在更改它没有意义。
- 5. 在 ListView 的 `InsertItemTemplate` 模板内部，对 Description Label 评估 `Eval` 语句，将其从 `Eval("Description")` 更改为 `Item.Description`。你最终得到的结果应该是：

```asp
<asp:Label ID="Description" runat="server" Text='<%# Item.Description %>' />
```

- 6. 对 ToolTip TextBox 重复步骤 5。同样，`ImageUrl` 在本章稍后会进行特殊处理，因此现在更改它没有意义。
- 7. 保存更改并在浏览器中请求 `NewPhotoAlbum.aspx`。插入新专辑，通过输入描述、工具提示并上传图像来添加一些功能。注意代码的行为仍然与之前一样。

![](img/9e033e3b9560597824f8b22941d6d8bb_561_0.png)

## 工作原理

你不需要通过更改来使 ListView 强类型化并获得 IntelliSense 的帮助和编译时检查。你所做的只是为 ListView 添加 `ItemType` 属性，并将 `Bind` 和 `Eval` 的调用替换为 `Item`。通过这些更改，控件的行为与之前完全相同。在运行时，控件会查看分配的属性并在浏览器中显示它们。当你将数据提交回服务器时，反向过程发生了：你在控件中输入的值由 Model Binder 检索并分配给 `Picture` 对象的属性，然后由 Entity Framework 存储在数据库中。建议尽可能使用强类型绑定，因为它们可以帮助你尽早发现错误并让编写代码变得更容易。现在用户需要手动为图像输入 URL。这显然对用户不友好。如果他们可以从本地计算机选择图像并上传到服务器，将会方便得多。你将在下一个练习中看到如何实现这一点。

使用 LINQ 查询模型绑定

# 尝试自定义 ListView 控件

在练习中添加的 ListView 控件模板在最简单的情况下是足够的。通常需要更多。例如，在 `ItemTemplate` 中，你可能希望显示实际图像而不是 `Label` 属性。同样，在 `InsertItemTemplate` 中你可能希望显示文件上传控件而不是文本框。在本练习中，你将看到如何更改这些模板以包含这些功能。此外，你将看到如何更新 `InsertItem` 将上传的文件保存到磁盘，并使用图像的 URL 更新数据库。对于此示例，Web 服务器需要权限读取并写入你在练习中创建的 `GPics` 文件夹。如果你在 IIS 方面遇到问题，请参阅第 19 章的“理解 IIS 安全”。

- 1. 在网站根目录下创建一个名为 `GPics` 的文件夹。此文件夹将包含用户上传的图片。
- 2. 在标记视图中打开 `ManagePhotoAlbum.aspx`，找到 `<ItemTemplate>` 元素。显示 `ImageUrl` 的 `Label` 替换为控件，将其 `ImageUrl` 设置为图片的。
- 3. 为了启用上传图像，你需要将 `ImageUrl` 属性的 `TextBox` 替换为 `FileUpload` 控件。你还需要删除 `ImageUrl` 文本。注意，上传的图像需要特殊处理，你将在代码后台编写一些代码。
- 4. 在标记中，为 `InsertItemTemplate` 添加三个验证控件：用于 `Description` 和 `Tooltip` 的两个 `RequiredValidator`，以及一个用于选择有效 .jpg 文件的 `CustomValidator`。为 `RequiredValidator` 分配 ID 为 `reqDesc` 和 `reqTooltip`，然后将 `Description` 文本框的 `TextMode` 设置为 `Multiline`。代码如下：

```
<asp:RequiredValidator ID="reqDesc" ControlValidate="Description" ErrorMessage="Enter a description." />
<asp:TextBox ID="Description" runat="server" TextMode="Multiline" Text='<%# Bind(BindItem.Description) %>' />
<asp:RequiredValidator ID="reqToolTip" ControlValidate="ToolTip" runat="server" ErrorMessage="Enter a tool tip." />
<asp:TextBox ID="ToolTip" runat="server" Text='<%# Bind(BindItem.ToolTip) %>' />
<asp:CustomValidator Id="cusValidation" runat="server" ErrorMessage="Select a valid .jpg file." />
<asp:Button Id="InsertButton" runat="server" CommandName="Insert" Text="Insert" />
```

- 5. 到代码后台并以下代码扩展 `ListView_ItemInserted`：

### VB.NET

```vb
UpdateModel(picture)
Dim FileUpload As FileUpload =
CType(ListView.InsertedItem.FindControl("FileUpload1"), FileUpload)
If Not FileUpload1.HasFile Or
    Not FileUpload1.FileName.ToLower().EndsWith(".jpg") Then
    Dim cusImage As CustomValidator =
    CType(ListView.InsertedItem.FindControl("cusImage"), CustomValidator)
    cusImage.IsValid = False
    ModelState.Add("Invalid", cusImage.ErrorMessage)
End If
```

### C#

```csharp
UpdateModel(picture);
FileUpload fileUpload = (FileUpload)ListView.InsertedItem.FindControl("FileUpload1");
if (!fileUpload.HasFile || !fileUpload.FileName.ToLower().EndsWith(".jpg"))
{
    CustomValidator cusImage = (CustomValidator)ListView.InsertedItem.FindControl("cusImage");
    cusImage.IsValid = false;
    ModelState.Add("Invalid", cusImage.ErrorMessage);
}
```

- 6. 在方法底部，图片实例分配专辑 ID 后，添加以下代码，将文件保存到磁盘并用新位置更新 `Picture` 的 `ImageUrl` 属性：

### VB.NET

```vb
picture.PhotoAlbumId = albumId
Dim virtualFolder As String = "~/GPics/"
Dim fileName As String = Guid.NewGuid().ToString()
Dim extension As String = System.IO.Path.GetExtension(FileUpload1.FileName)

FileUpload1.Save(System.IO.Path.Combine(virtualFolder, fileName))
picture.ImageUrl = virtualFolder + fileName
```

### C#

```csharp
picture.PhotoAlbumId = albumId;
string virtualFolder = "~/GPics/";
string fileName = Guid.NewGuid().ToString();
string extension = System.IO.Path.GetExtension(fileUpload.FileName);

fileUpload.Save(System.IO.Path.Combine(virtualFolder, fileName));
picture.ImageUrl = virtualFolder + fileName;
```

- 7. 保存所有更改，然后在浏览器中请求 `NewPhotoAlbum.aspx`（当你不小心请求了处理过的 PhotoAlbum.aspx 页面时）。为照片专辑输入新名称并点击插入链接。通过输入描述和工具提示、从硬盘上选择 .jpg 图片并点击插入按钮来插入几张图片。如果你收到类似下面的错误消息：

`Could not find a part of the path 'C:\ASPNET\Site\GigPic\7b26dd62-82f5-4942-ac80-6438ae4d062.jpg'.`

确保你已经在站点子目录下创建了 `GigPics` 文件夹。
- 8. 点击文件上传框的浏览按钮，选择一个有效的 .jpg 文件，再次点击插入按钮。文件现在成功上传了。

## 工作原理
