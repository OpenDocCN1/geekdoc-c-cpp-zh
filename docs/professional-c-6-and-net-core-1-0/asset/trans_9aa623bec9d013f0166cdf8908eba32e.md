

对于扩展方法，同样是针对分组子句解析为 `GroupBy` 方法。`GroupBy` 方法的一个有趣之处在于，它返回一个实现了 `IGrouping` 接口的对象枚举。`IGrouping` 接口定义了 `Key` 属性，因此你可以在调用此方法后访问分组的键：

```
public static IEnumerable<IGrouping<TKey, TSource>>
GroupBy<TSource, TKey>(
this IEnumerable<TSource> source, Func<TSource, TKey> keySelector);
```

`group r.Country into g` 子句被解析为 `GroupBy(r => r.Country)` 并返回分组序列。该分组序列首先通过 `OrderByDescending` 方法排序，然后通过 `ThenBy` 方法排序。接下来，调用你已经熟悉的 `Where` 和 `Select` 方法：

```
var countries = Formula1.GetChampions()
.GroupBy(r => r.Country)
.OrderByDescending(g => g.Count())
.ThenBy(g => g.Key)
.Where(g => g.Count() >= 2)
.Select(g => new { Country = g.Key,
Count = g.Count() });
```

## LINQ 查询中的变量

对于用于分组的 LINQ 查询，`Count` 方法被多次调用。你可以通过使用 `let` 子句来改变这一点。`let` 允许在 LINQ 查询中定义变量：

```
var countries = from r in Formula1.GetChampions()
group r by r.Country into g
let count = g.Count()
orderby count descending, g.Key
where count >= 2
select new
{
Country = g.Key,
Count = count
};
```

使用方法语法时，`Count` 方法同样被多次调用。为了定义要传递给下一个方法的额外数据（这正是 `let` 子句所做的事情），你可以使用 `Select` 方法来创建匿名类型。这里创建了一个带有 `Group` 和 `Count` 属性的匿名类型。具有这些属性的项目集合被传递给 `OrderByDescending` 方法，排序基于此匿名类型的 `Count` 属性：

```
var countries = Formula1.GetChampions()
.GroupBy(r => r.Country)
.Select(g => new { Group = g, Count = g.Count() })
.OrderByDescending(g => g.Count)
.ThenBy(g => g.Group.Key)
.Where(g => g.Count >= 2);
```

## 品味问题：

```
var racersAndTeams =
    (from r in
        from r1 in Formula1.GetChampions()
        from yr in r1.Years
        select new
        {
            Year = yr,
            Name = r1.FirstName + " " + r1.LastName
        }
        join t in
        from t1 in Formula1.GetConstructorChampions()
        from yt in t1.Years
        select new
        {
            Year = yt,
            Name = t1.Name
        }
        on r.Year equals t.Year
        orderby t.Year
        select new
        {
            Year = r.Year,
            Racer = r.Name,
            Team = t.Name
        }).Take(10);
```

输出显示了在同时举办车手和车队锦标赛的前 10 年中，来自匿名类型的数据：

| 年份 | 世界冠军 | 车队冠军 |
| --- | --- | --- |
| 1958 | Mike Hawthorn | Vanwall |
| 1959 | Jack Brabham | Cooper |
| 1960 | Jack Brabham | Cooper |
| 1961 | Phil Hill | Ferrari |
| 1962 | Graham Hill | BRM |
| 1963 | Jim Clark | Lotus |
| 1964 | John Surtees | Ferrari |
| 1965 | Jim Clark | Lotus |
| 1966 | Jack Brabham | Brabham |
| 1967 | Denny Hulme | Brabham |

## 左外连接

上一个连接示例的输出从 1958 年开始——这是车手和车队锦标赛同时开始的第一年。车手锦标赛更早开始，在 1950 年。使用内连接，只有在找到匹配记录时才会返回结果。要获得包含所有年份的结果，你可以使用左外连接。左外连接返回左侧序列中的所有元素，即使在右侧序列中未找到匹配项也是如此。

前面的 LINQ 查询被更改为左外连接。左外连接通过 `join` 子句结合 `DefaultIfEmpty` 方法定义。如果查询的左侧（车手）没有匹配的车队冠军，则右侧的默认值由 `DefaultIfEmpty` 方法定义（代码文件 EnumerableSample/Program.cs）：

