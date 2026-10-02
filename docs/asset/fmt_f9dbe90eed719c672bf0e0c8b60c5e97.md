
# 第 10 章 查询 LINQ

当你点击“新建项”对话框中的 OK 按钮将文件添加到项目中的后，Visual Studio 会通知你它想要将 LINQ to SQL 文件添加到网站的 `App_Code` 目录中。由于该文件位于那里，由 LINQ to SQL 类创建的数据可以从网站的任何地方访问。

文件添加后，Visual Studio 会自动在 LINQ to SQL 设计器中打开它。这个简单的对象/关系映射（Object/Relation）设计器允许你添加、创建、删除和关联数据对象。当你修改设计器时，LINQ to SQL 会生成镜像这些每个对象结构的对象类。稍后，当你开始针对数据对象编写 LINQ 查询时，这些类允许 Visual Studio 为你提供设计时的 IntelliSense 支持、强类型检查和编译时类型检查。由于 O/R 映射器主要设计用于配合 LINQ to SQL 使用，因此创建 SQL 对象（如表、视图和存储过程）的 CLR 对象表示是非常简单的。

LINQ to SQL 的演示使用了本章之前章节中相同的示例电影数据。在本节中，数据存储在 SQL Express LocalDB 数据库中。

> 一个名为 `Movies.mdf` 的数据库副本包含在 Wix 网站（www.wix.com）的可下载代码中。

设计打开并准备就绪后，打开服务器管理器（Visual Server Explorer）工具，找到 `Movies` 数据库并展开数据库的“表”文件夹。从服务器管理器中将 `Movies` 表拖到设计面上。注意，一旦你将数据库表拖到设计面上，它就会被自动查询以识别其结构。设计器会创建一个实体类并将其显示在设计面上。

当你将对象拖到 LINQ to SQL 设计面上时，Visual Studio 会检查表名，并在必要时尝试对它生成的类名进行自动“单数化”（singularize）。这样做是为了帮助你更紧密地遵循 .NET 框架的类命名标准。例如，如果你从数据库将一个名为 `Products` 的表拖到设计面上，它会自动选择单数名称 `Product` 作为生成的类的名称。

遗憾的是，尽管设计器在确定类名的正确单数版本方面做得良好，但并非 100% 准确。这一点——看当你把 `Movies` 拖到设计面上时，它是如何错误地将其单数化为 `Movie` 的。坦率地说，设计器也允许你在设计面上更改实体的名称。你可以通过选择设计面上的实体并点击实体的名称来实现。

当你添加了 `Movie` 实体后，将 `Genres` 表拖到设计面上。再次，Visual Studio 为此表创建了类表示（注意它给出了单数名称 `Genre`）。此外，它还检测到 `Movie` 和 `Genre` 之间存在的外键关系。由于检测到了这一点，两个表之间添加了一条虚线。箭头表示了两个表之间存在的外键关系的方向。图 10-10 显示了带有 `Movies` 和 `Genres` 表的 LINQ to SQL 设计表面。

![](img/67a6707ff505c052edb96c0128fb3096_444_0.png)

图 10-10

## 访问和查询数据

现在你已经好了 LINQ to SQL 文件，访问其数据上下文并查询其数据非常简单。

## 访问数据

首先，在要访问数据的 Web 表中创建数据上下文的实例，如代码段 10-24 所示。

代码段 10-24：创建新的数据上下文

### VB

```vb
<%@ Page Language="VB" %>

<script runat="server">
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim dc As New MoviesDataContext()
End Sub
</script>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>My Favorite Movies</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:GridView ID="GridView1" runat="server">
            </asp:GridView>
        </div>
    </form>
</body>
</html>
```

### C#

```csharp
<script runat="server">
protected void Page_Load(object sender, EventArgs e) {
    MoviesDataContext dc = new MoviesDataContext();
}
</script>
```

在这种情况下，你创建了一个 `MoviesDataContext` 实例，这是你之前添加的 LINQ to SQL 文件生成的数据类的名称。

