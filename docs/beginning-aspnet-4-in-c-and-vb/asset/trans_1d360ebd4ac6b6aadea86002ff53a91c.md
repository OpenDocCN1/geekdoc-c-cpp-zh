
## 使用 WPF 创建文档

### 本章内容？

-   创建流文档
-   创建固定文档
-   创建 XPS 文档
-   打印文档

创建文档是 WPF 的重要组成部分。命名空间 `System.Windows.Documents` 支持创建流文档和固定文档。该命名空间包含元素，可让你在流文档中获得类似 Word 的丰富体验，并创建所见即所得的固定文档。

*流*文档面向屏幕阅读；文档内容根据窗口大小排列，如果窗口大小改变，文档的流也会发生变化。*固定*文档主要用于打印和页面导向的内容，内容始终以相同的方式排列。

本章教你如何创建和打印流文档和固定文档，并涵盖命名空间 `System.Windows.Documents`、`System.Windows.Xps` 和 `System.IO.Packaging`。

## 文本元素

要构建文档内容，需要文档元素。这些元素的基类是 `TextElement`。该类定义了字体设置、前景色和背景色以及文本效果的通用属性。`TextElement` 是类 `Block` 和 `Inline` 的基类，其功能将在以下各节中探讨。

### 字体

文本的一个重要方面是文本的外观，因此是字体。使用 `TextElement`，字体可以通过属性 `FontWeight`、`FontStyle`、`FontStretch`、`FontSize` 和 `FontFamily` 指定。

-   预定义的 `FontWeight` 值由 `FontWeights` 类定义，该类提供诸如 `UltraLight`、`Light`、`Medium`、`Normal`、`Bold`、`UltraBold` 和 `Heavy` 等值。
-   FontStyle 值由 `FontStyles` 类定义，该类提供 Normal、Italic 和 Oblique。
-   使用 `FontStretch` 可以指定字体相对于正常纵横比的拉伸程度。`FontStretch` 定义了从 50%（UltraCondensed）到 200%（UltraExpanded）的预定义拉伸。中间的预定义值有 ExtraCondensed（62.5%）、Condensed（75%）、SemiCondensed（87.5%）、Normal（100%）、SemiExpanded（112.5%）、Expanded（125%）、ExtraExpanded（150%）
-   `FontSize` 的类型为 double，可在其中指定字体大小，单位为设备无关单位、英寸、厘米和磅。
-   使用 `FontFamily` 定义首选字体族的名称，例如 Arial 或 Times New Roman。通过此属性可以指定字体族名称列表，因此如果一种字体不可用，则使用列表中的下一个字体。（如果所选字体和备用字体均不可用，流文档将回退到默认的 `MessageFontFamily`。）你还可以从资源中引用字体族，或使用 URI 从服务器引用字体。对于固定文档，如果字体不可用则没有回退，因为字体随文档一起提供。

为了让你感受不同字体的外观，以下示例 WPF 应用程序包含一个 ListBox。ListBox 为列表中的每个项目定义一个 ItemTemplate。此模板使用四个 TextBlock 元素，其中 FontFamily 绑定到 FontFamily 对象的 Source 属性。使用不同的 TextBlock 元素设置 FontWeight 和 FontStyle：

```
<ListBox ItemsSource="{Binding}">
  <ListBox.ItemTemplate>
    <DataTemplate>
      <StackPanel Orientation="Horizontal" >
        <TextBlock Margin="3, 0, 3, 0"
          FontFamily="{Binding Path=Source}"
          FontSize="18" Text="{Binding Path=Source}" />
        <TextBlock Margin="3, 0, 3, 0"
          FontFamily="{Binding Path=Source}"
          FontSize="18" FontStyle="Italic" Text="Italic" />
        <TextBlock Margin="3, 0, 3, 0"
          FontFamily="{Binding Path=Source}"
          FontSize="18" FontWeight="UltraBold"
          Text="UltraBold" />
        <TextBlock Margin="3, 0, 3, 0"
          FontFamily="{Binding Path=Source}"
          FontSize="18" FontWeight="UltraLight"
          Text="UltraLight" />
      </StackPanel>
    </DataTemplate>
  </ListBox.ItemTemplate>
</ListBox>
```

*代码片段 ShowFonts/ShowFontsWindow.xaml*

在代码隐藏中，数据上下文被设置为 System.Windows.Media.Fonts 类的 SystemFontFamilies 属性的结果：

```
public partial class ShowFontsWindow : Window
{
    public ShowFontsWindow()
    {
        InitializeComponent();

        this.DataContext = Fonts.SystemFontFamilies;
    }
}
```

*代码片段 ShowFonts/ShowFontsWindow.xaml.cs*

运行应用程序后，你会得到一个包含斜体、粗体、超粗体和超细体特征的大量系统字体族列表，如图 37-1 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1138_0.png)

图 37-1

### TextEffect

接下来让我们了解一下 TextEffect，因为它也是所有文档元素的通用功能。TextEffect 在命名空间 System.Windows.Media 中定义，并派生自允许文本动画的基类 Animatable。

