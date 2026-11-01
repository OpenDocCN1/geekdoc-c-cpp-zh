
```
var r = entry.Entity as Racer;
if (r != null)
{
    Console.WriteLine("{0}: {1}", state, r.Lastname);
}
```

代码片段 Formula1Demo/Program.cs

运行应用程序时，已添加和已修改的车手会显示出来，并且已更改的属性会与其原始值和当前值一起显示：

- 已添加：Alguersuari
- 已修改：Alonso
- Fernando 的状态：Modified
- 已修改：Starts
- 原始值：138
- 当前值：139

## 附加和分离实体

当向调用方返回实体数据时，可能需要将对象从对象上下文中分离。这在例如从 Web 服务返回实体对象时是必要的。在这种情况下，如果客户端更改了实体对象，对象上下文并不知道该更改。

使用示例代码，ObjectContext 的 Detach() 方法分离名为 Fernando 的实体，因此对象上下文不会意识到对该实体所做的任何更改。如果已更改的实体对象从客户端应用程序传递到服务，则可以再次附加它。仅将其附加到对象上下文可能还不够，因为它不会提供对象已被修改的信息。相反，对象上下文内部必须存在原始对象。原始对象可以通过使用键使用 GetObjectByKey() 或 TryGetObjectByKey() 方法从存储中访问。如果实体对象已在对象上下文内部，则使用现有对象；否则它将从数据库中重新获取。调用 ApplyCurrentValues() 方法会将已修改的实体对象传递给对象上下文，如果有更改，则更改将在对象上下文内部具有相同键的现有实体中完成，并且 EntityState 设置为 EntityState.Modified。请记住，ApplyCurrentValues() 方法要求对象存在于对象上下文中；否则新的实体对象将以 EntityState.Added 添加：

```
using (var data = new Formula1Entities())
{
    ObjectQuery<Racer> racers = data.Racers.Where("it.Lastname='Alonso'");
    Racer fernando = racers.First();
    EntityKey key = fernando.EntityKey;
    data.Racers.Detach(fernando);

    // Racer is now detached and can be changed independent of the object context
    fernando.Starts++;
    Racer originalObject = data.GetObjectByKey(key) as Racer;
    data.Racers.ApplyCurrentValues(fernando);
}
```

代码片段 Formula1Demo/Program.cs

## 存储实体更改

在 ObjectStateManager 的帮助下，借助所有更改信息，可以使用 ObjectContext 类的 SaveChanges() 方法将已添加、已删除和已修改的实体对象写入存储。为了验证对象上下文中的更改，您可以将处理程序方法分配给 ObjectContext 类的 SavingChanges 事件。该事件在数据写入存储之前触发，因此您可以添加一些验证逻辑来查看是否应真正进行更改。SaveChanges() 返回已写入的实体对象的数量。

如果在读取记录后，数据库中由实体类表示的记录已被更改会怎样？答案取决于模型中设置的 ConcurrencyMode 属性。对于实体对象的每个属性，您可以将 ConcurrencyMode 配置为 Fixed 或 None。值 Fixed 表示该属性在写入时会被验证，以确定该值在此期间是否未被更改。None —— 这是默认值 —— 忽略任何更改。如果某些属性配置为 Fixed 模式，并且在读取和写入实体对象之间数据发生了更改，则会发生 OptimisticConcurrencyException。

您可以通过调用 Refresh() 方法来处理此异常，以将数据库中的实际信息读入对象上下文。此方法接受由 RefreshMode 枚举值配置的两种刷新模式：ClientWins 或 StoreWins。StoreWins 表示从数据库中获取实际信息并将其设置为实体对象的当前值。ClientWins 表示数据库信息被设置为实体对象的原始值，因此数据库值将在下一次 SaveChanges() 时被覆盖。Refresh() 方法的第二个参数是实体对象的集合或单个实体对象。您可以按实体决定刷新行为：

```csharp
private static void ChangeInformation()
{
    //...
    int changes = 0;
    try
    {
        changes += data.SaveChanges();
    }
    catch (OptimisticConcurrencyException ex)
    {
        data.Refresh(RefreshMode.ClientWins, ex.StateEntries);
        changes += data.SaveChanges();
    }
    Console.WriteLine("{0} entities changed", changes);
    //...
}
```

