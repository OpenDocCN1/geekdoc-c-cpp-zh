

```csharp
public class AddOperation : IBinaryOperation
{
    public double Operation(double x, double y) => x + y;
}
```

还有一个带有 `SpeedMetadata` `Speed.Slow` 的 Add 方法导出（代码文件 `UICalculator/AdvancedOperations/Operations.cs`）：

```csharp
[Export("Add", typeof(IBinaryOperation))]
[SpeedMetadata(Speed = Speed.Slow)]
public class SlowAddOperation : IBinaryOperation
{
    public double Operation(double x, double y)
    {
        Task.Delay(3000).Wait();
        return x + y;
    }
}
```

Speed 只是一个有两个值的枚举（代码文件 `UICalculator/CalculatorUtils/SpeedMetadata.cs`）：

```csharp
public enum Speed
{
    Fast,
    Slow
}
```

你可以通过创建一个应用了 `MetadataAttribute` 的特性类来定义元数据。然后该特性会像在 `AddOperation` 和 `SlowAddOperation` 类型中看到的那样应用到一个部件上（代码文件 `UICalculator/CalculatorUtils/SpeedMetadataAttribute.cs`）：

```csharp
[MetadataAttribute]
[AttributeUsage(AttributeTargets.Class)]
public class SpeedMetadataAttribute : Attribute
{
    public Speed Speed { get; set; }
}
```

> 注意 有关如何创建自定义特性的更多信息，请阅读第 16 章。

要通过导入访问元数据，则定义了类 `SpeedMetadata`。`SpeedMetadata` 定义的属性与 `SpeedMetadataAttribute` 相同（代码文件 `UICalculator/CalculatorUtils/SpeedMetadata.cs`）：

```csharp
public class SpeedMetadata
{
    public Speed Speed { get; set; }
}
```

定义了多个 Add 导出后，按之前所示使用 Import 属性会在运行时失败。多个导出无法匹配仅一个导入。如果存在同名同类型的多个导出，则使用属性 `ImportMany`。该属性应用于类型为数组或 `IEnumerable<T>` 的属性上。

由于元数据是随导出一起应用的，因此匹配 Add 导出的属性类型是 `Lazy<IBinaryOperation, SpeedMetadata>` 的数组（代码文件 `UICalculator/SimpleCalculator/Calculator.cs`）：

```csharp
[ImportMany("Add")]
public Lazy<IBinaryOperation, SpeedMetadata>[] AddMethods { get; set; }
```

`ImportMany` 将在下一节中更详细地解释。`Lazy` 类型允许使用泛型定义 `Lazy<T, TMetadata>` 来访问元数据。类 `Lazy<T>` 用于在首次使用时支持类型的延迟初始化。`Lazy<T, TMetadata>` 派生自 `Lazy<T>`，除了基类之外，还支持通过 `Metadata` 属性访问元数据信息。

对 Add 方法的调用现在改为遍历 `Lazy<IBinaryOperation, SpeedMetadata>` 元素的集合。通过 `Metadata` 属性检查该功能的关键；如果 `Speed` 功能的值为 `Speed.Fast`，则使用 `Lazy<T>` 的 `Value` 属性调用操作来调用操作（代码文件 `UICalculator/SimpleCalculator/Calculator.cs`）：

```csharp
public double Operate(IOperation operation, double[] operands)
{
    double result = 0;
    switch (operation.Name)
    {
        case "+":
            foreach (var addMethod in AddMethods)
            {
                if (addMethod.Metadata.Speed == Speed.Fast)
                {
                    result = addMethod.Value.Operation(operands[0], operands[1]);
                }
            }
            break;
        // etc.
```

## 使用元数据进行延迟加载

使用元数据进行 Microsoft Composition 不仅有助于根据元数据信息选择部件。另一个很好的用途是，在部件实例化之前向宿主应用程序提供有关该部件的信息。

以下示例实现了为计算器扩展 FuelEconomy 和 TemperatureConversion 提供标题、描述以及图像链接（代码文件 `UICalculator/CalculatorUtils/CalculatorExtensionMetadataAttribute.cs`）：

```csharp
[MetadataAttribute]
[AttributeUsage(AttributeTargets.Class)]
public class CalculatorExtensionMetadataAttribute : Attribute
{
    public string Title { get; set; }
    public string Description { get; set; }
    public string ImageUri { get; set; }
}
```

