
```csharp
Console.WriteLine();

if (selectedOperation == 0)
    break;

ICalculation operation = operations[selectedOperation - 1];
int a = ReadInt("a: ");
int b = ReadInt("b: ");
Console.WriteLine("Result = " + operation.Calculate(a, b));
Console.WriteLine();
Console.WriteLine();
}
}
```

注意我们根据实现操作的类的类型名称将所有操作打印到屏幕上。我们可以通过多种方式提供对操作名称的更多自定义（例如，通过向接口添加只读的 Name 字符串属性）。稍后，我们将看到另一种将此类描述性元数据与对象关联的方法，使用通过反射 API 发现的自定义属性。

在前面的代码中，我们使用了一个小的 ReadInt 辅助函数，它从控制台读取整数值，只要用户未提供有效输入就会重试：

```csharp
static int ReadInt(string prompt)
{
    int result = 0;
    bool valid = false;
    while (!valid)
    {
        Console.Write(prompt);
        valid = int.TryParse(Console.ReadLine(), out result);
    }
    return result;
}
```

如果我们坚持使用内置在线操作，则只需从 GetOperations 提供内置操作实例的列表（例如，使用迭代器如下所示）：

```csharp
static IEnumerable<ICalculation> GetOperations()
{
    yield return new Addition();
    yield return new Subtraction();
    yield return new Multiplication();
    yield return new Division();
    // You can add other built-in operations here easily...
}
```

在此简单实现的基础上，我们已经拥有一个有用的（承认是简单的）计算器，如图 21.6 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1093_0.png)

图 21.6 未加载任何扩展的可扩展计算器。

## 发现和加载扩展

除了内置扩展之外，我们还希望能够加载第三方供应商提供的所有扩展。这涉及两个契约方面：首先，需要实现我们的 ICalculation 接口；其次，需要将扩展程序集放在主机应用程序可以找到的位置（在图 21.4 中称为“存储库”）。我们假设扩展位于应用程序可执行文件旁边的 Extensions 文件夹中。

使用反射，我们现在可以在程序集中发现扩展类型。这有两个方面：我们首先需要找到所有程序集并加载它们。完成此操作后，我们需要扫描程序集以查找实现 ICalculation 的类型并创建其实例。我们假设扩展需要默认构造函数。

### 发现，更安全且简化

在此示例范围内，此发现过程因其对各种操作的反射使用而引起我们的兴趣。然而，以此处所示的方式实现时存在一些限制和缺点。首先，仅仅通过搜索 .dll 文件并尝试通过反射 API 加载它们来查找程序集是对事物的过度简化。我们可能希望不仅基于包含程序集的目录来发现类型，还要在其他地方查找。

其次，加载这些程序集可能因多种原因而失败。也许 .dll 文件不是程序集，而是原生 DLL 或某种因某种原因伪装成 .dll 扩展名的其他类型文件。

最后，除非包含的应用程序域整体卸载，否则程序集无法卸载。行为不端的程序集或没有任何有用扩展类型的程序集将被加载到程序的内存中。

像 System.Addins 和 MEF 这样的框架有助于避免此类问题。

```csharp
static IEnumerable<ICalculation> GetExtensions()
{
    if (Directory.Exists("Extensions"))
    {
        var icalc = typeof(ICalculation);

        foreach (var file in Directory.EnumerateFiles("Extensions", "*.dll"))
        {
            // For isolation, one will like to use AppDomains...
            var asm = Assembly.LoadFrom(file);

            // "LINQ to Reflection" to the rescue.
            var extTypes = from t in asm.GetTypes()
                           where t.GetInterfaces().Contains(icalc)
                           select t;

            foreach (var ext in extTypes)
                yield return (ICalculation)Activator.CreateInstance(ext);
        }
    }
}
```

