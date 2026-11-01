

带有用户界面并实现 `ICalculatorExtension` 接口的加载项。要连接到部件的导出，需要导入。

导入连接到导出。使用导出部件时，需要导入来建立连接。使用 `Import` 特性，可以连接到单个导出。如果应加载多个加载项，则需要 `ImportMany` 特性，并且需要将其定义为数组类型或 `IEnumerable<T>`。由于宿主计算器应用程序允许加载许多实现 `ICalculatorExtension` 接口的计算器扩展，因此类 `CalculatorExtensionImport` 定义了类型为 `IEnumerable<ICalculatorExtension>` 的属性 `CalculatorExtensions`，以访问所有计算器扩展部件。

![](img/d7d2ffa0a76feaab821930e95daace93_824_0.png)

图 28-3

```
using System.Collections.Generic;
using System.ComponentModel.Composition;

namespace Wrox.ProcSharp.MEF
{
    public class CalculatorExtensionImport
    {
        [ImportMany(AllowRecomposition=true)]
        public IEnumerable<ICalculatorExtension> CalculatorExtensions { get; set; }
    }
}
```

代码片段 WPFCalculator/CalculatorExtensionImport.cs

`Import` 和 `ImportMany` 特性允许使用 `ContractName` 和 `ContractType` 将导入映射到导出。这些特性还可以设置的其他属性包括 `AllowRecomposition` 和 `RequiredCreationPolicy`。`AllowRecomposition` 允许在应用程序运行时动态映射到新的导出，也允许卸载导出。使用 `RequiredCreationPolicy`，您可以选择部件在请求者之间是共享（`CreationPolicy.Shared`）还是不共享（`CreationPolicy.NonShared`），或者策略是否应由容器定义（`CreationPolicy.Any`）。

为了确认所有导入都成功，可以实现 `IPartImportsSatisfiedNotification` 接口。此接口仅定义了一个方法 `OnImportsSatisfied()`，当类的所有导入都成功时会调用该方法。在 `CalculatorImport` 类中，该方法触发 `ImportsSatisfied` 事件：

```
using System;
using System.ComponentModel.Composition;
using System.Windows.Controls;

namespace Wrox.ProcSharp.MEF
{
    public class CalculatorImport : IPartImportsSatisfiedNotification
    {
        public event EventHandler<ImportEventArgs> ImportsSatisfied;

        [Import(typeof(ICalculator))]
        public ICalculator Calculator { get; set; }

        public void OnImportsSatisfied()
        {
            if (ImportsSatisfied != null)
            ImportsSatisfied(this, new ImportEventArgs {
                StatusMessage = "ICalculator import successful" });
        }
    }
}
```

代码片段 WPFCalculator/CalculatorImport.cs

`CalculatorImport` 的事件在创建 `CalculatorImport` 时连接到事件处理程序，以将消息写入 `TextBlock` 来显示状态信息：

```
private void InitializeContainer()
{
    var catalog = new DirectoryCatalog(
        Properties.Settings.Default.AddInDirectory);
    container = new CompositionContainer(catalog);
    calcImport = new CalculatorImport();
    calcImport.ImportsSatisfied += (sender, e) =>
    {
        textStatus.Text += String.Format("{0}\n", e.StatusMessage);
    };
    container.ComposeParts(calcImport);
    InitializeOperations();
}
```

代码片段 WPFCalculator/MainWindow.xaml.cs

## 部件的延迟加载

默认情况下，部件是从容器中加载的，例如通过调用 `CompositionContainer` 上的扩展方法 `ComposeParts()`。借助 `Lazy<T>` 类，可以在首次访问时加载部件。类型 `Lazy<T>` 允许延迟实例化任何类型 T，并定义了属性 `IsValueCreated` 和 `Value`。`IsValueCreated` 是一个布尔值，返回所包含的类型 T 是否已实例化的信息。`Value` 在首次访问时初始化所包含的类型 T 并返回实例。

加载项的导入可以声明为 `Lazy<T>` 类型，如 `Lazy<ICalculator>` 示例所示。

```
[Import(typeof(ICalculator))]
public Lazy<ICalculator> Calculator { get; set; }
```

代码片段 WPFCalculator/CalculatorImport.cs