对于一个部件，会应用 `CalculatorExtensionMetadata` 特性。以下是一个示例——`FuelCalculatorExtension`（代码文件 `UICalculator/FuelEconomyShared/FuelCalculatorExtension.cs`）：

```csharp
[Export(typeof(ICalculatorExtension))]
[CalculatorExtensionMetadata(
    Title = "Fuel Economy",
    Description = "Calculate fuel economy",
    ImageUri = "Images/Fuel.png")]
public class FuelCalculatorExtension : ICalculatorExtension
{
    private object _control;
    public object UI => _control ?? (_control = new FuelEconomyUC());
}
```

部件可能会消耗大量内存。如果用户没有实例化该部件，就没有必要消耗这部分内存。相反，可以在实例化之前访问标题、描述和图像，以向用户提供有关该部件的信息。

## 导入部件

现在让我们看看如何使用用户控件部件与宿主应用程序。WPF 宿主应用程序的设计视图如图 26.6 所示。

![](img/3d365b72b289213a91ade7eb366b8f35_972_0.png)

**Figure 26.6**

对于每种部件类型，都会创建单独的导入、管理器和视图模型。对于使用实现 `ICalculator` 接口的部件，使用 `CalculatorImport` 来定义导入，使用 `CalculatorManager` 来创建 `CompositionHost` 并加载部件，使用 `CalculatorViewModel` 来定义绑定到用户界面的属性和命令。对于使用实现 `ICalculatorExtension` 接口的部件，则相应地定义 `CalculatorExtensionImport`、`CalculatorExtensionManager` 和 `CalculatorExtensionViewModel`。

让我们从 `CalculatorImport` 类开始。在第一个示例中，只是在 `Program` 类中定义了一个属性来导入部件。最好为导入定义一个单独的类。通过这个类，你还可以定义一个用 `OnImportsSatisfied` 属性标注的方法。该属性标记在导入匹配时被调用的方法。在示例代码中，会触发 `ImportsSatisfied` 事件。`Calculator` 属性应用了 Import 属性。这里的类型是 `Lazy<ICalculator>`，用于延迟实例化。部件仅在访问 `Lazy` 类型的值时才会被实例化（代码文件 `UICalculator/CalculatorViewModels/CalculatorImport.cs`）：

```csharp
public class CalculatorImport
{
    public event EventHandler<ImportEventArgs> ImportsSatisfied;

    [Import]
    public Lazy<ICalculator> Calculator { get; set; }

    [OnImportsSatisfied]
    public void OnImportsSatisfied()
    {
        ImportsSatisfied?.Invoke(this,
            new ImportEventArgs
            {
                StatusMessage = "ICalculator import successful"
            });
    }
}
```

`CalculatorManager` 类在构造函数中实例化 `CalculatorImport` 类。通过 `InitializeContainer` 方法，实例化 `ContainerConfiguration` 类以使用传递给该方法的类型创建 `CompositionHost` 容器。`SatisfyImports` 方法将导出与导入匹配（代码文件 `UICalculator/CalculatorViewModels/CalculatorManager.cs`）：

```csharp
public class CalculatorManager
{
    private CalculatorImport _calcImport;
    public event EventHandler<ImportEventArgs> ImportsSatisfied;

    public CalculatorManager()
    {
        _calcImport = new CalculatorImport();
        _calcImport.ImportsSatisfied += (sender, e) =>
        {
            ImportsSatisfied?.Invoke(this, e);
        };
    }

    public void InitializeContainer(params Type[] parts)
    {
        var configuration = new ContainerConfiguration().WithParts(parts);
        using (CompositionHost host = configuration.CreateContainer())
        {
            host.SatisfyImports(_calcImport);
        }
    }
    // etc.
}
```

`CalculatorManager` 的 `GetOperators` 方法调用 `Calculator` 的 `GetOperations` 方法。该方法用于在用户界面中显示所有可用的运算符。一旦定义了计算，就会调用 `InvokeCalculator` 方法来传递操作和操作数，进而在计算器中调用 `Operate` 方法（代码文件 `UICalculator/CalculatorViewModels/CalculatorManager.cs`）：

```csharp
public class CalculatorManager
{
    // etc.
    public IEnumerable<IOperation> GetOperators() =>
        _calcImport.Calculator.Value.GetOperations();
}
```

