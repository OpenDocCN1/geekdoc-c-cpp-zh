
现在，根据条件来筛选赛车手将会很有趣。这可以通过使用 `ObjectQuery<T>` 类的 `Where()` 方法来完成。`Where()` 是创建 Entity SQL 的查询构建器方法之一。此方法需要一个谓词字符串，以及可选的 `ObjectParameter` 类型参数。此处显示的谓词指定只返回来自巴西的赛车手。其中的 `it` 指定结果的项，`Country` 是列。`ObjectParameter` 构造函数的第一个参数引用谓词的 `@Country` 参数，但不带 @ 符号：

```
string country = "Brazil";
ObjectQuery<Racer> racers = data.Racers.Where("it.Country = @Country",
    new ObjectParameter("Country", country));
```

其中的奥妙可以通过访问查询的 `CommandText` 属性立即看到。使用 Entity SQL 时，`SELECT VALUE it` 声明了它来访问列：

```
SELECT VALUE it
FROM (
[Formula1Entities].[Racers]
) AS it
WHERE
it.Country = @Country
```

`ToTraceString()` 方法显示生成的 SQL 语句：

```
SELECT
[Extent1].[Id] AS [Id],
[Extent1].[Firstname] AS [Firstname],
[Extent1].[Lastname] AS [Lastname],
[Extent1].[Country] AS [Country],
[Extent1].[Starts] AS [Starts],
[Extent1].[Wins] AS [Wins]
FROM [dbo].[Racers] AS [Extent1]
WHERE [Extent1].[Country] = @Country
```

当然，你也可以指定完整的 Entity SQL：

```
string country = "Brazil";
ObjectQuery<Racer> racers = data.CreateQuery<Racer>(
    "SELECT VALUE it FROM [Formula1Entities].[Racers] AS " +
    "it WHERE it.Country = @Country",
    new ObjectParameter("Country", country));
```

`ObjectQuery<T>` 类提供了几个查询构建器方法，如下表所述。其中许多方法与你在第 11 章“语言集成查询”中了解的 LINQ 扩展方法非常相似。这里的方法的一个重要区别是，参数类型不是 `delegate` 或 `Expression<T>`，而是通常为 `string` 类型。

| OBJECTQUERY<T> QUERY BUILDER METHODS | DESCRIPTION |
|---|---|
| Where() | 此方法允许你根据条件筛选结果。 |
| Distinct() | 此方法创建具有唯一结果的查询。 |
| Except() | 此方法返回结果，但不包含满足 except 筛选条件的项。 |
| GroupBy() | 此方法创建新查询，根据指定条件对实体进行分组。 |
| Include() | 对于关系，你之前看到相关内容是延迟加载的。需要调用 `EntityCollection<T>` 类的 `Load()` 方法才能将相关实体加载到对象上下文中。除了使用 `Load()` 方法之外，你也可以使用 `Include()` 方法指定查询以预先加载相关实体。 |
| OfType() | 此方法指定仅返回特定类型的实体。这对于 TPH 关系非常有用。 |
| OrderBy() | 此方法用于定义实体的排序顺序。 |
| Select() SelectValue() | 这些方法返回结果的投影。`Select()` 以 `DbDataRecord` 形式返回结果项；`SelectValue()` 返回由泛型参数 `TResultType` 定义的标量或复杂类型的值。 |
| Skip() Top() | 这些方法对分页很有用。使用 `Skip()` 方法跳过若干项，并使用 `Top()` 方法获取指定数量的项。 |
| Intersect() Union() UnionAll() | 这些方法用于组合两个查询。`Intersect()` 返回仅包含两个查询中都存在的结果的查询。`Union()` 组合查询并返回没有重复的完整结果。`UnionAll()` 也包括重复项。 |

让我们用一个示例来了解如何使用这些查询构建器方法。在下一个代码片段中，使用 `Where()` 方法筛选赛车手，只返回来自美国的赛车手；`OrderBy()` 方法首先按获胜次数降序排序，然后按参赛次数排序。最后，使用 `Top()` 方法只将前三名赛车手放入结果中：

```
using (var data = new Formula1Entities())
{
    string country = "USA";
    ObjectQuery<Racer> racers = data.Racers.Where("it.Country = @Country",
        new ObjectParameter("Country", country))
        .OrderBy("it.Wins DESC, it.Starts DESC")
        .Top("3");
    foreach (var racer in racers)
    {
        Console.WriteLine("{0} {1}, wins: {2}, starts: {3}",
            racer.Firstname, racer.Lastname, racer.Wins, racer.Starts);
    }
}
```

代码片段 Formula1Demo/Program.cs

这是此查询的结果：

```
Mario Andretti, wins: 12, starts: 128
Dan Gurney, wins: 4, starts: 87
Phil Hill, wins: 3, starts: 48
```

## 更新

从存储中读取、搜索和筛选数据只是数据密集型应用程序通常需要完成的工作的一部分。将更改后的数据写回存储是你需要了解的另一部分。

接下来的章节涵盖以下主题：

- 对象跟踪
- 更改信息
- 附加和分离实体
- 存储实体更改

## 对象跟踪

为了允许修改和保存从存储中读取的数据，实体在加载后必须被跟踪。这还要求对象上下文能够感知某个实体是否已经从存储中加载。如果有多个查询访问相同记录，对象上下文需要返回已加载的实体。

