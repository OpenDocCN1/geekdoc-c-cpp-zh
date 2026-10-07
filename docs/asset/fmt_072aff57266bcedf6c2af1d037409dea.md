
```csharp
static void Main(string[] args)
{
    var serviceProvider = new ServiceCollection()
        .AddSingleton<ICarManufacturer, CarManufacturer>()
        .AddSingleton<ITruckManufacturer, TruckManufacturer>()
        .BuildServiceProvider();

    var carManufacturer = serviceProvider.GetService<ICarManufacturer>();
    carManufacturer.CreateCar();

    var truckManufacturer = serviceProvider.GetService<ITruckManufacturer>();
    truckManufacturer.CreateTruck();
}
```

在这个示例中，我们使用了 Microsoft Dependency Injection 。定义了两个接口组件：一个是 `ICarManufacturer`，另一个是 `ITruckManufacturer` 接口。`ICarManufacturer` 接口包含一个方法签名，该方法是 `CreateCar()`。同样，`ITruckManufacturer` 接口包含一个方法签名，即 `CreateTruck()` 方法。然后，有一个 `CarManufacturer` 类实现了 `ICarManufacturer` 接口。它包含了接口中 `CreateCar()` 方法的实现。该方法向控制台打印 "Car created" 消息。我们还暴露了一个 `TruckManufacturer` 类。该类实现了 `ITruckManufacturer` 接口，意味着它包含了 `CreateTruck()` 方法的实现。该方法向标准输出打印 "Truck created" 消息。依赖注入发生在 `Program` 类的 `Main` 方法中。在这里，我们创建了一个 `ServiceCollection` 对象，用于存储服务对象。

`AddSingleton()` 方法将 `CarManufacturer` 类作为 `ICarManufacturer` 类型添加到到 `serviceProvider` 变量中。该方法以单例模式（Singleton design pattern）的方式元素添加到 `serviceProvider` 集合中。单例模式也是你必须熟悉的内容，因此我们在这里对其进一步解释。单例模式表示在整个应用程序工作流中使用某种类型的唯一对象。在第一次调用单例对象时会发生实例化。但每次我们调用单例对象时，获取的都是第一次调用后创建的对象。这意味着在处理它们时，单例对象代表相同的引用。单例对象的最佳示例可以用 C# 属性的使用来描述。
下方显示了一个示例：

```csharp
private object syncObject = new object();
private List<int> intList;
public List<int> IntList
{
    get
    {
        if(intList == null)
        {
            lock (syncObject)
            {
                if(intList == null)
                {
                    intList = new List<int>();
                    return intList;
                }
            }
            return intList;
        }
    }
}
```

这个示例是一个线程安全的只读单例实现。`lock` 语句内部第二个空检查防止了字段在第一次空检查和 `lock` 语句之间被更改的可能性。

第一个空检查还防止了在不需要时执行 `lock` 语句，这通过允许所有线程执行普通程序路径而不互相相互阻塞，从而提高了性能。`lock` 语句防止多个线程根据锁对象进入受保护的代码块。`await` 关键字不能用于 `lock` 语句内部。

你可以看到，每当程序中调用 `IntList` 属性时，它始终返回同一个对象。该对象只创建一次，然后就会被复用。现在，当单例原则明确后，我们可以继续 DI 示例。`AddSingleton()` 方法将对象添加到集合中，每当该对象被使用并从集合中取出时，它将是同一个对象，而不会被创建多次。我们为 `ICarManufacturer` 类型创建映射，使用了 `CarManufacturer` 对象。对于 `ITruckManufacturer` 类型，使用了 `TruckManufacturer` 对象。在添加单例后，调用了 `BuildServiceProvider()` 方法，它创建了包含所提供集合服务的 `ServiceProvider`。这代表了依赖注入的注册部分。我们注册了类型和相关对象的映射，并将它们放在 `serviceProvider` 集合中。

下一步是解析（Resolving）。我们已经注册了映射。

