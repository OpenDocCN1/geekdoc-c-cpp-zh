
`new Movie ( Title="The Haunted", Director="Robert Mandel", Genre=1, ReleaseDate=DateTime.Parse("5/6/1991"), RunTime=100 )`

`new Movie ( Title="The Pledge", Director="Todd Phillips", Genre=0, ReleaseDate=DateTime.Parse("2/21/2003"), RunTime=91 )`

`new Movie ( Title="Anchorman: The Legend of Ron Burgundy", Director="Adam Mackay", ReleaseDate=DateTime.Parse("7/9/2004"), RunTime=94 )`

`new Movie ( Title="Baseball", Director="Tom Shadyac", Genre=1, ReleaseDate=DateTime.Parse("5/23/2003"), RunTime=101 )`

`new Movie ( Title="Ace Ventura: Pet Detective", Director="Tom Shadyac", Genre=0, ReleaseDate=DateTime.Parse("2/4/1994"), RunTime=86 )`

`new Movie ( Title="Goonies", Director="Richard Donner", Genre=0, ReleaseDate=DateTime.Parse("6/7/1985"), RunTime=114 )`

`new Movie ( Title="Six Candles", Director="John Hughes", Genre=1, ReleaseDate=DateTime.Parse("5/4/1984"), RunTime=93 )`

`new Movie ( Title="The Breakfast Club", Director="John Hughes", Genre=1, ReleaseDate=DateTime.Parse("2/15/1985"), RunTime=97 )`

`new Movie ( Title="Pretty in Pink", Director="Howard Deant", Genre=1, ReleaseDate=DateTime.Parse("2/28/1986"), RunTime=96 )`

`new Movie ( Title="Weird Science", Director="John Hughes", Genre=0, ReleaseDate=DateTime.Parse("8/2/1985"), RunTime=94 )`

`new Movie ( Title="Breakfast at Tiffany's", Director="Blake Edwards", Genre=1, ReleaseDate=DateTime.Parse("10/5/1961"), RunTime=105 )`

`new Movie ( Title="The Ghost", Director="Mike Nicholson", Genre=1, ReleaseDate=DateTime.Parse("4/2/1968"), RunTime=105 )`

`new Movie ( Title="Dazed and Confused", Director="Richard Linklater", Genre=0, ReleaseDate=DateTime.Parse("9/24/1993"), RunTime=103 )`

`new Movie ( Title="Arthur", Director="Steve Gordon", Genre=1, ReleaseDate=DateTime.Parse("9/25/1981"), RunTime=97 )`

`new Movie ( Title="Python and the Holy Grail", Director="Terry Gilliam", Genre=0, ReleaseDate=DateTime.Parse("5/10/1975"), RunTime=91 )`

`new Movie ( Title="Dirty Harry", Director="Don Siegel", Genre=2, ReleaseDate=DateTime.Parse("12/23/1971"), RunTime=102 )`

```
</script>
```

运行示例将生成一个典型的 ASP.NET Web 页面，其中包含一个显示所有 `Movie` 数据的小型网格。

现在，当你想要对电影列表开始查询时会发生什么呢？例如，你可能想过滤这些数据以只显示特定类型的电影。列表 9-3 显示了你可能执行此类过滤的一种方法。

### 列表 9-3：过滤 Movie 对象列表

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim movies = GetMovies()
    Dim query As New List(Of Movie)
    For Each m In movies
        If (m.Genre = 0) Then
            query.Add(m)
        End If
    Next
    Me.GridView.DataSource = query
    Me.GridView.DataBind()
End
```

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    var movies = GetMovies();
    var query = new List<Movie>();
    foreach (var m in movies)
    {
        if (m.Genre == 0) query.Add(m);
    }
    this.GridView.DataSource = query;
    this.GridView.DataBind();
}
```

如所示，要过滤数据使网格仅显示特定类型的 `Movies`，只需要创建一个新的临时集合，并使用 `foreach` 循环来遍历数据。

虽然这种技术看起来足够简单，但它仍然要求你定义想要查找的内容（该类型中的所有电影），并且还要显式地定义应该如何执行（使用临时集合和 `foreach` 循环）。此外，当你需要执行涉及分组或排序的更复杂的查询时会发生什么？现在代码的复杂度急剧增加，如列表 9-4 所示：对 `Movie` 对象进行分组和排序

```vb
Public Class Grouping
    Private _genre As Integer
    Private _movieCount As Integer
    Public Property Genre As Integer
        Get
            Return _genre
        End Get
        Set
            _genre = value
        End Property
    Public Property MovieCount As Integer
        Get
            Return _movieCount
        End Get
        Set
            _movieCount = value
        End Property
End Class
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim movies = GetMovies()
    Dim groups As New Dictionary(Of Integer, Grouping)
    For Each m In movies
        If Not groups.ContainsKey(m.Genre) Then
            groups.Add(m.Genre, New Grouping With {.genre = m.Genre, .movieCount = 0})
        End If
        groups(m.Genre).movieCount += 1
    Next
    Dim results = New List(Of Grouping)(groups.Values)
    results.Sort(Function(x, y)
        If x.MovieCount > y.MovieCount Then
            Return -1
        ElseIf x.MovieCount < y.MovieCount Then
            Return 1
        Else
            Return 0
        End If
    End)
    Me.GridView.DataSource = results
    Me.GridView.DataBind()
End
```

