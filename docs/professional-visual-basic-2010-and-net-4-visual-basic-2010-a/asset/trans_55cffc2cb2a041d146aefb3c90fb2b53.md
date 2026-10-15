
```
HorizontalAlignment="Right" Width="75"
Clip="{StaticResource RoundPanel}">
    <Button HorizontalAlignment="Stretch"
VerticalAlignment="Stretch" Name="ButtonNext"
Height="75" Width="75" Visibility="Hidden">
        <Image Margin="0,0,0,0" Stretch="Fill"
Source="/Resources/RightArrow.jpg"/></Image>
    </Button>
    </StackPanel>
    <StackPanel Background="Transparent" VerticalAlignment="Center"
Margin="25,0,0,0" Height="75" Name="StackPanelPrev"
HorizontalAlignment="Left" Width="75"
Clip="{StaticResource RoundPanel}">
    <Button HorizontalAlignment="Left"
VerticalAlignment="Center" Name="ButtonPrev"
Height="75" Width="75" Visibility="Hidden">
        <Image Margin="0,0,0,0" Stretch="Fill"
Source="/Resources/LeftArrow.jpg"/></Image>
    </Button>
    </StackPanel>
</Grid>
</UserControl>
```

来自 ImageRotator.xaml 的代码片段

前面的 XAML 应该看起来很熟悉。与上次我们作为 MainWindow 类的一部分查看此代码时相比，主要区别在于与用户控件声明和 ButtonBrowse 相关的更改。

就 UserControl 而言，它有几个属性，在类与命名空间定义方面应该非常熟悉。其中一个可能不熟悉的属性是标记为 mc 且与标记兼容性相关联的属性。该库也用于用户控件声明的属性中。`mc:Ignorable="d"` 表示处理此 XAML 时，命名空间为“d”的属性值可以被忽略。

DesignHeight 和 DesignWidth 是带有 `d:` 前缀的两个属性。在这种情况下，应该比较清楚发生了什么；我们引入的概念是：在设计此用户控件时，拥有一个可见的设计图面是很有用的。然而，在部署时，此用户控件应根据包含对象的需求调整大小。由于设计图面没有包含对象，这可能会导致问题，因为高度和宽度会默认为 0。防止这种情况的唯一方法是引入一个元素来强制用户控件的大小，当然这会影响部署并影响控件的使用。

mc:Ignorable 提供了一种在 XAML 中描述特定于设计时 UI 方面的方法。这样，在运行时就不必记得删除这些属性；它们会被忽略。

除了用于定义新用户控件类的元素外，另一个值得关注的变化涉及 ButtonBrowse。如前所述，ButtonBrowse 现在与图像位于同一显示区域。你会注意到按钮的高度和宽度现在已进行数据绑定，稍后将更详细地解释。

在讨论数据绑定并暂时抛开这段 XAML 的大部分内容之前，请注意图像是如何被放置为按钮的内容的。将图像放入按钮内容中，可以让代码利用 WPF 内置的命令路由。当有人点击图像时，图像不会处理点击事件。因此，该事件被传递给图像下方层叠的 UI 元素，即按钮。按钮当然会处理点击事件。因此，与 Windows Forms 时代不同，那时你会将图像附加到按钮上，按钮知道如何使用图像作为其表面；在 WPF 中，按钮完全不知道图像正在充当其内容。然而，这种图像与按钮的解耦在按钮的大小调整方面留下了一个缺口，而这正是将按钮的高度和宽度绑定到图像高度和宽度的意义所在。

## WPF 中的数据绑定

WPF 对绑定提供了强大的支持，无论是控件之间的绑定，还是绑定到数据源。绑定到源是一种将外部值与控件关联的非常声明式的方法。由于你指定了绑定的内容，因此如果绑定的项发生更改，WPF 就会自动在控件中反映该更改。这样，你无需管理状态，也无需尝试跟踪和更新更改；这成为“管道”的一部分，你只需期待它能正常工作。

为了管理数据绑定的一些复杂性，本章将考察控件之间的绑定、依赖属性的使用，以及绑定到外部数据源。

### WPF 控件之间的绑定

正如更新后的 Image1 控件 XAML 所述，ButtonBrowse 的大小已绑定到 Image1 控件的大小。Image1 控件恰好是 ButtonBrowse 的内容，仔细想想，这创建了一个有趣的依赖关系。然而，图像的大小受控件显示区域内可用空间以及所显示图像缩放比例的限制。因此，如果控件大小为 300×300 并加载了一个图像，控件将根据可用空间计算其缩放比例。对于高度大于宽度的图像，缩放后可能为 250×300。注意这一切都是自动处理的。

过去，你的下一步将是检测 Image 控件大小的变化，并将此大小变化传达给按钮，使其“隐藏”在图像后面。代码还需要捕获新图像加载的时机，因为这将导致图像大小调整，并再次通知按钮。此外，每次控件调整大小时都要添加另一个通知，等等。换句话说，你需要确保你的管道捕获 Image 控件尺寸的每次变化。

