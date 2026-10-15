

接下来，从设计图面删除标记为 View Images 的按钮。此时你可以就此打住，但为了帮你为后续其他设计更改做好准备，请重新审视 Prev 和 Next 按钮的放置位置。目前，这些按钮与网格的底部区域绑定在一起；相反，应删除第三个网格行定义，并将 Prev 和 Next 按钮居中放置在图像的侧边。此时，设计器应类似于图 17-7 所示。

![](img/d99870e80390742f93963da7be0b2e61_644_0.png)

**图 17-7**

这是一个更简洁、更清晰的界面。对应的 XAML 如下：

```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="25" />
        <RowDefinition Height="215*" />
    </Grid.RowDefinitions>
    <Button HorizontalAlignment="Stretch" Margin="0,0,100,2" Name="ButtonBrowse">Images Folder</Button>
    <Image Grid.Row="1" Margin="0,0,0,0" Name="Image1" Stretch="Uniform" />
    <Button Grid.Row="1" HorizontalAlignment="Right" Name="ButtonNext" VerticalAlignment="Center" Margin="0,0,15,8" Width="75">Next</Button>
    <Button Grid.Row="1" HorizontalAlignment="Left" Name="ButtonPrev" VerticalAlignment="Center" Margin="17,113,0,116" Width="75">Prev</Button>
</Grid>
```

> 代码片段来自 MainWindow.xaml

这表明 Grid 现在只有两个行定义，Image 控件也已更新到第 1 行，Prev 和 Next 按钮同样位于第 1 行。

现在你已准备好进行下一组更改，使这个应用程序在外观和行为上更像一个 WPF 应用程序。首先要去掉应用程序周围“丑陋”的 Windows 边框。（你的设计人员可能稍后想为这个应用程序定制皮肤，而那个边框无法支持所期望的外观。）其次，设计人员希望修改 Prev 和 Next 按钮，使其变为圆形而非方形，并使用图像代替文本；另外，为了保持一致，设计人员希望这些按钮在用户悬停之前保持隐藏。

## 移除边框

从应用程序中移除 Windows 边框实际上相当简单，因为你只需在窗体上设置两个属性。第一个是 WindowStyle，设置为 None；第二个是 AllowTransparency，设置为 True。你可以通过在窗口属性的结束括号前添加下面这一行来实现：

```
WindowStyle="None" AllowsTransparency="True"
```

一旦你在 XAML 中添加了这一行，即可在调试器中运行应用程序。这是一个很好的时机，不仅可以测试这一更改带来的效果，还可以测试你为减少应用程序中控件数量所做的其他更改。结果如图 17-8 所示。你可能会注意到，不再有任何与移动、调整大小、关闭或最大化窗口相关的控件。事实上，如果你不是在 Visual Studio 调试器中启动该应用程序，你将需要通过任务管理器来结束进程，因为你还没有通过用户界面提供任何结束此应用程序的方式。

![](img/d99870e80390742f93963da7be0b2e61_645_0.png)

**图 17-8**

为了能够为该应用程序定制皮肤，你需要提供一些控件，以实现大多数窗体开发人员习以为常的许多基本窗口行为。这并没有听起来那么难。主要挑战是添加一系列按钮，用于最大化并还原应用程序窗口、关闭应用程序，当然还有调整应用程序大小。因为你的设计人员想要定制皮肤，所以你决定处理调整大小能力的最佳方式是在右下角放置一个热点区域，代表该调整大小功能。

然而，你的首要任务是提供一种移动窗口的方式。为此，你将添加一个矩形区域，该区域映射到顶部 Grid.Row。这个矩形支持捕获 MouseDown 事件，并在用户按住鼠标按钮拖动窗口时做出响应。由于移动窗口本质上是一种鼠标按下并拖动的活动，而不是单击事件，因此 Rectangle 是快速简便地实现此功能的控件。只需在网格中作为第一个控件添加一行 XAML：

```
<Rectangle Name="TitleBar" HorizontalAlignment="Stretch" Margin="0,0,0,0" Stroke="Black" Fill="Green" VerticalAlignment="Stretch" />
```

当然，你现在已经用漂亮的绿色填充了默认矩形，以便于可见性，并在控件周围保留了黑色边框。这两个元素有助于你在这段 XAML 交给设计人员进行整理之前，看到矩形的位置。然而，除此之外，拥有一个控件只是完成了一半；另一半是检测并响应 DragMove 事件。

这可以通过下面的事件处理程序完成，该处理程序使用 VB 添加：

```
Private Sub Rectangle_MouseLeftButtonDown(ByVal sender As Object, _
    ByVal e As System.Windows.Input.MouseButtonEventArgs) _
    Handles TitleBar.MouseLeftButtonDown

    Me.DragMove()
End Sub
```

回顾一下，处理程序中只有一行代码——调用 Window 基类上的内置方法 DragMove。此方法处理将窗口拖动到新位置的操作。目前，处理程序只查找从名为 TitleBar 的控件上开始的拖动，但你可以将其更改为其他控件，甚至更改哪个控件被命名为 TitleBar。

