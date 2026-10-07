
```cs
class Truck:IVehicle {
    public int BedCapacity { get; }
    public bool _IsAutomatic { get; }
    public Truck(int _BedCapacity, bool _IsAutomatic) {
        BedCapacity = _BedCapacity;
        IsAutomatic = _IsAutomatic;
    }
}
```

```cs
interface IVehicle {
    bool IsAutomatic { get; }
}
```

```cs
class Program {
    static void Main(string[] args) {
        List<Vehicle> vehicles = new List<Vehicle>();
        Car car = new Car(1000, true);
        Truck truck = new Truck(3000, false);
        vehicles.Add(car);
        vehicles.Add(truck);
        Console.WriteLine("Is automatic: " + vehicles[0].IsAutomatic);
        Console.WriteLine("Is automatic: " + vehicles[1].IsAutomatic);
        Console.WriteLine("The trunk capacity is: " + ((Car)vehicles[0].TrunkCapacity));
        Console.WriteLine("The bed capacity is: " + ((Truck)vehicles[1].BedCapacity));
    }
}
```

在这个示例中，有一个名为 `IVehicle` 的接口。在该接口内部，有一个属性，即 `IsAutomatic` 只读属性。该接口由两个类实现。第一个被称为 `Car` 类。该类实现了接口中的 `IsAutomatic` 属性，并且包含一个自己的属性。`Car` 类包含的属性是 `TrunkCapacity`。实例化 `Car` 类都需要这两个属性。构造函数接受两个参数，一个用于 `TrunkCapacity`，第二个用于 `IsAutomatic` 属性。

`Truck` 类做了类似的操作。它也实现了接口中的只读属性 `IsAutomatic`，并且它有一个自己的属性——`BedCapacity`。与上一个类一样，在这里也需要这两个属性来创建一个 `Truck` 对象的实例。这是因为构造函数接受两个参数，一个用于 `BedCapacity` 赋值，一个用于 `IsAutomatic` 属性赋值。在程序类的 `Main()` 方法中，我们创建了一个 `IVehicle` 元素的空列表。之后，我们实例化两个对象，一个 `Car` 类对象，另一个是 `Truck` 类型对象。

这种情况发生时，矩形对象（一个 `Rectangle` 类对象）被赋值给 `ShapeManager` 类对象内部的 `shape` 字段。之后，我们调用了 `shapeManager` 对象的 `DrawShape()` 方法。由于 `Rectangle` 类被注入到 `shapeManager` 的私有字段中，这将触发 `Rectangle` 类的 `Draw()` 方法。因此，它会在控制台输出“'Drawing rectangle...'”。绘制完成后，我们再次调用了 `ShapeManager` 对象的 `StopDrawing()` 方法。由于上述原因，这也会调用 `Rectangle` 类的 `Stop()` 方法。因此，它会在控制台输出“'Drawing rectangle stopped.'”。你可能已经注意到了那行创建 `Circle` 对象实例的注释代码。如果你取消该行的注释并将圆形对象放入 `ShapeManager` 注入中，你将获得不同的值和方法实现。这些值将来自 `Circle` 类的方法实现。这个示例完美地展示了依赖倒置原则，因为模块之间没有紧密耦合。

例如，我们可以轻松地再添加一个名为 `Triangle` 的类，它也会实现 `IShape` 接口。`Triangle` 对象也可以被注入到 `ShapeManager` 类的构造函数中，而无需更改 `Main()` 方法中的任何。实现了松耦合。

# 第 8 章：高级主题

在高级章节中，我们将尝试教你如何处理更复杂的 C# 编程技术。你还将学习更多关于异步编程的内容。此外，你将熟悉 C# 中的并行编程。我们将教你其他内容，如 C# 中的 LINQ 查询语法、依赖注入设计模式、映射器（Mappers）以及对象关系映射器。完成本章后，你将完全准备好进行 C# 编码并测试你的技能。本章之后的一切都取决于你自己。享受编程吧，让我们开始吧！

## 8.1 - 异步编程

异步编程代表了程序中处理事件的一种。当代表某些任务或事件的单一工作单元独立于主应用程序线程运行时，就会发生这种情况。执行后，事件任务将通知调用线程执行的成功或失败。你可能在想什么时候使用它以及它对你的软件有什么种好处。使用异步编程技术最大的好处是提高了软件的响应能力和性能。被标记为异步的操作始终独立于主进程执行而运行。

