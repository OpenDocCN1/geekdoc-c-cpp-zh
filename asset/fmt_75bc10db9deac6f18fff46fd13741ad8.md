
（注：由于提供的文本在结尾处中断且逻辑倒置，以上翻译已完全按照您的原文物理顺序完成。）

在添加或更改控件时需要反复设置相同的属性和值时，一致性就变得非常重要。你执行同一操作的次数越多，至少出错一次的概率就越大！

在 UWP 应用中，你可以定义可重用的样式。你可以通过创建一个资源字典（resource dictionary）将其实现为应用级资源，以便应用中所有页面的控件可以使用。你还可以在该页面的 XAML 标记中定义仅适用于单个页面的本地资源。

在接下来的练习中，你将为 Customers 应用定义一些简单的样式，并将这些应用到 Customers 表单的控件上。

## 为 Customers 表单定义样式

1. 在解决方案管理器（Solution Explorer）中，右键点击 `Customers` 项目，指向 `Add`（添加），然后选择 `New Item`（新建项）。

2. 在“添加新项 – Customers”对话框的左侧面板中，选择 `Visual C#`。在中间面板中，选择 `Resource Dictionary`（资源字典）。在名称框中，选择 `AppStyles.xaml`，并点击 `Add`（添加）。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1002_0.png)

`AppStyles.xml` 文件出现在代码和文本编辑器窗口中。资源字典是一个包含应用可以使用的资源的 XAML 文件。`AppStyles.xml` 文件看起来如下：

点击此处查看代码图像

```
<ResourceDictionary

  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
</ResourceDictionary>
```

样式是资源的一种示例，你还可以添加其他项目。事实上，你将添加的第一个资源实际上并不是样式，而是一个 ImageBrush 资源，它将用于绘制 Customers 表单上外层 Grid 控件的背景。

3. 在解决方案管理器中，右键点击 `Customers` 项目，指向 `Add`（添加），然后选择 `New Folder`（新建文件夹）。将新文件夹重命名为 `Images`。

4. 右键点击 `Images` 文件夹，指向 `Add`（添加），然后选择 `Existing Item`（现有项）。

5. 在“添加项 - Customers”对话框中，浏览到文档文件夹中的 `\Microsoft Press\VCSBS\Chapter25Resources` 文件夹，选择 `wood.jpg`，然后点击 `Add`（添加）。

`wood.jpg` 文件被添加到 `Customers` 项目的 `Images` 文件夹中。该文件包含一张美味木质背景图像，你将将其用于 Customers 表单。

6. 在显示 `AppStyles.xml` 文件的代码和文本编辑器窗口中，以加粗形式添加以下 XAML 标记：

点击此处查看代码图像

```
<ResourceDictionary

  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">

  <Image x:Key="WoodBrush" ImageSource="Images/wood.jpg"/>
</ResourceDictionary>
```

此标记创建了一个名为 `WoodBrush` 的 `ImageBrush` 资源，它基于 `wood.jpg` 文件。你可以使用此图像来设置控件的背景，它将显示 `wood.jpg` 文件中的图像。

7. 在 `ImageBrush` 资源下方，在 `AppStyles.xaml` 文件中添加此处加粗所示的的样式：

点击此处查看代码图像

```
<ResourceDictionary
  ...
  <ImageBrush x:Key="WoodBrush" ImageSource="Images/wood.jpg"/>
  <Style x:Key="PageStyle" TargetType="Page">
    <Setter Property="Background" Value="StaticResource WoodBrush"/>
  </Style>
</ResourceDictionary>
```

此标记显示了如何定义样式。`Style` 元素应该有一个名称（一个允许在应用其他地方引用的键），并且应该指定样式可以应用的控件。你将此样式与 `Page` 控件配合。

样式的主体由一个或多个 `Setter` 元素组成。在本示例中，背景属性被设置为 `WoodBrush` 资源。然而，语法有点奇怪。在值中，你可以引用适当的系统定义值之一（例如如果你想将背景设置为纯红色，可以使用 `Red`），或者指定你在其他处定义的资源。要引用在其他处定义的资源，使用 `StaticResource` 关键字并将整个表达式放在花括号中。

