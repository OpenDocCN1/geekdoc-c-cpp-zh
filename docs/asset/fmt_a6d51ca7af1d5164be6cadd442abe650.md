
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

```
writer.WriteLine($"{DateTimeOffset.Now:T} - {level}: {message}");

}
}
}
```

那么，让我们回到`PeopleController`类，修改几个变量类型。目前，`logger`变量的类型指定为接口`IPeopleLogger`，所以我们调用`LogException`是有效的。如果我将这个变量类型改为`FileLogger`，对`LogException`的调用就不起作用了，错误会告诉我们`FileLogger`类不包含`LogException`的定义；如果我们使用`var`，也会得到同样的结果。

```csharp
var logger = new FileLogger();

try
{
    ViewData["Title"] = "Using FileLogger";
    return GetPeople(logger);
}
catch (Exception ex)
{
    logger.LogException(ex);
    return View(...);
}
```

`CS1061: 'FileLogger' does not contain a definition for 'LogException' and no accessible extension method 'LogException' accepting a first argument of type 'FileLogger' could be found (are you missing a using directive or an assembly reference?)`

提醒一下，当我们使用`var`时，最终得到的类型就是赋给变量的类型，在本例中即`FileLogger`类型。正因如此，我们在`LogException`方法上会遇到同样的错误。

与显式实现一样，我们可以使用强制转换。因此，我们可以将`logger`变量强制转换为`IPeopleLogger`，现在就可以访问`LogException`方法了。所以，就像接口具有显式实现时那样，我们需要使用接口类型才能调用带默认实现的接口成员。但遗憾的是，事情可能会变得令人困惑。让我们看看`useConsoleLogger`方法，它使用的是`ConsoleLogger`类。

```csharp
namespace PeopleViewer.Controllers
{
    public class PeopleController : Controller
    {
        public IActionResult UseConsoleLogger()
        {
            ConsoleLogger logger = new ConsoleLogger();
            try
            {
                ViewData["Title"] = "Using Console Logger";
                return GetPeople(logger);
            }
            catch (Exception ex)
            {
                logger.LogException(ex);
                return View("Error", new ErrorViewModel());
            }
        }
        public IActionResult UseFileLogger()
        {
            var logger = new FileLogger();
            try
```

看看如果我们把这个变量类型改成`ConsoleLogger`会发生什么。在这种情况下，调用`LogException`时不会出现错误；如果我按 F12 查看`ConsoleLogger`类，就能明白原因。`ConsoleLogger`确实有自己的`LogException`实现，这意味着我们既可以通过类访问它，也可以通过接口访问它。无论哪种情况，它都不依赖默认实现。

实现。这有点令人困惑，因为有时具体类型有效，有时却无效。这取决于类是依赖于默认实现，还是提供自己的实现。确保每次都能正常工作的唯一方法是引用接口类型。我们已经看到了如何向接口添加新方法并提供默认实现。这意味着实现该接口的现有类无需更改，但我们需要考虑一些事情。其中重要的一点是，我们需要意识到对类将如何实现接口所做的假设。不幸的是，我遇到过一篇博客文章，其中有人对接口的实现方式做出了错误的假设，这可能导致意外的行为。下面是一个默认实现做出错误假设的示例。

```csharp
public interface IPeopleLogger
{
    public void Log(PeopleLogLevel level, string message);
    public void LogException(Exception ex)
    {
        Console.WriteLine($"{this.GetType()} - Exception: {ex.Message}");
    }
}
```

假设我们有一个现有的`IPeopleLogger`接口，它只有一个实现者，即控制台记录器。如果我们添加一个新方法，很容易直接写入控制台，因为控制台记录器就是这样做的，但这假设所有记录器都会使用控制台。如果我们有记录到文件或进行操作系统级跟踪日志的记录器，此实现将无法按预期工作。这个简单示例似乎显而易见，但编程时，我们很容易只关注当前拥有的实现，而不考虑其他实现，包括可能用于单元测试的实现。

这里有一种可以避免错误假设的方法：使用现有的接口成员。

```csharp
public interface IPeopleLogger
{
    public void Log(PeopleLogLevel level, string message);
    public void LogException(Exception ex)
    {
        Log(PeopleLogLevel.Error, ex.Message);
    }
}
```

在此示例中，我们有一个带默认实现的`LogException`方法，但在实现内部，我们调用了现有的日志方法。这意味着如果记录器记录到控制台，新方法也会记录到控制台。如果它记录到文件，新方法将记录到文件，因此这在一定程度上保护了我们。如果我们局限于接口的现有成员，那么也限制了我们扩展接口的方式。在此示例中，我们有一个包含`GetPeople`和`GetPerson`方法的存储库接口。

```csharp
public interface IPersonRepository
{
    IReadOnlyCollection<Person> GetPeople();
    Person GetPerson(int id);
    void SavePerson(Person person)
    {
        // ???
    }
}
```