> 注意：由于数据类上下文是由 LINQ to SQL 文件自动生成的，因此每当你创建一个新的 LINQ to SQL 文件时，它的名称都会发生变化。此类的名称通过在你的 LINQ to SQL 类文件名后附加 `DataContext:` 后缀来确定的，因此，如果你将 LINQ to SQL 文件命名为 `AdventureWorksdbml`，那么数据类上下文将是 `AdventureWorksDataContext`。

## 编写 LINQ 查询

将数据上下文添加到页面后，你就可以开始针对它编写 LINQ 查询了。如之前所述，LINQ to SQL 生成的对象类镜像了数据库表的结构，但 IntelliSense 将会支持你的 LINQ 查询。代码段 10-25 显示了之前章节中过的相同基本电影查询。

代码段 10-25：从 LINQ to SQL 查询电影数据

### VB

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim dc As New MoviesDataContext()

    Dim query = From m in dc.Movies
    Select m

    Me.GridView.DataSource = query
    Me.GridView.DataBind()
End Sub
```

### C#

```csharp
protected void Page_Load(object sender, EventArgs e) {
    MoviesDataContext dc = new MoviesDataContext();

    var query = from m in dc.Movies
    select m;

    this.GridView1.DataSource = query;
    this.GridView1.DataBind();
}
```

如图 10-11 所示，运行代码会在数据库中生成原始电影列表。

![](img/67a6707ff505c052edb96c0128fb3096_446_0.png)

图 10-11

注意你不需要编写创建这些所需的代码。LINQ 已经处理了这些，甚至通过编写 LINQ 语法生成了 SQL。你可以通过 Visual Studio 输出窗口查看查询生成的 SQL，如代码段 10-26 所示。

正如你所看到的，生成的 SQL 是标准 SQL， LINQ 在优化它生成的查询方面非常出色，对于代码段 10-27 所示的更复杂的查询。

代码段 10-27：分组 LINQ to SQL 数据

### VB

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim dc As New MoviesDataContext()

    Dim query = From m in dc.Movies
    Group By m.Genre g = Group, Count()

    System.Diagnostics.Debug.WriteLine(query)

    Me.GridView.DataSource = query
    Me.GridView.DataBind()
End Sub
```

### C#

```csharp
protected void Page_Load(object sender, EventArgs e) {
    MoviesDataContext dc = new MoviesDataContext();

    var query = from m in dc.Movies
    group by m.Genre g
    select new { Genre = g.Key, Count = g.Count() };

    System.Diagnostics.Debug.WriteLine(query);

    this.GridView1.DataSource = query;
    this.GridView1.DataBind();
}
```

![](img/67a6707ff505c052edb96c0128fb3096_447_0.png)

图 10-12

图 10-13 显示了此查询生成的 SQL。

![](img/67a70ff505c05edb96c012fb3096_448_0.png)

图 10-13

注意 SQL 生成的 SQL 适用于你正在使用的 SQL Server 版本。LINQ 还包含一个通过设置数据上下文属性来启用日志的功能。

## 使用其他 SQL 查询方法

尽管 LINQ to SQL 能够出色地生成 SQL 查询，但有时使用其他 SQL 查询方法更好，例如存储过程或视图。

## 使用 SQL 视图

要在 LINQ to SQL 中使用视图，请将视图拖到 LINQ to SQL 设计面上，就像你操作标准表一样。视图显示在设计面上，你可以像之前操作表一样对其执行查询，如代码 10-28 所示。

代码 10-28：使用视图查询 LINQ to SQL 数据

### VB

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim dc As New MoviesDataContext()

    Dim query = From dc.AllMovies
    Select m

    System.Diagnostics.Debug.WriteLine(query)

    Me.GridView.DataSource = query
    Me.GridView.DataBind()
End Sub
```

### C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    MoviesDataContext dc = new MoviesDataContext();

    var query = from m in dc.AllMovies
        select m;

    System.Diagnostics.Debug.WriteLine(query);

    this.GridView.DataSource = query;
    this.GridView.DataBind();
}
```

## 使用 LINQ 查询存储过程