在使用此样式之前，你必须通过在 `App.xaml` 文件中添加对 `AppStyles.xaml` 引用来更新应用的全局资源字典。

8. 在解决方案管理器中，双击 `App.xaml` 以在代码和文本编辑器窗口中显示它。`App.xaml` 文件看起来如下：

点击此处查看代码图像

```
<Application
  x:Class="Customers.App"
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  xmlns:local="using:Customers">
</Application>
```

目前，`App.xml` 文件仅定义了应用对象并引入了几个命名空间。全局资源字典是空的。

9. 在 `App.xml` 文件中添加此处加粗的代码：

点击此处查看代码图像

```
<Application
    x:Class="Customers.App"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Customers">

    <Application.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <ResourceDictionary Source="AppStyles.xml"/>
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

此标记将 `AppStyles.xml` 中定义的资源添加到全局资源字典。这些资源现在可以可以使用。

10. 在解决方案管理器中，切换到显示 UI 的 `MainPage` 文件。查看 `Page` 的标记：

```
<Page
    x:Class="Customers.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Customers">
    Background="ThemeBrush">
```

11. 在此控件的 XAML 标记中，将 `Background` 属性替换为引用 `PageStyle` 的 `Style` 属性，如下所示：

点击此处查看代码图像

```
<Page
    x:Class="Customers.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Customers">
    Style="StaticResource PageStyle">
```

12. 在 `生成` 菜单上，选择重新生成解决方案（`Rebuild Solution`）。设计视图中 `Grid` 控件的背景将切换并显示木质背景，如下：

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1006_0.png)

### 注意

确保应用于页面或控件的任何背景图像在设备因子和方向变化时保持其美感。在 30 英寸显示器上看起来很酷的图像在平板电脑上可能会失真和压缩。可能需要为不同的视图和方向提供替代背景，并使用视觉状态管理器在视觉状态更改时切换控件的背景属性。

13. 回到代码和文本编辑器窗口中的 `AppStyles.xaml`，在 `PageStyle` 样式之后添加以下 `FontStyle`：

```
<Style x:Key="PageStyle" TargetType="Page">

</Style>
<Style x:Key="FontStyle" TargetType="TextBlock">
  <Setter Property="FontFamily" Value="Segoe Print"/>
</Style>
```

此样式应用于 `Text` 元素并将字体更改为 `Segoe Print`。这种字体类似于手写体。

在此阶段，可以在每个需要此字体的 `TextBlock` 控件中引用 `FontStyle`，但这种方法与在每个控件的标记中直接设置 `FontFamily` 没有优势。样式的真正威力在于组合多个属性时，正如你将在接下来几个步骤中看到的。

14. 在 `AppStyles.xaml` 文件中添加此处所示的 `HeaderStyle` 样式：

```
<Style x:Key="FontStyle" TargetType="TextBlock">
...
</Style>
<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn="[StaticResource FontStyle]">
  <Setter Property="HorizontalAlignment" Value="Center"/>
  <Setter Property="TextWrapping" Value="Wrap"/>
</Style>
```

```xml
<Setter Property="VerticalAlignment" Value="Center"/>
<Setter Property="Foreground" Value="SteelBlue"/>
</Style>
```

这是一个复合样式，用于设置 `TextBlock` 对象的 `HorizontalAlignment`、`TextWrapping`、`VerticalAlignment` 和 `Foreground` 属性。此外，`HeaderStyle` 通过 `BasedOn` 属性引用了 `FontStyle`。`BasedOn` 属性为样式提供了简单形式的继承。

你将使用此样式对在 `customersTableView` 和 `customersColumn` 控件顶部显示的标签进行格式化。然而，这些标题具有不同的字体大小（表格布局的标题比列式布局的标题大），因此，你将创建另外两个样式来扩展 `HeaderStyle`。

15. 将此处**加粗**所示的样式添加到 `AppStyles.xaml` 文件中：

点击此处查看代码图片

```xml
<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn={StaticResource FontStyle}
  ..
