
# 第 10 章 使用 LINQ 进行查询

## 传统查询的复杂性

```vb
Public Class Grouping
    Public Property Genre() As Integer
    Public Property MovieCount() As Integer
End Class

Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim movies = GetMovies()

    Dim groups = New Dictionary(Of String, Grouping)
    groups = New Dictionary(Of String, Grouping)

    For Each m in movies
        If (Not groups.ContainsKey(m.Genre)) Then
            groups(m.Genre) = New Grouping With (.Genre = m.Genre, .MovieCount = 0)
        End If
        groups(m.Genre).MovieCount = groups(m.Genre).MovieCount + 1
    Next

    Dim results = New List(Of Grouping)(groups.Values)
    results.Sort(AddressOf MovieSort)

    Me.GridView1.DataSource = results
    Me.GridView1.DataBind()
End Sub
```

```csharp
public class Grouping
{
    public int Genre { get; set; }
    public int MovieCount { get; set; }
}

protected void Page_Load(object sender, EventArgs e)
{
    var movies = GetMovies();

    Dictionary<int, Grouping> groups = new Dictionary<int, Grouping>();
    foreach (Movie m in movies)
    {
        if (!groups.ContainsKey(m.Genre))
        {
            groups[m.Genre] = new Grouping { Genre = m.Genre, MovieCount = 0 };
        }
        groups[m.Genre].MovieCount++;
    }

    List<Grouping> results = new List<Grouping>(groups.Values);
    results.Sort(delegate(Grouping x, Grouping y)
    {
        return x.MovieCount < y.MovieCount ? -1 :
               x.MovieCount > y.MovieCount ? 1 : 0;
    });
    this.GridView.DataSource = results;
    this.GridView.DataBind();
}
```

将数据移动到类型中并统计每个类型中的电影数量，需要添加新类、创建一个字典以及实现一个委托——对于一个看似简单的任务来说，这些都是相当复杂的要求。而且，你不仅要具体定义想要做什么，还要显式地定义应该如何做。

此外，当你需要执行涉及分组或排序的更复杂查询时，会发生什么？现在代码的复杂性剧增。

## 用 LINQ 替换传统查询

LINQ 是为了解决现有 .NET 功能的缺陷而创建的。在本节中，我们展示了如何使用 LINQ 查询集合。通过使用 LINQ，你可以简化代码并使其更具读性。LINQ 是一组功能，允许你使用统一的语法查询各种数据源。LINQ 的主要优势是它允许以更自然、表现力的方式处理对象。

## LINQ 查询和投影

### 列表 10-5：使用 LINQ 创建查询

#### VB

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim movies = GetMovies()

    Dim query = From m In movies
        Select m
    GridView1.DataSource = query
    GridView1.DataBind()
End Sub
```

#### C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    var movies = GetMovies();

    var query = from m in movies
                select m;

    this.GridView1.DataSource = query;
    this.GridView1.DataBind();
}
```

如果你构建代码示例，可以看到正在发生的三个操作。首先，代码使用 `GetMovies()` 方法获取泛集合。接下来，代码使用非常简单的 LINQ 查询从泛集合中选择所有 `Movie` 对象。注意此特定的 LINQ 查询在查询语句中使用了 `from` 和 `select` 等关键字。这些语法是 .NET 语言的基础成员；Visual Studio 可以为你提供开发辅助，例如强类型检查和 IntelliSense，这使得发现修复代码中的问题变得更容易。

查询还定义了一个新变量 `m`。该变量在查询中有两种用法。首先，通过在 `from` 语句中定义它，指示 LINQ 使用该变量表示单个集合项，在这种情况下这是一个 `Movie` 对象。告诉 LINQ 这使得它能够理解你正在查询的对象结构，并且正如我们稍后看到的，还能提供 IntelliSense 来帮助创建查询。

`m` 的第二个用法是在 `select` 语句中。在 `select` 语句中使用 `m` 通知 LINQ 输出一个与查询匹配的投影。投影是将对象转换为新形式的操作，这种形式通常只包含你目的所需的属性。在这种情况下，LINQ 创建了一个与 `Movie` 对象结构匹配的投影。

你完全可以通过在 `select` 操作符中使用 `new` 关键字显式定义你从查询返回的字段，来创建你自己的自定义投影，如列表 10-6 所示。

### 列表 10-6：使用 LINQ 创建自定义投影

#### VB

```vb
Dim query = From m In movies
    Select New {m.Title, m.Genre}

Me.GridView1.DataSource = query
Me.GridView1.DataBind()
End Sub
```

#### C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    var movies = GetMovies();
    var query = from m in movies
        select new { m.Title, m.Genre };
    this.GridView1.DataSource = query;
    this.GridView1.DataBind();
}
```

注意，在选择 `m` 之后，你定义了一个仅包含 `Title` 和 `Genre` 值的投影。

你甚至可以显式地定义结果数据集中对象将暴露的字段名。例如，你可能希望更显式地命名 `Title` 和 `Genre` 字段，以完全描述你的内容。使用 LINQ，这项命名任务非常简单，如列表 10-7 所示。

### 列表 10-7：创建投影字段名

#### VB

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim movies = GetMovies()

    Dim query = From m in movies
    Select New With {.MovieTitle = m.Title, .MovieGenre = m.Genre };

    Me.GridView1.DataSource = query
    Me.GridView1.DataBind()
End Sub
```

#### C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    var movies = GetMovies();
    var query = from m in movies
        select new { MovieTitle = m.Title, MovieGenre = m.Genre };