如果我们想通过添加`save`方法来扩展此接口，实际上无法安全地添加一个只使用现有成员的默认实现，因为功能并不存在。因此，默认实现的使用方式存在一些限制，并且我们需要注意可能影响功能或性能的假设。如果我们牢记这些要点，那么我们可以安全地使用默认实现。

因此，我将右键单击`PeopleViewer`，选择“在文件资源管理器中打开文件夹”，然后转到`bin`、`Debug`、`net5.0`。这里我们有`Log.txt`文件。我将打开它并删除其内容，所以现在该文件是空的。然后关闭此文件并返回 Visual Studio。像之前一样，我将仅启动`PeopleViewer`应用程序，因此右键单击`PeopleViewer`项目，选择“调试”和“启动新实例”。同样，这会启动我们的应用程序，但不会启动它所需的 Web 服务。

## 错误。

处理您的请求时发生错误。

## 开发模式

切换到开发环境将显示有关所发生错误的更详细信息。

开发环境不应为已部署的应用程序启用。它可能导致向最终用户显示异常中的敏感信息。对于本地调试，可通过将`ASPNETCORE_ENVIRONMENT`环境变量设置为`Development`并重启应用来启用开发环境。

因此，让我们首先单击控制台记录器，等待错误消息。如果我们转到控制台窗口，会看到我们的日志条目，这是之前示例中的详细条目。这来自`ConsoleLogger`类本身的`LogException`方法。

```
System.Net.WebException - Exception: No connection could be made because the target machine actively refused it. [::ffff:127.0.0.1]:9874 (localhost:9874)
```

这里没有使用默认实现。因此，让我们回到应用程序并单击文件记录器链接。现在我们有了错误屏幕，让我们回到文件资源管理器并打开`Log.txt`文件。我们会看到这个日志文件仍然是空的，所以我们的日志没有写入正确的位置。现在让我们回到控制台窗口。

在我们的控制台窗口中，还有一条额外的消息，这来自接口本身的`LogException`方法。由于我们在接口中做出的假设，这条消息被写入了错误的位置。`LogException`方法正在写入控制台，这不是一个好的假设，因为记录器会写入各种位置。这个例子表明，在向接口添加默认实现时，我们需要小心。接口可以通过多种不同的方式实现。我们需要确保默认实现尊重这一点。我们无法总是避免默认实现的问题，但如果我们坚持使用现有的接口成员，我们的代码更有可能按预期工作。向接口添加成员的另一个解决方案是使用接口继承。当接口继承另一个接口时，该接口包含它定义的所有成员，以及父接口的所有成员。因此，这是在不更改原始接口的情况下扩展接口功能的一种方式。这不是 C# 8 新增的功能。它从一开始就存在，因此我们可以在任何 C# 应用程序中使用它。之前，在查看`IEnumerable`接口时，我们看到了接口继承。`IEnumerable<T>`接口继承自`IEnumerable`接口。

```csharp
public interface IEnumerable<T> : IEnumerable
```

因此，`IEnumerable<T>`包含它定义的所有成员，以及`IEnumerable`中定义的所有成员。我们可以做类似的事情。对于我们的示例代码，我们一直在使用一个存储库。我们的`IPersonReader`接口有`GetPeople`方法和`GetPerson`方法，但没有任何更改数据的方法。

```csharp
public interface IPersonReader
{
    IEnumerable<Person> GetPeople();
    Person GetPerson(int id);
}
```

如果我们想添加更新功能怎么办？一种方法是使用接口继承。这里有一个`IPersonRepository`接口，它同时具有读写功能。写功能来自接口中的`AddPerson`、`UpdatePerson`和`DeletePerson`方法。它继承了`IPersonReader`接口。

```csharp
public interface IPersonRepository : IPersonReader
{
    void AddPerson(Person newPerson);
    void UpdatePerson(int id, Person updated);
    void DeletePerson(int id);
}
```

这意味着它还包括读操作`GetPeople`和`GetPerson`。当一个类实现`IPersonRepository`接口时，它必须实现所有方法。这里我们有一个实现`IPersonRepository`接口的`SQLRepository`类。

在类中，我们为两个接口的所有成员提供了实现。我喜欢使用接口继承的一点是，它能让我们的接口保持专注。

```csharp
public interface IPersonReader
{
    IEnumerable<Person> GetPeople();
    Person GetPerson(int id);
}
public interface IPersonRepository :
    IPersonReader
{
    void AddPerson(...);
    void UpdatePerson(...);
    void DeletePerson(...);
}
```

如果代码的某部分只需要读操作，它可以使用`IPersonReader`接口。如果代码的某部分需要读写操作，可以使用`IPersonRepository`接口。对于实现接口的类也是如此。例如，如果一个类无法更新数据，它访问的 Web 服务只有读操作，那么它可以实现该接口。如果一个类可以支持读写操作，那么它可以扩展为实现更新的读/写接口。