```csharp
public class Grouping
{
    private int _genre;
    private int _movieCount;
    public int Genre { get => _genre; set => _genre = value; }
    public int MovieCount { get => _movieCount; set => _movieCount = value; }
}
protected void Page_Load(object sender, EventArgs e)
{
    var movies = GetMovies();
    var groups = new Dictionary<int, Grouping>();
    foreach (var m in movies)
    {
        if (!groups.ContainsKey(m.Genre))
        {
            groups.Add(m.Genre, new Grouping { Genre = m.Genre, MovieCount = 0 });
        }
        groups[m.Genre].MovieCount++;
    }
    var results = new List<Grouping>(groups.Values);
    results.Sort((x, y) =>
    {
        if (x.MovieCount > y.MovieCount)
            return -1;
        if (x.MovieCount < y.MovieCount)
            return 1;
        return 0;
    });
    this.GridView.DataSource = results;
    this.GridView.DataBind();
}
```

LINQ 的创建是为了解决在前节中讨论的查询数据集合的许多缺点。LINQ 不再要求你指定具体如何查询，而是赋予了你从更抽象的级别进行查询的能力。只需定义你想要查询返回的内容，让 .NET 及其编译器来决定查询运行的具体细节。

## 第9 章：使用 LINQ 进行查询

### 基础 LINQ 查询与投影

为了将之前的章节示例修改为使用 LINQ 查询，你首先需要向 Web 页面添加 LINQ 命名空间，如列表 9-5 所示。

#### 列表 9-5：添加 LINQ 命名空间

```
<% Import Namespace="System.Linq" %>
```

添加此命名空间后，页面就可以访问所有的基础 LINQ 功能。如果你使用的是代码后（code-behind）开发模型，那么 LINQ 命名空间应该已经包含在你的代码后类中了。

> 注意，Visual Basic 站点附带的默认 `web.config` 文件已经包含了 `System.Linq` 命名空间声明，如果你使用的是这种类型的项目，则不需要手动添加该命名空间。

接下来，你可以尝试修改列表 9-2 中的代码。如果你还记得，这个基础示例只是生成了一个电影的泛型列表（`List`），并将该列表绑定到 `GridView` 控件。列表 9-6 显示了如何使用 LINQ 修改代码来查询电影列表并将结果绑定到 `GridView`。

#### 列表 9-6：使用 LINQ 创建查询

```VB
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim movies = GetMovies()
    Dim query = From m in movies
            Select m
    Me.GridView1.DataSource = query
    Me.GridView1.DataBind()
```

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

如果我们解构这段代码示例，会发生三个基本操作。首先，代码使用 `GetMovies()` 方法获取泛型 `List<Movie>` 集合。

接下来，代码使用非常简单的 LINQ 查询从泛型 `movies` 集合中选择所有的 `Movie` 对象。注意，这个特定的 LINQ 查询在查询语句使用了如 `from` 和 `select` 这样的新语言关键字。这些语法扩展是 .NET 语言的一等成员，因此 Visual Studio 2008 可以为你提供开发辅助，例如强类型检查和 IntelliSense（智能提示），使你更容易发现并修复代码中的问题。

查询还定义了一个新变量 `m`。该变量在查询中有两种用法。首先，通过在 `from m` 语句中定义它，我们告诉 LINQ 让 `m` 代表集合中的单个项目，即一个 `Movie` 对象。告诉 LINQ 可以让它理解我们正在查询的对象结构，并且正如你稍后看到的，可以使用 IntelliSense 来帮助创建查询。

`m` 在 `select` 语句中的第二个用法。`select` 语句中的 `m` 告诉 LINQ 输出一个与 `m` 结构匹配的投影。在这种情况下意味着 LINQ 创建了一个匹配 `Movie` 对象结构的投影。

我们可以通过使用 `new` 关键字配合 `select` 操作符显式定义想要从查询返回的字段，从而轻松创建自己的自定义投影。这在下面的列表 9-7 中所示。

#### 列表 9-7：使用 LINQ 创建自定义投影

```VB
Protected Sub Page_Load(ByVal sender Object, ByVal e As System.EventArgs)
    Dim movies = GetMovies()
    Dim query = From m in movies
                Select New With (m.Title, m.Genre)
    Me.GridView.DataSource = query
    Me.GridView.DataBind()
End Sub
```

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    var movies = GetMovies();
    var query = from m in movies
                select new { m.Title, m.Genre };
    this.GridView.DataSource = query;
    this.GridView.DataBind();
}
```

注意，我们没有选择 `m`，而是定义了一个只包含 `Title` 和 `Genre` 值的的新投影。

你甚至可以显式定义结果集中对象将暴露的字段名。例如，你可能想显式地命名 `Title` 和 `Genre` 字段以完全描述它们的内容。使用 LINQ 很容易实现这一点，如列表 9-8 所示。

#### 列表 9-8：创建自定义投影字段名

```VB
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim movies = GetMovies()
    Dim query = From m in Movies
                Select New With (.MovieTitle = m.Title, .MovieGenre = m.Genre)
    Me.GridView.DataSource = query
    Me.GridView.DataBind()
End Sub
```

```csharp
```
