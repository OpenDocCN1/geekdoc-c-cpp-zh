
### 样式与模板

```xml
<ContentPresenter SnapsToDevicePixels="{TemplateBinding SnapsToDevicePixels}" HorizontalAlignment="{TemplateBinding HorizontalContentAlignment}" Margin="{TemplateBinding Padding}" VerticalAlignment="{TemplateBinding VerticalContentAlignment}" RecognizesAccessKey="True"/>
</Microsoft_Windows_Themes:ButtonChrome>
<ControlTemplate.Triggers>
    <Trigger Property="IsKeyboardFocused" Value="true">
        <Setter Property="RenderDefaulted" TargetName="Chrome" Value="true"/>
    </Trigger>
    <Trigger Property="ToggleButton.IsChecked" Value="true">
        <Setter Property="RenderPressed" TargetName="Chrome" Value="true"/>
    </Trigger>
    <Trigger Property="IsEnabled" Value="false">
        <Setter Property="Foreground" Value="#ADADAD"/>
    </Trigger>
</ControlTemplate.Triggers>
</ControlTemplate>
</Setter.Value>
</Setter>
</Style>
```

在上述代码块中有两行值得关注。第一行涉及实际定义的按钮样式。样式经常引用其他资源；与早期的 C 编译器类似，引用必须在实际引用之前定义。因此，上述代码块中定义的样式实际上是最后一个样式条目：

```xml
<Style x:Key="ButtonStyle1" TargetType="{x:Type Button}">
```

这一行在代码块中以粗体突出显示，表示这组资源定义了一个键为 `ButtonStyle1` 的样式。由于此样式是使用键定义的，因此它不是应用于目标类型所有控件的默认样式。样式总是定义目标类型，因为不同的控件类型期望在样式的所有详细元素中定义不同的特定值。

要让每个控件按钮都使用相同的样式，可以不提供 `ButtonStyle1` 样式的键，而只提供类型定义。如果在某个时候你希望不同类型的对象共享某些特征，可以通过定义资源并将其应用于每种类型的样式来实现。如果随后这些样式在没有键的情况下被指定，那么它们默认应用于该类型的每个对象。

接下来，如果你想找到一种方法来移除鼠标悬停在按钮上时出现的默认高亮效果，那么你需要确定样式是如何指定该效果的。好消息是导致该行为的钩子实际上包含在此文件中；坏消息是它引用了一个模板，然后该模板被分配给该行为。下面的 XAML 行显示了 `RenderMouseOver` 属性正在与模板的 `IsMouseOver` 关联：

```
RenderMouseOver="{TemplateBinding IsMouseOver}"
```

正是这个模板导致按钮改变其外观以反映此状态。因此，要获得没有此默认行为的按钮，你需要定义一个新模板，或者从自定义样式中删除此 XAML 元素。

当然，你可以获取前面的代码块，进行必要的更改，并将其粘贴到应用程序的 XAML 中。如果你还执行了其他需要执行的步骤，这当然会奏效。然而，从长远来看，前面的 XAML 块是特定于 `Button` 类型控件的。此外，前面所有代码实际上都是生成的。如果你需要自定义另一种控件类型的运行时行为，则需要为该控件生成默认样式。`Expression Blend` 虽然不再是必需的，但仍然是执行此操作的一个不错选择。

### 数据绑定到数据源

本章要讨论的最后一项是绑定到数据源。为简洁起见，此示例使用一个简单的 XML 文件 `People.xml`，它是 `ProVB_WPF_Step3` 项目的一部分。该文件的内容如下：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<People xmlns="">
    <Person PersonID="187012">
        <FirstName>Johnny</FirstName>
        <LastName>Climber</LastName>
        <JobTitle>Danger Boy</JobTitle>
        <working_folder>C:\Users\WSheldon\Pictures\Johnny</working_folder>
    </Person>
    <Person PersonID="181810">
        <FirstName>Billy</FirstName>
        <LastName>Karate</LastName>
        <JobTitle>Gold Belt</JobTitle>
        <working_folder>C:\Users\WSheldon\Pictures\Billy</working_folder>
    </Person>
