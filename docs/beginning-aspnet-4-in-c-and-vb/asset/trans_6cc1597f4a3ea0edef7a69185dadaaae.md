
## 类型筛选

基于类型进行筛选时，可以使用 OfType() 扩展方法。这里数组 data 同时包含 string 和 int 对象。使用 OfType() 扩展方法，将 string 类传递给泛型参数，只会返回集合中的字符串：

```
object[] data = { "one", 2, 3, "four", "five", 6 };
var query = data.OfType<string>();
foreach (var s in query)
{
    Console.WriteLine(s);
}
```

运行此代码，将显示字符串 one、four 和 five：

```
one
four
five
```

## Compound from

如果需要基于对象本身是一个序列的成员进行筛选，可以使用复合 from。Racer 类定义了一个属性 Cars，其中 Cars 是一个字符串数组。要筛选出所有曾驾驶法拉利夺冠的车手，可以使用如下所示的 LINQ 查询。第一个 from 子句访问 Formula1.GetChampions() 返回的 Racer 对象。第二个 from 子句访问 Racer 类的 Cars 属性，以返回所有类型为 string 的车辆。接下来使用 where 子句对车辆进行筛选，只保留曾驾驶法拉利夺冠的车手：

```
var ferrariDrivers = from r in Formula1.GetChampions()
                     from c in r.Cars
                     where c == "Ferrari"
                     orderby r.LastName
                     select r.FirstName + " " + r.LastName;
```

如果你好奇此查询的结果，所有驾驶法拉利的 F1 冠军是：

- Alberto Ascari
- Juan Manuel Fangio
- Mike Hawthorn
- Phil Hill
- Niki Lauda
- Kimi Räikkönen
- Jody Scheckter
- Michael Schumacher
- John Surtees

C# 编译器会将 LINQ 查询中的复合 from 子句转换为 SelectMany() 扩展方法。SelectMany() 可用于迭代一个序列的序列。示例中使用的 SelectMany 方法的重载如下所示：

```
public static IEnumerable<TResult> SelectMany<TSource, TCollection, TResult> (
    this IEnumerable<TSource> source,
    Func<TSource, IEnumerable<TCollection>> collectionSelector,
    Func<TSource, TCollection, TResult> resultSelector);
```

第一个参数是隐式参数，接收来自 GetChampions() 方法的 Racer 对象序列。第二个参数是 collectionSelector 委托，在其中定义内部序列。使用 Lambda 表达式 r => r.Cars 应返回车辆集合。第三个参数是一个委托，对每辆车都会被调用，并接收 Racer 和 Car 对象。Lambda 表达式创建一个具有 Racer 和 Car 属性的匿名类型。其结果是

排序后的结果如下所示：

```
Argentina: Fangio, Juan Manuel
Australia: Brabham, Jack
Australia: Jones, Alan
Austria: Lauda, Niki
Austria: Rindt, Jochen
Brazil: Fittipaldi, Emerson
Brazil: Piquet, Nelson
Brazil: Senna, Ayrton
Canada: Villeneuve, Jacques
Finland: Häkkinen, Mika
```

使用扩展方法实现相同功能时，使用 OrderBy() 和 ThenBy() 方法：

```
var racers = Formula1.GetChampions()
    .OrderBy(r => r.Country)
    .ThenBy(r => r.LastName)
    .ThenBy(r => r.FirstName)
    .Take(10);
```

## 分组

要基于键值对查询结果进行分组，可以使用 group 子句。现在应按国家对 F1 冠军进行分组，并列出每个国家内的冠军人数。子句 group r by r.Country into g 根据 Country 属性对所有车手进行分组，并定义一个新的标识符 g，可稍后用于访问分组结果信息。group 子句的结果基于应用于分组结果的扩展方法 Count() 进行排序，如果计数相同，则按键进行排序。这是国家，因为这是用于分组的键。where 子句基于至少包含两项的分组筛选结果，select 子句创建一个具有 Country 和 Count 属性的匿名类型：

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
    Console.WriteLine("{0,-10} {1}", item.Country, item.Count);
}
```

结果显示具有 Country 和 Count 属性的对象集合：

```
UK 9
Brazil 3
Australia 2
Austria 2
Finland 2
Italy 2
USA 2
```

使用扩展方法实现相同功能时，group by 子句被解析为 GroupBy() 方法。GroupBy() 方法的声明有趣之处在于它返回实现 IGrouping 接口的对象的枚举。IGrouping 接口定义了 Key 属性，因此在调用此方法后可以访问组的键：

```
public static IEnumerable<IGrouping<TKey, TSource>> GroupBy<TSource, TKey>(
    this IEnumerable<TSource> source, Func<TSource, TKey> keySelector);
