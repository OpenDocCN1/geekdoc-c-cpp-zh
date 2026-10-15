
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

如果我们迎来一个新客户，而该客户使用不同的数据存储技术，那么我们就需要重新编译整个应用程序。如果现有客户决定改变其数据存储方式，我们也需要重新编译整个应用程序。这带来的另一个副作用是，每个客户端应用程序都包含了所有数据读取器的代码，尽管它们只需要其中一个。接着就是支持问题。如果我们不断需要为客户端重新编译应用程序，那就意味着不同的客户端可能拥有不同版本的应用程序，每个版本都有一组需要修复的bug。这使得支持变得非常困难，尤其是在客户数量众多的情况下。我们的动态读取器工厂将不会对数据读取器有任何编译时引用。相反，它会在运行时从文件系统加载相应的数据读取器程序集。这意味着我们可以将核心应用程序与任何数据读取器分开编译。这也意味着每个数据读取器都可以单独编译。这样，我们就可以只为每个客户端提供他们需要的那一个数据读取器。一个重要的效果是，每个客户端都可以拥有相同版本的核心应用程序，这使得支持变得更加容易。我们的动态工厂方法使用反射

在运行时加载相应的数据读取器程序集。以下是基本步骤。首先，我们检查配置，看看需要加载哪种类型的数据读取器以及可以在哪个程序集中找到它。接下来，我们从文件系统加载程序集。然后，我们在该程序集中查找特定的数据读取器类型。有了这些信息，我们就可以创建数据读取器的实例，然后从工厂返回该实例。如果你不理解这段代码的细节，不用担心。展示这段代码的主要原因是让你对使用接口时可以实现的功能有一个清晰的认识。我发现这项技术非常有用，但确实花了我一段时间才完全掌握其中的细节。

## 第6章 动态读取器工厂

在本示例中，我们将回顾已添加到应用程序中的动态加载代码。有了这些代码，我们的应用程序将不会对任何特定的数据读取器产生编译时引用。这意味着我们可以在不重新编译应用程序的情况下更改应用程序所使用的数据读取器。这将使我们能够轻松支持具有不同数据源的多个客户端，而不会陷入部署和支持的噩梦。这一次，我们在Visual Studio中打开了动态加载解决方案。这个应用程序与我们之前处理的略有不同。让我们运行它，然后查看代码。在这种情况下，我们只有一个链接用于使用运行时读取器。此时，我们的应用程序设置为使用服务读取器。那么让我们回去看看我们的项目。在我们的Readers文件夹中，我们只有接口和工厂的项目。这里没有任何具体的数据读取器。我们确实有一个ReadersForCompile文件夹，其中包含我们所有的数据读取器。尽管这些项目包含在解决方案中，但我们的其他项目都没有直接引用它们。

```
using PersonReader.Interface;
using System.Collections.Generic;

namespace PeopleViewer.Controllers
{
    public class PeopleController : Controller
    {
        private ReaderFactory readerFactory;

        public PeopleController(IConfiguration configuration)
        {
            readerFactory = new ReaderFactory(configuration);
        }

        public IActionResult UseRuntimeReader()
        {
            IPersonReader reader = readerFactory.GetReader();
            IEnumerable<Person> people = reader.GetPeople();

            ViewData["Title"] = "Using a Runtime Reader";
            ViewData["ReaderType"] = reader.GetType().ToString();
            return View("Index", people);
        }
    }
}
```

这些文件放在这里是为了让相应的文件能够自动复制到我们应用程序的输出文件夹中。这是设置此环境的最简单方式，以便你可以自己尝试代码，而无需执行太多步骤。那么让我们转到PeopleViewer项目，打开Controllers文件夹，查看我们的PeopleController。与我们上一个示例类似，PeopleController构造函数接受一个IConfiguration参数。但与之前的示例不同，它没有直接使用配置，而是将其传递给ReaderFactory的构造函数。稍后我们将看到ReaderFactory如何使用它。如果我们查看UseRuntimeReader操作，我们会调用readerFactory上的GetReader方法，但请注意GetReader方法不带任何参数。我们其余的代码看起来与之前看到的相同。大多数有趣的代码都发生在ReaderFactory中，所以让我们转到PersonReader.Factory项目并打开ReaderFactory文件。现在我们不会详细讨论这段代码的所有细节。这超出了本书的范围。我们将概述每个部分的作用。

