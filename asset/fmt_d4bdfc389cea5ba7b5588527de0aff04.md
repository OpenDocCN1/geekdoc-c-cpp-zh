
> *来自 MainWindow.xaml 的代码片段*

请注意，如果你不是跟着文本操作，而是直接查看示例下载，请记住，下载中包含了第一步创建过程中将要进行的所有更改。

前面的代码片段包含一些你现在可以重现的编辑。请注意，窗口的标题已被修改为与项目名称匹配。

`XAML` 现在包含了一个与 `Grid.RowDefinitions` 相关的新部分。这个部分包含了网格中各点对应区域的规范。当你在设计器中选择这些点时，实际上就是在定义这些区域。与每个区域高度关联的默认语法是像素数后跟一个星号。星号表示当窗口调整大小时，该行也应调整大小。对于此应用程序，只有中间区域应调整大小，因此已从顶部和底部的行定义中移除了星号。

这提供了一组定义好的区域，可用于对齐本窗体中的控件。因此，下一步是向窗体添加一些控件并创建基本用户界面。在这种情况下，这些操作对于任何使用过 Windows Forms 或 ASP.NET 窗体的开发人员来说都应该非常熟悉。

### 控件

`WPF` 提供了一套完全不同的库来开发应用程序。然而，尽管这些控件存在于不同的库中，但从 Visual Basic 中与它们交互的方式通常是相同的。每个控件都有一组你可以利用的属性、事件和方法。`XAML` 文件可能会以 XML 的声明式格式分配这些值，但你仍然可以在 Visual Basic 代码中引用框架创建的对象实例上的相同属性。

从网格的最顶部区域（`Grid.Row` 0）开始，将以下控件从工具箱拖到窗体上：一个 `Label`、一个 `TextBox` 和一个 `Button`。可以按照添加时的相同顺序将它们对齐到这个区域中。确保标签绑定到窗口的左侧和顶部，而按钮绑定到窗口的右侧和顶部。同时，文本框应绑定到窗口的顶部和两侧，这样当窗口被拉伸时，文本框的宽度会增加。生成的 `XAML` 应该类似于下面这样：

```xml
<Window x:Class="MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="ProVB_WPF" Height="350" Width="525" Name="MainWindow">
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition Height="45" />
            <RowDefinition Height="215*" />
            <RowDefinition Height="40" />
        </Grid.RowDefinitions>
    </Grid>
</Window>
```

<Label Margin="0,11,0,0" Name="Label1" HorizontalAlignment="Left" Width="80" Height="23" VerticalAlignment="Top">Image Path:</Label>

<TextBox Margin="81,13,92,0" Name="TextBox1" Height="21" VerticalAlignment="Top" />

<Button HorizontalAlignment="Right" Margin="0,11,9,11" Name="ButtonBrowse" Width="75">Images . . .</Button>
</Grid>
</Window>

来自 MainWindow.xaml 的代码片段

如新增行所示（加粗），每个控件都被分配了一个名称并定义了一组可编辑属性。请注意，这些名称可以在代码中引用，并且您可以根据该控件的命名实例来处理每个控件的事件。目前，只需调整标签中的文本，以指示其右侧的文本框将包含图像的文件夹路径，并调整按钮控件。将按钮控件重命名为 `ButtonBrowse`，并使用文本 `Images . . .` 作为按钮标签。显然，这个按钮还有更多工作要做，但目前你可以完成初始用户界面的创建。

接下来，按以下顺序添加以下控件。首先，添加一个 `Image` 控件。为了实现与图 17-2 所示类似的设计表面，将 `Image` 控件放置使其同时覆盖网格显示的中间和底部两个部分。现在在显示的底部部分添加三个按钮。此时控件可以进行对齐。你可以通过直接编辑 `XAML` 和在屏幕上定位相结合的方式来实现。例如，使用设计表面将 `Image` 控件扩展到两个底部网格行的极限；同样，在设计表面上视觉上对齐按钮。

![](img/d99870e80390742f93963da7be0b2e61_632_0.png)

图 17-2

如图所示，两个行定义的分隔在设计表面中描述，并且每个按钮都有自定义标签。请注意，`Next` 按钮后面跟着一对大于号符号，但 `Prev` 按钮缺少匹配的一对小于号符号。它们本可以作为 `&lt` 符号添加，但 Visual Basic 代码中要进行的一项更改就是在按钮标签中添加这些符号。

首先，回顾 `XAML` 代码并确保，例如，`Image` 控件被分配到 `Grid.Row` 1，并且属性 `Grid.RowSpan` 为 2。与 `Grid.Row` 0 中的项目不同，其他行中的项目必须显式分配。同样，网格底部行中每个按钮的名称和标题都被修改以反映该控件的行为。以下 `XAML` 中显示了这些以及类似的更改：

