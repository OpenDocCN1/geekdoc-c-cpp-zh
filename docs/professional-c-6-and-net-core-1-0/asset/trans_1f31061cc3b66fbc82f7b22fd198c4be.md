
`LINQIntro/Program.cs`:

```csharp
static void ExtensionMethods()
{
    var champions = new List<Racer>(Formula1.GetChampions());
    IEnumerable<Racer> brazilChampions =
        champions.Where(r => r.Country == "Brazil").
            OrderByDescending(r => r.Wins).
            Select(r => r);

    foreach (Racer r in brazilChampions)
    {
        WriteLine($"{r:A}");
    }
}
```

## 延迟查询执行

在运行时，查询表达式不会在定义时立即执行。只有在迭代项时才会执行查询。

让我们再看一下扩展方法 `Where`。这个扩展方法使用 `yield return` 语句返回谓词为 `true` 的元素。由于使用了 `yield return` 语句，编译器会创建一个枚举器，并在从枚举中访问项时立即返回这些项：

```csharp
public static IEnumerable<T> Where<T>(this IEnumerable<T> source,
    Func<T, bool> predicate)
{
    foreach (T item in source)
    {
        if (predicate(item))
        {
            yield return item;
        }
    }
}
```

这会产生一个非常有趣且重要的效果。在下面的示例中，创建了一个字符串元素集合，并用名字填充。接下来，定义了一个查询，用于获取集合中首字母为 J 的所有名字。该集合还应进行排序。迭代不会在定义查询时发生，而是在使用 `foreach` 语句迭代所有项时发生。集合中只有一个元素以字母 J 开头，满足 `where` 表达式的要求：Juan。迭代完成并将 Juan 写入控制台后，向集合中添加了四个新名字。然后再次进行迭代：

```csharp
var names = new List<string>
{ "Nino", "Alberto", "Juan", "Mike", "Phil" };

var namesWithJ = from n in names
                 where n.StartsWith("J")
                 orderby n
                 select n;

WriteLine("First iteration");
foreach (string name in namesWithJ)
{
    WriteLine(name);
}
WriteLine();
names.Add("John");
names.Add("Jim");
names.Add("Jack");
names.Add("Denny");

WriteLine("Second iteration");
foreach (string name in namesWithJ)
{
    WriteLine(name);
}
```

由于迭代不会在定义查询时发生，而是在每次 `foreach` 时发生，因此可以看到变化，正如应用程序的输出所示：

```
First iteration
Juan

Second iteration
Jack
Jim
John
Juan
```

当然，你还必须意识到，扩展方法在每次迭代中使用查询时都会被调用。大多数时候这非常实用，因为你可以检测源数据中的变化。但有时这也可能不实用。你可以通过调用 `ToArray`、`ToList` 等扩展方法来改变这种行为。在下面的示例中，你可以看到 `ToList` 会立即遍历集合，并返回一个实现 `IList<string>` 的集合。返回的列表随后会被遍历两次；在两次遍历之间，数据源会获得新名字：

```csharp
var names = new List<string>
{ "Nino", "Alberto", "Juan", "Mike", "Phil" };
var namesWithJ = (from n in names
                  where n.StartsWith("J")
                  orderby n
                  select n).ToList();

WriteLine("First iteration");
foreach (string name in namesWithJ)
{
    WriteLine(name);
}
WriteLine();
names.Add("John");
names.Add("Jim");
names.Add("Jack");
names.Add("Denny");
WriteLine("Second iteration");
foreach (string name in namesWithJ)
{
    WriteLine(name);
}
```

