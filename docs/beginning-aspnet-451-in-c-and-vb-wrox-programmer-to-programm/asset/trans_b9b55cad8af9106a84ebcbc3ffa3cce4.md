

# 理解 Profile | 637

## VB.NET

```
Profile.FirstName = "Your first name here"
```

## C#

```csharp
Profile.FirstName = "Your first name here";
```

虽然在这个练习中没有用到，但你访问组属性的方式几乎相同。你只需要在属性名前名前加上组名和一个点即可。以 `PostalAddress` 为例，你可以这样存储该地址的街道信息：

## VB.NET

```
Profile.PostalAddress.Street = "Some Street"
```

## C#

```csharp
Profile.PostalAddress.Street = "Some Street";
```

对 profile 的更改会在 `EndRequest` 事件期间自动为你保存，该事件在 ASP.NET 页面生命周期的非常晚阶段触发。通过这种方式，你可以在生命周期的许多阶段更改 profile，而无需担心手动显式地保存 profile。第一列包含所属 profile 的用户的唯一 ID。第二列包含为当前用户保存的属性列表，以及值的起始索引和长度。例如，对于姓氏（LastName），你使用：

```
LastName:4:10
```

这表示存储在 `PropertyValues` 列中的 `LastName` 属性值从位置 4 开始（因为位置是从零开始的），长度为 10 个字符。这种紧凑格式允许 Profile 在单个列中存储许多不同的属性，从而消除了每次 profile 更改时与数据库架构合并的需求。早期版本的 Profile 使用 `PropertyValueBinary` 来存储图像等二进制对象。然而，Profile 现在也会将这些转换为字符串并存储在 `PropertyValues` 列中。

你将在下一节中学习更多关于从 profile 读取到写入的知识。

## 使用 Profile

正如你在上一节看到的，向 profile 写入数据是简单的。要更改像 `FirstName` 这样的属性，你只需要一行代码。Profile 会跟踪你对其所做的更改，并在必要时在 `EndRequest` 自动保存更改。从 profile 读取数据同样简单；你只需要访问它的属性之一。以下代码段显示了如何向 `TextBox` 填充 profile 的第一个名字：

## VB.NET

```
FirstName.Text = Profile.FirstName
```

## C#

```csharp
FirstName.Text = Profile.FirstName;
```

检索组中的属性几乎完全相同。要访问之前示例中讨论的 `Street` 属性，你需要此代码：

## VB.NET

```
PostalAddressStreet.Text = Profile.PostalAddress.Street
```

## C#

```csharp
PostalAddressStreet.Text = Profile.PostalAddress.Street;
```

访问 `FavoriteGenres` 属性略有不同。因为此属性是一个集合，你不应该直接给它赋值。相反，请使用它的方法和属性来获取数据的输出。下面的示例清空了整个列表，然后为其添加了两个流的 ID：

## VB.NET

```
Profile.FavoriteGenres.Clear()
Profile.FavoriteGenres.Add(7)
Profile.FavoriteGenres.Add(11);
```

## C#

```csharp
Profile.FavoriteGenres.Clear();
Profile.FavoriteGenres.Add(7);
Profile.FavoriteGenres.Add(11);
```

以下练习显示了如何在用户的 profile 中存储基本数据。你将在稍后的练习中看到使用 `FavoriteGenres` 列表的实际实现。

## 尝试一下 在 Profile 中存储基本用户数据

在本次尝试中，你将修改 Profile 页面以便将其名字、姓氏、生日和简短介绍保存到他们的 profile 中。

- 1. 再次打开 MyProfile.aspx 并切换到代码后台（Code Behind）。删除 `Page_Load` 中设置姓名的两行代码。

- 2. 切换到设计视图，将光标置于段和 `ChangePassword` 控件之间。要定位光标，先点击 `ChangePassword` 选中它，然后按左箭头键。通过选择 表 ⇞ 插入表格创建一个五行三列的 TextBox 表格。

- 3. 在四行的每第二列中，拖入 `TextBox` 控件并重命名它们，从第一行到最后一行分别为 `FirstName`、`LastName`、`DateOfBirth` 和 `Bio`（通过设置它们的 `ID` 属性）。图 17-3 为你精确展示了 TextBox 控件应该放置的位置。

