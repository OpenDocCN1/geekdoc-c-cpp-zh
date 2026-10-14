

| 操作 | 执行方法 |
|---|---|
| 创建一个新的 UWP 应用 | 使用 Visual Studio 2015 中的 UWP 模板之一，例如 Blank App 模板。 |
| 实现可缩放至不同设备形态和方向的用户界面 | 使用 *Grid* 控件。将 *Grid* 控件划分为行和列，并将控件放置在这些行和列中，而不是相对于 *Grid* 边缘指定绝对位置。 |
| 实现可适应不同显示宽度的用户界面 | 为每个视图创建不同的布局，以适当的方式显示控件。使用 Visual State Manager 在视觉状态更改时选择要显示的布局。 |
| 创建自定义样式 | 向应用添加资源字典。使用 `<Style>` 元素在此字典中定义样式，并指定每个样式更改的属性。例如：
```
<Style x:Key="GridStyle" TargetType="Grid">
    <Setter Property="Background" Value="{StaticResource WoodBrush}"/>
</Style>
``` |
| 将自定义样式应用于控件 | 设置控件的 *Style* 属性并按名称引用样式。例如：
```
<Grid Style="{StaticResource GridStyle}">
``` |

## 第 26 章 在 Universal Windows Platform 应用中显示和搜索数据

完成本章后，你将能够：

- 解释如何使用 Model-View-ViewModel 模式来实现 Universal Windows Platform 应用的逻辑。
- 使用数据绑定在视图中显示和修改数据。
- 创建视图可以与模型交互的 ViewModel。
- 将 Universal Windows Platform 应用与 Cortana 集成以提供语音激活的搜索功能。

第 25 章“为 Universal Windows Platform 应用实现用户界面”演示了如何设计可适应客户运行你的应用时可能使用的不同设备形态、方向和视图的用户界面（UI）。该章中开发的示例应用是一个简单的应用，旨在显示和编辑客户的详细信息。

在本章中，你将了解如何在 UI 中显示数据，并学习 Windows 10 中用于在应用中搜索数据的功能。在执行这些任务时，你还将了解如何构建 UWP 应用的结构。本章涵盖了大量内容。特别是，你将了解如何使用数据绑定将 UI 连接到其显示的数据，以及如何创建 ViewModel 以将用户界面逻辑与应用的数据模型和业务逻辑分离。你还将了解如何将 UWP 应用与 Cortana 集成以使用户能够执行语音激活的搜索。

### 实现 Model-View-ViewModel 模式

结构良好的图形应用将用户界面的设计与应用使用的数据以及构成应用功能的业务逻辑分离。这种分离有助于消除各个组件之间的依赖关系，使能够在无需更改业务逻辑或底层数据模型的情况下以不同方式呈现数据。这种方法还为不同元素由具有适当专业技能的人员设计和实现扫清了道路。例如，图形艺术家可以专注于设计有吸引力且直观的 UI，数据库专家可以专注于实现用于存储和访问数据的优化数据结构，而 C# 开发者可以将她的精力集中在实现应用的业务逻辑上。这是许多开发方法共同的目标，而不仅仅是 UWP 应用，过去几年中已经设计出许多技术来帮助以这种方式构建应用。

可以说，最流行的方法是遵循 Model-View-ViewModel（MVVM）设计模式。在此设计模式中，模型提供应用使用的数据，而视图表示数据在 UI 中显示的方式。ViewModel 包含连接两者的逻辑，将用户输入转换为对模型执行业务操作的命令，并将数据从模型中取出并以视图期望的方式格式化。以下图表显示了 MVVM 模式元素之间简化的关系。请注意，应用可能提供同一数据的多个视图。例如，在 UWP 应用中，你可能会实现不同的视图状态，这些状态可以使用不同的屏幕布局来呈现信息。ViewModel 的一项工作是确保来自同一模型的数据可以由许多不同的视图显示和操作。在 UWP 应用中，视图可以利用数据绑定连接到 ViewModel 呈现的数据。此外，视图可以请求 ViewModel 更新模型中的数据或通过调用 ViewModel 实现的命令来执行业务任务。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_763_0.png)

### 使用数据绑定显示数据

在为 Customers 应用实现 ViewModel 之前，先了解更多关于数据绑定以及如何将此技术应用于在 UI 中显示数据会有所帮助。使用数据绑定，你可以将控件的属性链接到对象的属性；如果指定对象的属性值更改，则链接到该对象的控件中的属性也会更改。此外，数据绑定可以是双向的：如果使用数据绑定的控件中的属性值更改，则修改会传播到控件所链接的对象。以下练习提供了数据绑定用于显示数据方式的快速介绍。它基于第 25 章的 Customers 应用。

### 使用数据绑定显示 Customer 信息

- 1. 如果尚未运行，请启动 Visual Studio 2015。
- 2. 打开 Customers 项目，该项目位于你的 Documents 文件夹中的 \Microsoft Press\VCSBS\Chapter 26\Data Binding 文件夹中。

这是第 25 章中开发的 Customers 应用的一个版本，但 UI 的布局已略微修改——控件显示在蓝色背景上，使其更容易突出。

### 注意

蓝色背景是通过使用跨越与显示标题和数据的 TextBlock 和 TextBox 控件相同的行和列的 Rectangle 控件创建的。矩形使用 LinearGradientBrush 填充，该画刷使矩形的颜色从顶部较浅的蓝色逐渐变为底部的非常深的蓝色。显示在 customersTabularView Grid 控件视图中的 Rectangle 控件的 XAML 标记如下所示（customersColumnarView Grid 控件的 XAML 标记包含一个类似的 Rectangle 控件，跨越该布局使用的行和列）：

点击此处查看代码图像

```
<Rectangle Grid.Row="0" Grid.RowSpan="6" Grid.Column="1" Grid.ColumnSpan="7" ...>
    <Rectangle.Fill>
        <LinearGradientBrush EndPoint="0.5,1" StartPoint="0.5,0">
            <GradientStop Color="#FF0E3895"/>
            <GradientStop Color="#FF141415" Offset="0.929"/>
        </LinearGradientBrush>
    </Rectangle.Fill>
</Rectangle>
```

- 3. 在 Solution Explorer 中，右键单击 Customers 项目，指向 Add，然后单击 Class。

- 4. 在 Add New Items – Customers 对话框中，确保选择了 Class 模板。在 Name 框中，键入 Customer.cs，然后单击 Add。

你将使用此类来实现 Customer 数据类型，然后实现数据绑定以在 UI 中显示 Customer 对象的详细信息。

- 5. 在显示 Customer.cs 文件的 Code and Text Editor 窗口中，将 Customer 类设为 public 并添加以下以粗体显示的私有字段和属性：

点击此处查看代码图像

```
public class Customer
{
    public int _customerID;
    public int CustomerID
    {
        get { return this._customerID; }
```