在这段代码中，我们在 Extension 子文件夹（相对于工作目录；即应用程序可执行文件所在的位置）中找到所有 .dll 文件。加载文件后通过 Assembly.LoadFrom（也在 System.Reflection 命名空间中），我们使用 LINQ 根据实现 ICalculation 接口的类型过滤程序集的类型。为此，我们依赖于 System.Type 上的 GetInterfaces 方法。

最后，在找到所有实现 ICalculation 接口的类型后，我们可以使用之前见过的 Activator.CreateInstance 方法实例化每一个。这假设存在默认构造函数。

给定前述方法，我们现在可以调整 GetExtensions 方法以同时包含已发现的和内置的操作（再次使用 LINQ 运算符）：

```csharp
static IEnumerable<ICalculation> GetOperations()
{
    return GetBuiltinOperations().Concat(GetExtensions());
}

static IEnumerable<ICalculation> GetBuiltinOperations()
{
    // And seen earlier...
}
```

```csharp
static IEnumerable<ICalculation> GetExtensions()
{
    // As seen above...
}
```

## 关于构造函数和状态的思考

我们对所有使用该操作类型的计算重用同一实例这一事实意味着这些类型应谨慎处理状态。如果计算对象的某次使用中的状态保留下来并可能影响后续操作，你可能会遇到麻烦。

或者，我们可以在每次重用时创建计算对象的新实例。在这种配置下，你仍然希望只发现一次类型，但将实例创建调用推迟到每次使用时。

这让我们进一步讨论关于扩展要求特定构造函数（无法在接口中捕获）的隐式契约。因为我们承担了所有发现任务，直到找到符合特定接口契约的类型为止，我们负责创建实例。

或者，你可以考虑使用一个接口，该接口具有单个成员 GetExtensions，每个扩展程序集都需要用于发现目的。但这样我们所做的只是给扩展提供者增加了更多负担，而且我们仍然需要发现这个假设的 IExtensionProvider 实现，同样需要调用某个构造函数。

### 编写和部署扩展

扩展的开发发生在单独的项目中，导致创建单独的程序集，通常由第三方创建。鉴于我们的简单接口，此类扩展的定义应该是自解释的。例如：

```csharp
using Extensibility;
namespace Geometry
{
    public class Pythagoras : ICalculation
    {
        public int Calculate(int a, int b)
        {
            return (int)Math.Sqrt(a * a + b * b);
        }
    }
}
```

现在我们需要将生成的 Geometry.dll 文件放在主机应用程序查找扩展的 Extensions 子文件夹中。在真实场景中，部署扩展到终端用户机器时将使用某些安装程序来促进此任务，但

出于演示（和开发）目的，我们可以简单地复制它。需要以下文件夹结构：

ExtensiCalc
- ExtensiCalc.exe
- Extensions
- Geometry.dll

为了简化调试由主机应用程序加载的我们自己的扩展，我们可以在 Visual Studio 中为 Geometry 项目配置构建过程，并添加一个后构建步骤。图 21.7 说明了使用某些相对路径将构建文件复制到适当位置的配置。因为我们构建到 Geometry 文件夹下的 bin\Debug 文件夹，所以我们需要向上移动三级，以便转入 ExtensiCalc（主机应用程序）构建文件夹。从这里，我们构造到 ExtensiCalc 可执行文件旁边的 Extensions 子文件夹的路径，同样在 bin\Debug 下（假设你在 Debug 配置下构建）。$(TargetPath) 变量由 MSBuild 提供，包含构建的程序集文件的完整路径。此类变量可以通过使用编辑后生成按钮来发现。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1096_0.png)

图 21.7 配置后生成事件以复制构建的程序集文件。

最后，当我们现在运行应用程序时，我们应该在操作菜单中看到 Pythagoras 条目出现，如图 21.8 所示。

## 受管扩展框架

有助于在 .NET 平台上创建可扩展应用程序的框架之一是 MEF。虽然对 MEF 的全面讨论超出了本章范围，但简要介绍是必要的，尤其是因为 .NET 4 是首次开箱即用地提供此新技术的框架版本。