</Style>
<Style x:Key="TabularHeaderStyle" TargetType="TextBlock" BasedOn={StaticResource HeaderStyle}>
  <Setter Property="FontSize" Value="40"/>
</Style>
<Style x:Key="ColumnarHeaderStyle" TargetType="TextBlock" BasedOn={StaticResource HeaderStyle}>
  <Setter Property="FontSize" Value="30"/>
</Style>
```

注意，这些样式的字体大小比 `Grid` 控件中标题当前使用的字体大小略小。这是因为 `Segoe Print` 字体比默认字体大。点击此处查看代码图片

```xml
<TextBlock Grid.Row="0" HorizontalAlignment="Center"
TextWrapping="Wrap"
```

17. 将此控件的属性更改为引用 `TabularHeaderStyle`，如下代码**加粗**所示：

点击此处查看代码图片

```xml
<TextBlock Grid.Row="0" Style={StaticResource TabularHeaderStyle}
Text="Adventure Works"/>
```

设计视图中显示的标题应该像这样改变颜色、大小和字体：img/4fc1423ece9eb794a4edb8b1746d_109_0.png

18. 找到 `customersColumnGrid` 控件中 `Customers` 标签的 `TextBlock` 控件的 XAML 标记：

点击此处查看代码图片

```xml
<TextBlock Grid.Row="0" HorizontalAlignment="Center"
TextWrapping="Wrap"
Text="Customers" VerticalAlignment="Center" FontSize="30"/>
```

将此控件的标记修改为引用 `ColumnarHeaderStyle`，如下所示：

点击此处查看代码图片

```xml
<TextBlock Grid.Row="0" Style={StaticResource ColumnarHeaderStyle}
Text="Customers"/>
```

设计视图中看不到此更改，因为 `customersColumnGrid` 默认是折叠的。但当你运行应用程序时，将会看到此更改的效果。

19. 返回编辑器中的 `AppStyles` 样式。使用示例所示的附加 `Setter` 元素修改 `HeaderStyle`：

点击此处查看代码图片

```xml
<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn="StaticResource FontStyle">
  <Setter Property="HorizontalAlignment" Value="Center"/>
  <Setter Property="TextWrapping" Value="Wrap"/>
  <Setter Property="VerticalAlignment" Value="Center"/>
  <Setter Property="Foreground" Value="SteelBlue"/>
  <Setter Property="RenderTransformOrigin" Value="0.5,0.5"/>
  <Setter Property="RenderTransform">
    <RotateTransform Rotation="-5"/>
  </Setter>
</Style>
```

此示例使用变换将标题中的文字绕中点旋转 5 度。img/4fc1423ece9eb794a4edb8b1746d_110_0.png

20. 重新生成解决方案。

21. 打开 `MainPage.xaml` 文件。在设计视图中，标题现在应该倾斜显示。（在应用更新的样式之前，你可能需要重新生成应用程序。）img/4fc1423ece9eb794a4edb8b1746d_111_0.png

22. 在 `AppStyles.xaml` 文件中添加以下样式：

点击此处查看代码图片

```xml
<Style x:Key="LabelStyle" TargetType="TextBlock" BasedOn="StaticResource FontStyle">
  <Setter Property="FontSize" Value="20"/>
  <Setter Property="HorizontalAlignment" Value="Center"/>
  <Setter Property="TextWrapping" Value="Wrap"/>
  <Setter Property="VerticalAlignment" Value="Center"/>
  <Setter Property="Foreground" Value="AntiqueWhite"/>
</Style>
```

你将此样式应用于为用户输入信息的各种 `TextBox` 和 `ComboBox` 控件提供标签。该样式引用与标题相同的字体，但将其他属性设置为适用于标签的值。
