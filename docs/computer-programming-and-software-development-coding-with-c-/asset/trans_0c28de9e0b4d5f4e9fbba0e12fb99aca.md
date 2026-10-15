
![](img/0155736aec718cf18821e9f10a5d308d_897_0.png)

这是一个类库，由另一个团队负责管理，该团队负责为我们提供所需的数据。People.Service 项目是一个服务，它提供类库使用的数据；Common 项目则存放所有项目之间共享的一些文件。如果你不熟悉 ASP.NET MVC，不用担心。我们只会查看这个项目中的几个文件，并确保这些文件易于找到。在编写我们的代码之前，我想看看另一个团队为我们提供的代码。这些代码位于 People.Library 项目中的 PersonReader 类里。既然另一个团队管理着这些细节，我们就不去操心了。相反，我想看看他们提供的方法签名。他们为我们提供了一个 GetPeople 方法，返回 Person 对象数组；以及一个 GetPerson 方法，接收一个 id 参数，返回单个人员。

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

让我们来看看这个 Person 类长什么样。我会选择“速览定义”，这样就会显示一个包含六个属性的类——这些属性就是我们的数据形态——以及一个对 ToString 方法的重写。

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

那么，让我们在自己的代码中使用这个 GetPeople 方法。为此，我们将进入 PeopleViewer 项目，打开 Controllers 文件夹，找到 PeopleController 类。这是我们负责编写的其中一个类。

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

在这个类的顶部，有一个字段，用于保存一个新的 PersonReader 对象。这个对象就是我们刚才看到的那个类库中的类。然后我们有两个方法：UseConcreteType 和 UseAbstractType，它们与网站上的链接一一对应。那么，让我们先来填充 UseConcreteType 方法的代码。为此，我会查看类库返回了什么。如果我说 reader.GetPeople 然后把鼠标悬停在这个方法上，可以看到它返回一个 Person 对象数组。由于我们在 UseConcreteType 方法中，所以会创建一个名为 people 的 Person 数组，然后将它赋值为该方法返回的内容。

```csharp
reader.GetPeople();
ViewData["Title"]
return View("Index", null);
Person[] PersonReader.GetPeople()
```

所以我们的 people 变量是一个 Person 数组，一种具体的集合类型。要使用这个变量，我们会把它传入视图，稍后我们就会看到它的工作方式。这段代码已经足以让它运行起来。我会按 F5 来生成并运行应用程序，然后会看到两个窗口弹出，接着是浏览器。

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

弹出的那两个控制台窗口，一个代表提供数据的 Web 服务，另一个代表我们正在开发的 PeopleViewer 应用程序。Visual Studio 中的解决方案已设置为让这两者自动启动。但是这个 people 变量在视图内部是如何使用的呢？为此，我们将转到另一个文件。在 PeopleViewer 项目的 Views 文件夹中，我们可以进入 People 文件夹，然后查看 Index.cshtml。Index.cshtml 是一个 Razor 视图，它结合了 C# 和 HTML 两种语言。

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

当我们传递 people 变量时，它会以 Model 属性的形式出现在视图中。所以如果我们查看 foreach 语句，可以看到我们正在遍历模型中的每一项并显示数据。我们对这个模型所做的唯一事情就是使用 foreach 遍历它。我们不尝试索引它，也不尝试修改其中的任何内容，因此让我们看看 foreach 到底需要什么。如果我点击 foreach 并按 F1，它就会打开帮助，告诉我们 foreach 适用于任何实现了 IEnumerable 或 IEnumerable<T> 接口的对象，而这个接口是一种我们可以在代码中引用的抽象。事实上，如果我们查看视图代码，在我设置的顶部，模型是一个 IEnumerable，因此视图本身只引用了接口，而不是任何特定的具体集合类型。我们可以在 PeopleController 代码中做同样的事情。因此，让我们通过填充 UseAbstractType 方法来实现这一点。我在这里使用的变量类型将是 IEnumerable，所以我们将使用抽象类型而不是具体类型。我们将其命名为 people，然后调用 reader.GetPeople。

如果我们把 people 变量改为使用 var，那么我们的代码会以相同的方式工作，但在处理代码的方式上有一个根本性的区别。当我们使用 var 时，我们实际上是在说：给我这个方法返回的任何类型。在这种情况下，如果我们将鼠标悬停在 var 上，会看到它是一个 List（T 为 Person），所以这个 people 变量是一个 List。当我们使用 IEnumerable 时，我们是在说：给我这个方法返回的任何类型，只要它具有我所需要的行为。如果我们没有指定所需的行为，那么以后可能会遇到问题。在本书后面讨论显式实现和默认接口实现时，我们会看到相关示例。就我个人而言，在很多情况下我都会使用 var，在接下来的更多示例中，你会看到它的身影；但当我关心某个特定功能时，我会确保指定我需要的类型或接口。

到目前为止，我们已经了解了接口是什么以及为什么需要接口。接口是一种约定。当一个类实现了接口时，它就承诺将以属性、方法、事件和索引器的形式提供一组特定的功能。我们讨论了使用具体类、抽象类和接口时的区别。在多边形示例中，我们看到，如果子类没有重写 getArea 方法，具体类可能会给我们带来运行时错误。而使用抽象类或接口时，我们则被迫提供 getArea 的实现。否则，我们的代码将无法编译。我们还看到了如何将公共功能放入抽象基类中。在后面的章节中，我们将更深入地了解接口和抽象类之间的异同。然后我们看到了接口如何让我们的代码更加灵活。当我们使用具体类进行编程时，代码是脆弱的。当底层集合发生变化时，我们的代码就会崩溃。当我们使用抽象（即接口）进行编程时，我们指定我们只关心……
