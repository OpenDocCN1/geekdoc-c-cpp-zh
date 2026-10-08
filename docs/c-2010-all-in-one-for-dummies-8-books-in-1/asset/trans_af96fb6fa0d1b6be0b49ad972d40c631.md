

# 第 3 章：WPF 中的数据绑定

本章内容

- 理解依赖属性
- 理解绑定模式
- 定义一个示例绑定对象
- 编辑、转换和数据视觉化

数据绑定允许将你的应用程序对象（绑定源）中的数据显示在你的用户界面元素（绑定目标）中。这意味着你可以将 `TextBox` 的 `Text` 属性（例如）绑定到 `Car` 类实例的 `Name` 属性上。根据设置该关系时使用的绑定模式，`TextBox` 的 `Text` 属性值的更改会自动更新你的 `Car` 对象的底层 `Name` 属性（反之亦然），而无需任何代码。

在如今，大多数应用程序都处理数据已不是什么秘密了。作为一名 WPF 开发人员，你对数据的展示方式拥有完全的创意权，用户输入的信息也可以被验证并用于更新你的底层对象。WPF 的优势之一就是丰富的数据绑定支持。本章将带你了解这些细节。

# 认识依赖属性

当你在绑定源与绑定目标属性之间建立关系时，就会发生绑定。绑定目标对象必须是一个 `DependencyObject`，而目标属性必须是一个 `DependencyProperty`。

理解依赖属性对于牢掌握 WPF 技术至关重要。依赖属性存在于自 `DependencyObject` 的对象中。从根本上说，依赖属性通过增加一组服务（也称为 WPF 属性系统）扩展了 CLR 对象上已有的普通属性的功能（`DependencyObject` 和 `DependencyProperty` 共同构成了该属性系统）。依赖属性的值可以由多个输入源决定，这意味着它们的值可以通过 `Style` 或数据绑定表达式获取。依赖属性的作用类似于普通属性，允许你根据以下内容设置值：

- 默认值：这些值在属性上是预先定义的。
- 计算表达式（类似于 Web 领域中的 CSS 表达式）：这可以是一个数据绑定表达式，也可以是对应用程序定义的资源的引用。
- 数据绑定：这实际上是建立在上述项目之上的，但是绑定在源对象上。
- 属性值继承：不要与对象继承混淆，属性继承允许设置属性的值传播到其子元素。例如，如果你在 `Window` 元素（根元素）上设置了 `FontSize` 值，子元素如 `TextBlock` 和 `Label` 会自动继承这些属性。你可以通过查看第 1 章中引入的附加属性（Attached Properties）概念来看到另一个示例。
- 样式：每个样式通常包含用于设置一个或多个属性值的 setter（设置器）。

WPF 属性系统提供了内置的属性值更改通知和属性值验证功能，我将在本章详细介绍。

归根结底，依赖属性赋予了开发者在 XAML 和代码中直接设置属性值的能力。它的优点是你可以保持代码整洁，并将对象的属性初始化留给 XAML。

# 探索绑定模式

你对所创建的绑定关系的行为具有完全控制权。WPF 提供了多种绑定模式，包括：

- `OneTime`（一次性）绑定模式用于源属性仅在初始时设置目标值。源属性的后续更改不会反映在目标属性中。同样，目标属性的更改也不会反映在源属性中。
- `OneWay`（单向）绑定模式通常用于只读行为的属性。在这种绑定模式下，源属性的数据设置目标属性的初始值。源属性的后续更改将自动更新绑定目标属性的值。相反，对目标属性值的任何后续更改都不会反映在源属性中。
- `OneWayToSource`（单向到源）绑定模式本质上是 `OneWay` 绑定模式的反面。在这种模式下，源属性的数据初始化目标属性值。源属性值的后续更改不会更新目标属性。然而，对目标属性值的更新将自动更新源属性。
- `TwoWay`（双向）绑定模式合并了 `OneWay` 和 `OneWayToSource` 绑定模式的功能。在这种模式下，源属性的值初始化目标属性值。源属性值的后续更改将更新目标属性值。同样，对目标属性值的更新将更新源属性。

# 调查绑定对象

绑定可以使用代码或 XAML 定义。这里我们从 XAML 版本开始。为了看到如何将数据绑定到 UI 元素，我们首先定义一组用于测试的数据。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_606_0.png)

完整的解决方案可以在 www.csharpfordummies.net 的章节下载中通过 `BindingSample1` 找到。

# 使用 XAML 定义绑定

按照以下步骤使用 XAML 创建绑定：

1. 创建一个新的 WPF 项目，命名为 `BindingSample1`。
2. 通过向解决方案添加一个名为 `Car.cs` 的新类来定义简单的 `Car` 类。代码如下：

```assembly
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace BindingSample
{
    public class Car
    {
        private string _make;

        public string Make
        {
            get { return _make; }
            set { _make = value; }
        }
        private string _model;
        public string Model
        {
            get { return _model; }
            set { _model = value; }
        }
        public Car()
        {
        }
    }
}
```

3. 在 `MainWindow.xaml` 中，替换 `grid` 以定义列和行。在每个网格单元中添加一个标签：

```xml
<Grid>
  <Grid.ColumnDefinitions>
    <ColumnDefinition/>
    <ColumnDefinition/>
  </Grid.ColumnDefinitions>
  <Grid.RowDefinitions>
    <RowDefinition/>
  </Grid.RowDefinitions>
  <Label Name="lblCarMake" Grid.Row="0" Grid.Column="0" Content="{Binding Make, Mode=OneWay}" />
  <Label Name="lblCarModel" Grid.Row="0" Grid.Column="1" Content="{Binding Model, Mode=OneWay}" />
</Grid>
```

4. 打开 `MainWindow.xaml` 后置代码，创建一个 `GenerateData` 方法，实例化 `Car` 对象并将其赋值给窗口的 `DataContext`：

```csharp
private void GenerateData()
{
    Car car = new Car() { Make = "Aton", Model = "XYZ" };
    this.DataContext = car;
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_607_0.png)

DataContext 定义了所有元素获取其值的根对象（只要子元素的 DataContext 值没有直接由 XAML 直接设置）。

5. 在 `MainWindow` 构造函数中，紧接 `InitializeComponent()` 之后调用 `GenerateData()` 方法。

```csharp
public MainWindow()
{
    InitializeComponent();
    GenerateData();
}
```

现在，回到 XAML 文件 (MainWindow.xaml)，第一个标签 `lblCarMake` 将绑定到 `DataContext` 属性。值是从 Path 组件指定的属性中检索的。同样，第二个标签 `lblCarModel` 将绑定到 `DataContext` 的 `Model` 属性，正如绑定表达式 Path 所示。这些绑定都使用 `OneWay` 模式，这意味着无论底层属性如何更改，标签只会绑定一次。

6. 运行应用程序。

你可以看到标签现在了赋值给窗口 DataContext 的 Car 对象的 `Make` 和 `Model`。（参见图 3-1。）

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_608_0.png)

# 使用 C# 定义绑定

绑定也可以完全通过 XAML 文件中的两个标签来完成。现在 XAML 标记应该移除以下内容：

```xml
<Label Name="lblCarMake" Grid.Row="0" Grid.Column="0" />
<Label Name="lblCarModel" Grid.Row="0" Grid.Column="1" />
```

修改 `MainWindow.xaml` 中的 `GenerateData()` 方法，在代码中实现绑定定义。为了实现这一点，你必须直接实例化 `Binding` 对象。`Binding` 对象的构造函数接收字符串 Path 值。使用 `BindingOperations` 类将绑定应用到标签的 `Content` 属性上。

