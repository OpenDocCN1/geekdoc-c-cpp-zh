
using System.Text;

using WhatsNewAttributes;

using static System.Console;

namespace LookUpWhatsNew

{

包含主程序入口点以及其他方法的类是 `Program`。你定义的所有方法都在这个类中，该类还有两个静态字段——`outputText` 和 `backDateTo`。`outputText` 包含在准备写入消息框时构建的文本；`backDateTo` 存储你选择的日期。将显示自该日期以来所做的所有修改。通常，你会显示一个对话框，邀请用户选择此日期，但我们不想陷入那种代码中。因此，`backDateTo` 被硬编码为 2015 年 2 月 1 日。你下载代码后可以轻松更改此日期：

class Program

{

    private static readonly StringBuilder outputText = new StringBuilder(1000);

    private static DateTime backDateTo = new DateTime(2015, 2, 1);

    static void Main()

    {

        Assembly theAssembly = Assembly.Load(new AssemblyName("VectorClass"));

        Attribute supportsAttribute = theAssembly.GetCustomAttribute(

            typeof(SupportsWhatsNewAttribute));

        string name = theAssembly.FullName;

        AddToMessage($"Assembly: {name}");

        if (supportsAttribute == null)

        {

            AddToMessage("This assembly does not support WhatsNew attributes");

            return;

        }

        else

        {

            AddToMessage("Defined Types:");

        }

        IEnumerable<Type> types = theAssembly.ExportedTypes;

        foreach(Type definedType in types)

        {

            DisplayTypeInfo(definedType);

        }

    }

}

AddToOutput($"{method.ReturnType} {method.Name} ()");

foreach (Attribute attribute in attributesToMethods)

{

    WriteAttributeInfo(attribute);

}

}

}

请注意，在此方法中，你首先做的是检查传递给你的 `Type` 引用是否实际表示一个类。因为为了简单起见，你已指定 `LastModified` 属性只能应用于类或成员方法，所以如果该项不是类（它可能是类、委托或枚举），进行任何处理都会浪费时间。

接下来，你使用 `type.GetTypeInfo().GetCustomAttributes()` 方法来确定该类是否附加了任何 `LastModifiedAttribute` 实例。如果是，则使用辅助方法 `WriteAttributeInfo` 将它们的详细信息添加到输出文本中。

最后，你使用 `TypeInfo` 类型的 `DeclaredMembers` 属性来遍历此数据类型的所有成员方法，然后对每个方法执行与类相同的操作——检查它是否附加了任何 `LastModifiedAttribute` 实例；如果是，则使用 `WriteAttributeInfo` 显示它们。

接下来的代码展示了 `WriteAttributeInfo` 方法，该方法负责确定为给定的 `LastModifiedAttribute` 实例显示什么文本。请注意，此方法接收一个 `Attribute` 引用，因此它需要先将其转换为 `LastModifiedAttribute` 引用。完成转换后，它使用你最初为此属性定义的属性来检索其参数。它会确认该属性的日期足够新，然后才将其实际添加到要显示的文本中：

private static void WriteAttributeInfo(Attribute attribute)

{

    LastModifiedAttribute lastModifiedAttrib =

        attribute as LastModifiedAttribute;

    if (lastModifiedAttrib == null)

    {

        return;

    }

    // check that date is in range

    DateTime modifiedDate = lastModifiedAttrib.DateModified;

    if (modifiedDate < backDateTo)

    {

        return;

    }

    AddToOutput($" modified: {modifiedDate:D}: {lastModifiedAttrib.Changes}");

    if (lastModifiedAttrib.Issues != null)

    {

        AddToOutput($" Outstanding issues: {lastModifiedAttrib.Issues}");

    }

}

#### 最后，这里是辅助方法 `AddToOutput`：

static void AddToOutput(string message)

{

    outputText.Append("\n" + message);

}

#### 运行此代码会产生如下所示的结果：

What's New since Sunday, February 1, 2015

Assembly: VectorClass, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null

Defined Types:

class Vector

  modified: Saturday, June 6, 2015: updated for C# 6 and .NET Core

  changes to methods of this class:

System.String ToString()

