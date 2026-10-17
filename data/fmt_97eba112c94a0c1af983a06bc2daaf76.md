
在 `MainWindow.xaml` 文件中，`Data` 和 `Information` 类在 `Window` 的资源中被引用并初始化（代码文件 `PriorityBindingDemo/MainWindow.xaml`）：

```xml
<Window.Resources>
    <local:Data x:Key="data1" />
    <local:Information x:Key="info" />
</Window.Resources>
```

`PriorityBinding` 在 `Label` 的 `Content` 属性中替代普通绑定。它由多个 `Binding` 元素组成，其中除最后一个之外的所有元素都将 `IsAsync` 属性设置为 `True`。因此，如果第一个绑定表达式的结果不能立即获得，绑定过程就会选择下一个。第一个绑定引用了 `Data` 类的 `ProcessSomeData` 属性，该属性需要一些时间。因此，下一个绑定开始起作用，并引用 `Information` 类的 `Info2` 属性。`Info2` 不会立即返回结果，并且由于设置了 `IsAsync`，绑定过程不会等待，而是继续到下一个绑定。最后一个绑定使用 `Info` 属性。如果它不能立即返回结果，您将等待该结果，因为 `IsAsync` 被设置为默认值 `False`：

```xml
<Label>
    <Label.Content>
        <PriorityBinding>
            <Binding Path="ProcessSomeData" Source="{StaticResource data1}"
                IsAsync="True" />
            <Binding Path="Info2" Source="{StaticResource info}"
                IsAsync="True" />
            <Binding Path="Info1" Source="{StaticResource info}"
                IsAsync="False" />
        </PriorityBinding>
    </Label.Content>
</Label>
```

当应用程序启动时，您可以在用户界面中看到消息“请稍候…”。几秒钟后，`Info2` 属性的结果返回为“请再稍等一会儿”。它代替了输出。

### 35

### 使用 WPF 创建文档

#### 本章内容

- 使用文本元素

- 创建流文档

- 创建固定文档

- 创建 XPS 文档

- 打印文档

#### 本章的 Wrox.com 代码下载

本章的 wrox.com 代码下载可在 `www.wrox.com/go/professionalcsharp6` 的 Download Code 选项卡中找到。本章代码分为以下几个主要示例：

- Show Fonts

- Text Effects

- Table

- Flow Documents

- Create XPS

- Printing

#### 简介

创建文档是 WPF 的一个重要部分。命名空间 `System.Windows.Documents` 支持创建流文档和固定文档。该命名空间包含多种元素，借助这些元素，您可以在流文档中获得类似 Word 的丰富体验，并创建所见即所得（WYSIWYG）的固定文档。

`流文档` 面向屏幕阅读；文档内容根据窗口大小进行排列，如果调整窗口大小，文档的流动方式也会随之改变。`固定文档` 主要用于打印和面向页面的内容，其内容始终以相同方式排列。

本章介绍如何创建和打印流文档与固定文档，并涵盖命名空间 `System.Windows.Documents`、`System.Windows.Xps` 和 `System.IO.Packaging`。

#### 文本元素

要构建文档内容，需要文档元素。这些元素的基类是 `TextElement`。该类定义了字体设置、前景色和背景色以及文本效果的公共属性。`TextElement` 是 `Block` 和 `Inline` 类的基类，其功能将在以下各节中探讨。

#### 字体

文本的一个重要方面是外观，因此字体非常重要。使用 `TextElement`，可以通过 `FontWeight`、`FontStyle`、`FontStretch`、`FontSize` 和 `FontFamily` 属性指定字体：

- `FontWeight`——预定义值由 `FontWeights` 类指定，该类提供 `UltraLight`、`Light`、`Medium`、`Normal`、`Bold`、`UltraBold` 和 `Heavy` 等值。

- `FontStyle`——值由 `FontStyles` 类定义，该类提供 `Normal`、`Italic` 和 `Oblique`。

- `FontStretch`——使用此属性指定字体相对于正常宽高比的拉伸程度。`FontStretch` 定义了一系列预定义的拉伸，范围从 50%（`UltraCondensed`）到 200%（`UltraExpanded`）。介于两者之间的预定义值有 `ExtraCondensed (62.5%)`、`Condensed (75%)`、`SemiCondensed (87.5%)`、`Normal (100%)`、`SemiExpanded (112.5%)`、`Expanded (125%)` 和 `ExtraExpanded (150%)`。