```

此示例显式定义了结果集将以 `MovieTitle` 和 `MovieGenre` 暴露的字段。你可以在图 10-1 中看到，由于此更改，`GridView` 中的列标题也随之更改以保持匹配。

![](img/67a6707ff505c052edb96c0128fb3096_428_0.png)

最后，代码将 `GridView` 绑定到 LINQ 查询返回的 `Movie` 对象可枚举列表。

如图 10-2 所示，运行列表 10-5 中的代码会与本章节早期列表 10-2 生成的相同的原生网页。

![](img/67a6707ff505c052edb96c0128fb3096_428_1.png)

LINQ 还允许你使用 `by` 语句对结果进行排序。与 SQL 一样，你可以选择按升序或降序排列结果，如列表 10-8 所示。

### 列表 10-8：使用 LINQ 控制数据排序

#### VB

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim moves = GetMovies()

    Dim query = From m in moves
    Order By m.Title Descending
    Select New With {.MovieTitle = m.Title, .MovieGenre = m.Genre}

    Me.GridView1.DataSource = query
    Me.GridView1.DataBind()
End Sub
```

#### C#

```csharp
void Page_Load(object sender, EventArgs e)
{
    var moves = GetMovies();

    var query = from m in moves
                orderby m.Title descending
                select new { Title = m.Title, MovieGenre = m.Genre };

    this.GridView1.DataSource = query;
    this.GridView1.DataBind();
}
```

LINQ 语法的另一个伟大特性是它极大地提高了代码的可读性和可理解性。LINQ 允许你表达查询的意图，告诉编译器你想让代码做什么，但将如何执行留给编译器来决定。

> 尽管这些关键字允许你使用简单且清晰的类 SQL 语法来构建 LINQ 查询，但请放心，并没有发生任何魔法。这些关键字实际上映射到 `movies` 集合上的扩展方法。你实际上可以直接使用这些扩展方法来编写 LINQ 查询，如下：

#### VB

```vb
Dim query = moves.Select(Function(m as Movie) m)
```

#### C#

```csharp
var query = moves.Select(m => m);
```

这是编译器在编译过程中将关键字语法翻译成的内容的形式。你可能会好奇 `Select` 方法是如何添加到泛型 `List<Movie>` 集合中的，因为如果你查看 `List<T>` 的对象结构，并没有 `Select` 方法。LINQ 使用扩展方法将 `Select` 方法以及它使用的许多其他方法添加到基础枚举类中。因此，任何实现 `IEnumerable` 的类都通过 LINQ 启用了这些方法。你可以在 Visual Studio 中右键点击 `Select` 方法并从上下文菜单中选择查看定义来查看 LINQ 添加的所有方法。这样做会导致 Visual Studio 显示 LINQ `Enumerable` 类的类元数据。如果你滚动此类，你不仅会看到 `Select`，还有如 `Where`、`Count`、`Min`、`Max` 以及其他 LINQ 自动添加到任何实现 `IEnumerable` 接口的对象上的方法。

## 使用自定义比较器排序结果

当你使用 `order by` 语句或 `OrderBy` 和 `OrderDescending` 扩展方法时，排序类型的默认比较器会在值之间进行比较。在某些情况下，你对结果的顺序需要比默认比较器提供的更多控制。在这种情况下，你可以创建一个自定义比较器并将其传递给 `OrderBy` 或 `OrderDescending` 扩展方法。如列表 10-9 所示，你可以创建一个自定义比较器来按名称进行排序。

### 列表 10-9：按名称排序的比较器

#### VB

```vb
Class LastNameComparator
    Implements IComparable(Of String)

    Function Compare(x As String, y As String) As Integer
        Dim director1 = x.Substring(" ")
        Dim director2 = y.Substring(" ")
        Return director1.CompareTo(director2)
    End Function
End Class
```

#### C#

```csharp
using System.Generic;

public class LastNameComparator : IComparer<string>
{
    public int Compare(string x, string y)
    {
        string director1 = x.Substring(" ");
        string director2 = y.Substring(" ");
        return director1.CompareTo(director2);
    }
}
```

### 列表 10-10：使用比较器排序

#### VB

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim movies = GetMovies()

    Dim query = From m in movies
    Order By m.Title Descending New LastNameComparator
    Select New With {.MovieTitle = m.Title, .MovieGenre = m.Genre}

    Me.GridView1.DataSource = query
    Me.GridView1.DataBind()
End Sub
```

#### C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    var movies = GetMovies();

    var query = from m in movies
                orderby m.Title descending new LastNameComparator()
                select new { Title = m.Title, MovieGenre = m.Genre };

    this.GridView1.DataSource = query;
    this.GridView1.DataBind();
}
```

最后，代码将 `GridView` 绑定到 LINQ 查询返回的 `Movie` 对象可枚举列表。

如图 10-3 所示，运行列表 10-5 中的代码会与本章节早期列表 10-2 生成的相同的原生网页。

![](img/67a6707ff505c052edb96c0128fb3096_431_0.png)

结果已添加到结果中，现在按导演姓氏降序排列。

| MovieDirector | MovieTitle | MovieGenre |
|---|---|---|
| Steven Spielberg | Ocean's Eleven | |
| Don Siegel | Dirty Hairy | |
| Tom Shadyac | Bruce Almighty | |
| Tom Shadyac | Ace Ventura: Pet Detective | |
| Tony Scott | Top Gun | |