对象上下文使用 `ObjectStateManager` 来跟踪已加载到上下文中的实体。

下面的示例演示了，如果执行两个不同的查询并返回数据库中的相同记录，状态管理器确实能感知到这一点，并且不会创建新实体。相反，会返回相同的实体。可以通过 `ObjectStateManager` 属性访问与对象上下文关联的 `ObjectStateManager` 实例。`ObjectStateManager` 类定义了一个名为 `ObjectStateManagerChanged` 的事件，每次对象上下文添加或删除新对象时，都会触发该事件。这里，将方法 `ObjectStateManager_ObjectStateManagerChanged` 分配给该事件，以获取有关更改的信息。

这里使用两个不同的查询来返回一个实体对象。第一个查询获取来自奥地利、姓 Lauda 的第一个赛车手。第二个查询获取来自奥地利的赛车手，按获胜场数排序，并获取第一个结果。事实上，这是同一个赛车手。为了验证返回的是同一个实体对象，使用 `Object.ReferenceEquals()` 方法来检查两个对象引用是否确实引用同一个实例：

```
private static void TrackingDemo()
{
    using (var data = new Formula1Entities())
    {
        data.ObjectStateManager.ObjectStateManagerChanged +=
            ObjectStateManager_ObjectStateManagerChanged;

        Racer niki1 = data.Racers.Where("it.Country='Austria' && it.Lastname='Lauda'").First();

        Racer niki2 = data.Racers.Where("it.Country='Austria'").OrderBy("it.Wins DESC").First();
        if (Object.ReferenceEquals(niki1, niki2))
        {
            Console.WriteLine("the same object");
        }
    }
}

static void ObjectStateManager_ObjectStateManagerChanged(object sender,
    CollectionChangeEventArgs e)
{
    Console.WriteLine("Object State change - action: {0}", e.Action);
    Racer r = e.Element as Racer;
    if (r != null)
        Console.WriteLine("Racer {0}", r.Lastname);
}
```

代码片段 Formula1Demo/Program.cs

运行应用程序，可以看到 `ObjectStateManager` 的 `ObjectStateManagerChanged` 事件只发生一次，并且引用 `niki1` 和 `niki2` 确实是相同的：

```
Object State change – action: Add
Racer Lauda
The same object
```

## 更改信息

对象上下文还能够感知实体的更改。下面的示例向对象上下文添加并修改一个赛车手，并获取有关更改的信息。首先，使用 `ObjectSet<T>` 类的 `AddObject()` 方法添加一个新赛车手。此方法以 `EntityState.Added` 信息添加新实体。接下来，查询一个姓氏为 Alonso 的赛车手。对于此实体类，`Starts` 属性递增，因此实体被标记为 `EntityState.Modified` 信息。在后台，`ObjectStateManager` 会基于接口实现 `INotifyPropertyChanged` 得知对象中的状态更改。此接口在实体基类 `StructuralObject` 中实现。`ObjectStateManager` 订阅了 `PropertyChanged` 事件，并且每次属性更改时都会触发此事件。

要获取所有已添加或已修改的实体对象，可以调用 `ObjectStateManager` 的 `GetObjectStateEntries()` 方法，并像此处这样传递一个 `EntityState` 枚举值。此方法返回一个 `ObjectStateEntry` 对象集合，其中包含有关实体的信息。辅助方法 `DisplayState` 遍历此集合以提供详细信息。

你还可以通过将 `EntityKey` 传递给 `GetObjectStateEntry()` 方法来获取单个实体的状态信息。`EntityKey` 属性可用于实现了 `IEntityWithKey` 接口的实体对象，`EntityObject` 基类就是这种情况。返回的 `ObjectStateEntry` 对象提供了 `GetModifiedProperties()` 方法，你可以使用该方法读取所有已更改的属性值，并通过 `OriginalValues` 和 `CurrentValues` 索引器访问属性的原始信息和当前信息：

```csharp
private static void ChangeInformation()
{
    using (var data = new Formula1Entities())
    {
        var jaime = new Racer
        {
            Firstname = "Jaime",
            Lastname = "Alguersuari",
            Country = "Spain",
            Starts = 0
        };
        data.Racers.AddObject(jaime);
        Racer fernando = data.Racers.Where("it.Lastname='Alonso'").First();
        fernando.Starts++;
        DisplayState(EntityState.Added.ToString(),
            data.ObjectStateManager.GetObjectStateEntries(EntityState.Added));
        DisplayState(EntityState.Modified.ToString(),
            data.ObjectStateManager.GetObjectStateEntries(EntityState.Modified));
        ObjectStateEntry stateOfFernando =
            data.ObjectStateManager.GetObjectStateEntry(fernando.EntityKey);
        Console.WriteLine("state of Fernando: {0}",
            stateOfFernando.State.ToString());
        foreach (string modifiedProp in stateOfFernando.GetModifiedProperties())
        {
            Console.WriteLine("modified: {0}", modifiedProp);
            Console.WriteLine("original: {0}",
                stateOfFernando.OriginalValues[modifiedProp]);
            Console.WriteLine("current: {0}",
                stateOfFernando.CurrentValues[modifiedProp]);
        }
    }
}
static void DisplayState(string state, IEnumerable<ObjectStateEntry> entries)
{
    foreach (var entry in entries)
    {
```
