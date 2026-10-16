

Select(r => r);

## 使用索引进行筛选

一种无法使用 LINQ 查询的场景是 Where 方法的重载。使用 Where 方法的重载时，可以传递第二个参数，即索引。索引是过滤器返回的每个结果的计数器。可以在表达式中使用索引来基于索引执行某些计算。在下面的示例中，Where 扩展方法调用的代码中使用了索引，以返回仅当索引为偶数时姓氏以 A 开头的车手（代码文件 EnumerableSample/Program.cs）：

```
var racers = Formula1.GetChampions().
    Where((r, index) => r.LastName.StartsWith("A") && index % 2 == 0);
foreach (var r in racers)
{
    WriteLine($"{r:A}");
}
```

姓氏以字母 A 开头的车手是 Alberto Ascari、Mario Andretti 和 Fernando Alonso。由于 Mario Andretti 位于奇数索引中，因此他不在结果中：

```
Alberto Ascari, Italy; starts: 32, wins: 10
Fernando Alonso, Spain; starts: 252, wins: 32
```

## 类型筛选

对于基于类型的筛选，可以使用 OfType 扩展方法。这里数组 data 包含 string 和 int 对象。使用 OfType 扩展方法，将 string 类传递给泛型参数，只返回集合中的字符串（代码文件 EnumerableSample/Program.cs）：

```
object[] data = { "one", 2, 3, "four", "five", 6 };
var query = data.OfType<string>();
foreach (var s in query)
{
    WriteLine(s);
}
```

运行此代码，将显示字符串 one、four 和 five：

```
one
four
five
```

## 复合 from

如果需要基于对象本身就是一个序列的成员进行筛选，可以使用复合 from。Racer 类定义了 Cars 属性，其中 Cars 是一个字符串数组。对于筛选所有曾驾驶法拉利夺冠的车手，可以使用下面所示的 LINQ 查询。第一个 from 子句访问 Formula1.GetChampions 返回的 Racer 对象。第二个 from 子句访问 Racer 类的 Cars 属性，以返回所有类型为 string 的汽车。接下来使用 where 子句筛选仅驾驶法拉利夺冠的车手（代码文件 EnumerableSample/Program.cs）：

```
var ferrariDrivers = from r in Formula1.GetChampions()
    from c in r.Cars
    where c == "Ferrari"
    orderby r.LastName
    select r.FirstName + " " + r.LastName;
```

如果你好奇此查询的结果，以下是所有驾驶法拉利的 F1 冠军：

- Alberto Ascari
- Juan Manuel Fangio
- Mike Hawthorn
- Phil Hill
- Niki Lauda
- Kimi Räikkönen
- Jody Scheckter
- Michael Schumacher
- John Surtees

C# 编译器将 LINQ 查询中的复合 from 子句转换为 SelectMany 扩展方法。SelectMany 可用于迭代序列的序列。示例中使用的 SelectMany 方法的重载如下所示：

```
public static IEnumerable<TResult> SelectMany<TSource,
TCollection, TResult> (
    this IEnumerable<TSource> source,
    Func<TSource,
    IEnumerable<TCollection>> collectionSelector,
    Func<TSource, TCollection, TResult> resultSelector);
```

第一个参数是隐式参数，接收来自 GetChampions 方法的 Racer 对象序列。第二个参数是 collectionSelector 委托，在其中定义内部序列。使用 lambda 表达式 r => r.Cars，应返回汽车集合。第三个参数是一个委托，现在为每辆车调用，并接收 Racer 和 Car 对象。lambda 表达式创建了一个具有 Racer 和 Car 属性的匿名类型。由此 SelectMany 方法的结果是，车手和汽车的层次结构被展平，并返回每个汽车的匿名类型的新对象集合。

此新集合传递给 Where 方法，以便仅筛选驾驶法拉利的车手。最后调用 OrderBy 和 Select 方法：

```
var ferrariDrivers = Formula1.GetChampions()
    .SelectMany(r => r.Cars, (r, c) => new { Racer = r, Car = c })
    .Where(r => r.Car == "Ferrari")
    .OrderBy(r => r.Racer.LastName)
    .Select(r => r.Racer.FirstName + " " + r.Racer.LastName);
```