与表或视图不同（LINQ to SQL 将它们暴露为属性），存储过程需要参数。因此，LINQ to SQL 将它们暴露为方法调用，允许你提供值，这些值会被 LINQ 转换为存储过程参数。代码 10-29 显示了一个你可以用于从数据库检索特定类型的存储过程。

代码 10-29：简单存储过程

```sql
CREATE PROCEDURE dbo.GetGenre
(
  @id int
)
AS
 SELECT * From Genre WHERE ID = @id
```

你可以通过从服务器管理器拖到 LINQ to SQL 设计面上，将存储过程添加到 LINQ to SQL 设计器中，就像你之前操作表一样。如果你期望存储过程返回数据库表的数据集合，你应该将存储过程拖到代表查询返回类型的 LINQ 类上。代码 10-27 中的存储过程将返回匹配 ID 的所有记录。因此，将 `GetGenre` 拖到 Visual Studio 设计器中的 `Genre` 表会让设计器生成一个返回通用 `Genre` 对象集合的方法。

![](img/67a70ff505c05edb96c012fb3096_449_0.png)

图 10-14

添加存储过程后，你可以像之前访问表和视图一样通过数据上下文访问它们。然而，LINQ to SQL 将它们暴露为方法调用。因此，你可能需要提供参数，如代码 10-30 所示。

代码 10-30：从存储过程选择数据

### VB

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim dc As New MoviesDataContext()

    Me.GridView.DataSource = dc.GetGenre(1)
    Me.GridView.DataBind()
End Sub
```

### C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    MoviesDataContext dc = new MoviesDataContext();

    this.GridView.DataSource = dc.GetGenre(1);
    this.GridView.DataBind();
}
```

## 通过 LINQ 插入、更新和删除

你不仅可以使用 LINQ 创建从源选择数据的强大查询，还可以用它进行插入、更新或删除。使用 LINQ 插入数据只需创建对象的新实例、将其添加到集合并调用 `SubmitChanges`。LINQ 提供了两个方法——`InsertSubmit` 和 `InsertAllSubmit`——`InsertSubmit` 接受单个实体，而 `InsertAllSubmit` 接受集合。当你运行代码 10-31 时，LINQ 将通过调用 `SubmitChanges` 生成 SQL 语句以持久化更改。

代码 10-31：使用 LINQ 插入数据

### VB

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim dc As New MoviesDataContext()

    Dim m As New Movie {.Title = "The Princess", Director = "Reiner", Genre = 0, ReleaseDate = DateTime.Parse("9/25/1987"), Runtime = 98}

    dc.InsertSubmit(m)
    dc.SubmitChanges()
End Sub
```

### C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    MoviesDataContext dc = new MoviesDataContext();

    Movie m = new Movie { Title = "The Princess", Director = "Reiner", Genre = 0, ReleaseDate = DateTime.Parse("9/25/1987"), Runtime = 98 };

    dc.InsertSubmit(m);
    dc.SubmitChanges();
}
```

## 使用存储过程插入数据

当然，你可能已经写了一个复杂的存储过程来处理对数据库表的简单插入。要执行此操作，在 LINQ to SQL 设计面上，选择你想要插入数据的实体，在本例中是 `Movies` 实体。选择实体后，打开其属性窗口并找到 `Default Methods` 部分，如图 10-15 所示。

`Default Methods` 部分包含三个属性——`Delete`、`Insert` 和 `Update`，它们定义了 LINQ 在 `Movies` 表上执行这些操作时应使用的行为。默认情况下，每个属性都设置为 `UseRuntime` 值，这告诉 LINQ 动态生成 SQL。因为你想使用存储过程向表插入数据，请打开 `Insert` 属性的 `Configure Behavior` 对话框。

在对话框中，将 `Behavior` 选择从 `Runtime` 更改为 `Customize`。接下来，从单选按钮下方的列表中选择存储过程。当你选择存储过程时，LINQ 会尝试匹配表列和存储过程的输入参数。但是，如果需要，你可以手动更改这些内容。

最后的 `Configure Behavior` 对话框如图 10-16 所示。

现在，当你运行代码 10-31 时，LINQ 将使用你配置的存储过程而不是动态生成 SQL 语句。