许多功能都有预先准备好的参数语句；它们易于调用，就像被调用的任何方法一样。ORM 抽象了数据库层，使其易于进行修改。它还为你提供了面向对象编程的使用，例如数据继承。然而，使用 ORM 也有缺点。例如，它在性能因素方面并不理想。对于大型应用程序系统，一切都可能变慢，因为在很多情况下存在许多不需要的关系。在这种情况下，使用 SQL 编写查询是一个更安全的解决方案。

C# 很好地支持几个 ORM 框架。目前最合适的可能是 Entity Framework Core ORM。让我们更深入地介绍一下这个流行的 ORM。

## Entity Framework

Entity Framework 是微软发布的一种 ORM，旨在为 C#.NET 应用程序创建最佳的 ORM。Entity Framework 的主要目的是让 C# 应用程序与关系型数据库之间的交互成为可能。Entity Framework 代表了一个更简单的工具，用于将代码中的对象映射到特定数据库中的表和列。重要的是，Entity Framework 是作为 .NET 运行时环境一部分开源工具。因此，它可以免费使用。Entity Framework 负责执行数据库命令并自动获取查询结果。该 ORM 可以将查询结果实例化为 C# 类对象。Entity Framework 能够生成与数据库交互所需的命令，以便为你写入数据并执行它。它具有将查询结果实例化为应用程序内部对象实例的机制。然后你可以访问对象的属性来获取某些列值，或者可以使用 LINQ 选择进一步相关的对象或多个对象。在 Entity Framework 中，可以将多个实体映射到单个表，也可以将单个实体映射到多个数据库表。这是 Entity Framework 提供的自定义功能。

微软推荐在所有的 C# 软件开发过程中使用此框架。Entity Framework Core 代表了应用程序内部的对象模型；它与用于持久化应用程序数据的数据库模型不同。这种方法完全不同。模型可以与数据库架构对齐，也可以非常不同，这提供了灵活性。使用 Entity Framework Core 有两种可能的方法。第一种方法被称为代码优先（Code-First Approach）。在这种方法中，你必须在代码内部创建表示数据库中表的类。当类及其属性被创建后，你可以执行执行命令来更新数据库架构。此时刻，数据库将发生更改，以创建或更新映射到代码的表。另一种方法是数据库优先（Database-First approach）。在这种方法中，执行的是相反的操作。首先，我们必须通过 SQL 或任何能够执行此操作的工具创建或更新数据库架构。在数据库架构更改后，我们可以执行命令在应用程序代码内部创建或更新类模型，这些模型将映射到数据库中的表。任何符合你的需求和应用程序设计的设计都可以选择。

现在我们将展示一个 Entity Framework Core ORM 的用法示例：

```csharp
public class Car
{
    public int Id { get; set; }
    public string Make { get; set; }
    public string Model { get; set; }
    public int Year { get; set; }
    public bool IsTurboCharged { get; set; }
}

class CarContext : DbContext
{
    public CarContext() { }
    public CarContext(DbContextOptions<CarContext> options) : base(options) {
    public DbSet<Car> Cars { get; set; }
    protected override void OnConfiguring(DbContextBuilder optionsBuilder)
    {
        if (!optionsBuilder.IsConfigured)
        {
            throw new Exception("Must pass optionsBuilder for use");
        }
    }
}
```

在这个示例中，我们将演示一个使用 Entity Framework Core 对象-关系映射器的程序。在这里，你可以看到一个名为 `Car` 的类模型。`Car` 类有几个属性，每个属性都将代表 `Car` 表中的一列。

- 在这个示例中，我们将演示一个 `DbContext`
- 在这个示例中，我们将演示一个使用 Entity Framework Core 对象-关系映射器的程序。在这里，你可以看到一个名为 `Car` 的类模型。`Car` 类有几个属性，每个属性都将代表 `Car` 表中的一列。

示例代码部分如下：
```csharp
protected override void OnConfiguring(DbContextBuilder optionsBuilder)
{
    if (!optionsBuilder.IsConfigured)
    {
        throw new Exception("Must pass optionsBuilder for use");
    }
}
```