## 第14章 附加功能与抽象类

到目前为止，我们使用的方法具有默认实现，但我们也可以将其用于其他接口成员，例如属性。默认实现可以与属性一起使用，但它实际上只对计算属性有意义，也就是说属性只有`getter`，没有`setter`。接口不允许有字段，因此很难在具有默认实现的`property`上使用`setter`。我们设置什么值呢？

```csharp
public class ConcreteRegularPolygon
{
    public int NumberOfSides { get; set; }
    public int SideLength { get; set; }
    //...
}
public interface IRegularPolygon
{
    int NumberOfSides { get; set; }
    int SideLength { get; set; }
    //...
}
```

因此，最好只将默认实现考虑在属性的`get`部分上。另一个限制与自动属性有关。在本书开头我们的第一个示例中，我们看到一个具体的正多边形，它有两个属性，具有空的`get`和`set`块。这些是自动属性，意味着编译器为我们创建了`backing field`和默认行为。但当我们查看`IRegularPolygon`接口时，我们有相同的语法，但含义不同。在接口中，当我们有空的`get`和`set`块时，这是一个声明，意味着实现类必须具有这些属性，并且同时具有`getter`和`setter`，但实现类必须提供它们。不幸的是，没有办法使用默认实现在接口中创建自动属性。从功能角度来看，我希望有这个功能，但接口是抽象的，而属性需要属于类特定实例的数据。因此，即使它很有用，它也不符合接口提供的抽象。

接口的另一个功能是我们可以对成员使用访问修饰符。在 C# 8 之前，访问修饰符是不允许的。一切都是自动公开的。这就是为什么常见的是看到接口成员上没有访问修饰符。它们是不允许的。现在接口可以具有明确标记为`public`的成员。这是默认值。因此，较旧的接口在没有访问修饰符的情况下继续以相同的方式工作。`Public`成员对任何有权访问接口的人都是可见的。接口成员也可以标记为`private`。这些成员仅在接口内部可见。正因为如此，它们必须具有默认实现。如果实现没有在接口内部提供，就没有其他方式提供它。好消息是编译器会强制你为私有成员提供实现。接口成员也可以标记为`protected`或`internal`或各种组合。你可能只想在接口继承和默认实现的特定组合中使用这些。在这些情况下事情可能会很快变得混乱。如果你想深入研究，你可能需要更详细地研究这些功能。我给出了一些关于如何使用默认实现与属性的建议。你可能想了解其背后的原因。访问修饰符也是如此。我展示了一些基本规则，但你可能想查找一些代码示例。

C# 8 中添加的另一件事是接口上可以有静态成员的能力。接口上的静态成员的工作方式与类上的相同，因此我们不会花时间查看具体细节。而且还有一篇关于在接口中使用静态成员的文章。除了文章之外，随着 .NET 和 C# 的新版本发布，附加资源将包含更新的代码示例，因此请务必查看它们。

在本书开头，我们使用正多边形来探索接口和抽象类之间的相似性和差异。它们共享共同的特性，例如具有抽象成员并允许实现代码。现在我们对接口有了更多的了解，让我们比较具体的方面。从概念上讲，接口的主要目的是它定义了一个契约。抽象类的目的是具有一些共享实现以及一些定义的抽象。一个类可以实现任意数量的接口。之前，我们看到`List of T`实现了七个不同的接口。相比之下，一个类只能从单个基类继承。当我们使用抽象类时，它填补了该继承槽。接口具有有限的实现代码。我们可以使用默认实现，但我们不能创建与类特定实例相关的自动属性或引用字段。抽象类对实现代码没有限制。

抽象类实现可以具有我们在具体类中拥有的任何实现。接口不能定义自动属性，它只能声明属性存在。由实现类提供这些属性。抽象类可以具有自动属性，并且这些属性对所有其后代类自动可用。最后的区别是关于我们允许使用哪些类型的成员。接口仅限于属性、方法、事件和索引器。抽象类可以具有属性、方法、事件、索引器、字段、构造函数和析构函数。

其中一些差异很微妙，那么我们如何决定使用接口还是抽象类呢？当我需要选择时，我会问自己有多少实现代码是共享的。如果有大量共享代码，那么我倾向于使用抽象类。如果共享代码很少或没有，我倾向于使用接口。我喜欢在可能的情况下使用接口，因为一个类可以实现多个接口，并且它也使继承槽保持开放，以便我可以从另一个类继承。让我们再看一下我们的一些示例。这里是我们第一次看到的正多边形。让我们思考一下所有不同形状——正方形、三角形、八边形等——共享多少代码。`NumberOfSides`属性由所有形状共享。

```
// Polygon
public int NumberOfSides {...}
```
