
单击“下一步”进入“选择数据库对象和设置”对话框。

4. 在此对话框中，展开 Tables，再展开 dbo，然后勾选 Genre 和 Review 表。如果看到 sysdiagrams 表，请保持不勾选。这是 SQL Server 内部使用的表，你的 Planet Wrox 模型中不需要它。如果你使用的是英文版 VS，会看到一个选项，可以自动对模型中的名称进行复数化或单数化处理，请保持勾选。对于其他语言版本，你需要像下一步那样手动完成此操作。最后，确保勾选“在模型中包含外键列”的选项。本章后面你会看到该选项的用途。单击“完成”将模型添加到站点。如果出现安全警告，请单击“不再显示此消息”，然后单击“确定”。Visual Studio 使用所谓的 T4 模板为你生成代码，默认情况下你需要授予执行此模板的权限。

![](img/eadab2ccd79b253c01a3fdff2321202d_547_0.png)

图 14-2

5. VS 会添加一个名为 PlanetWrox.edmx 的文件和两个带有 .tt 扩展名的文件，然后在主编辑器窗口中打开实体设计器，如图 14-2 所示。它还在站点根目录下创建了一个 Bin 文件夹，并添加了实体框架所需的程序集和 XML 文档文件。

此实体设计器显示根据数据库中的表生成的 .NET 类。VS 绘制了一条连接两个类的线，表示它识别出了你在第 12 章中为底层表创建的关系。如果你没有看到这条线，或者没有在 Genre 类的底部看到 Reviews，或在 Reviews 类的底部看到 Genre，请确保你按照第 12 章的说明正确设置了数据库。

6. 如果你使用的是非英文版 VS，则需要自己将实体集和属性的名称复数化。为此，请在设计器中单击 Genre 类，按 F4 打开其属性网格，将实体集名称从 Genre 改为 Genres。对 Review 类重复此操作，并将其实体集名称改为 Reviews。最后，在关系图中单击 Genre 类的 Review 属性（位于图 14-2 中的“导航属性”标题下方），按 F2 重命名该项，并输入 Reviews 作为新名称。由于一条 Review 只属于一个 Genre，因此你不需要将 Review 类的 Genre 属性复数化。

7. 单击设计器表面的空白处，按 F4 打开属性网格。将“代码生成策略”属性从 None 改为 Default。

8. 保存并关闭关系图，然后从 App_Code 文件夹中删除 PlanetWrox.tt 和 PlanetWrox.Context.tt 文件。

9. 打开 Reviews 文件夹中的 All.aspx，切换到设计视图，从工具箱中将一个 GridView 拖到页面上。如果你没有此页面，现在创建它，并以自定义模板为基础。

10. 在灰色的只读区域双击页面，让 VS 为页面的 Load 事件设置处理程序，并添加以下代码。请务必阅读代码示例后的下一段内容，了解如何解决输入此代码时可能出现的错误。

### VB.NET

```vbnet
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    Using myEntities As New PlanetWroxEntities()
        Dim authorizedReviews = From review In myEntities.Reviews
                                Where review.Authorized = True
                                Order By review.CreateDateTime Descending
                                Select review
        GridView1.DataSource = authorizedReviews
        GridView1.DataBind()
    End Using
End Sub
```

