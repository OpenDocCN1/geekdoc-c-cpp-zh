

# 在 647 上上手你的 ViewModel

# 依赖注入 (DI)

此架构中的 ViewModel 依赖于获取客户数据和销售区域数据。在实际环境中，硬编码伪存储库（repositories）并不是一个好主意。我曾不止一次在发布软件时，代码中仍留有测试值：“我会在发布前修改那个的”——这种想法在发布的两步走流程中往往会化为乌有。

依赖注入是一种技术，它要求需要依赖的类获取这些依赖项。这有助于防止这种情况发生。WPF 中依赖注入的常用工具是 Unity，但也存在许多其他高质量的开源工具，例如 Ninject。在大多数情况下，用代码自己实现一套 DI 并不难（请参考网站 http://sharp102.info）。依赖注入远超本书的涉及范围，但它是软件开发中一种极具价值的模式。

实用 WPF

# 列表 2-45：视图代码代码（Code-Behind）

```sharp
public class CustomerMaintenance : Window
{
    public CustomerMaintenance()
    {
        InitializeComponent();
        DataContext = new CustomerMaintenanceViewModel();
    }
}
```

等等！我们不是说过想从代码后文件中移除所有代码吗？并不是所有代码，是几乎所有的代码。包含逻辑的事件处理程序是肯定的。但构造函数中必须保留两行代码：`Initialize()`，它负责渲染所有的 XAML，以及 `DataContext` 的赋值。你可能会遇到在代码后文件中添加额外代码逻辑的情况，而这些情况可能是完全有效的。在开始于无法测试或重用的地方添加代码之前，请进行批判性思考。

使用 ViewModel 模式后，命令绑定（Command Binding）表达式会变得非常不同。正如列表 4-26 所示，它们实际上变得更简单了一些。因为基类将命令挂钩到 CommandManager，因此消除了 `Windows.CommandBindings` 部分的需求。

# 列表 2-46：添加客户按钮的 XAML

```xml
<Button HorizontalAlignment="Right" Margin="3,0,3,0"
    Command="Binding Path=AddCustomerCmd"
    CommandParameter="Binding Path=Customers"
    Content="Binding RelativeSource=(RelativeSource Mode=Self),Path=Command.Text"/>/>
```

# 648 上手你的 ViewModel

内容与之前的示例没有变化。

同样，ComboBox 将其 `ItemsSource` 属性绑定到 ViewModel 中的 `IList<T>` 属性。列表 2-4 显示了窗口上 ComboBox 的 XAML 如何。

# 列表 2-4：带有 ViewModel 的 ComboBox XAML

```xml
<ComboBox ItemsSource="{Binding Path=Customers}"
    DisplayMemberPath="Name" />
<ComboBox ItemsSource="{Binding Path=Regions}"
    DisplayMemberPath="Name"
    SelectedItem="{Binding ElementName=CustomerList, Path=SelectedItem.SalesRegion}"/>
```

第二个 ComboBox 显示了 WPF 数据绑定的威力。`SelectedItem` 被设置为客户 `SalesRegion` 属性的值。通过绑定实现这一点，是将项设置为 `CustomerList` 的 `SelectedItem`。这返回了一个 Customer 对象，允许在 Path 中选择该 Customer 的任何属性（在本例中为 SalesRegion 属性）。

# 总结

最近我询问使用 ViewModel 模式是否值得，因为看起来需要大量的额外工作。这是 WPF 开发人员的一个共同话题，考虑到该模式的新颖性、实际应用中的各种变体以及对该主题的冲突性意见，这并不令人意外。

简而言之，绝对值得。ViewModel 带来的最大好处是具有可测试规模的真正的关注点分离。每当你可以做到这一点，这种价值就体现出来了。