将泛型 SelectMany 方法解析为此处使用的类型，类型解析如下。在此情况下，source 的类型为 Racer，筛选后的集合为 string 数组，当然返回的匿名类型的名称未知，这里显示为 TResult：

```
public static IEnumerable<TResult> SelectMany<Racer, string, TResult> (
    this IEnumerable<Racer> source,
    Func<Racer, IEnumerable<string>> collectionSelector,
    Func<Racer, string, TResult> resultSelector);
```

由于查询只是从 LINQ 查询转换为扩展方法，结果与之前相同。

## 排序

为了对序列进行排序，已经使用了 orderby 子句。本节回顾了之前的示例，现在使用 orderby descending 子句。这里车手是根据按降序指定的键选择器中的获胜次数进行排序的（代码文件 EnumerableSample/Program.cs）：

```
var racers = from r in Formula1.GetChampions()
    where r.Country == "Brazil"
    orderby r.Wins descending
    select r;
```

orderby 子句解析为 OrderBy 方法，而 orderby descending 子句解析为 OrderByDescending 方法：

```
var racers = Formula1.GetChampions()
    .Where(r => r.Country == "Brazil")
    .OrderByDescending(r => r.Wins)
    .Select(r => r);
```

OrderBy 和 OrderByDescending 方法返回 IOrderedEnumerable<TSource>。此接口派生自接口 IEnumerable<TSource>，但包含一个额外的方法 CreateOrderedEnumerable<TSource>。此方法用于对序列进行进一步排序。如果两个项目基于键选择器相同，则可以使用 ThenBy 和 ThenByDescending 方法继续排序。这些方法需要一个 IOrderedEnumerable<TSource> 来工作，但也返回此接口。因此，你可以添加任意数量的 ThenBy 和 ThenByDescending 方法来对集合进行排序。

使用 LINQ 查询，你只需将用于排序的所有不同键（用逗号分隔）添加到 orderby 子句中。在下一个示例中，对所有车手的排序首先基于国家/地区，接下来基于姓氏，最后基于名字。添加到 LINQ 查询结果的 Take 扩展方法用于返回前 10 个结果：

```
var racers = (from r in Formula1.GetChampions()
    orderby r.Country, r.LastName, r.FirstName
    select r).Take(10);
```

排序后的结果如下所示：

- Argentina: Fangio, Juan Manuel
- Australia: Brabham, Jack
- Australia: Jones, Alan
- Austria: Lauda, Niki
- Austria: Rindt, Jochen
- Brazil: Fittipaldi, Emerson
- Brazil: Piquet, Nelson
- Brazil: Senna, Ayrton
- Canada: Villeneuve, Jacques
- Finland: Hakkinen, Mika

使用扩展方法执行相同操作会使用 `OrderBy` 和 `ThenBy` 方法：

```
var racers = Formula1.GetChampions()
    .OrderBy(r => r.Country)
    .ThenBy(r => r.LastName)
    .ThenBy(r => r.FirstName)
    .Take(10);
```

## 分组

为了基于键值对查询结果进行分组，可以使用 `group` 子句。现在应按国家/地区对 F1 冠军进行分组，并列出每个国家/地区的冠军人数。子句 `group r by r.Country into g` 根据 `Country` 属性对所有车手进行分组，并定义一个新的标识符 `g`，可在以后用于访问分组结果信息。`group` 子句的结果基于应用于分组结果的扩展方法 `Count` 进行排序；如果计数相同，则基于键进行排序。这是国家/地区，因为这是用于分组的键。`where` 子句基于具有至少两个项目的组来筛选结果，而 `select` 子句创建具有 `Country` 和 `Count` 属性的匿名类型（代码文件 `EnumerableSample/Program.cs`）：

```
var countries = from r in Formula1.GetChampions()
    group r by r.Country into g
    orderby g.Count() descending, g.Key
    where g.Count() >= 2
    select new {
        Country = g.Key,
        Count = g.Count()
    };

foreach (var item in countries)
{
    WriteLine($"{item.Country, -10} {item.Count}");
}
```

结果显示具有 `Country` 和 `Count` 属性的对象集合：

| Country | Count |
| ------- | ----- |
| UK | 10 |
| Brazil | 3 |
| Finland | 3 |
| Australia | 2 |
| Austria | 2 |
| Germany | 2 |
| Italy | 2 |