调用导入的属性也需要一些更改，以访问 `Lazy<T>` 类型的 `Value` 属性。`calcImport` 是类型为 `CalculatorImport` 的变量。`Calculator` 属性返回 `Lazy<ICalculator>`。`Value` 属性延迟实例化导入的类型并返回 `ICalculator` 接口，现在可以调用 `GetOperations()` 方法从计算器加载项获取所有支持的操作。

```
private void InitializeOperations()
{
    Contract.Requires(calcImport != null);
    Contract.Requires(calcImport.Calculator != null);

    var operators = calcImport.Calculator.Value.GetOperations();
    foreach (var op in operators)
    {
        var b = new Button();
        b.Width = 40;
```

要动态移除导出，可在 `MenuItem` 标头内的 `CheckBox` 控件上设置 `Unchecked` 事件。可以从 `MenuItem` 控件的 `Tag` 属性访问 `ICalculatorExtension`，因为它在先前的代码片段中已设置。要从容器中移除部件，必须创建一个包含要移除部件的 `CompositeBatch` 对象。`CompositeBatch` 类的 `RemovePart()` 方法需要 `ComposablePart` 对象；对于特性化对象没有重载。借助 `AttributedModelServices` 类，可以使用 `CreatePart()` 方法从特性化对象创建 `ComposablePart`。然后将 `CompositionBatch` 传递给 `CompositionContainer` 的 `Compose()` 方法，以从容器中移除该部件：

```
```csharp
menuCheck.Unchecked += (sender1, e1) =>
{
    MenuItem mi = (sender1 as CheckBox).Tag as MenuItem;
    ICalculatorExtension ext = mi.Tag as ICalculatorExtension;
    ComposablePart part = AttributedModelServices.CreatePart(ext);
    var batch = new CompositionBatch();
    batch.RemovePart(part);
    container.Compose(batch);
    MenuItem parentMenu = mi.Parent as MenuItem;
    parentMenu.Items.Remove(mi);
};
```
```

> 仅当 `Import` 特性的 `AllowRecomposition` 属性设置为 true 时，才能移除部件。

使用导出提供程序，您可以通过实现 `ExportsChanged` 事件的处理程序来获取有关添加和移除的导出的信息。类型为 `ExportsChangedEventArgs` 的参数 e 包含已添加导出和已移除导出的列表，这些列表会被写入 `TextBlock` 控件：

```
```csharp
var container = new CompositionContainer(catalog);
container.ExportsChanged += (sender, e) =>
{
    var sb = new StringBuilder();

    foreach (var item in e.AddedExports)
    {
        sb.AppendFormat("added export {0}\n", item.ContractName);
    }
    foreach (var item in e.RemovedExports)
    {
        sb.AppendFormat("removed export {0}\n", item.ContractName);
    }
    this.textStatus.Text += sb.ToString();
};
```
```

## 目录

目录定义了 MEF 搜索所需部件的位置。示例应用程序使用 `DirectoryCatalog` 从指定目录加载包含部件的程序集。使用 `DirectoryCatalog`，您可以通过 `Changed` 事件获取更改信息，并遍历所有添加和移除的定义。`DirectoryCatalog` 本身不注册文件系统更改。相反，您需要调用 `DirectoryCatalog` 的 `Refresh()` 方法，如果自上次读取以来发生了更改，则会触发 `Changing` 和 `Changed` 事件。

```
```csharp
private void InitializeContainer()
{
    catalog = new DirectoryCatalog(Properties.Settings.Default.AddInDirectory);
    container = new CompositionContainer(catalog);
```
```

底部显示状态信息。您还可以从加载项目录中移除 `ICalculatorExtender` 加载项（在应用程序未运行时），在应用程序运行时将加载项复制到目录中，然后刷新加载项以在运行时查看新的加载项。

![](img/d7d2ffa0a76feaab821930e95daace93_830_0.png)

图 28-4

## 总结

在本章中，您了解了 .NET 4 中的一项新技术：MEF。MEF 实现使用特性来查找和连接加载项。您了解了如何创建和加载加载项，以及使用接口或方法进行导出的可能性。您学习了如何使用目录动态查找加载项，以及如何使用容器将导入映射到导出。

本书还有另一章关于加载项的内容：在线第 50 章介绍了 MAF，它通过单独的应用域和单独的进程在宿主和加载项之间提供了更好的分离，但开发成本也更高。

下一章将介绍如何读写文件、目录和注册表。