例如，在 C# 中，程序开始从 `Main()` 方法执行代码，在所有工作完成后，程序在 `Main()` 方法返回值时结束。所有调用都按顺序执行，并且每次一个操作都会等待上一个操作完成其工作。C# 中实现异步编程的方式略有不同。

在这里，我们将演示主要原理。如果你想明确某个方法是异步的并强制它异步执行工作，你需要在访问修饰符旁边放置 `async` 关键字。之后，你就可以异步调用此函数。当你准备好一个异步运行的函数后，你可能想在某处调用它。这通过在方法调用之前编写 `await` 关键字来实现。这意味着将其标记为异步执行。

在进入示例之前，关于 .Net 有几点是你应该知道的。C# 程序使用的运行时库中，有几个类被称为 `System.Threading.Task` 和 `System.Threading.Task<T>`，这些类允许你创建事件任务并让它们异步运行。`task`（任务）是代表应该完成某些作业的对象。任务负责让你知道操作是否有结果。它负责任务的完成情况。它还允许创建异步逻辑，除了 `async` 和 `await` 关键字外，这些逻辑看起来是同步的。与其他回调方法等编写异步逻辑的方法相比，这些关键字允许更容易维护维护异步逻辑。要完全理解任务，了解线程是什么也是至关重要的。C# .NET 系统类库在 `System.Threading` 命名空间中包含了线程相关的类。该命名空间包含一组异步和并行编程所需的组件。线程代表一小段可执行指令，并由 `System.Threading.Thread` 类表示。`Task` 返回异步（async）方法的类型。现在，让我们通过一个示例来演示：

```csharp
static void Main(string[] args)
{
    Console.WriteLine("Hello World!");
    var response = SomeAsyncCode().Result;
    Console.WriteLine($"{response}");
}
static async Task<string> SomeAsyncCode()
{
    await Task.Delay(3000);
    return "All done!";
}
```

在这个示例中，我们使用 `async` 和 `await` 来处理异步操作。`Task.Delay(3000)` 模拟了一个耗时操作，而 `await` 关键字确保方法在任务完成之前暂停执行，且不会阻塞主线程。

![](img/989605394af9c1cdcfc5a952af3b7bd1_968_0.png)

这导致了打印顺序混乱。这些线程根据“谁执行得更快”的基础上进行“竞争”。但是，如果我们能让它等待异步方法完成。以下是修改后的代码：

```c
static void Main(string[] args)
{
    Execute(obj);
}
public static async void Execute(object obj)
{
    Task<int> task = AsyncMethod();
    await NonAsyncMethod();
    int iterations = await task;
    Console.WriteLine(iterations);
}
public static async Task<int> AsyncMethod()
{
    int count = 0;
    await Task.Run(() => {
        for (int i = 0; i < 1000; i++) {
            Console.WriteLine("Async print");
            count += 1;
        }
    });
    return count;
}
public static void NonAsyncMethod()
{
    for (int i = 0; i < 2500; i++) {
        Console.WriteLine("Non async print");
    }
}
```

由于 `Main()` 方法不能被标记为 `async`，我们创建了一个异步方法 `ExecuteJob()` 并添加了上一个示例中的两个方法。首先，我们从 `AsyncMethod()` 创建了一个 `Task<int>` 引用，并将其放入 `task` 变量中。执行了 `NonAsyncMethod()` 和 `AsyncMethod()`。`AsyncMethod()` 会等待，并在执行完成后打印结果。输出如下：

![](img/989605394af9c1cdcfc5a952af3b7bd1_969_0.png)

## 8.2 - 并行编程

并行编程原理是一种模型，它将进程的执行划分为更小的部分，这些部分将同时完成。这也被称为并发编程。

它是通过多个处理器（或处理器的核心）来实现的，以便在代码执行中获得更好的性能。通过拆分操作以并发工作，缩短了任务完成的时间，这显然提升了性能以及用户在特定应用程序中的工作体验。随着处理器的演进，作为一种硬件设备，并发编程在编程中已经占据了重要地位。