- 4. 在四行的每第一列中，放入 `Label` 控件并按照如下设置设置属性，以便每个标签与该行中的 `TextBox` 关联。

# 理解 Profile | 639

| Text | AssociatedControlID |
|---|--|
| First name | FirstName |
| Last name | LastName |
| Date of birth | DateOfBirth |
| Biography | Bio |

- 5. 在第五行的第二个单元格中，绘制一个 `Button` 并将其 `ID` 设置为 `SaveButton`，`Text` 设置为 `Save profile`。设计视图应该看起来像图 17-3。

![](img/9e033e3b9560597824f8b22941d6d8bb_676_0.png)

图 17-3

- 6. 在前三行的每最后一列中，绘制 `RequiredFieldValidator` 控件。按照如下设置它们的属性，以便验证器与同一行中的 `TextBox` 对齐。记住：你可以先按住 Ctrl 键选择所有控件，然后为所有控件设置 `Display` 属性。

| ControlToValidate | Display | ErrorMessage |
|---|---|--|
| FirstName | Dynamic | First name is required. |
| LastName | Dynamic | Last name is required. |
| DateOfBirth | Dynamic | Date of birth is required. |

- 7. 在 `DateOfBirth` 框验证器旁边，拖入一个 `Comparator` 并按照如下设置它的属性：

| Property | Value |
|---|---|---|
| Display | Dynamic |
| ErrorMessage | Please enter a valid date. |
| ControlToValidate | DateOfBirth |
| Operator | DataTypeCheck |
| Type | Date |

- 8. 将 `Bio` 的 `TextMode` 设置为 `Multiline`，并将其 `Height` 和 `Width` 属性分别设置为 `75px` 和 `300px`。

- 9. 修改上方表格，表示用户现在可以不仅仅是单独更改密码。你的设计视图应该像图 17-4。

![](img/9e033e3b9560597824f8b22941d6d8bb_677_0.png)

图 17-4

- 10. 双击 Save 按钮，并在 VS 为你添加的 `Click` 事件处理程序中，编写以下加粗代码：

```
VB.NET
Protected Sub SaveButton_Click(sender As Object, e As EventArgs) Handles SaveButton.Click
If Page.IsValid Then
Profile.FirstName = FirstName.Text
Profile.LastName = LastName.Text
Profile.DateOfBirth = DateTime.Parse(DateOfBirth.Text)
Profile.Bio = Bio.Text
End If
```

# C#

```csharp
protected void SaveButton_Click(object sender, EventArgs e)
{
    if (Page.IsValid)
    {
        Profile.FirstName = FirstName.Text;
        Profile.LastName = LastName.Text;
        Profile.DateOfBirth = DateTime.Parse(DateOfBirth.Text);
        Profile.Bio = Bio.Text;
    }
}
```

- 11. 在同一页的 `Page_Load` 处理程序中，添加以下代码，用 profile 数据填充文本控件：

```
VB.NET
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    If Not Page.PostBack Then
        FirstName.Text = Profile.FirstName
        LastName.Text = Profile.LastName
        Dateof.Text = Profile.DateOfBirth.ToDateString()
        Bio.Text = Profile.Bio
    End If
End Sub
```

# C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    if (!Page.PostBack)
    {
        FirstName.Text = Profile.FirstName;
        LastName.Text = Profile.LastName;
        DateBirth.Text = Profile.DateOfBirth.ToShortDateString();
        Bio.Text = Profile.Bio;
    }
}
```

- 12. 保存所有更改并在浏览器中请求页面。如果要求先登录，输入你的详细信息，点击 Login 按钮并浏览到 My Profile 页面。你应该看到之前在尝试练习中输入的名字和姓氏已经填充。此外，生日字段已填充了 DateTime 的默认值：0001年1月1日。使用你的详细信息填写表单并点击 Save 按钮。

- 13. 重启浏览器并请求 MyProfile.aspx 页面。注意你的更改在两次浏览器会话之间得到了持久化。

# 工作原理

你在练习中看到的很多内容现在应该已经熟悉。页面包含许多 `TextBox` 控件，这些控件使用 `RequiredFieldValidator` 和 `CompareValidator` 控件进行验证。此外，`Label` 控件通过以下方式与其对应的 `TextBox` 控件关联：

