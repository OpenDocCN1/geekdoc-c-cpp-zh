
包含 this 关键字的 `Where()` 方法的返回类型为 `IEnumerable<T>`。这样，`Where()` 方法就可以用于所有实现了 `IEnumerable<T>` 的类型。实现了该接口的类型示例包括数组和 `List<T>`。第二个参数是 `Func<T, bool>` 委托，它引用一个返回布尔值且需要一个 `T` 类型参数的方法。在实现中会调用这个谓词，以检查 `IEnumerable<T>` 源中的项是否应进入目标集合。如果该方法被委托引用，`yield return` 语句就会将项从源返回到目标：

```csharp
public static IEnumerable<TSource> Where<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate)
{
    foreach (TSource item in source)
        if (predicate(item))
            yield return item;
}
```

由于 `Where()` 是作为泛型方法实现的，因此它适用于集合中包含的任何类型。任何实现了 `IEnumerable<T>` 的集合都受支持。

![](img/d7d2ffa0a76feaab821930e95daace93_334_0.png)

现在可以使用 `Enumerable` 类中的扩展方法 `Where()`、`OrderByDescending()` 和 `Select()` 了。由于这些方法都返回 `IEnumerable<TSource>`，因此可以一个接一个地调用方法，并使用前一个方法的结果。对于扩展方法的参数，可以使用为委托参数定义实现的匿名方法：

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
        Console.WriteLine("{0:A}", r);
    }
}
```

代码片段 LINQIntro/Program.cs

## 延迟查询执行

当在运行时定义查询表达式时，查询不会执行。查询会在迭代项时执行。

让我们再次看看扩展方法 `Where()`。该扩展方法使用 `yield return` 语句返回谓词为 true 的元素。由于使用了 `yield return` 语句，编译器会创建一个枚举器，并在从枚举中访问项时立即返回这些项：

```csharp
public static IEnumerable<T> Where<T>(this IEnumerable<T> source,
Func<T, bool> predicate)
{
```

```
where n.StartsWith("J")
orderby n
select n.ToList();

Console.WriteLine("First iteration");
foreach (string name in namesWithJ)
{
    Console.WriteLine(name);
}
Console.WriteLine();

names.Add("John");
names.Add("Jim");
names.Add("Jack");
names.Add("Denny");

Console.WriteLine("Second iteration");
foreach (string name in namesWithJ)
{
    Console.WriteLine(name);
}
```

在结果中，你可以看到，在两次迭代之间，尽管集合值已经改变，输出却保持不变：

```
First iteration
Juan

Second iteration
Juan
```

## 标准查询运算符

`Where`、`OrderByDescending` 和 `Select` 只是 LINQ 定义的查询运算符中的一小部分。LINQ 查询为最常见的运算符定义了一种声明式语法。`Enumerable` 类中还有很多其他查询运算符可用。

下表列出了 `Enumerable` 类定义的标准查询运算符：

| 标准查询运算符 | 说明 |
|---|---|
| Where OfType<TResult> | 筛选运算符定义了对返回元素的限制。使用 Where 查询运算符，可以使用谓词（例如，由返回 bool 的 Lambda 表达式定义）。OfType<TResult> 根据类型筛选元素，并且只返回 TResult 类型的元素。 |
| Select SelectMany | 投影运算符用于将一个对象转换为不同类型的新对象。Select 和 SelectMany 定义一个投影，基于选择器函数选择结果的值。 |
| OrderBy ThenBy OrderByDescending ThenByDescending Reverse | 排序运算符更改返回元素的顺序。OrderBy 按升序对值进行排序；OrderByDescending 按降序对值进行排序。如果第一次排序产生相似结果，ThenBy 和 ThenByDescending 运算符用于二次排序。Reverse 反转集合中的元素。 |
| Join GroupJoin | 联接运算符用于合并可能不直接相关的集合。使用 Join 运算符，可以基于键选择器函数联接两个集合。这类似于你在 SQL 中了解的 JOIN。GroupJoin 运算符联接两个集合并对结果进行分组。 |
| GroupBy ToLookup | 分组运算符将数据放入组中。GroupBy 运算符将具有共同键的元素分组。ToLookup 通过创建一对多字典来对元素分组。 |
| Any All Contains | 限定符运算符在序列中的元素满足特定条件时返回一个布尔值。Any、All 和 Contains 是限定符运算符。Any 确定集合中是否有任何元素满足谓词函数；All 确定集合中的所有元素是否都满足谓词。Contains 检查集合中是否包含特定元素。这些运算符返回一个布尔值。 |
| Take Skip TakeWhile SkipWhile | 分区运算符返回集合的一个子集。Take、Skip、TakeWhile 和 SkipWhile 是分区运算符。使用它们可以得到部分结果。使用 Take，你必须指定从集合中获取的元素个数；Skip 会忽略指定数量的元素并取其余元素。TakeWhile 只要条件为 true，就获取元素。 |
| Distinct Union Intersect Except Zip | 集运算符返回一个集合集。Distinct 从集合中移除重复项。除 Distinct 之外，其他集运算符需要两个集合。Union 返回出现在两个集合中任意一个的唯一元素。Intersect 返回同时出现在两个集合中的元素。Except 返回仅出现在一个集合中的元素。Zip 是 .NET 4 中的新运算符，它将两个集合合并为一个。 |
| First FirstOrDefault Last LastOrDefault ElementAt ElementAtOrDefault Single SingleOrDefault | 元素运算符只返回一个元素。First 返回满足条件的第一个元素。FirstOrDefault 与 First 类似，但如果未找到元素，则返回该类型的默认值。Last 返回满足条件的最后一个元素。使用 ElementAt，你可以指定要返回的元素的位置。Single 只返回满足条件的那一个元素。如果多于一个元素满足条件，则抛出异常。 |
| Count Sum Min Max Average Aggregate | 聚合运算符从集合中计算单个值。使用聚合运算符，你可以获得所有值的总和、所有元素的数量、具有最低或最高值的元素、平均值等等。 |
| ToArray AsEnumerable ToList ToDictionary Cast<TResult> | 转换运算符将集合转换为数组：IEnumerable、IList、IDictionary 等等。 |
| Empty Range Repeat | 生成运算符返回一个新序列。使用 Empty 运算符时集合为空；Range 返回数字序列；Repeat 返回包含一个重复值的集合。 |

以下各节是使用这些运算符的示例。

## 筛选

看一下查询的一些示例。

使用 where 子句，你可以组合多个表达式；例如，只获取来自巴西和奥地利且获胜超过 15 场的赛车手。传递给 where 子句的表达式的返回类型只需要是 bool 类型：

```csharp
var racers = from r in Formula1.GetChampions()
    where r.Wins > 15 &&
        (r.Country == "Brazil" || r.Country == "Austria")
    select r;

foreach (var r in racers)
{
    Console.WriteLine("{0:A}", r);
}
```

代码片段 Enumerablesample/Program.cs

使用此 LINQ 查询启动程序，将返回 Niki Lauda、Nelson Piquet 和 Ayrton Senna，如下所示：

```
Niki Lauda, Austria, Starts: 173, Wins: 25
Nelson Piquet, Brazil, Starts: 204, Wins: 23
Ayrton Senna, Brazil, Starts: 161, Wins: 41
```

并非所有查询都可以使用 LINQ 查询完成。并非所有扩展方法都映射到 LINQ 查询子句。高级查询需要使用扩展方法。为了更好地理解使用扩展方法的复杂查询，最好看看简单查询是如何映射的。使用扩展方法 `Where()` 和 `Select()` 生成的查询与之前完成的 LINQ 查询非常相似：

```csharp
var racers = Formula1.GetChampions().
    Where(r => r.Wins > 15 &&
        (r.Country == "Brazil" || r.Country == "Austria")).
    Select(r => r);
```

## 带索引的筛选

不能使用 LINQ 查询的一个示例是 `Where()` 方法的重载。通过 `Where()` 方法的重载，你可以传递第二个参数，即索引。索引是筛选返回的每个结果的一个计数器。你可以在表达式中使用索引，基于索引进行某些计算。这里，索引在 `Where()` 扩展方法调用的代码中使用，以便在索引为偶数时只返回姓氏以 A 开头的赛车手：

```csharp
var racers = Formula1.GetChampions().
    Where((r, index) => r.LastName.StartsWith("A") && index % 2 != 0);
foreach (var r in racers)
{
    Console.WriteLine("{0:A}", r);
}
```

所有姓氏以字母 A 开头的赛车手包括 Alberto Ascari、Mario Andretti 和 Fernando Alonso。由于 Mario Andretti 位于一个奇数索引处，因此他不在结果中：

```
Alberto Ascari, Italy; starts: 32, wins: 10
Fernando Alonso, Spain; starts: 132, wins: 21
```