| 运算符 | 描述 |
| --- | --- |
| `GroupBy`<br>`ToLookup` | `GroupBy` 运算符根据公共键对元素进行分组。`ToLookup` 通过创建一对多字典来对元素进行分组。 |
| `Any`<br>`All`<br>`Contains` | *量词运算符* 在序列的元素满足特定条件时返回布尔值。`Any`、`All` 和 `Contains` 都是量词运算符。`Any` 确定集合中是否存在满足谓词函数的元素；`All` 确定集合中是否所有元素都满足谓词。`Contains` 检查集合中是否存在特定元素。 |
| `Take`<br>`Skip`<br>`TakeWhile`<br>`SkipWhile` | *分区运算符* 返回集合的子集。`Take`、`Skip`、`TakeWhile` 和 `SkipWhile` 都是分区运算符。使用这些运算符可以得到部分结果。使用 `Take` 时，需要指定要从集合中获取的元素数量；`Skip` 会忽略指定数量的元素并获取其余元素。`TakeWhile` 在条件为 true 时获取元素。`SkipWhile` 在条件为 true 时跳过元素。 |
| `Distinct`<br>`Union`<br>`Intersect`<br>`Except`<br>`Zip` | *集合运算符* 返回一个集合。`Distinct` 从集合中移除重复项。除 `Distinct` 之外，其他集合运算符都需要两个集合。`Union` 返回两个集合中任一集合出现的唯一元素。`Intersect` 返回两个集合中都出现的元素。`Except` 返回仅在一个集合中出现的元素。`Zip` 将两个集合合并为一个。 |
| `First`<br>`FirstOrDefault`<br>`Last`<br>`LastOrDefault`<br>`ElementAt`<br>`ElementAtOrDefault`<br>`Single`<br>`SingleOrDefault` | *元素运算符* 只返回一个元素。`First` 返回满足条件的第一个元素。`FirstOrDefault` 与 `First` 类似，但如果找不到元素，则返回该类型的默认值。`Last` 返回满足条件的最后一个元素。通过 `ElementAt`，可以指定要返回的元素位置。`Single` 只返回满足条件的一个元素。如果满足条件的元素不止一个，则会抛出异常。所有 `XXOrDefault` 方法都与具有相同前缀的方法类似，但如果找不到元素，它们会返回该类型的默认值。 |
| `Count`<br>`Sum`<br>`Min`<br>`Max`<br>`Average`<br>`Aggregate` | *聚合运算符* 从集合中计算单个值。使用聚合运算符，可以获得所有值的总和、所有元素的数量、最低或最高值的元素、平均值等。 |
| `ToArray`<br>`AsEnumerable`<br>`ToList`<br>`ToDictionary`<br>`Cast<TResult>` | *转换运算符* 将集合转换为数组、`IEnumerable`、`IList`、`IDictionary` 等。`Cast` 方法将集合中的每一项强制转换为泛型参数类型。 |
| `Empty`<br>`Range`<br>`Repeat` | *生成运算符* 返回一个新序列。使用 `Empty` 运算符时集合为空；`Range` 返回数字序列；`Repeat` 返回包含一个重复值的集合。 |

以下各节提供了一些示例，演示如何使用这些运算符。

## 筛选

本节将介绍一些查询示例。

使用 `where` 子句，可以组合多个表达式——例如，仅获取来自巴西和奥地利且获胜超过 15 场比赛的车手。传递给 `where` 子句的表达式的返回类型只需为 `bool` 类型：

```csharp
var racers = from r in Formula1.GetChampions()
             where r.Wins > 15 &&
                 (r.Country == "Brazil" || r.Country == "Austria")
             select r;

foreach (var r in racers)
{
    WriteLine($"{r:A}");
}
```

使用此 LINQ 查询启动程序会返回 Niki Lauda、Nelson Piquet 和 Ayrton Senna，如下所示：

```
Niki Lauda, Austria, Starts: 173, Wins: 25
Nelson Piquet, Brazil, Starts: 204, Wins: 23
Ayrton Senna, Brazil, Starts: 161, Wins: 41
```

并非所有查询都可以使用 LINQ 查询语法完成，也并非所有扩展方法都映射到 LINQ 查询子句。高级查询需要使用扩展方法。为了更好地理解使用扩展方法的复杂查询，最好看看简单查询是如何映射的。使用扩展方法 `Where` 和 `Select` 生成的查询与之前的 LINQ 查询非常相似：

```csharp
var racers = Formula1.GetChampions().
    Where(r => r.Wins > 15 &&
        (r.Country == "Brazil" || r.Country == "Austria")).
    Select(r => r);
```