## LINQ TO ENTITIES

在本书的多个章节中，您已经看到 LINQ 用于查询对象、数据库和 XML。当然，LINQ 也可用于查询实体。

使用 LINQ to Entities，LINQ 查询的源是 ObjectQuery<T>。由于 ObjectQuery<T> 实现了 IQueryable 接口，因此为查询选择的扩展方法是在 System.Linq 命名空间的 Queryable 类中定义的。此类中定义的扩展方法具有 Expression<T> 参数；因此编译器将表达式树写入程序集。您可以在第 11 章中阅读有关表达式树的更多信息。然后表达式树由 ObjectQuery<T> 类解析为 SQL 查询。

您可以使用此处所示的简单 LINQ 查询来返回赢得超过 40 场赛事的车手：

```csharp
using (var data = new Formula1Entities())
{
    var racers = from r in data.Racers
                 where r.Wins > 40
                 orderby r.Wins descending
                 select r;
}
```

```
foreach (Racer r in racers)
{
    Console.WriteLine("\t{0} {1}", r.Firstname, r.Lastname);
}
```

访问 Formula1 数据库的结果如下：

Michael Schumacher
Alain Prost
Ayrton Senna

您也可以定义 LINQ 查询来访问关系，如下所示。变量 r 引用车手，变量 rr 引用所有比赛结果。过滤器使用 where 子句定义，仅检索来自瑞士且在领奖台上获得过比赛位置的车手。为了获得领奖台成绩，结果会被分组，并计算领奖台次数。排序基于领奖台成绩进行：

```
using (var data = new Formula1Entities())
{
    var query = from r in data.Racers
                from rr in r.RaceResults
                where rr.Position <= 3 && rr.Position >= 1 &&
                      r.Country == "Switzerland"
                group r by r.Id into g
                let podium = g.Count()
                orderby podium descending
                select new
                {
                    Racer = g.FirstOrDefault(),
                    Podiums = podium
                };
    foreach (var r in query)
    {
        Console.WriteLine("\t{0} {1} {2}", r.Racer.Firstname, r.Racer.Lastname, r.Podiums);
    }
}
```

运行应用程序时，会返回来自瑞士的三名车手的名字：

Clay Regazzoni 28
Jo Siffert 6
Rudi Fischer 2

## 摘要

在本章中，您已经看到了 ADO.NET Entity Framework 的功能。ADO.NET Entity Framework 基于 CSDL、MSL 和 SSDL 定义的映射 —— 描述实体、映射和数据库架构的 XML 信息。使用这种映射技术，您可以创建不同类型的关系来将实体类映射到数据库表。

您已经看到对象上下文如何保留有关检索和更新的实体的知识，以及如何将更改写入存储。

LINQ to Entities 只是 ADO.NET Entity Framework 的一个方面，它允许您使用新的查询语法访问实体。

## 32

## 数据服务

## 本章内容？

- WCF Data Services 概述
- 使用 CLR 对象托管 WCF Data Services
- 通过 HTTP 客户端访问 WCF Data Services
- 对 WCF Data Services 的 URL 查询
- WCF Data Services 与 ADO.NET Entity Framework
- 使用 WCF Data Services .NET 客户端提供程序
- 跟踪、更新和批处理

在上一章中，您看到了 ADO.NET Entity Framework 如何轻松创建对象模型以映射到数据库结构。Entity Framework 并未提供跨不同层获取对象的方法。这就是 WCF Data Services 发揮作用的地方。WCF Data Services 提供了一个 WCF 服务，可轻松访问由实体数据模型或实现 IQueryable<T> 接口的简单 CLR 对象提供的数据。

## 概述

ADO.NET Entity Framework 提供映射并创建代表数据库的实体类。借助 Entity Framework 的数据上下文，数据上下文会了解数据的更改，以便知道应更新什么内容。在创建跨多层解决方案时，Entity Framework 并没有帮助。

使用 WCF Data Services，您可以在服务器端使用 Entity Framework（或简单的 CLR 对象模型），并从客户端向服务发送 HTTP 查询以检索和更新数据。图 32-1 显示了一个典型场景，其中 Windows 客户端或使用 HTML 和 JavaScript 发送 HTTP 请求到服务器的网页。

![](img/d7d2ffa0a76feaab821930e95daace93_946_0.png)
