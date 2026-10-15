

我们现在拥有的代码是 PopulatePeopleView 方法只关心接口。它需要一个具有 GetPeople 方法的对象，但它不关心具体的 data reader，只要它实现了该接口即可。

```
{
    public IActionResult UseService()
    {
        ViewData["Title"] = "Using a Web Service";
        IPersonReader reader = new ServiceReader();
        return PopulatePeopleView(reader);
    }

    public IActionResult UseCSV()
    {
        ViewData["Title"] = "Using a CSV File";
        IPersonReader reader = new CSVReader();
        return PopulatePeopleView(reader);
    }

    public IActionResult UseSQL()
    {
        ViewData["Title"] = "Using a SQL Database";
        IPersonReader reader = new SQLReader();
        return PopulatePeopleView(reader);
    }

    private IActionResult PopulatePeopleView(IPersonReader reader)
    {
        IEnumerable<Person> people = reader.GetPeople();
```

我不喜欢这段代码的一点是，我们的 UI 在实例化数据读取器。

![](img/0155736aec718cf18821e9f10a5d308d_931_0.png)

这超出了我们 UI 代码的职责范围，所以我们真的应该把它移到别处。为此，我们将使用工厂方法来创建适当的数据读取器。让我们快速了解一下工厂方法是什么，然后再更新代码。为了继续前进，我们将为数据读取器使用一个工厂方法。工厂方法负责为我们提供一个对象的实例。在我们的例子中，工厂将返回一个实现了我们的 IPersonReader 接口的对象。所以让我们来看一下这段代码。GetReader 方法返回一个 IPersonReader。

```
public IPersonReader GetReader(string readerType)
{
    switch (readerType)
    {
        case "Service": return new ServiceReader();
        case "CSV": return new CSVReader();
        case "SQL": return new SQLReader();
        default: throw new ArgumentException(...);
    };
}
```

控制器中的 UI 代码可以调用此方法，而不是自己承担创建对象的责任。工厂方法将字符串作为参数。字符串将指示我们想要哪种类型的读取器。根据参数的值，我们会实例化一个 ServiceReader、一个 CSVReader 或一个 SQLReader。现在我们将付诸实践。我们将添加工厂方法来创建读取器，然后在 UI 代码中使用它。这意味着我们可以从 Controller 类中的 UI 代码中删除对特定读取器的引用。核心应用程序将只知道接口。这使 UI 代码与它不应该关心的细节隔离开来。这就是我们刚刚处理的扩展性项目。我们将把工厂方法放到一个单独的项目中。这样我们的 PeopleViewer 项目就可以只引用工厂，而不需要知道任何特定的数据读取器或其项目。所以让我们在 Readers 文件夹上，依次选择 Add、New Project，我们将像之前一样选择一个类库，并将其命名为 PersonReader.Factory。和之前一样，我们将选择 .NET 5.0 项目。接下来，我将添加对我们数据读取器的引用，所以我将点击 Dependencies，选择 Add Project Reference，然后我们将选择 PersonReader.CSV、PersonReader.Service 和 PersonReader.SQL，我们还需要对接口 PersonReader.Interface 的引用。然后，接下来，我们将把文件从 Class1 重命名为 ReaderFactory。所以我们的 ReaderFactory 是一个 public 类，它将有一个 public 方法返回 IPersonReader。我再次使用 Control+. 来引入 using 语句，并将其命名为 GetReader。

```
using PersonReader.Interface;
using System;

namespace PersonReader.Factory
{
    public class ReaderFactory
    {
        public IPersonReader GetReader(string readerType)
        {
            switch
        }
    }
}
```

它将以一个字符串作为参数，我们称之为 readerType。有几种方法可以实现代码。我将使用 switch 语句。其他选项包括 switch 表达式和 also members。C# 有很多选项。我将让 Visual Studio 帮我一点点。如果我输入 switch，Visual Studio 会为我提供一个代码片段，说按两次 Tab 插入。所以我这样做，它问你想在什么上进行 switch？在这种情况下，我将选择 readerType。当我按 Enter 时，它会关闭片段。让我们填入一些 case。我们从 Service 开始。所以如果有人把 Service 作为参数发送给我们，我们将返回一个新的 ServiceReader，我将大量使用 Ctrl+. 来引入 using 语句。如果有人要求 CSV 读取器，那么我们将返回一个新的 CSVReader。如果有人要求 SQL 读取器，我们将返回一个新的 SQLReader。如果我们命中 default case，出了问题，所以我们将抛出一个新的 ArgumentException。我们传回的消息是 Invalid reader type，然后我们将传入作为参数收到的 readerType。

```
using PersonReader.CSV;
using PersonReader.Interface;
using PersonReader.Service;
using PersonReader.SQL;
using System;

namespace PersonReader.Factory
{
    public class ReaderFactory
    {
        public IPersonReader GetReader(string readerType)
        {
            switch (readerType)
            {
                case "Service": return new ServiceReader();
                case "CSV": return new CSVReader();
                case "SQL": return new SQLReader();
                default:
                    throw new ArgumentException($"Invalid reader type: {readerType}");
            }
        }
    }
}
```

所以这里我们有一个工厂方法，根据传入的参数，它会给我们返回一个实现了 IPersonReader 接口的类。我们当前的选项是 ServiceReader、CSVReader 或 SQLReader，但我们可以轻松扩展它。所以让我们回到我们的 PeopleViewer 应用程序并使用它。在 PeopleViewer 项目中，我将添加对我们刚刚创建的项目 PersonReader.Factory 的引用。然后我们将返回到 Controllers 文件夹并打开我们的 PeopleController。在我的 PeopleController 类的顶部，我将为我们的新 ReaderFactory 添加一个私有字段。然后我们将在我们的 PopulatePeopleView 方法中使用它。所以与其让 IPersonReader 作为参数传入，我们将要求读取器工厂为我们提供它。所以我们将调用 factory.GetReader 并将其分配给一个 IPersonReader 变量。我们确实需要向 GetReader 传递一个参数来指定读取器类型。所以让我们为 PopulatePeopleView 方法添加一个参数，我们称之为 readerType。由于我们更改了 PopulatePeopleView 中的方法签名，我们也需要更新所有其他方法。所以在我们的 UseService 方法中，我们传入字符串 Service。对于 UseCSV，我们传入 CSV，对于 UseSQL，我们传入 SQL。所以现在我们已经更新了代码，让我们运行并确保一切仍然正常工作。

```
public IActionResult UseService()
{
    ViewData["Title"] = "Using a Web Service";
    return PopulatePeopleView("Service");
}

public IActionResult UseCSV()
{
    ViewData["Title"] = "Using a CSV File";
    return PopulatePeopleView("CSV");
}

public IActionResult UseSQL()
{
    ViewData["Title"] = "Using a SQL Database";
    return PopulatePeopleView("SQL");
}

private IActionResult PopulatePeopleView(string readerType)
{
    IPersonReader reader = factory.GetReader(readerType);
    IEnumerable<Person> people = reader.GetPeople();
    ViewData["ReaderType"] = reader.GetType().ToString();
    return View("Index", people);
}
```

如果我们点击 Service 链接，我们会看到我们的类型是 PersonReader.Service.ServiceReader。如果我们返回主页并点击 CSV，我们会看到我们正在从 CSV 读取器获取数据。如果我们返回并点击 SQL 链接，我们会看到我们从 SQL 读取器获取数据。所以我们的应用程序仍然以相同的方式运行，但我们对代码做了非常有趣的事情。如果我们回到我们的 PeopleController 类，该类指定了我们应用程序的 UI 功能，我们会发现其中几个 using 语句变灰了