解决了第一个问题之后，你可以转向第二个问题：实现最小化、最大化和关闭所需的三个按钮。在每种情况下，所需操作只在单击事件之后发生。按钮的一个独特特性是它能检测单击事件，因此它是实现这些操作的自然选择。这里的按钮应为图像按钮，所以第一步是创建一些简单的图像。

示例项目中已添加了四个图像引用。是的，这些图像很丑，但这里的目标并不是创建华丽的设计元素。你完全可以花上几天时间微调次要的 UI 元素，但这不应成为你的重点。这里的重点是创建可在 UI 中使用的元素。按钮的颜色、关闭按钮是否看起来像 Windows 图标等在此刻都是无关紧要的。你在这里关心的是提供一个带有基本元素的按钮，以便设计人员日后自定义。通常来说，不要将设计与实现混在一起。

工程师创建图形最简单的方式是使用举世闻名的画图程序。这并非最佳方式，甚至不是唯一方式，毕竟连 Visual Studio 也自带一个基本的图像编辑器。这里的目标不是精美的图像，而是合理且有意义的图像。创建四个必要的 .jpg 文件，尺寸为 24×24 像素，并为窗口的调整大小手柄包含一个图像。接下来，访问 MyProject 页面并选择 Resources 选项卡。然后，选择你的每一个 .jpg 文件，并将它们作为 Image 资源添加到项目中，如图 17-9 所示。

![](img/d99870e80390742f93963da7be0b2e61_646_0.png)

**图 17-9**

注意，Visual Studio 会自动将这些项目放入项目的 Resources 文件夹中。接下来，请验证在每个文件的属性中，BuildAction 属性是否设置为 Resource。为了能在 XAML 中引用这些资源，它们必须被指定为资源，而不仅仅位于此文件夹中。现在对你的项目执行一次完整生成，以便资源被编译。

此时，你可以回到 XAML 设计器，添加用于最小化、最大化和关闭的三个按钮。就你的目的而言，它们应位于显示区域的右上角，并且大小应与你新的图形差不多。将一个按钮拖到设计图面上，然后编辑 XAML，将其放置在右上角，并将高度和宽度设置为 20 像素。完成此操作后，一种简单的做法是复制第一个按钮，并在 XAML 中再粘贴两个类似的按钮。然后你只需要更改按钮名称和位置即可。瞧——三个按钮。

当然，你的目标是在这些按钮上显示图像，因此你需要向窗体添加一个 Image 控件，然后移动该控件，使其成为第一个按钮的内容。在这种情况下，只需使用 Margin 属性将图像控件绑定到按钮的边界，然后向按钮添加源。这里，源是你对 .jpg 资源的本地引用，因此在 ButtonClose 的情况下，source 值设置为 /Resources/20by_Exit.jpg。向另外两个按钮添加 Image 控件，并引用关联的资源，最终得到如下 XAML：

```xml
<Button Height="20" Width="20" HorizontalAlignment="Right" Margin="0,1,1,0" Name="ButtonClose" VerticalAlignment="Top">
    <Image Margin="0,0,0,0" Name="Image2" Stretch="Fill" Source="/Resources/20by_Exit.JPG"/>
</Button>
<Button Height="20" Width="20" HorizontalAlignment="Right" Margin="0,1,25,0" Name="ButtonMax" VerticalAlignment="Top" >
    <Image Margin="0,0,0,0" Name="Image3" Stretch="Fill" Source="/Resources/20by_Max.JPG"/>
</Button>
<Button Height="20" Width="20" HorizontalAlignment="Right" Margin="0,1,47,0" Name="ButtonMin" VerticalAlignment="Top" >
    <Image Margin="0,0,0,0" Name="Image4" Stretch="Fill" Source="/Resources/20by_Min.JPG"/>
</Button>
```

> 代码片段来自 MainWindow.xaml

至此，在此应用程序上实现自定义外壳所需的基本 XAML 元素已经就位。注意每个按钮都有特定的名称：ButtonClose、ButtonMax 和 ButtonMin。你会需要这些名称，而且设计不能更改它们，因为你将使用按钮名称来处理每个按钮的 Click 事件。在每种情况下，你都需要执行一个简单操作：

```
Private Sub ButtonMin_Click(ByVal sender As Object, _
    ByVal e As RoutedEventArgs) _
    Handles ButtonMin.Click

    Me.WindowState = WindowState.Minimized
End Sub

Private Sub ButtonMax_Click(ByVal sender As Object, _
    ByVal e As RoutedEventArgs) _
    Handles ButtonMax.Click

    If (Me.WindowState = WindowState.Maximized) Then
        Me.WindowState = WindowState.Normal
    Else
        Me.WindowState = WindowState.Maximized
    End If
End Sub

Private Sub ButtonClose_Click(ByVal sender As Object, _
    ByVal e As RoutedEventArgs) _
    Handles ButtonClose.Click

    Me.Close()
End Sub
```

> 代码片段来自 MainWindow.vb