```
<Window x:Class="MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="ProVB_WPF" Height="350" Width="525" Name="MainWindow">
<Grid>
<Grid.RowDefinitions>
<RowDefinition Height="45" />
<RowDefinition Height="215*" />
<RowDefinition Height="40" />
</Grid.RowDefinitions>
<Label Margin="0,11,0,0" Name="Label1" HorizontalAlignment="Left" Width="80" Height="23" VerticalAlignment="Top">Image Path:</Label>
<TextBox Margin="81,13,92,0" Name="TextBox1" Height="21" VerticalAlignment="Top" />
<Button HorizontalAlignment="Right" Margin="0,11,9,11" Name="ButtonBrowse" Width="75">Images . . .</Button>
<Image Grid.Row="1" Grid.RowSpan="2" Margin="0,0,0,0" Name="Image1" Stretch="Fill" />
<Button Grid.Row="2" HorizontalAlignment="Right" Margin="0,0,15,8" Name="ButtonNext" Width="75" Height="23" VerticalAlignment="Bottom">Next >></Button>
<Button Grid.Row="2" HorizontalAlignment="Left" Margin="15,0,0,8" Name="ButtonPrev" Width="75" Height="23" VerticalAlignment="Bottom">Prev</Button>
<Button Grid.Row="2" Margin="150,0,150,8" Name="ButtonLoad" Height="23" VerticalAlignment="Bottom">View Images</Button>
</Grid>
</Window>
```

来自 MainWindow.xaml 的代码片段

请注意加粗部分中对新控件的描述。`Image` 控件排在第一位，它被放置在 `Grid.Row` 编号为 1 的位置，由于 .NET 数组始终从零开始，这就是第二行。该节点上的第二个属性表示它将在网格中跨越不止一行。目前，该控件使用默认名称，并且已设置使其拉伸以填充包含它的区域。

在 `Image` 控件之后是显示底部三个按钮的定义。目前，这些按钮将控制图像的加载；在本章的后续部分中，这些按钮将被删除或大幅重做。这些按钮的顺序并不重要，因此按照文件中出现的顺序，第一个按钮与其他按钮一样位于网格的最后一行。该按钮被放置在此区域的右侧，并绑定到显示的底部和右角。其名称已更改为“`ButtonNext`”，其标签为“`Next >>`”。

下一个按钮是 `Prev` 按钮，它被放置并绑定到显示的左侧和底部。其名称已更改为“`ButtonPrev`”，其显示文本已更改为“`Prev`”。如前所述，箭头符号不在按钮名称中；正如你可以在自己的代码中测试的那样，尝试在此处添加它们会导致错误。

最后是居中于显示区域的 `ButtonLoad` 按钮。它已绑定到显示的两侧以保持其居中位置。该按钮的标签为“`View Images`”，这当然是该应用程序的目标。然而，为了实现这一点，你需要该按钮的事件处理程序；事实上，为了实现应用程序的基本行为，你需要多个事件处理程序。

### 事件处理程序

在以前版本的 Visual Studio 中，你可以单击一个控件，Visual Studio 会自动为该控件在代码中生成默认事件处理程序。幸运的是，`WPF` 也提供了这种行为，因此生成以下事件处理程序：

- 双击窗体的标题栏以生成 `MainWindow_Loaded` 事件处理程序。
- 双击 `Images` 按钮以创建 `ButtonBrowse_Click` 处理程序。
- 双击 `Load` 按钮以创建 `ButtonLoad_Click` 处理程序。
- 双击 `Prev` 按钮以创建 `ButtonPrev_Click` 处理程序。
- 双击 `Next` 按钮以创建 `ButtonNext_Click` 处理程序。

要创建每个处理程序，你需要返回到设计视图并单击相关控件，但在创建后你可以大部分时间停留在代码视图中。看看 `ButtonBrowse_Click` 事件处理程序的方法存根：

```
Private Sub ButtonBrowse_Click(ByVal sender As System.Object, _
    ByVal e As System.Windows.RoutedEventArgs) _
    Handles ButtonBrowse.Click
End Sub
```

前面的代码使用行扩展字符重新格式化以提高可读性，但这基本上就是每个事件处理程序的样子。作为 Visual Basic 开发人员，你应该对这种语法非常熟悉。请注意，方法名称是基于控件名称和所处理的事件生成的。参数列表使用“`sender`”和 `e` 参数值生成，尽管 `e` 值现在引用 `System.Windows` 命名空间中的不同对象。最后，这里定义了 VB 特有的 `Handles` 语法，指示此方法是一个事件处理程序，以及它处理的具体事件或事件。

虽然这是一种非常熟悉、强大且甚至推荐的在 VB 和 `WPF` 中定义事件处理程序的方式，但它并不是唯一的方式。`WPF` 允许你在 `XAML` 代码中定义事件处理程序。说实话，如果这是一本关于 C# 的书，我们可能会花相当多的时间介绍这种类型的事件处理程序声明的优点。毕竟，C# 不支持将事件处理程序声明与处理该事件的方法直接关联；因此，C# 开发人员更喜欢在 `XAML` 中声明他们的事件处理程序。