TextEffect 允许你为剪切区域、前景画刷和变换设置动画。使用属性 PositionStart 和 PositionCount 指定动画应用于文本中的位置。

为了应用文本效果，将 Run 元素的 TextEffects 属性设置为。属性中指定的 TextEffect 元素定义了前景色和变换。对于前景，使用名为 brush1 的 SolidColorBrush，并通过 ColorAnimation 元素对其进行动画处理。变换使用名为 scale1 的 ScaleTransform，并通过两个 DoubleAnimation 元素对其进行动画处理：

```
<TextBlock>
    <TextBlock.Triggers>
        <EventTrigger RoutedEvent="TextBlock.Loaded">
            <BeginStoryboard>
                <Storyboard>
                    <ColorAnimation AutoReverse="True" RepeatBehavior="Forever" From="Red" To="Yellow" Duration="0:0:3" Storyboard.TargetName="brush1" Storyboard.TargetProperty="Color" />
                    <DoubleAnimation AutoReverse="True" RepeatBehavior="Forever" From="0.2" To="12" Duration="0:0:6" Storyboard.TargetName="scale1" Storyboard.TargetProperty="ScaleX" />
                    <DoubleAnimation AutoReverse="True" RepeatBehavior="Forever" From="0.2" To="12" Duration="0:0:6" Storyboard.TargetName="scale1" Storyboard.TargetProperty="ScaleY" />
                </Storyboard>
            </BeginStoryboard>
        </EventTrigger>
    </TextBlock.Triggers>
<Run FontFamily="Mangal">
some elements
    <Run.TextEffects>
        <TextEffect PositionStart="0" PositionCount="30" >
```

```
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

代码片段 TextEffectsDemo/MainWindow.xaml

运行应用程序后，你可以看到大小和颜色的变化，如图 37-2 和 37-3 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1139_0.png)

图 37-2

![](img/d7d2ffa0a76feaab821930e95daace93_1139_1.png)

图 37-3

### Inline

所有内联流内容元素的基类是 Inline。你可以在流文档的段落中使用 Inline 元素。因为在段落中一个 Inline 元素可以跟在另一个之后，Inline 类提供了 PreviousInline 和 NextInline 属性以在元素之间导航。你也可以使用 SiblingInlines 获取所有同级内联的集合。

之前用于书写文本的 Run 元素是用于格式化或未格式化文本的 Inline 元素，但还有更多。Run 元素之后的新行可以使用 LineBreak 元素实现。

Span 元素派生自 Inline 类，允许对 Inline 元素进行分组。Span 内容中只允许 Inline 元素。自解释的 Bold、Hyperlink、Italic 和 Underline 类都派生自 Span，因此具有相同的功能，允许 Inline 元素作为其内容，但对这些元素的作用不同。以下 XAML 代码演示了使用 Bold、Italic、Underline 和 LineBreak，如图 37-4 所示。

```
<Paragraph FontWeight="Normal">
    <Span>
        <Span>Span Normal</Span>
        <Bold>Bold</Bold>
        <Italic>Italic</Italic>
        <LineBreak />
        <Underline>Underline</Underline>
    </Span>
</Paragraph>
```

代码片段 FlowDocumentsDemo/FlowDocument1.xaml

AnchoredBlock 是一个派生自 Inline 的抽象类，用于将 Block 元素锚定到流内容。Figure 和 Floater 是派生自 AnchoredBlock 的具体类。因为这两个内联元素与块相关变得有趣，所以本章后面会讨论这些元素。

![](img/d7d2ffa0a76feaab821930e95daace93_1140_0.png)

图 37-4

另一个映射在前几章中使用过的 UI 元素的 Inline 元素是 InlineUIContainer。InlineUIContainer 允许将所有 UIElement 对象（例如 Button）添加到文档中。以下代码段向文档添加了包含 ComboBox、RadioButton 和 TextBox 元素的 InlineUIContainer。结果如图 37-5 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1140_1.png)

图 37-5

![](img/d7d2ffa0a76feaab821930e95daace93_1140_2.png)

```
<Paragraph TextAlignment="Center" >
    <Span FontSize="36">
        <Italic>some elements</Italic>
    </Span>
</Paragraph>
<LineBreak />
<LineBreak />
<InlineUIContainer>
<Grid>
<Grid.RowDefinitions>
<RowDefinition />
<RowDefinition />
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
<ColumnDefinition />
<ColumnDefinition />
</Grid.ColumnDefinitions>
<ComboBox Width="140" Margin="3" Grid.Row="0">
<ComboBoxItem>Filet Mignon</ComboBoxItem>
<ComboBoxItem>Rib Eye</ComboBoxItem>
<ComboBoxItem>Sirloin</ComboBoxItem>
</ComboBox>
<StackPanel Grid.Row="0" Grid.RowSpan="2" Grid.Column="1">
<RadioButton>Raw</RadioButton>
<RadioButton>Medium</RadioButton>
<RadioButton>Well done</RadioButton>
</StackPanel>
