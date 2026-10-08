
代码非常简单。位于 `Python.Hosting` 命名空间的 Python 对象负责管理运行时环境。你可以获取该对象的引用（在当前的 C# 上文中命名为 `calculator`），以访问 `Calculate.py` 迷你程序定义的操作：

```
var ipy = Python.CreateRuntime();
dynamic calculator = ipy.UseFile("Calculate.py");
```

你可以通过 `calculator` 对象调用 Python 代码段中定义的 `Add` 操作：

```sharp
calculator.Add("Welcome in IronPython on ",
DateTime.Now.ToShortString());
calculator.Add(i, j)
```

作为动态行为的优势，你可以向 `Add` 传递两个字符串或整数，它会动态将调用映射为拼接或加法。当然，`Add` 也接受许多其他类型组合。图 10-4 显示了控制台程序的输出。

![](img/b5597c749e848b27b0d305153ae16106_448_0.png)

图 10-4：应用程序的输出

> IronPython 运行时带有一个简短的语言教程。打开安装文件夹下的 `Tutorial\Tutorial.htm` 文件，通过修改 `Calculate.py` 和 `Program.cs` 文件来尝试该语言。

## ExpandoObject 示例

DLR 在 `System.Dynamic` 命名空间中定义了一个有趣的类型 de `ExpandoObject`。现在是演示 DLR 与 C# 4.0 结合使用的强大功能的时机，C# 4.0 现在支持动态操作（在运行时解析的操作）。与其告诉你这个类型是做什么的，让我们先看一个示例。

创建一个 C# 控制台应用程序并命名为 `ExpandoObjectDemo`。列表 10-2 显示了复制到 `Program.cs` 文件中的代码。

## 列表 10-2：ExpandoObjectDemo 的 Program.cs 文件

```sharp
using System;
using System.Dynamic;

namespace ExpandoObjectDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            dynamic customer = new ExpandoObject();
            customer.Id = 116;
            customer.Name = "John Doe";
            Console.WriteLine("{0}, {1}", customer.Id, customer.Name);

            dynamic address = new ExpandoObject();
            address.Id = "SHIP";
            address.Line1 = "xxxx 7th Street";
            address.Line2 = "My Great Company";
            address.City = "Los Angeles";
            address.State = "CA";
            Console.WriteLine("address type and State: {0}, {1}", address.Id, address.State);
        }
    }
}
```

可以在 Wrox.com 下载代码文件 [Program.cs]

读到这里，第一个问题可能是：“这段代码真的能运行吗？” 它创建了两个 `ExpandoObject`。第一次，它被作为具有 `Id` 和 `Name` 属性的 `Customer` 对象使用；第二次作为具有 `Id`、`Line1`、`State` 等属性的 `Address` 对象使用。

答案是该对象可以编译并运行，没有任何错误或警告，这是因为 `ExpandoObject` 的动态行为。此外，以下代码段也是有效的。你可以将其插入 10-2 中。

```csharp
dynamic triangle = new ExpandoObject();
triangle.A = new { X = 0, Y = 0, Z = 0 };
triangle.B = new { X = 100, Y = 100, Z = 0 };
triangle.C = new { X = 0, Y = 100, Z = 100 };
```

`ExpandoObject` 是一个“顽皮的小丑”，其成员可以在运行时动态地添加和删除。该类型定义的唯一公共成员是它的默认构造函数，当然它还继承了 `System.Object` 的公共方法。图 10-5 显示了所有这些成员，正如在编辑代码时在 IntelliSense 列表中所示。

这种行为的关键在于用于声明引用动态实例的动态类型。这是 C# 中的一种新类型，它指示编译器使用 DLR 动态地对所引用对象上的所有操作进行处理。

对于设置 `ExpandoObject` 属性的语句，编译器不再直接编译 MSIL 来设置这些属性，而是向对象发送发送消息，例如“将属性 id 设置为 '116'”（无论如何，无法发出 MSIL 属性设置器指令，因为 `ExpandoObject` 没有 id 属性）。

DLR 在运行时将消息发送给对象，并将属性的名称和值存储在字典中。当准备读取 id 属性时，它会“获取名为 id 的属性的值”，并使用 `ExpandoObject` 及其字典来查找并检索该值。

