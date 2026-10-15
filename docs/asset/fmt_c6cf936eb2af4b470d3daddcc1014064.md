
这意味着，在我们的 `Octagon` 类中，我们必须提供所有这些实现。如果我注释掉 `GetPerimeter` 方法并尝试构建应用程序，我们会得到一个构建错误。并且如果我们查看错误，它会说，`'Octagon'` 未实现接口成员 `GetPerimeter()`。所以就像抽象类中的抽象成员一样，如果我们不提供接口所需实现，我们会得到编译器错误。

![](img/0155736aec718cf18821e9f10a5d308d_891_0.png)

这只是一个快速概述，以便我们可以了解具体类、抽象类和接口的工作方式。抽象类和接口之间有几个相似之处，但也有相当多的不同之处。我们将在本书后面更详细地研究这些差异。

## 第 2 章 面向抽象编程

现在我们已经看到了接口是什么，是时候开始了解为什么我们想要使用它们了。一个很大的优势是接口可以使我们的代码更灵活。这在面对变化时提供了弹性，而应用程序不断变化以满足用户需求。这种弹性意味着当我们在应用程序的一个部分进行更改时，我们减少或消除了在应用程序其他部分进行更改的需求。我们的代码会弯曲而不是断裂。这也使我们的代码与实现细节隔离。我们可以通过关注功能的结果而不是深入功能本身的细节来在更高层次处理代码。当然，如果需要，我们可以深入这些细节，但它们被放在一边，这样我们只有在需要时才这样做。有一种通用的建议在许多情况下都适用，即面向抽象编程而不是面向具体类型。当我们处理抽象时，我们处理的是更高层次的代码，我们可以避免陷入细节。在我们的示例中，我们将这种建议翻译为面向接口编程而不是面向具体类。接口是一种抽象，它为我们的代码添加了一个缝隙，这就是我们可以专注于更高层次功能的方式。我们可以盲目地遵循这一建议，但这会导致麻烦。最好理解其背后的原因，然后我们就可以决定何时遵循建议以及何时可以安全地忽略它。接口是工具，有时它们有用，有时它们没有用。我们之前看到具体类只是我们每天使用的常规类。这些可以是我们自己创建的类，也可以是各种库中的类。对于下一个示例，我们将使用 .NET 集合类。这里是我们可用的不同类型的集合列表。

`List<T>`

`Array`

`ArrayList`

`SortedList<TKey, TValue>`

`HashTable`

`Queue` / `Queue<T>`

`Stack` / `Stack<T>`

`Dictionary<TKey,TValue>`

`ObservableCollection<T>`

我们有 `List<T>`，它给我们一个对象集合。我们有 `HashTable`，它是一个无序的对象包。这可以为我们提供对单个项目的非常快速的访问。我们还有队列，它提供先进先出的集合。我们有栈，它提供后进先出的集合。有很多选择。集合有一系列接口来表示不同的功能。`List<T>` 实现了七个不同的接口。`IList<T>`、`IList`、`ICollection<T>`、`IReadOnlyList<T>`、`IReadOnlyCollection<T>`、`IEnumerable<T>` 和 `IEnumerable`。

开发者或不同团队在应用程序的各个部分工作。这个应用程序是该场景的一个缩小版本。我们的责任是网站的用户交互代码。另一个团队正在处理提供我们显示数据的库。对于此示例，我们使用解决方案。如果我们运行应用程序，我们会看到我们有一个网站，有两个链接，一个用于使用具体类型获取人员，一个用于使用抽象类型获取人员。

![](img/0155736aec718cf18821e9f10a5d308d_896_0.png)

## 请选择

- 使用具体类型获取人员
- 使用抽象类型获取人员

这是一个 ASP.NET MVC 应用程序，我故意让事情有点无聊。这样我们可以专注于接口，而不是陷入如何构建一个好网站的细节中。这些链接目前什么都不做，所以让我们回到代码并填入一些内容。但在我们这样做之前，让我们先看看我们现有的项目。`PeopleViewer` 项目是一个 ASP.NET MVC 应用程序。这是我们负责的代码。我们将从 `People.Library` 项目获取数据。

![](img/0155736aec718cf18821e9f10a5d308d_897_0.png)

这是一个类库，由另一个团队负责管理，该团队负责为我们提供所需的数据。`People.Service` 项目是一个服务，它提供类库使用的数据；`Common` 项目则存放所有项目之间共享的一些文件。如果你不熟悉 ASP.NET MVC，不用担心。我们只会查看这个项目中的几个文件，并确保这些文件易于找到。在编写我们的代码之前，我想看看另一个团队为我们提供的代码。这些代码位于 `People.Library` 项目中的 `PersonReader` 类里。既然另一个团队管理着这些细节，我们就不去操心了。相反，我想看看他们提供的方法签名。他们为我们提供了一个 `GetPeople` 方法，返回 `Person` 对象数组；以及一个 `GetPerson` 方法，接收一个 `id` 参数，返回单个人员。