</People>
```

该文件的内容相当简单，代表了一个人力资源风格的应用程序。每个条目都有一个内部 ID 和一系列字段。`working_folder` 节点是特定于机器的，因此当你考虑运行此应用程序时，需要将其映射到本地机器上存在的文件夹。否则，你将看不到任何图像。

虽然此文件将在主窗口中进行数据绑定，但第一步是更新 `ImageRotator` 控件。其转换的第一部分涉及获取只读的 `ImageURI` 属性，并将其转换为可读写的依赖属性。如前所述，先前引用的只读属性在示例下载代码中已被注释掉并折叠在一个区域中。最终代码的开始方式与原始代码类似，它定义了一个标准类属性。然而，在这种情况下，该属性支持一个 `Set` 方法，该方法调用本地方法来更新 `Image` 控件中显示的图像。

更新后的属性代码如下，从更新后的 `ImageURI` 属性开始：

```
Public Property ImageURI As String
    Get
        Return m_curImagePath
    End Get
    Set(ByVal value As String)
        m_curImagePath = value
        LoadImages()
    End Set
End Property

Private Shared ImageProp As DependencyProperty =
    DependencyProperty.RegisterAttached("ImageURI",
        GetType(String),
        GetType(ProVB_WPF_Step3.ImageRotator),
        New FrameworkPropertyMetadata(Nothing,
            FrameworkPropertyMetadataOptions.AffectsRender,
            New PropertyChangedCallback(AddressOf UriChanged)))

Public Shared Sub UriChanged(ByVal prop As DependencyObject,
    ByVal args As DependencyPropertyChangedEventArgs)
    CType(prop, ImageRotator).ImageURI = args.NewValue