> Visual Basic 提供了 `WPF` 的默认实现，鼓励与 C# 相比 UI 与应用程序代码的耦合更少。

然而，`XAML` 的目标之一是将应用程序逻辑与 UI 分离，而在 UI 中放置事件处理程序的名称实际上将 UI 与应用程序逻辑耦合起来。UI 不应关心 `Click` 事件或 `DoubleClick` 或任何其他事件是否被自定义逻辑处理。因此，虽然本节介绍了如何在 `XAML` 中直接定义事件的方法，但建议使用实现处理程序的代码来定义事件处理程序。

为了在代码中演示这一点，请返回到窗体的设计视图。选择 `Images` 按钮并将光标定位在命名此节点的单词 `Button` 之后。按下空格键。你会看到出现了 IntelliSense，指示在此控件上可用的属性和事件。输入 `c` 会调整 IntelliSense 显示，使你看到 `click` 事件。通过按 Tab 选择此事件，你会看到如图 17-3 所示的显示。

![](img/d99870e80390742f93963da7be0b2e61_635_0.png)

### FIGURE 17-3

如图所示，不仅 `XAML` 编辑器支持为控件选择属性和事件的完整 IntelliSense，当选择事件时，它会显示可处理此事件的可能方法列表。特别值得注意的是列表中的第一项，它使你能够请求在代码中创建新的事件处理程序。选择此项会告诉 Visual Studio 生成与双击控件时创建的相同事件处理程序存根；但是，与其将 `Handles` 子句放在此方法上，该方法的事件处理程序定义保留在 `XAML` 中。

这会导致两个问题。首先，如果你只查看代码，那么没有任何明确的指示表明代码中的某个方法是否确实是事件处理程序。这使得维护代码变得有点（不是很多）更困难。其次，如果你处理的是特定于 Windows 而非 Web 的事件，那么你的 `XAML` 就无法移植。这两种副作用都不 desirable。因此，鉴于 VB 将事件定义为方法声明的一部分的语法，本章中的代码避免了嵌入式 `XAML` 风格的声明标准 Windows 事件处理程序的方式。

此时，你可以运行你的应用程序。它除了允许你关闭它之外什么也不会做，但你可以验证其行为符合预期并保存你的工作。

### Adding Behavior

几乎是时候让这个 UI 做点什么了，但在开始处理代码之前还有一步。作为此应用程序的一部分，你希望允许用户选择应显示图像的目录。理论上，你可以（并且在实践中，在某个时候很可能会）编写一个用于选择或导航到图像目录的自定义界面。然而，对于此应用程序来说这并不重要，你想要一个快速简单的解决方案。

不幸的是，`WPF` 没有提供任何原生控件来支持快速轻松地查看文件系统。然而，Windows Forms 提供了，而且在这种情况下你希望利用此控件。好消息是你可以使用它，更好的消息是你不需要 Windows 互操作库即可做到这一点。因为像 Browse Folders 对话框之类的东西并不是托管在你的窗体上的控件，你可以从代码中引用它。因此，虽然对于任何基于 UI 的控件，你需要本章 16 中讨论的 Windows Forms Integration Library 和 `WindowsFormsHost` 控件，但在这种情况下代码只需要引用 `System.Windows.Forms` 库。

由于 `System.Windows.Forms` 库不会自动作为 `WPF` 应用程序的引用包含在内，你需要手动添加对该库的引用。请记住，此库在 `WPF` 的 rich client 实现之外对你不可用。因此，此功能仅限于在客户端运行的 `WPF`；对于其他场景，你将更改选择图像的方式。打开 My Project 显示并选择 References 选项卡。单击 Add 按钮打开 Add Reference 对话框，然后选择 `System.Windows.Forms` 库，如图 17-4 所示。你不能在不利用 `Windows.Forms.Integration` 库的情况下向 `WPF` 窗体添加控件，但你可以在幕后继续引用 Windows Forms 的控件和功能。

![](img/d99870e80390742f93963da7be0b2e61_636_0.png)

FIGURE 17-4

有了这个额外的引用，你就可以开始向此应用程序放置一些代码。从 `window_loaded` 事件开始。此事件是你将定义图像库的默认路径、设置 `Prev` 按钮的标签以及更改网格控件的默认属性以使其按你想要的方式处理图像的地方：

```
Private Sub MainWindow_Loaded(ByVal sender As System.Object, _
    ByVal e As System.Windows.RoutedEventArgs) _
    Handles MyBase.Loaded
' Append the << to the text for the button since these are _
' reserved characters within XAML
ButtonPrev.Content = "<< " & ButtonPrev.Content.ToString()
' Set the default path from which to load images
TextBox1.Text = _
    Environment.GetFolderPath(Environment.SpecialFolder.MyPictures)
' Have the images maintain their aspect ration
Image1.Stretch = Stretch.Uniform
End Sub
```
