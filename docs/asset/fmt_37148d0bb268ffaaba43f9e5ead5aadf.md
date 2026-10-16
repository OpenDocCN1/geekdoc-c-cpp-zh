
```
#if WPF
using TemperatureConversionWPF;
#endif
#if WINDOWS_UWP
using TemperatureConversionUWP;
#endif
using System.Composition;

namespace Wrox.ProCSharp.Composition
{
    [Export(typeof(ICalculatorExtension))]
    [CalculatorExtensionMetadata(
        Title ="Temperature Conversion",
        Description ="Temperature conversion",
        ImageUri ="Images/Temperature.png")]
    public class TemperatureConversionExtension:
ICalculatorExtension
    {
```

```
private object _control;
public object UI =>
	_control ?? (_control = new TemperatureConversionUC());
}
```

目前，忽略上一段代码片段中使用的 `CalculatorExtension` 属性。它将在本章后面的“导出元数据”部分进行解释。

第二个实现接口 `ICalculatorExtension` 的用户控件是 `FuelEconomy`。使用此控件，可以计算每加仑英里数或每 100 公里升数。用户界面如图 26.5 所示。

![](img/3d365b72b289213a91ade7eb366b8f35_965_0.png)

下面的代码片段显示了类 `FuelEconomyViewModel`，它定义了多个从用户界面绑定的属性，例如 `FuelEcoTypes` 列表，使用户可以在英里和公里之间选择，以及由用户填充的 `Fuel` 和 `Distance` 属性（代码文件 UI Calculator/FuelEconomyShared/FuelEconomyViewModel.cs）：

```
public class FuelEconomyViewModel: BindableBase
{
	public FuelEconomyViewModel()
	{
		InitializeFuelEcoTypes();
		CalculateCommand = new DelegateCommand(OnCalculate);
	}
}
```

```
}

public DelegateCommand CalculateCommand { get; }

// etc.

public List<FuelEconomyType> FuelEcoTypes { get; } =
    new List<FuelEconomyType>();

private void InitializeFuelEcoTypes()
{
    var t1 = new FuelEconomyType
    {
        Id ="lpk",
        Text ="L/100 km",
        DistanceText ="Distance (kilometers)",
        FuelText ="Fuel used (liters)"
    };
    var t2 = new FuelEconomyType
    {
        Id ="mpg",
        Text ="Miles per gallon",
        DistanceText ="Distance (miles)",
        FuelText ="Fuel used (gallons)"
    };
    FuelEcoTypes.AddRange(new FuelEconomyType[] { t1, t2 });
}

private FuelEconomyType _selectedFuelEcoType;

public FuelEconomyType SelectedFuelEcoType
{
    get { return _selectedFuelEcoType; }
    set { SetProperty(ref _selectedFuelEcoType, value); }
}

private string _fuel;
public string Fuel
{
    get { return _fuel; }
    set { SetProperty(ref _fuel, value); }
}

private string _distance;
public string Distance
{
    get { return _distance; }
    set { SetProperty(ref _distance, value); }
}

private string _result;
public string Result
{
    get { return _result; }
    set { SetProperty(ref _result, value); }
}
}
```

> 注意 与示例代码一起使用的基类 `BindableBase` 只是提供了接口 `INotifyPropertyChanged` 的实现。此类位于 `CalculatorUtils` 项目中。

计算在 `OnCalculate` 方法内进行。`OnCalculate` 是计算按钮的 `Click` 事件的处理程序（代码文件 UICalculator/FuelEconomyShared/FuelEconomyViewModel.cs）：

```
public void OnCalculate()
{
    double fuel = double.Parse(Fuel);
    double distance = double.Parse(Distance);
    FuelEconomyType ecoType = SelectedFuelEcoType;
    double result = 0;
    switch (ecoType.Id)
    {
        case"lpk":
            result = fuel / (distance / 100);
            break;
        case"mpg":
            result = distance / fuel;
            break;
        default:
            break;
    }
    Result = result.ToString();
}
```

再次，接口 `ICalculatorExtension` 被实现并通过 `Export` 属性导出（代码文件 UICalculator/FuelEconomyShared/FuelCalculatorExtension.cs）：

```
[Export(typeof(ICalculatorExtension))]
[CalculatorExtensionMetadata(
    Title ="Fuel Economy",
    Description ="Calculate fuel economy",
    ImageUri ="Images/Fuel.png")]
public class FuelCalculatorExtension: ICalculatorExtension
{
    private object _control;
    public object UI => _control ?? (_control = new FuelEconomyUC());
}
```

在继续主机应用程序导入用户控件之前，让我们看看导出还有哪些其他选项。部件本身可以导入其他部件，并且可以向导出添加元数据信息。

### 部件使用部件

`Calculator` 类现在不再直接实现 `Add` 和 `Subtract` 方法，而是使用执行这些操作的其它部件。为了定义提供单一操作的部件，接口 `IBinaryOperation` 被定义（代码文件 UICalculator/CalculatorContract/IBinaryOperation.cs）：

```
public interface IBinaryOperation
{
    double Operation(double x, double y);
}
```

类 `Calculator` 定义了一个属性，其中匹配的 `Subtract` 方法的部件将被导入。导入被命名为 `Subtract`，因为并非所有 `IBinaryOperation` 的导出都是必需的——只需要命名为 `Subtract` 的导出（代码文件 `UICalculator/SimpleCalculator/Calculator.cs`）：

```
[Import("Subtract")]
public IBinaryOperation SubtractMethod { get; set; }
```

类 `Calculator` 中的 `Import` 与 `SubtractOperation` 的 `Export` 匹配（代码文件 `UICalculator/AdvancedOperations/Operations.cs`）：

```
[Export("Subtract", typeof(IBinaryOperation))]
public class SubtractOperation: IBinaryOperation
{
    public double Operation(double x, double y) => x-y;
}
```

现在只需更改 `Calculator` 类的 `Operate` 方法的实现即可使用内部部件。`Calculator` 本身无需创建容器来匹配内部部件。只要导出的部件在已注册的类型或程序集中可用，这就已由主机容器自动完成（代码文件 `UICalculator/SimpleCalculator/Calculator.cs`）：

```
public double Operate(IOperation operation, double[] operands)
{
    double result = 0;
    switch (operation.Name)
    {
        // etc.
        case"-":
            result = SubtractMethod.Operation(operands[0], operands[1]);
            break;
        // etc.
```

### 导出元数据

使用导出时，还可以附加元数据信息。元数据使您能够提供除名称和类型之外的额外信息。这可用于添加功能信息，并在导入端确定应使用哪些导出。

`Calculator` 类不仅为 `Subtract` 方法使用内部部件，也为 `Add` 方法使用内部部件。以下代码片段中的 `AddOperation` 使用名为 `Add` 的 `Export` 属性，结合 `SpeedMetadata` 属性。`SpeedMetadata` 属性指定 `Speed` 信息 `Speed.Fast`（代码文件 `UICalculator/AdvancedOperations/Operations.cs`）：

```
[Export("Add", typeof(IBinaryOperation))]
[SpeedMetadata(Speed = Speed.Fast)]
```

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

### 使用元数据进行延迟加载

使用元数据进行 Microsoft Composition 不仅有助于根据元数据信息选择部件。另一个很好的用途是，在部件实例化之前向宿主应用程序提供有关该部件的信息。

以下示例实现了为计算器扩展 FuelEconomy 和 TemperatureConversion 提供标题、描述以及图像链接（代码文件 `UICalculator/CalculatorUtils/CalculatorExtensionMetadataAttribute.cs`）：