End Sub
```

来自 `ImageRotator.vb` 的代码片段

对引用 `DependencyPropertyKey` 的原始调用也已更新，代码现在引用了真正的 `DependencyProperty` 更新。然而，你的关注点应放在 `RegisterAttached` 方法的第四个参数上。虽然前三个参数保持不变，但第四个参数现在传递了两个新的属性。

`FrameworkPropertyMetadata` 的新构造函数对“默认值”参数为 `null`。它随后传递一个选项标志，指示当此属性更新时，窗口的渲染会受到影响并且需要更新。这是对的，因为对该属性的更新将导致选择新的图像，该图像需要被调整大小并显示。

然而，最后一个参数，即新的 `PropertyChangedCallback`，才是重要的。这是在向属性注册，当对该属性进行更改时应通知哪个方法。正如前面所述，当你将依赖属性视为属性加事件且具有双向通信时，你需要一个能够接收传入通信的位置。此回调方法本质上是当在本地类外部触发 `PropertyChanged` 事件时的事件处理程序。

在这种情况下，传递了 `UriChanged` 方法的地址。该方法就是剩余的新代码。正如你通过查看代码会注意到的，`UriChanged` 方法是一个 `Shared` 方法，这意味着它不能仅引用本地属性。幸运的是，第一个参数是需要更新的 `DependencyObject` 的实例，而 `EventArgs` 参数中传递的值之一确实是新值。因此，该方法只需要一行代码，将传入的依赖对象强制转换为本地类型，然后在本地类上调用适当的属性并传递新值。

这创建了一个支持双向通信的基础设施，其中你的对象会通知对该属性值感兴趣的各方其更改，而需要更新该属性的各方可以通知你的对象新的建议值。请注意，如果例如有人传递了一个无效的路径，那么你就可以拒绝该值的赋值。如果你正在查看下载代码，那么你就知道还有最后一组需要注释掉的更改，即此类 `Load` 事件中的一些行；然而，该更改作为此过程的最后一步进行了介绍。

代码现在支持与图像路径关联的双向属性，允许通过主窗口 XAML 中的绑定将更新发送到控件。请注意，`ImageRotator.xaml` 文件或 `MainWindow.xaml.vb` 文件没有更新。数据绑定集中在 `MainWindow.xaml` 文件上，该文件在长度上再次增长，因此复杂性也随之增加。为了帮助管理这一点，下一个代码块解决了对该文件资源和数据上下文的更改，而对单个控件绑定的更新则是第二个块的重点。

以下 XAML 显示了窗口的一些细微修改，但粗体行是数据绑定的重点。由于这些行位于顶部附近，我们将在代码之前讨论它们。第一个是分配给顶级网格的新 `DataContext`。该网格没有名称，但它是所有其他控件的父级，作为绑定上下文的中央清除。

第一个突出显示的行，即为网格创建数据上下文，实际上将其绑定到新的 `ListBox` 控件。`ListBox` 中的选定项随后绑定到网格。通过在窗口中的所有其他控件上引用此上下文，这些控件可以使用此数据上下文作为其当前上下文。由于对列表中选定项的更新会自动更新到此上下文，因此每个控件都可以与网格中的选定项保持同步，而无需进一步的代码。

接下来可能引起你兴趣的是下一个突出显示的部分，其中包含网格资源。大多数时候，开发人员会传统地将这些资源映射到 `ListBox` 中的选定项。然而，正如刚才使用 WPF 讨论的那样，网格绑定到 `ListBox` 中的选定项；因此，所有其他控件都可以继承该上下文作为数据上下文。

其含义是唯一不会继承的是 `ListBox`。相反，正如你稍后会看到的，`ListBox` 显式绑定到网格资源的第一个，即 `XmlDataProvider`。此类可用于提供一种方式让 XAML 加载 XML 文件并绑定到其内容。提供程序可以使用 `Source` 属性，或者你也可以在 `x:Data` 块中嵌入数据。一旦绑定，提供程序将被分配一个键，以便可以从其他控件中引用。在此示例中，只有 `ListBox` 控件实际上会绑定到此数据源，但理论上其他控件也可以绑定到它。此外，`XPath` 查询的顶级节点被定义为 `People`。当代码请求一个属性时，它将基于 `People` 下的条目获取一个属性。这是应用程序将使用的非常简单的 `XPath` 的起点。

数据提供程序的创建简短而甜美；接下来出现的却是数据模板。名为 `PersonName` 的模板定义了输出格式。它也由 `ListBox` 控件使用，尽管例如它可用于填充窗口标题，如果你想要窗口上的不同标题。内部是一个简短的 WPF 片段，描述了一个容器——在本例中为 `StackPanel` 以及 `StackPanel` 上的控件。这意味着 `DataTemplate` 可以是一种极其强大的方式来格式化复杂的数据结构。内部的控件直接映射到默认数据源，在本例中引用了 XML 中 `Person` 结构中的两个节点。

这些代表了 XML 第一部分中用于绑定的唯一突出显示区域。接下来的一块包括显示部分透明背景的顶级窗口，通过标题栏矩形上的按钮：

```xml
<Window x:Class="MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="ProVB_WPF" Height="363" Width="444" Name="MainWindow"
    WindowStyle="None" AllowsTransparency="True" xmlns:my="clr-namespace:ProVB_WPF_Step3"
    WindowStartupLocation="CenterScreen" Background="#B4FFFFFF">
    <Grid OpacityMask="Black" Opacity="1"
        DataContext="{Binding ElementName=ListBox1, Path=SelectedItem}">
        <Grid.RowDefinitions>
            <RowDefinition Height="25*" />
            <RowDefinition Height="215*" />
        </Grid.RowDefinitions>
        <Grid.Resources>
            <XmlDataProvider Source="People.xml" x:Key="People"
                XPath="People">
            </XmlDataProvider>
            <DataTemplate x:Key="PersonName">
```

```xml
<StackPanel Orientation="Horizontal">
    <TextBlock>
        <TextBlock.Text>
            <Binding XPath="FirstName"/></Binding>
        </TextBlock.Text>
    </TextBlock>
    <TextBlock Text=" "/></TextBlock>
    <TextBlock>
        <TextBlock.Text>
            <Binding XPath="LastName"/></Binding>
        </TextBlock.Text>
    </TextBlock>
</StackPanel>
</DataTemplate>
</Grid.Resources>
<Rectangle Name="TitleBar" HorizontalAlignment="Stretch" Margin="0,0,0,0" Stroke="#00000000" VerticalAlignment="Stretch" Opacity="0.5">
    <Rectangle.Fill>
        <LinearGradientBrush EndPoint="1,0.5" StartPoint="0,0.5">
            <GradientStop Color="#FF0AFF0A" Offset="0" />
            <GradientStop Color="Blue" Offset="1" />
            <GradientStop Color="#0059C4B" Offset="0.474" />
            <GradientStop Color="#00638F54" Offset="0.785" />
            <GradientStop Color="#9D0000FF" Offset="0.826" />
            <GradientStop Color="#FF00ED00" Offset="0.359" />
        </LinearGradientBrush>
    </Rectangle.Fill>
</Rectangle>
```