### C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    using (PlanetWroxEntities myEntities = new PlanetWroxEntities())
    {
        var authorizedReviews = from review in myEntities.Reviews
                                where review.Authorized == true
                                orderby review.CreatedDateTime descending
                                select review;
        GridView1.DataSource = authorizedReviews;
        GridView1.DataBind();
    }
}
```

请注意，当你输入 PlanetWroxEntities 时，会立刻出现错误，因为它定义在某个不在作用域内的命名空间中。你可以通过两种方式解决此问题。如果使用 VB.NET，可以在代码文件顶部输入 `Imports PlanetWroxModel`；如果使用 C#，则输入 `using PlanetWroxModel;`。或者，你可以单击一次 PlanetWroxEntities 一词，然后按 Ctrl+.（Ctrl+点）调出一个对话框，让你选择解决问题的修复方式，如图 14-3 所示（针对 C# 语言）。选择第一项，VS 会为你添加必要的 Imports/using 语句。在 C# 中，你也可以右键单击 PlanetWroxEntities 一词，然后点击“解析”菜单，调出类似的菜单。

![](img/eadab2ccd79b253c01a3fdff2321202d_548_0.png)

图 14-3

11. 保存所有更改，然后按 Ctrl+F5 打开页面。你会看到一屏从数据库的 Review 表中检索出的评论，如图 14-4 所示。

由于数据在 GridView 中的呈现方式，页面看起来相当杂乱，但在后面的练习中你会看到如何改进网格和数据的布局。

![](img/eadab2ccd79b253c01a3fdff2321202d_549_0.png)

图 14-4

## 工作原理

EF 附带了一个对象关系设计器（可在 VS 中访问），使你能够基于数据库中的表创建一个可通过代码访问的对象模型。通过向此设计器添加表，VS 会为你生成代码，使你无需编写大量代码即可访问数据库中的底层数据。添加到设计器中的类存储在 .edmx 文件及其代码隐藏文件中。设计器文件（PlanetWrox.edmx 文件的代码隐藏）包含一个继承自 ObjectContext 的类，ObjectContext 是 EF 中提供对数据库访问的主要对象。在上一个练习中，该类名为 PlanetWroxEntities（以 .edmx 文件命名），你使用它来访问添加到关系图中的表中的数据。虽然通常不需要查看生成的代码，但你可以打开 PlanetWrox.designer.vb 或 PlanetWrox.designer.cs 文件，查看为你生成了哪些代码。你删除的 *.tt 文件使你能够自定义基于底层数据模型生成的代码。然而，在大多数情况下，你不需要这样做，而是可以依赖默认的代码生成。这就是为什么你删除了这些文件，并将 EF 模型配置为使用其默认代码生成策略。

设计器足够智能，能够检测数据库中的关系，因此也能够在代码中创建必要的关系，正如你在图 14-2 中看到的。该模型定义了两个主要的对象类型：Review 和 Genre，两者也分别有名为 Reviews 和 Genres 的集合对应项。这些集合被称为实体集。请注意，在英文版 VS 上，设计器已正确地将 Review 和 Genre 表的名称复数化（分别为 Reviews 和 Genres），从而更容易看出哪个是集合（Reviews），哪个是单个对象实例（Review）。对于其他语言版本的 VS，你需要使用实体设计器自己应用此逻辑。

模型生成后，你可以对其执行 LINQ 查询，以从底层数据库中获取数据。要访问数据，你需要一个 ObjectContext 类的实例，该实例在代码的 Using 块中创建。Using 块（C# 中为 using）用于包装创建必须在用完时立即释放（从内存中清除）的变量的代码。由于 myEntities 变量持有与 SQL Server 数据库的（稀缺）连接，因此最好将使用它的代码包装在 Using 块中，以便在块结束时销毁该对象并释放连接。然后，这个 myEntities 对象会公开你的数据（如评论和流派），你可以在查询中使用这些数据：

### VB.NET

```vbnet
Using myEntities As New PlanetWroxEntities()
    Dim authorizedReviews = From review In myEntities.Reviews
        Where review.Authorized = True
        Order By review.CreateDateTime Descending
        Select review
    ...
End Using
```

### C#

```csharp
using (PlanetWroxEntities myEntities = new PlanetWroxEntities())
{
    var authorizedReviews = from review in myEntities.Reviews
        where review.Authorized == true
        orderby review.CreatedDateTime descending
        select review;
    ...
}
```

请注意，此查询看起来与你在之前章节中学到的 SQL 类似。在底层，运行时将此 LINQ 查询转换为其对应的 SQL，并针对底层数据库执行。在此查询中，From 子句中的变量 review 用于引用查询其他部分（Where、Order By 和 Select）中的 review，使你能够指定选择、筛选和排序条件。

需要认识到的重要一点是，EF 使用一种称为“延迟加载”的机制，这意味着子对象在你显式要求加载之前不会被加载。这意味着在上一个示例中，你查询的 Review 对象的 Genre 属性在 C# 中为 null，在 VB.NET 中为 Nothing，并且不包含任何数据。一旦你的代码尝试访问它们，就会通过向数据库执行另一个查询来加载它们。如果你不需要这些子对象，这可以极大地提高性能。但是，如果你事先确定在代码中需要它们，则为每个项执行单独的 SQL 语句会导致大量开销。在这种情况下，你可以在初始查询中预加载这些对象。要表示你希望同时包含这些对象，请对要查询的类型使用 Include 方法：

### VB.NET

```vbnet
Dim authorizedReviews = From review In myEntities.Reviews.Include("Genre")
    Where review.Authorized = True
    ...
```

### C#

```csharp
var authorizedReviews = from review in myEntities.Reviews.Include("Genre")
    where review.Authorized == true
    ...
```

通过对查询进行此添加，Review 对象的 Genre 属性现在已正确填充数据。虽然这乍看起来可能有点反直觉且适得其反，但实际上它是相当……

