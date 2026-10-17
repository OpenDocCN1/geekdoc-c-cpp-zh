
```xml
<Window Class="AddingBorders.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="AddingBorders" Height="350" Width="525">
<Grid>
    <Border Background="Pink" BorderBrush="Black" BorderThickness="5"
           CornerRadius="30">
        <Button BorderBrush="Blue" Height="100" Width="100" BorderThickness="4" Background="Violet"/>
    </Border>
</Grid>
</Window>
```

在列表 9.9 中，为 `Grid` 和 `Button` 控件添加了边框。背景颜色和边框颜色分别通过 `Background` 和 `BorderBrush` 属性设置。你可以使用 `CornerRadius` 属性来设置边框各角的圆角程度。按 `F5` 键运行应用程序。

列表 9.9 的输出如图 9.35 所示：

![](img/17af790174c480761404624aeed9b30b_431_1.png)

图 9.35：AddingBorders 应用程序的输出

# 使用 PasswordControl

`PasswordControl` 是一种简单的 `TextBox` 类型，它以加密格式显示用户输入的文本。让我们使用 XAML 代码为 WPF 应用程序添加一个 `PasswordControl`。创建一个名为 `PasswordControl` 的 WPF 应用程序，并将列表 9.10 单元代码添加到 `MainWindow.xaml` 文件中。

```xml
Listing 9.10 PasswordControl 应用程序的代码
<Window x:Class="PasswordControl" width="120" height="250"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="PasswordControl" Height="325">
    <Grid>
        <Border Background="Peachpuff" CornerRadius="10">
            <StackPanel HorizontalAlignment="Center" VerticalAlignment="Center" Margin="10,0,10,0">
                <Label Name="label1" HorizontalAlignment="Left" Margin="0,5">Enter Name:</Label>
                <TextBox Name="textbox1" width="120"/>
                <Label Name="label2" HorizontalAlignment="Left" Margin="0,5">Password:</Label>
                <PasswordBox Name="password1" width="120"/>
                <Button Name="button1" Margin="0,24,0,110" Content="Submit" VerticalAlignment="Top" />
            </StackPanel>
        </Border>
    </Grid>
</Window>
```

在列表 9.10 中，窗口中添加了一个 `Passwordbox`。你可以使用 `TextBox` 的 `MaxLength` 属性来设置 `PasswordBox` 中允许的最大字符数。你可以通过设置 `PasswordChar` 属性来更改 `PasswordControl` 中显示的字符。默认情况下，框内会出现一个黑点（*）；但你可以更改它。在我们案例中，`PasswordBox` 的字符被设置为星号（*）。现在，按 `F5` 键运行应用程序。

图 9.36 显示了输入名称和密码后的输出：

![](img/17af790174c480761404624aeed9b30b_432_0.png)

**图 9.36：PasswordControl 应用程序的输出**

## 在 WPF 应用程序中创建滚动区域

在 WPF 中，你可以使用 `ScrollViewer` 和 `ScrollBar` 控件创建滚动区域。这些控件主要用于启用窗口内内容的滚动。当你的内容大于窗口大同时，你可以在 WPF 应用程序中添加 `ScrollViewer`。`ScrollView` 允许你滚动查看窗口的所有内容。通过设置 `VerticalScrollVisibility` 属性设置垂直滚动，通过设置 `HorizontalScrollVisibility` 属性设置水平滚动区域：让我们通过 XAML 代码为 WPF 应用程序添加 `ScrollViewer`。创建一个名为 `ScrollableArea` 的 WPF 应用程序，并将列表 9.11 的代码添加到 `MainWindow.xaml` 文件。

### 第9章：使用 WPF 4.5 资源、样式、模板和命令

列表 9.11：ScrollableArea 应用程序的代码

<window x:Class="ScrollableArea.MainWindow"

      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"

      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"

      Title="ScrollableArea">

  <Grid>

    <ScrollView HorizontalScrollVisibility="Auto" VerticalScrollVisibility="Auto">

        <Rectangle Fill="Red" Width="1000" Height="1000"/>

    </ScrollView>

  </Grid>

</window>

在列表 9.11 中，为应用程序添加了一个 `Rectangle`，其大小超过了窗口。`ScrollView` 允许你滚动查看窗口的全部内容。按 `F5` 键运行应用程序。

图 9.37：ScrollableArea

![](img/17af790174c480761404624aeed9b30b_433_png)

## 使用 Slider

在 WPF 中，正如“深度”节中讨论的那样，你可以使用 `Slider` 来创建一个滚动区域。`Slider` 主要用于在某个范围内选择值。让我们通过 XAML 代码为 WPF 应用程序添加 `Slider`。创建一个名为 `SliderControl` 的 WPF 应用程序，并将列表 9.12 的代码添加到 `MainWindow.xaml` 文件。

列表 9.12：Slider 应用程序的代码

<window x:Class="SliderControl.MainWindow"

      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"

      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"

      Title="Slider" Height="350" Width="525">

  <Grid>

    <Slider Minimum="0" Maximum="100" TickFrequency="10" TickPlacement="Bottom"/>

  </Grid>

</window>

在列表 9.12 中，窗口中添加了一个 `Slider`。列表 9.12 的输出如图 9.38 所示：

![](img/17af790174c480761404624aeed9b30b_433_1.png)

图 9.38：Slider 应用程序的输出

## 使用 Viewbox