使用 WPF，你可以简单地将按钮的高度与 Image 控件用于其高度的相同值关联起来，然后就可以放手了。Image 控件如何以及何时改变大小并不重要；当高度改变时，两个控件都会随之改变。对 Width 属性也做同样处理，就这样；无需自定义代码，无需自定义事件——什么都不需要。

ButtonBrowse 控件中使用的格式可以称为绑定的内联格式：

```
```xml
<Button Height="{Binding ElementName=Image1, Path=Height}"
        Width="{Binding ElementName=Image1, Path=Width}" Name="ButtonBrowse" >
```
```

注意，Height 和 Width 属性仍是 Button 的 XML 节点的属性。当你只需要绑定几个属性时，这种方法很方便。本章稍后将讨论第二种绑定方法。

当然，控件之间的绑定并不是唯一的绑定形式；你也不仅限于绑定到另一个命名控件。实际上，在某些情况下，绑定到命名控件并不现实。例如，如果你正在使用数据网格，你可能会希望绑定到当前行，这意味着一种关联绑定。在这种情况下，你希望使用 RelativeSource 绑定，以便能够指示数据网格中与你的控件关联的那一行就是你正在绑定的行。该行不会有名称，只有直接的父级关系。请记住，此示例仅展示了一组绑定参数；为了支持不同需求，还有其他几个参数可用。

就限制而言，你可以绑定到任何继承自 DependencyObject 的对象。该类位于 System.Windows.Controls 命名空间中所有控件的类层次结构中。它也可以位于你自己的自定义类的类层次结构中。然而，你的属性也需要实现为依赖属性，这就是下一节的主题。

### 依赖属性

并非所有属性都是依赖属性，但在设计允许数据绑定的情况下，任何被使用的属性通常都会实现为依赖属性。就本章而言，只需要了解依赖属性的几件事即可。首先，它们通常用于将资源和样式作为动态资源引用，而不是静态资源。其次，它们在 WPF 组件的文档中有明确标识。最后，为了帮助你扩展对绑定的理解，请记住 Style 属性实际上是一个依赖属性。

每个控件都可以与一个或多个样式关联。在开发过程中，你可以像创建资源一样创建样式。样式的分配方式与资源类似——也就是说，在将新样式分配给控件实例时，可以按名称引用它们；也可以创建与给定类型的所有实例关联的样式。无论哪种情况，控件的 Style 属性都是所谓的依赖属性。

当你听到“dependency”这个术语时，最初可能会认为这意味着该属性依赖于某个其他项。然而，在 WPF 上下文中，思考“dependency”一词的更好方式是：“它取决于谁在定义该属性的对象中设置了该特定值。”依赖属性并不依赖于某个外部项；属性的值会随着时间变化，具体取决于对该属性的最后一次更新。

深入探讨为什么会发生这种情况的细节超出了本章的范围。然而，依赖属性与更改通知逻辑相结合，并在动画和 3D 布局等方面发挥着重要作用。就我们的目的而言，目标是展示依赖属性的实用性以及如何创建自定义依赖属性。

为此，首先假设你希望 ImageRotator 控件在图像路径更改时通知其父容器。使用自定义事件来实现此目的的传统方式在 ImageRotator 控件的代码中进行了演示：

```
Public Class ImageRotator

    Private m_imageList As String() = {}
    Private m_curIndex As Integer = 0
    Private m_curImagePath As String = ""
    Private thename As String

    Public Event ImagePathChanged(ByVal sender As Object, ByVal e As String)

    Private Sub Grid1_Loaded(ByVal sender As System.Object,
        ByVal e As System.Windows.RoutedEventArgs) Handles
    Grid1.Loaded
        m_curImagePath = Environment.GetFolderPath(Environment.SpecialFolder.MyPictures)
        RaiseEvent ImagePathChanged(Me, m_curImagePath)
        LoadImages()
    End Sub

    Private Sub ButtonBrowse_Click(ByVal sender As System.Object,
        ByVal e As System.Windows.RoutedEventArgs) Handles
    ButtonBrowse.Click
        Dim folderDialog As System.Windows.Forms.FolderBrowserDialog =
            New System.Windows.Forms.FolderBrowserDialog()
        folderDialog.Description = "Select the folder for images."
        folderDialog.SelectedPath = m_curImagePath
        Dim res As System.Windows.Forms.DialogResult = folderDialog.ShowDialog()
        If res = System.Windows.Forms.DialogResult.OK Then
            m_curImagePath = folderDialog.SelectedPath
            RaiseEvent ImagePathChanged(Me, m_curImagePath)
            LoadImages()
        End If
    End Sub

    Private Sub LoadImages()
        Image1.Source = Nothing
```