```
var racersAndTeams =
    (from r in racers
    join t in teams on r.Year equals t.Year into rt
    from t in rt.DefaultIfEmpty()
    orderby r.Year
    select new
    {
        Year = r.Year,
        Champion = r.Name,
        Constructor = t == null ? "no constructor championship" :
                t.Name
    }).Take(10);
```

使用此查询运行应用程序，输出从 1950 年开始，如下所示：

| 年份 | 冠军 | 车队冠军 |
| --- | --- | --- |
| 1950 | Nino Farina | 无车队锦标赛 |
| 1951 | Juan Manuel Fangio | 无车队锦标赛 |
| 1952 | Alberto Ascari | 无车队锦标赛 |
| 1953 | Alberto Ascari | 无车队锦标赛 |
| 1954 | Juan Manuel Fangio | 无车队锦标赛 |
| 1955 | Juan Manuel Fangio | 无车队锦标赛 |
| 1956 | Juan Manuel Fangio | 无车队锦标赛 |
| 1957 | Juan Manuel Fangio | 无车队锦标赛 |
| 1958 | Mike Hawthorn | Vanwall |
| 1959 | Jack Brabham | Cooper |

## 分组连接

左外连接使用了分组连接以及 `into` 子句。它部分使用了与分组连接相同的语法。分组连接只是不需要 `DefaultIfEmpty` 方法。

使用分组连接，可以将两个独立的序列连接起来，其中一个序列包含另一个序列中某个元素的列表项。

以下示例使用两个独立的序列。一个是你从前面的示例中已经知道的冠军列表。第二个序列是 `Championship` 类型的集合。`Championship` 类型在下一个代码片段中显示。该类包含锦标赛年份以及该年获得第一、第二和第三名的车手，属性为 `Year`、`First`、`Second` 和 `Third`（代码文件 DataLib/Championship.cs）：

```
public class Championship
{
    public int Year { get; set; }
    public string First { get; set; }
    public string Second { get; set; }
    public string Third { get; set; }
}
```

锦标赛集合从 `GetChampionships` 方法返回，如下面的代码片段所示（代码文件 DataLib/Formula1.cs）：

```
private static List<Championship> championships;
public static IEnumerable<Championship> GetChampionships()
{
    if (championships == null)
    {
        championships = new List<Championship>();
        championships.Add(new Championship
        {
            Year = 1950,
            First = "Nino Farina",
            Second = "Juan Manuel Fangio",
            Third = "Luigi Fagioli"
        });
        championships.Add(new Championship
        {
            Year = 1951,
            First = "Juan Manuel Fangio",
            Second = "Alberto Ascari",
            Third = "Froilan Gonzalez"
        });
        // …
```

冠军列表应当与每年锦标赛前三名中的车手列表相结合，并显示每一年的结果。

应显示的信息由 `RacerInfo` 类定义，如下所示（代码文件 `EnumerableSample/RacerInfo.cs`）：

```
public class RacerInfo
{
    public int Year { get; set; }
    public int Position { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```

使用 join 语句可以将两个列表中的车手组合起来。

因为在锦标赛列表中每个项目包含三名车手，所以需要首先展平此列表。一种方法是使用 `SelectMany` 方法。`SelectMany` 使用一个 lambda 表达式，该表达式为列表中的每个项目返回一个包含三个项目的列表。在 lambda 表达式的实现中，由于 `RacerInfo` 包含 `FirstName` 和 `LastName` 属性，而接收到的集合仅包含带有 `First`、`Second` 和 `Third` 属性的名称，因此需要拆分字符串。你可以借助扩展方法 `FirstName` 和 `LastName` 来完成此操作（代码文件 `EnumerableSample/Program.cs`）：

```
var racers = Formula1.GetChampionships()
    .SelectMany(cs => new List<RacerInfo>()
    {
        new RacerInfo {
            Year = cs.Year,
            Position = 1,
            FirstName = cs.First.FirstName(),
            LastName = cs.First.LastName()
        },
        new RacerInfo {
            Year = cs.Year,
            Position = 2,
            FirstName = cs.Second.FirstName(),
```