`Viewbox` 是一种简单的控件，它会缩放内容以适应可用空间。让我们使用 XAML 代码为 WPF 应用程序添加 `Viewbox`。创建一个名为 `Viewbox` 的 WPF 应用程序，并将列表 9.13 的代码添加到 `MainWindow.xaml` 文件。

```xml
Listing 9.13 Viewbox 应用程序的代码
<window x:Class="Viewbox.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Viewbox" Height="350" Width="525">
    <Viewbox>
        <Canvas>
            <Ellipse Height="350" width="400" Background="BlancheAlmond"/>
        </Canvas>
    </Viewbox>
</window>
```

在列表 9.13 中，为窗口添加了一个 `Viewbox`。`Viewbox` 缩放内容以适应可用空间。注意 `Ellipse` 的大小为 350x400，但它被缩放到适应窗口。

## 为控件分配键

`AccessText` 控件用于为其他控件添加访问。`AccessText` 键可以通过键盘选择控件。如果内容包含多个下划线，第一个是访问键，其余的普通文本。让我们学习为 `Button` 控件分配访问键。

创建一个名为 `AccessKeys` 的 WPF 应用程序，并将列表 9.14 所示的代码添加到 `MainWindow.xaml` 文件。

列表 9.14：AccessKeys 应用程序的代码

```xml
<window class="AccessKeys.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="AccessKeys" Height="350" Width="525">
    <StackPanel>
    <Grid>
        <TextBlock Margin="10,10,10,3" FontSize="24">A_ccessText</TextBlock>
    </Grid>
    <DockPanel Height="150" width="300">
        <Button Name="myButton" Click="myButton_Click">Submit</Button>
    </DockPanel>
    </StackPanel>
</window>
```

### 第 9 章：使用 WPF 4.5 控件、资源、样式和命令

```xml
<AccessText>Hello</AccessText>
<Button Name="myButton1" Height="198"
Click="myButton1_Click_Hel_lo_wor_d"/>
<DockPanel>
<TextBox Name="textBox1" Width="50" Height="30"/>
<Label Width="200" Target="{Binding ElementName=textBox1}">
<AccessText wrapping="wrapwithoverflow">
<AccessText>
这是一个 _usingAccessText 的示例。
</AccessText>
</Label>
</DockPanel>
</StackPanel>
<Window>
```

列表 9.14 显示了两个控件：一个 `TextBox` 控件、一个按钮（`Button`）和一个窗口标签（label）。访问键（access key）已分配给按钮和标签。

现在，将列表 9.15 所示的代码添加到 `MainWindow.xaml.cs` 文件中：

列表 9.15：为 AccessKey_Controls 添加 MainWindow.xaml.cs 文件的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Media;
using System.Windows.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
namespace AccessKeys_Controls
{
    /// <summary>
    /// MainWindow.xaml 的交互逻辑
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }
        private void myButton_Click(object sender, RoutedEventArgs e)
        {
            MessageBox.Show("Hello button");
        }
        private void myButton1_Click(object sender, RoutedEventArgs e)
        {
            MessageBox.Show("Hello button");
        }
    }
}
```

添加代码后，按 `F5` 键运行应用程序。现在，当你点击 `myWeb` 按钮时，会出现一个带有有“Hello button”文本的消息框。同样，当你点击 `myButton` 按钮时，会出现一个带有“HelloWorld button”文本的消息框。若要查看控件的访问键，可以按下键盘上的 `ALT` 键。按下 `ALT` 键会在相应的控件上显示带有下划线的访问键。现在，当你按下键盘上的 `H` 键时，会出现带有“Hello button”文本的消息框。同样，当你按下键盘上的 `W` 键时，会出现带有“HelloWorld”文本的消息框。要选择窗口上的 Label，请按 `u` 键。`H` 键和 `u` 键分别是相应控件的访问键。现在，按 `F5` 键运行应用程序。`AccessKeys_Controls` 应用程序的输出如图 9.40 所示：

![](img/17af790174c480761404624aeed9b30b_436_0.png)

图 9.40：AccessKeys_Controls 应用程序的输出

## 使用 Expander 控件

`Expander` 控件用于在类似于窗口的可折叠区域内提供内容。让我们在名为 `ExpanderControl` 的 WPF 应用程序中添加一个 `Expander` 控件。创建一个 WPF 应用程序，并将图 9.16 所示的代码添加到 `MainWindow.xaml` 中：

列表 9.16：实现 Expander 控件的代码

```xml
<window xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" Title="ExpanderControl" height="200" width="525">
<Grid>
<Expander horizontalContentAlignment="Center">
<Expander.header>
<TextBlock>点击箭头</TextBlock>
</Expander.header>
<Expander.content>
<ScrollView Height="50">
<TextBlock TextWrapping="Wrap">
这是一个 expander 控件的示例。这同样是一个使用
应用程序 scrollviewer 控件的示例。你可以同时使用这两个控件为你的应用程序提供良好的外观和感受。
</TextBlock>
</ScrollView>
</Expander.content>
</Expander>
</Grid>
</window>
```

在列表 9.16 中，`Expander` 被包含在带有 `ScrollViewer` 控件的应用程序中。`ScrollView` 控件提供了一种滚动展开内容的方法。当你按 `F5` 键运行应用程序时，会出现一个带有箭头的窗口。当你点击箭头时，窗口上会显示文本，如图 9.41 所示：

![](img/17af790174c480761404624aeed9b30b_436_1.png)

图 9.41：ExpanderControl 应用程序的输出