```

需要一个字符串参数并返回 IEnumerable<Racer>，与之前实现的方法类似。为此定义了多个泛型 Func<> 委托，因此无需声明自己的委托。Lambda 表达式被赋给变量 racersByCar。Lambda 表达式的左侧定义了一个 car 变量，其类型为 Func 委托的第一个泛型参数（string）。右侧定义了使用 where 子句的 LINQ 查询，其中使用了该参数：

```
Func<string, IEnumerable<Racer>> racersByCar =
    car => from r in Formula1.GetChampions()
           from c in r.Cars
           where c == car
           orderby r.LastName
           select r;
```

现在可以使用 Intersect() 扩展方法获取所有曾驾驶法拉利和迈凯伦夺冠的车手：

```
Console.WriteLine("World champion with Ferrari and McLaren");
foreach (var racer in racersByCar("Ferrari").Intersect(
    racersByCar("McLaren")))
{
    Console.WriteLine(racer);
}
```

结果只有一个车手，Niki Lauda：

```
World champion with Ferrari and McLaren
Niki Lauda
```

> 集合操作通过调用实体类的 GetHashCode() 和 Equals() 方法来比较对象。对于自定义比较，还可以传递实现 IEqualityComparer<> 接口的对象。在此示例中，GetChampions() 方法始终返回相同的对象，因此默认比较有效。

## Zip

Zip() 方法在 .NET 4 中新增，可使用谓词函数将两个相关序列合并为一个。

首先创建两个相关序列，两者都具有相同的筛选条件（国家为意大利）和排序。对于合并而言这很重要，因为第一个集合的第 1 项与第二个集合的第 1 项合并，第 2 项与第 2 项合并，以此类推。如果两个序列的计数不同，Zip() 只会在到达较小的集合末尾时停止。

第一个集合中的项具有 Name 属性，第二个集合中的项具有 LastName 和 Starts 属性。

对集合 racerNames 使用 Zip() 方法需要将第二个集合 racerNamesAndStarts 作为第一个参数。第二个参数的类型为 Func<TFirst, TSecond, TResult>。该参数以 Lambda 表达式实现，并使用参数 first 接收第一个集合的元素，使用参数 second 接收第二个集合的元素。实现创建并返回一个字符串，其中包含第一个元素的 Name 属性和第二个元素的 Starts 属性：

```
var racerNames = from r in Formula1.GetChampions()
                 where r.Country == "Italy"
                 orderby r.Wins descending
                 select new
{
    Name = r.FirstName + ' ' + r.LastName
};

var racerNamesAndStarts = from r in Formula1.GetChampions()
    where r.Country == "Italy"
    orderby r.Wins descending
    select new
    {
        LastName = r.LastName,
        Starts = r.Starts
    };

var racers = racerNames.Zip(racerNamesAndStarts,
    (first, second) => first.Name + ", starts: " + second.Starts);
foreach (var r in racers)
{
    Console.WriteLine(r);
}
```

此合并的结果如下所示：

```
Alberto Ascari, starts: 32
Nino Farina, starts: 33
```

## 分区

诸如 Take() 和 Skip() 扩展方法之类的分区操作可用于轻松分页，例如一次显示 5 名车手。

在此处所示的 LINQ 查询中，扩展方法 Skip() 和 Take() 添加到查询末尾。Skip() 方法首先忽略基于页面大小和实际页码计算出的若干项；Take() 方法随后基于页面大小获取若干项：

```
int pageSize = 5;

int numberPages = (int)Math.Ceiling(Formula1.GetChampions().Count() /
    (double)pageSize);

for (int page = 0; page < numberPages; page++)
{
    Console.WriteLine("Page {0}", page);
    var racers =
        (from r in Formula1.GetChampions()
         orderby r.LastName
         select r.FirstName + " " + r.LastName).
        Skip(page * pageSize).Take(pageSize);
    foreach (var name in racers)
    {
        Console.WriteLine(name);
    }
    Console.WriteLine();
}
```

以下是前三页的输出：

```
Page 0
Fernando Alonso
Mario Andretti
Alberto Ascari
Jack Brabham
```