- `FontSize`——类型为 `double`，可用于以设备无关单位、英寸、厘米和磅为单位指定字体大小。

- `FontFamily`——用于定义首选字体族的名称，例如 Arial 或 Times New Roman。使用此属性可以指定字体族名称列表，因此如果某个字体不可用，则使用列表中的下一个字体。（如果所选字体和备用字体均不可用，流文档将回退到默认的 `MessageFontFamily`。）您还可以从资源中引用字体族，或使用 URI 引用服务器中的字体。对于固定文档，由于字体随文档提供，因此不会回退到不可用的字体。

为了让您感受不同字体的外观，以下示例 WPF 应用程序包含一个 `ListBox`。该 `ListBox` 为列表中的每一项定义了一个 `ItemTemplate`。此模板使用四个 `TextBlock` 元素，其中 `FontFamily` 绑定到 `FontFamily` 对象的 `Source` 属性。不同的 `TextBlock` 元素分别设置 `FontWeight` 和 `FontStyle`（代码文件 `DocumentsDemos/ShowFontsDemo/MainWindow.xaml`）：

```xml
<ListBox ItemsSource="{Binding}">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <StackPanel Orientation="Horizontal" >
                <StackPanel.Resources>
                    <Style TargetType="TextBlock">
                        <Setter Property="Margin" Value="3,0,3,0" />
                        <Setter Property="FontSize" Value="18" />
                        <Setter Property="FontFamily" Value="{Binding Source}" />
                    </Style>
                </StackPanel.Resources>

                <TextBlock Text="{Binding Path=Source}" />
                <TextBlock FontStyle="Italic" Text="Italic" />
                <TextBlock FontWeight="UltraBold" Text="UltraBold" />
                <TextBlock FontWeight="UltraLight" Text="UltraLight" />
            </StackPanel>
        </DataTemplate>
    </ListBox.ItemTemplate>
</ListBox>
```

在后台代码中，数据上下文设置为 `System.Windows.Media.Fonts` 类的 `SystemFontFamilies` 属性的结果。这将返回所有可用的字体（代码文件 `DocumentsDemos/ShowFontsDemo/MainWindow.xaml.cs`）：

```csharp
public partial class ShowFontsWindow: Window
{
    public ShowFontsWindow()
    {
        InitializeComponent();

        this.DataContext = Fonts.SystemFontFamilies;
    }
}
```

运行该应用程序时，您会看到一长串系统字体族，分别显示为斜体、粗体、超粗体和超细体特征，如图 35.1 所示。

![](img/3d365b72b289213a91ade7eb366b8f35_1382_0.png)

图 35.1

#### TextEffect

现在让我们看看 `TextEffect`，因为它也是所有文档元素的共同特性。`TextEffect` 定义在命名空间 `System.Windows.Media` 中，并继承自基类 `Animatable`，后者支持文本动画。

`TextEffect` 使您能够对裁剪区域、前景画笔和变换进行动画处理。通过 `PositionStart` 和 `PositionCount` 属性，可以指定动画应用于文本中的位置。

为了应用文本效果，需要设置 `Run` 元素的 `TextEffects` 属性。该属性中指定的 `TextEffect` 元素定义了前景和变换。前景使用名为 `brush1` 的 `SolidColorBrush`，它通过 `ColorAnimation` 元素进行动画处理。变换使用名为 `scale1` 的 `ScaleTransform`，它由两个 `DoubleAnimation` 元素驱动动画（代码文件 `DocumentsDemos/TextEffectsDemo/MainWindow.xaml`）：