```csharp
namespace People.Library
{
    public class PersonReader
    {
        Service initializers
        public Person[] GetPeople() [...]
        public Person GetPerson(int id) [...]
    }
}
```

让我们来看看这个 `Person` 类长什么样。我会选择“速览定义”，这样就会显示一个包含六个属性的类——这些属性就是我们的数据形态——以及一个对 `ToString` 方法的重写。

```csharp
{
    public class Person
    {
        public int Id { get; set; }
        public string? GivenName { get; set; }
        public string? FamilyName { get; set; }
        public DateTime StartDate { get; set; }
        public int Rating { get; set; }
        public string? FormatString { get; set; }
        public override string ToString()
        {
            if (string.IsNullOrEmpty(FormatString))
                FormatString = "{0} {1}";
            return string.Format(FormatString, GivenName, FamilyName);
        }
    }
}
```

那么，让我们在自己的代码中使用这个 `GetPeople` 方法。为此，我们将进入 `PeopleViewer` 项目，打开 `Controllers` 文件夹，找到 `PeopleController` 类。这是我们负责编写的其中一个类。

```csharp
namespace PeopleViewer.Controllers
{
    public class PeopleController : Controller
    {
        PersonReader reader = new PersonReader();
        public IActionResult UseConcreteType()
        {
            // TODO: Get data
            ViewData["Title"] = "Using Concrete Type";
            return View("Index", null);
        }
        public IActionResult UseAbstractType()
        {
            // TODO: Get data
            ViewData["Title"] = "Using Abstract Type";
            return View("Index", null);
        }
    }
}
```

在这个类的顶部，有一个字段，用于保存一个新的 `PersonReader` 对象。这个对象就是我们刚才看到的那个类库中的类。然后我们有两个方法：`UseConcreteType` 和 `UseAbstractType`，它们与网站上的链接一一对应。那么，让我们先来填充 `UseConcreteType` 方法的代码。为此，我会查看类库返回了什么。如果我说 `reader.GetPeople` 然后把鼠标悬停在这个方法上，可以看到它返回一个 `Person` 对象数组。由于我们在 `UseConcreteType` 方法中，所以会创建一个名为 `people` 的 `Person` 数组，然后将它赋值为该方法返回的内容。

```csharp
reader.GetPeople();
ViewData["Title"]
return View("Index", null);
Person[] PersonReader.GetPeople()
```

所以我们的 `people` 变量是一个 `Person` 数组，一种具体的集合类型。要使用这个变量，我们会把它传入视图，稍后我们就会看到它的工作方式。这段代码已经足以让它运行起来。我会按 `F5` 来生成并运行应用程序，然后会看到两个窗口弹出，接着是浏览器。

```csharp
namespace PeopleViewer.Controllers
{
    public class PeopleController : Controller
    {
        PersonReader reader = new PersonReader();
        public IActionResult UseConcreteType()
        {
            Person[] people = reader.GetPeople();
            ViewData["Title"] = "Using Concrete Type";
            return View("Index", people);
        }
        public IActionResult UseAbstractType()
        {
            // TODO: Get data
            ViewData["Title"] = "Using Abstract Type";
            return View("Index", null);
        }
    }
}
```

弹出的那两个控制台窗口，一个代表提供数据的 Web 服务，另一个代表我们正在开发的 `PeopleViewer` 应用程序。Visual Studio 中的解决方案已设置为让这两者自动启动。但是这个 `people` 变量在视图内部是如何使用的呢？为此，我们将转到另一个文件。在 `PeopleViewer` 项目的 `Views` 文件夹中，我们可以进入 `People` 文件夹，然后查看 `Index.cshtml`。`Index.cshtml` 是一个 Razor 视图，它结合了 C# 和 HTML 两种语言。

```csharp
@using Common
@model IEnumerable<Person>
<h1>Commanders - @ViewData["Title"]</h1>
<section>
    @foreach (Person person in Model)
    {
        <div data="@person.StartDate.Year.ToString()[2]">
            <span class="name">@person.ToString()</span>
            <span class="year">@person.StartDate.Year</span>
            <span class="rating">@person.Rating/10 stars</span>
        </div>
    }
</section>
```

当我们传递 `people` 变量时，它会以 `Model` 属性的形式出现在视图中。所以如果我们查看 `foreach` 语句，可以看到我们正在遍历模型中的每一项并显示数据。我们对这个模型所做的唯一事情就是使用 `foreach` 遍历它。我们不尝试索引它，也不尝试修改其中的任何内容，因此让我们看看 `foreach` 到底需要什么。如果我点击 `foreach` 并按 `F1`，它就会打开帮助，告诉我们 `foreach` 适用于任何实现了 `IEnumerable` 或 `IEnumerable<T>` 接口的对象，而这个接口是一种我们可以在代码中引用的抽象。事实上，如果我们查看视图代码，在我设置的顶部，模型是一个 `IEnumerable`，因此视图本身只引用了接口，而不是任何特定的具体集合类型。我们可以在 `PeopleController` 代码中做同样的事情。因此，让我们通过填充 `UseAbstractType` 方法来实现这一点。我在这里使用的变量类型将是 `IEnumerable`，所以我们将使用抽象类型而不是具体类型。我们将其命名为 `people`，然后调用 `reader.GetPeople`。