```
```csharp
{
    public class ReaderFactory
    {
        private IConfiguration Configuration;
        public ReaderFactory(IConfiguration configuration)
        {
            Configuration = configuration;
        }

        private IPersonReader? reader;

        public IPersonReader GetReader()
        {
            if (reader != null)
                return reader;

            // Check configuration
            string? readerAssemblyName = Configuration["DataReader:ReaderAssembly"];
            string readerLocation = AppDomain.CurrentDomain.BaseDirectory
                                   + "ReaderAssemblies"
                                   + Path.DirectorySeparatorChar
                                   + readerAssemblyName;

            // Load the assembly
```
```

在ReaderFactory的构造函数中，我们获取了对配置的引用，并将其存储在私有字段中，然后在GetReader方法中使用它。在“检查配置”部分，我们获取DataReader:ReaderAssembly的配置值。让我们转到appsettings文件看看它的样子，因此我们将在PeopleViewer项目中打开appsettings.json。

```
```json
{
  "DataReader": {
    "ReaderAssembly": "PersonReader.Service.dll",
    "ReaderType": "PersonReader.Service.ServiceReader"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "AllowedHosts": "*"
}
```
```

这里我们有一个DataReader配置项，它有两个值，一个用于ReaderAssembly，一个用于ReaderType。ReaderAssembly是文件系统上DLL的名称，在本例中是PersonReader.Service.dll。ReaderType是DataReader的类型名称。目前，它设置为PersonReader.Service.ServiceReader。回到我们的工厂方法，我们从Configuration中获取程序集的名称，然后设置位置，当我们运行应用程序时，我们将看到该位置在文件系统上的样子。下一步是加载程序集。这会从文件系统加载文件，并使程序集对我们的应用程序可用。下一步是查找类型。这使用反射来查看已加载的程序集，并尝试找到我们正在寻找的类型，在本例中是名为PersonReader.Service.ServiceReader的东西。

```
```csharp
public IPersonReader GetReader()
{
    if (reader != null)
        return reader;

    // Check configuration
    string readerAssemblyName = Configuration["DataReader:ReaderAssembly"];
    string readerLocation = AppDomain.CurrentDomain.BaseDirectory
                          + "ReaderAssemblies"
                          + Path.DirectorySeparatorChar
                          + readerAssemblyName;

    // Load the assembly
    ReaderLoadContext loadContext = new ReaderLoadContext(readerLocation);
    AssemblyName assemblyName = new AssemblyName(Path.GetFileNameWithoutExtension(readerLocation));
    Assembly readerAssembly = loadContext.LoadFromAssemblyName(assemblyName);

    // Look for the type
    string? readerTypeName = Configuration["DataReader:ReaderType"];
    Type readerType = readerAssembly.ExportedTypes
        .First(t => t.FullName == readerTypeName);
}
```

一旦我们有了类型，就可以创建读取器。这使用Activator类来创建我们的数据读取器的实例。最后一步是返回我们的读取器。那么让我们再次构建并运行应用程序，然后仔细查看文件。根据我们应用程序当前的配置方式，如果我们点击“运行时读取器”链接，我们会使用ServiceReader获取数据。但现在让我们转到文件系统，仔细看看这是如何工作的。为此，我将右键单击PeopleViewer项目，然后选择“在文件资源管理器中打开文件夹”。然后我们将转到输出文件夹bin、Debug、net5.0。我想指出的第一件事是ReaderAssemblies文件夹。其中包含数据读取器所需的所有DLL。如果我们查看，可以看到PersonReader.CSV.dll、PersonReader.Service.dll和PersonReader.SQL.dll的文件。所有其他文件都是支持程序集。