你必须了解的概念是线程。线程代表了系统分配处理器时间执行的进程执行。在并发编程中，如果硬件中有多个 CPU 或 CPU 核心，一个进程可以拥有多个线程以并行方式执行某些操作。硬件和 CPU 组件越好，并行执行某些代码的可能性就越大，获得比通常技术更快结果的可能性也越大。

在 C# 中，定义几个与并行编程相关的术语是非常重要的。`ConcurrentBag` 表示一个支持以某种无序方式存储数据的集合。该类支持重复项，并且是一个线程安全的类，允许多个线程利用它。

`Parallel` 类是 C# 的内置类，为并行执行执行的循环提供支持。到目前为止我们使用的每个循环语句都是按顺序执行代码的。`Parallel` 类使循环能够并行执行它们的迭代。还有一些关键方法，例如 `Parallel.Invoke()`、`Parallel.For()` 和 `Parallel.ForEach()`。现在我们来展示一个示例来进一步解释并行编程的概念：

```c
class Program {
    static void Main(string[] args) {
        ConcurrentBag<int> parallelIntegers = new ConcurrentBag<int>();
        List<int> integers = new List<int>();
        int numberOfIntegers = 5;
        while (numberOfIntegers-- > 0) {
            parallelIntegers.Add(numberOfIntegers);
            integers.Add(numberOfIntegers);
        }
        Parallel.Invoke(
            () => {
                integers.ForEach(integer => {
                    Thread.Sleep(1000);
                });
                Console.WriteLine("Linear done");
            },
            () => {
                parallelIntegers.ForEach(integer => {
                    Thread.Sleep(1000);
                });
                Console.WriteLine("Parallel done");
            }
        );
    }
}
```

![](img/989605394af9c1cdcfc5a952af3b7bd1_974_0.png)

第二条消息也会打印到控制台输出，程序执行完毕。通过此，我们演示了并行编程的概念。很酷，对吧？

## 8.3 - LINQ

语言集成查询（Language integrated query，通常称为 LINQ）代表了 C# 中的查询语法，用于对不同的对象源进行检索和过滤。LINQ 为各种类型的对象和变量产生单一的查询接口。这种查询语法被集成到 C# 以及 Visual Basic 中。为了提高理解，我们将提供一个示例来进一步解释。因此，你可能知道 SQL，即结构化查询语言。SQL 用于从数据库中获取和保存数据，它是一种专为与数据库紧密协作设计的语言。

与 SQL 类似，LINQ 用于获取和过滤不同的数据源，如集合、数据集等。你有许多方法可以使用 LINQ；它通过实现 `IQueryable` 接口用于查询对象集合、数据集、ADO.Net 数据集、XML 文档、Entity Framework Core 数据集、SQL 数据库直接查询和其他数据源。LINQ 就像程序中某些数据和变量之间的桥梁。它是很好的，是因为它能够在数据集上使用面向对象的方法。使用 LINQ 时，你不需要担心将数据设置转换为对象。LINQ 提供了一种从任何数据来源查询数据的方法。它支持编译时语法检查，因此如果你在编写 LINQ 时出错，编译器会立即通知你。LINQ 允许你查询每个集合，例如 `List` 和 `Array` 类等。它还允许你查询接口，如 `IEnumerable` 接口。

### 我们现在来看这些示例：

```csharp
class Program
{
    static void Main(string[] args)
    {
        List<Car> cars = new List<Car>() {
            new Car(100, true, false),
            new Car(200, false, true),
            new Car(300, true, true),
            new Car(400, false, false),
            new Car(500, false, true)
        };
        var carsThatAreAutomatic = cars.Where(s => s.IsAutomatic).ToList();
        carsThatAreAutomatic.ForEach(carThatIsAutomatic => {
            Console.WriteLine($"The trunk capacity of {carThatIsAutomatic.TrunkCapacity} is automatic");
        });
    }
    class Car
    {
        public int TrunkCapacity { get; }
        public bool IsAutomatic { get; }
        public bool IsTurboCharged { get; }
        public Car(int trunkCapacity, bool isAutomatic, bool isTurboCharged)
        {
            TrunkCapacity = trunkCapacity;
            IsAutomatic = isAutomatic;
            IsTurboCharged = isTurboCharged;
        }
    }
}
```