如果我们把 `people` 变量改为使用 `var`，那么我们的代码会以相同的方式工作，但在处理代码的方式上有一个根本性的区别。当我们使用 `var` 时，我们实际上是在说：给我这个方法返回的任何类型。在这种情况下，如果我们将鼠标悬停在 `var` 上，会看到它是一个 `List<T>`，其中 `T` 为 `Person`，所以这个 `people` 变量是一个 `List`。当我们使用 `IEnumerable` 时，我们是在说：给我这个方法返回的任何类型，只要它具有我所需要的行为。如果我们没有指定所需的行为，那么以后可能会遇到问题。在本书后面讨论显式实现和默认接口实现时，我们会看到相关示例。就我个人而言，在很多情况下我都会使用 `var`，在接下来的更多示例中，你会看到它的身影；但当我关心某个特定功能时，我会确保指定我需要的类型或接口。

到目前为止，我们已经了解了接口是什么以及为什么需要接口。接口是一种约定。当一个类实现了接口时，它就承诺将以属性、方法、事件和索引器的形式提供一组特定的功能。我们讨论了使用具体类、抽象类和接口时的区别。在多边形示例中，我们看到，如果子类没有重写 `getArea` 方法，具体类可能会给我们带来运行时错误。而使用抽象类或接口时，我们则被迫提供 `getArea` 的实现。否则，我们的代码将无法编译。我们还看到了如何将公共功能放入抽象基类中。在后面的章节中，我们将更深入地了解接口和抽象类之间的异同。然后我们看到了接口如何让我们的代码更加灵活。当我们使用具体类进行编程时，代码是脆弱的。当底层集合发生变化时，我们的代码就会崩溃。当我们使用抽象（即接口）进行编程时，我们指定我们只关心……

关于一组特定的功能，而不是任何具体的实现。这使我们的代码能够接受不同的集合类型，而无需修改。在下一章中，我们将通过创建和实现自己的接口来深入探讨具体做法，这将使我们的应用程序易于扩展。

## 第3章 如何创建接口以增加可扩展性

我们已经看到接口如何帮助我们让代码经得起未来的考验。现在，是时候看看接口如何让我们的代码易于扩展了。如果我们制定一个核心应用程序可以使用的契约，那么我们就可以接入任意数量的符合该契约的不同实现。为此，我们将探讨接口的具体做法。首先，我们将看到如何创建自己的接口。在这种情况下，是一个仓储接口，帮助我们连接不同的数据源。然后我们将看到如何通过编写多个仓储来实现这个接口。这些仓储将让我们能够从Web服务、文本文件和SQL数据库获取数据。在创建了这些不同的实现之后，我们将通过使用工厂方法来消除重复代码。这将把具体细节移到项目的不同部分，这样我们就可以专注于正在处理的代码的重要功能。在我自己的工作中，我创建了一个规则引擎，允许轻松添加不同的规则类型。我还组装了自定义工作流，允许完全控制每一步，我还使用过一个授权客户端，它可以连接到不同类型的用户存储。这些可扩展的应用程序都是通过接口实现的。

假设我们有一个将部署到多个客户端站点的应用程序。每个客户端对于存储和检索数据都有自己的偏好。我们的应用程序需要从各种来源获取数据。可能是一个Web服务，它给我们返回数据的表示形式，其中`JSON`代表`JavaScript Object Notation`，或者是一个包含值的`CSV`文本文件，或者是一个关系数据库，如`Microsoft SQL Server`或`SQLite`。也可能是一个文档数据库，或者是一个云中的服务，如`Amazon AWS`，或者是一个`Azure`函数调用，为我们提供所需的数据。与每个数据源交互都有特定的方式。当我们使用Web服务时，我们通过网络进行`HTTP`调用。对于文本文件，我们使用文件输入/输出操作。但是我们不希望核心应用程序代码处理这些细节。相反，我们将建立一个仓储。以下是`Martin Fowler`对仓储模式的描述。仓储模式使用一个用于访问领域对象的接口，在领域层和数据映射层之间进行中介。让我们探讨一下这意味着什么。仓储模式让我们将应用程序代码与特定的数据存储技术分离。我们不希望应用程序代码需要知道如何进行`HTTP`调用或打开文件系统上的文件。相反，仓储负责这些细节。然后，仓储将数据作为应用程序可以使用的标准C#对象公开。在我们的案例中，我们将创建几个不同的仓储。服务仓储将知道如何向返回`JSON`数据的Web服务发出`HTTP`调用，这些数据使用`JavaScript Object Notation`格式化。`CSV`仓储将知道如何打开文件系统上的文件并解析值。`SQL`仓储将知道如何使用`Entity Framework`连接到`SQLite`数据库。那么这些如何接入我们的应用程序呢？通过接口。我们将创建一个仓储接口，作为我们的契约，其中包含与数据交互的方法。

```csharp