System.Collections.Generic.IEnumerator`1[System.Double] GetEnumerator()

  modified: Saturday, June 6, 2015: added to implement IEnumerable<T>

请注意，当你列出 `VectorClass` 程序集中定义的类型时，实际上会拾取两个类：`Vector` 和嵌入的 `VectorEnumerator` 类。此外，请注意，因为此示例中硬编码了 `backDateTo` 日期为 2 月 1 日，所以你实际拾取的是日期为 6 月 6 日（即代码改为支持 Core CLR 时）的属性，而不是更早日期的属性。

### 使用动态语言扩展进行反射

到目前为止，你一直使用反射来读取元数据。你还可以使用反射从编译时未知的类型动态创建实例。下一个示例演示了在编译器编译时不知道 `Calculator` 类的情况下创建该类的实例。程序集 `CalculatorLib` 在未添加引用的情况下被动态加载。在运行时，实例化 `Calculator` 对象，并调用一个方法。在你知道如何使用反射 API 之后，你将使用 C# 的 `dynamic` 关键字做同样的事情。自 C# 4 版本以来，该关键字一直是 C# 语言的一部分。

#### 创建 Calculator 库

被加载的库是一个简单的类库（包），包含 `Calculator` 类型，该类型带有 `Add` 和 `Subtract` 方法的实现。由于这些方法非常简单，它们使用表达式语法实现（代码文件 `CalculatorLib/Calculator.cs`）：

namespace CalculatorLib

{

    public class Calculator

    {

        public double Add(double x, double y) => x + y;

        public double Subtract(double x, double y) => x - y;

    }

}

编译库之后，将 DLL 复制到文件夹 `c:/addins`。要从类库（包）项目生成输出，请在“项目属性”的“生成”选项卡中，选择“生成时生成输出”选项（参见图 16.1）。

![](img/3d365b72b289213a91ade7eb366b8f35_574_0.png)

图 16.1

根据你使用的是 .NET Core 还是 .NET Framework 版本的客户端应用程序，你需要将相应的库复制到 `c:/addins` 文件夹。若要从 Visual Studio 内部选择运行应用程序的平台，请在“项目属性”中选择“调试”设置，并选择“平台”设置，如图 16.2 所示。

![](img/3d365b72b289213a91ade7eb366b8f35_574_1.png)

图 16.2

### 动态实例化类型

为了使用反射动态创建 Calculator 实例，你需要创建一个名为 ClientApp 的控制台应用程序（包）。

常量 `CalculatorLibPath`、`CalculatorLibName` 和 `CalculatorTypeName` 分别定义了库的路径、程序集的名称以及 Calculator 类型的名称（包括命名空间）。`Main` 方法调用了执行反射的两种变体方法 `ReflectionOld` 和 `ReflectionNew`（代码文件 `DynamicSamples/ClientApp/Program.cs`）：

class Program

{

    private const string CalculatorLibPath = @"c:/addins/CalculatorLib.dll";

    private const string CalculatorLibName = "CalculatorLib";

    private const string CalculatorTypeName = "CalculatorLib.Calculator";

    static void Main()

    {

        ReflectionOld();

        ReflectionNew();

    }

    // etc.

}

在使用反射调用方法之前，你需要实例化 Calculator 类型。有多种方法可以做到这一点。使用 .NET Framework 时，`GetCalculator` 方法通过 `Assembly.LoadFile` 方法动态加载程序集，并使用 `CreateInstance` 方法创建 Calculator 类型的实例。使用预处理器指令 `#if NET46`，这部分代码仅针对 .NET 4.6 编译（代码文件 `DynamicSamples/ClientApp/Program.cs`）：

#if NET46

private static object GetCalculator()

{

    Assembly assembly = Assembly.LoadFile(CalculatorLibPath);

    return assembly.CreateInstance(CalculatorTypeName);

}

#endif

该代码片段在编译 .NET 4.6 代码时使用了 NET46 符号。之所以可能，是因为对于 project.json 文件中列出的框架，会自动创建同名的符号；框架名称只是转换为大写。你还可以在 `compilationOptions` 声明中定义自己的符号。在框架声明的 `compilationOptions` 中指定 define 部分时，该符号仅针对特定框架定义。以下代码片段仅在应用程序为 .NET Core 编译时定义符号 DOTNETCORE（代码文件 `DynamicSamples/ClientApp/project.json`）：

{

  "frameworks": {

    "net46": {

      "defines": [ "NET46" ]

    },

    "netcoreapp1.0": {

      "defines": [ "DOTNETCORE" ]

    }

  }

}

{

  "frameworks": {

    "net46": {},

    "netstandard1.0": {

      "dependencies": {},

      "compilationOptions": {

        "define": ["DOTNETCORE"]

      }

    }

  }

}

.NET Core 的实现需要跨平台；因此不可能为 .NET Core 编译前面的代码。这里需要更多代码来加载程序集。首先，获取 `IAssemblyLoadContext` 以从文件系统加载程序集。获取加载上下文后，添加 `DirectoryLoader`（下一步将实现）以从文件系统加载程序集。设置好上下文后，可以使用 `Load` 方法加载程序集，并通过 `Activator` 类的 `CreateInstance` 方法动态实例化类型（代码文件 `DynamicSamples/ClientApp/Program.cs`）：

#if DOTNETCORE

private static object GetCalculator()

{

    IAssemblyLoadContext loadContext = PlatformServices.Default.

        AssemblyLoadContextAccessor.Default;

    using (PlatformServices.Default.AssemblyLoaderContainer.AddLoader(

        new DirectoryLoader(CalculatorLibPath, loadContext)))

    {

        Assembly assembly = Assembly.Load(new AssemblyName(CalculatorLibName));

        Type type = assembly.GetType(CalculatorTypeName);

        return Activator.CreateInstance(type);

    }

}

#endif

与加载上下文一起使用的 `DirectoryLoader` 类实现了 `IAssemblyLoader` 接口。该接口定义了 `Load` 和 `LoadUnmanagedLibrary` 方法。由于示例应用只加载托管程序集，因此只需要实现 `Load` 方法。该实现利用上下文来加载程序集文件（代码文件 `DynamicSamples/ClientApp/Program.cs`）：

public class DirectoryLoader : IAssemblyLoader

{

    private readonly IAssemblyLoadContext _context;

    private readonly string _path;

    public DirectoryLoader(string path, IAssemblyLoadContext context)

    {

        _path = path;

        _context = context;

    }

    public Assembly Load(AssemblyName assemblyName) =>

        _context.LoadFile(_path);

    public IntPtr LoadUnmanagedLibrary(string name)

    {

        throw new NotImplementedException();

    }

}