```xml
<TextBlock>
    <TextBlock.Triggers>
        <EventTrigger RoutedEvent="TextBlock.Loaded">
            <BeginStoryboard>
                <Storyboard>
                    <ColorAnimation AutoReverse="True"
RepeatBehavior="Forever"
                        From="Blue" To="Red" Duration="0:0:16"
                        Storyboard.TargetName="brush1"
                        Storyboard.TargetProperty="Color" />
                    <DoubleAnimation AutoReverse="True"
                        RepeatBehavior="Forever"
                        From="0.2" To="12" Duration="0:0:16"
                        Storyboard.TargetName="scale1"
                        Storyboard.TargetProperty="ScaleX" />
                    <DoubleAnimation AutoReverse="True"
                        RepeatBehavior="Forever"
                        From="0.2" To="12" Duration="0:0:16"
                        Storyboard.TargetName="scale1"
                        Storyboard.TargetProperty="ScaleY" />
                </Storyboard>
            </BeginStoryboard>
        </EventTrigger>
    </TextBlock.Triggers>
    <Run FontFamily="Segoe UI">
        cn|elements
        <Run.TextEffects>
            <TextEffect PositionStart="0" PositionCount="30">
                <TextEffect.Foreground>
                    <SolidColorBrush x:Name="brush1" Color="Blue" />
                </TextEffect.Foreground>
                <TextEffect.Transform>
                    <ScaleTransform x:Name="scale1" ScaleX="3" ScaleY="3" />
                </TextEffect.Transform>
            </TextEffect>
        </Run.TextEffects>
    </Run>
</TextBlock>
```

运行该应用程序时，您可以看到大小和颜色的变化，如图 35.2 和图 35.3 所示。

![](img/3d365b72b289213a91ade7eb366b8f35_1384_0.png)

图 35.2

![](img/3d365b72b289213a91ade7eb366b8f35_1384_1.png)

图 35.3

#### 内联元素

所有内联流内容元素的基类是 `Inline`。您可以在流文档的段落中使用 `Inline` 元素。由于在一个段落中，一个 `Inline` 元素可以跟在另一个 `Inline` 元素后面，因此 `Inline` 类提供了 `PreviousInline` 和 `NextInline` 属性，用于从一个元素导航到另一个元素。还可以通过 `SiblingInlines` 获取所有同级内联元素的集合。

前面用于写入文本的 `Run` 元素是一种用于格式化或非格式化文本的 `Inline` 元素，但还有很多其他元素。可以在 `Run` 元素后面使用 `LineBreak` 元素来换行。

`Span` 元素派生自 `Inline` 类，并支持对 `Inline` 元素进行分组。`Span` 的内容中只允许包含 `Inline` 元素。顾名思义，`Bold`、`Hyperlink`、`Italic` 和 `Underline` 类都派生自 `Span`，因此同样支持将 `Inline` 元素作为其内容，但对这些元素的作用方式不同。下面的 XAML 代码演示了如何使用 `Bold`、`Italic`、`Underline` 和 `LineBreak`，如图 35.4 所示（代码文件 `DocumentsDemos/FlowDocumentsDemo/FlowDocument1.xaml`）：

```xml
<Paragraph FontWeight="Normal">
    <Span>
        <Span>Normal</Span>
        <Bold>Bold</Bold>
        <Italic>Italic</Italic>
        <LineBreak />
        <Underline>Underline</Underline>
    </Span>
</Paragraph>
```

![](img/3d365b72b289213a91ade7eb366b8f35_1385_0.png)

图 35.4

`AnchoredBlock` 是一个派生自 `Inline` 的抽象类，用于将 `Block` 元素锚定到流内容中。`Figure` 和 `Floater` 是派生自 `AnchoredBlock` 的具体类。由于这两个内联元素与块元素相关时更有意思，因此本章稍后将讨论这些元素。

> **注意** 添加到解决方案中的流文档需要设置为 `Build Action` = `Content` 以及 `Copy to Output Directory` = `Copy if newer`，方法是在 Visual Studio 属性窗口中进行设置，以便这些文档与可执行文件位于同一目录中。

另一个用于映射前面章节中所用 UI 元素的 `Inline` 元素是 `InlineUIContainer`。`InlineUIContainer` 允许将所有 `UIElement` 对象（例如 `Button`）添加到文档中。以下代码片段将包含 `ComboBox`、`RadioButton` 和 `TextBox` 元素的 `InlineUIContainer` 添加到文档中（结果如图 35.5 所示）（代码文件 `DocumentsDemos/FlowDocumentsDemo/FlowDocument2.xaml`）：

```xml
<Paragraph TextAlignment="Center">

    <Span FontSize="36">

        <Italic>c|elements</Italic>

    </Span>

    <LineBreak />

    <LineBreak />
```