## DynamicObject 示例

DLR 为你提供了可以创建自定义动态对象的实用类型。在运行时，动态操作按以下步骤分发到目标对象：

- 1. 如果目标是 COM 对象，操作将通过 `Dispatch` 接口动态分发。
- 2. 如果目标类型实现了 `System.Dynamic` 命名空间中的 `DynamicMetaToObject` 接口，则使用该接口并请求目标执行操作。
- 3. 否则，目标是标准的 .NET 对象，操作将使用对其类型的反射进行分发，并使用 C# “运行时绑定器”，它在运行时实现了 C# 的查找和重载解析语义。

`DynamicMetaToObject` 接口包含大约十个方法需要实现。DLR 提供了 `DynamicObject` 类型，作为你动态对象的基类来实现此接口。

让我们创建一个简单的类，用属性语法来解析环境变量。例如，你不需要编写类似这样的代码：

```csharp
Environment.GetVariable("Path")
```

相反，你可以使用这样的动态快捷方式：

```csharp
envObject.Path =
```

![](img/b5597c749e848b27b0d305153ae16106_450_0.png)

图 10-5：IntelliSense 中的 ExpandoObject 成员

从 C# 示例应用程序开始，将其命名为 `DynamicObjectDemo`。向项目添加名为 `DynamicEnvironment.cs` 的新类文件。列表 10-3 显示了你应该复制到该文件的代码。

## 列表 10-3：DynamicEnvironment.cs

```csharp
using System;
using System.Dynamic;

namespace DynamicObjectDemo
{
    public class DynamicEnvironment: DynamicObject
    {
        private EnvironmentTarget _TargetEnv;
        private bool _ignoreMissingProperty;

        public DynamicEnvironment(EnvironmentTarget targetEnv, bool ignoreMissingProperty = false)
        {
            _TargetEnv = targetEnv;
            _ignoreMissingProperty = ignoreMissingProperty;
        }

        public override bool TryGet(Binder binder, out object result)
        {
            result = Environment.GetVariable(binder.Name, _TargetEnv);
            return result != null || _ignoreMissingProperty;
        }
    }
}
```

可以在 Wrox.com 下载代码文件 [DynamicEnvironment.cs]

构造函数允许你传递可选的 `EnvironmentTarget`，以设置你是否希望将对象绑定到机器或用户。`ignoreMissingProperty` true 值允许在属性不存在时返回空值，而不是抛出异常。属性解析由重写的 `TryGet` 方法处理。它接受两个参数。绑定器接收来自 DLR 的操作。在这种情况下，它处理要解析的属性名称。结果应设置为从操作检索的值，如果属性名称指向存在的环境变量，则解析成功并检索该值；否则返回空，取决于 `ignoreMissingProperty` 的值。

如果操作可以由该方法处理，则方法的返回值设置为 true；否则为 false。该方法的逻辑非常简单。列表 10-4 显示了 `Program.cs`。

## 列表 10-4：DynamicObjectDemo 的 Program.cs 文件

```csharp
using System;

namespace DynamicObjectDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            dynamic env = new DynamicEnvironment(ignoreMissingProperty: true);
            Console.WriteLine(env.Path);
            Console.WriteLine(env.Temp);
            Console.WriteLine(env.NonExisting ?? "null");
        }
    }
}
```

此程序按预期运行。由于没有名为 `NonExisting` 的环境变量，第三行将显示 "null"。将 `ignoreMissingProperty` 值设为 false，以便 `DynamicEnvironment` 在使用未知属性时抛出异常。现在运行程序将抛出 `RuntimeBinderException`（如图 10-6 所示），告诉你无法解析 `NonExisting` 属性。

![](img/b5597c749e848b27b0d305153ae16106_452_0.png)

图 10-6：抛出的 RuntimeBinderException

> 这非常简单，并不真正健壮。例如，它无法解析 USERNAME 或 MACHINENAME，因为这些无法通过 `Environment.GetVariable` 方法获取。尝试此示例，并尝试通过扩展这些功能来使其更有用！

## 类型等效

.NET 4 极大改进了 COM 互操作性。从 CLR 的角度来看，最重要的特性是类型等效。它要求在部署应用程序时，无需为其操作的 COM 组件部署 PIA。此功能实现在

