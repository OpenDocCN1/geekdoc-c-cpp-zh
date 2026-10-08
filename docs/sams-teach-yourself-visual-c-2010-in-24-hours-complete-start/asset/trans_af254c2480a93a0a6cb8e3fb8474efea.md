

尽管这是一个巨大的优势，但由于执行的代码是由编译器生成的，当绑定未能正确工作时，诊断问题可能会很困难。

现在，你已准备好为布局添加其余的控件。窗口左侧包含一个 ListBox 控件，用于显示照片；还有一个 Slider 控件，允许你调整列表中显示图像的大小。窗口右侧包含一个 StackPanel，由一系列 Label 控件组成，用于显示关于所选照片的属性。完成后的布局应如图 17.17 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_398_0.png)

实现此布局所需的 XAML 如清单 17.8 所示。

## 清单 17.8 剩余布局的 XAML

```xml
<DockPanel Grid.Row="1" Grid.Column="0" Margin="5,0,7,5">
    <DockPanel DockPanel.Dock="Bottom" Margin="5">
        <Label DockPanel.Dock="Left">Zoom:</Label>
        <Slider Name="ZoomSlider" Margin="10,0,0,0" Orientation="Horizontal"
            Minimum="80" Maximum="320" Value="160" TickFrequency="80"
            TickPlacement="BottomRight" SmallChange="5" LargeChange="20" />
    </DockPanel>
    <GroupBox>
        <ScrollViewer VerticalScrollBarVisibility="Auto"
            HorizontalScrollBarVisibility="Disabled">
            <ListBox IsSynchronizedWithCurrentItem="True" Name="PhotosListBox"
                Margin="5" SelectionMode="Extended" ItemsSource="{Binding}"
                SelectedIndex="0">
            </ListBox>
        </ScrollViewer>
    </GroupBox>
</DockPanel>

<GridSplitter Grid.Column="1" Grid.RowSpan="2" HorizontalAlignment="Left"
    VerticalAlignment="Stretch" Width="15" Background="Transparent"
    ShowsPreview="True" />

<GroupBox Grid.Column="1" Grid.Row="1" Margin="7,0,5,5">
    <ScrollViewer VerticalScrollBarVisibility="Auto"
        HorizontalScrollBarVisibility="Disabled">
        <StackPanel>
            <Label>Source:</Label><Label Content="{Binding Path=Source}" />
            <Label>Size:</Label><Label/>
            <Label>Date Image Taken:</Label><Label/>
            <Label>Camera Manufacturer:</Label><Label/>
            <Label>Camera Model:</Label><Label/>
            <Label>Creation Software:</Label><Label/>
            <Label>Lens Aperture:</Label><Label/>
            <Label>Focal Length:</Label><Label/>
            <Label>ISO Speed:</Label><Label/>
            <Label>Exposure Time:</Label><Label/>
            <Label>Exposure Mode:</Label><Label/>
            <Label>Exposure Compensation:</Label><Label/>
            <Label>White Balance Mode:</Label><Label/>
            <Label>Color Representation:</Label><Label/>
        </StackPanel>
    </ScrollViewer>
</GroupBox>
```

虽然创建一个功能有限的用户界面似乎是一项繁重的工作，但它比传统的用户界面开发具有几个显著优势。最简单但可能最重要的优势是，你可以将 XAML 文件交付给面向图形的人员，他们可以应用样式和其他视觉资源使应用程序脱颖而出，同时你可以继续开发应用程序的核心功能。只要底层的用户界面控件不发生变化，设计师和开发人员就可以继续工作而互不干扰。

## 为布局添加样式

为布局添加样式实际上可以指代许多不同的含义，每种含义具有不同程度的复杂性。在光谱的一端，是直接将颜色、背景图像和其他各种视觉元素应用于控件。在另一端，则是创建完整的样式表（类似于 Web 开发中的级联样式表 [CSS]）以及数据模板，这些模板可以彻底改变控件的外观。

每个 WPF `Window` 和 `Application` 都可以包含定义样式和数据模板的资源。在 `Window` 中定义的资源放置在 `Window.Resources` 元素中，并且仅局部用于该窗口。如果你需要整个应用程序可用的资源，可以将它们放置在 `App.xaml` 文件中的 `Application.Resources` 元素中。

由于样式和数据模板可能会变得相当庞大，WPF 还支持资源字典的概念。资源字典仅仅是一个在 `ResourceDictionary` 元素内包含样式和数据模板的 XAML 文件。要包含资源字典，只需向 `Window.Resources` 或 `Application.Resources` 添加一个 `ResourceDictionary` 元素，并提供包含这些资源的 XAML 文件。

例如，查看照片查看器应用程序的用户界面，你可能希望提供简单的渐变着色。如果不使用样式，你设置的每个属性都必须在每个标签上重复。然而，通过创建样式模板，你可以一次创建样式，然后将其应用于每个标签。只要样式的键名不改变，你就可以更改样式定义，而无需更改可能正在使用它的任何 XAML。

`PhotoViewer` 项目已经包含一个名为 `Resources.xaml` 的资源字典，但它未包含在 `Application.Resources` 中。将其添加到 `Application.Resources` 中，如清单 17.9 所示。

## 清单 17.9 带有资源字典的 App.xaml

```xml
<Application x:Class="PhotoViewer.App"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    StartupUri="MainWindow.xaml">
    <Application.Resources>
        <ResourceDictionary Source="Resources.xaml"/>
    </Application.Resources>
</Application>
```

此资源字典已经包含几个样式模板。其中一些只需包含资源字典即可自动应用，因为它们适用于特定控件的任何实例。为 `GroupBox` 定义的样式就是一个例子。

清单 17.10 显示了一个简单的样式，可以应用于 `StackPanel` 控件中的每个标题标签。

## 清单 17.10 Label 控件的样式

```xml
<Style x:Key="MetadataHeader" TargetType="{x:Type Label}">
    <Setter Property="Background">
        <Setter.Value>
            <LinearGradientBrush StartPoint="0,0.5" EndPoint="1,0.5" >
                <LinearGradientBrush.GradientStops>
                    <GradientStop Offset="0.5"
                        Color="{x:Static SystemColors.ControlDarkDarkColor}" />
                    <GradientStop Offset="2" Color="Transparent" />
                </LinearGradientBrush.GradientStops>
            </LinearGradientBrush>
        </Setter.Value>
    </Setter>
    <Setter Property="Foreground"
        Value="{StaticResource {x:Static SystemColors.ControlTextColor}}" />
    <Setter Property="FontWeight" Value="Bold" />
</Style>
```

x:Key 属性定义了样式的名称。你在 XAML 文件中将该名称应用于用户界面元素时使用此名称。TargetType 定义样式将应用到的类的类型名称。在清单 17.10 中，你定义了一个名为 MetadataHeader 的样式，它将被应用于 Label 类型的任何实例。此样式为背景属性定义了线性渐变，并设置了文本前景颜色和字体粗细。要应用此样式，请向 StackPanel 中每个用于标题的 Label 控件添加以下属性：

Style="{StaticResource MetadataHeader}"

如果你再次运行应用程序，你应该看到新的样式，如图 17.18 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_401_0.png)

**图 17.18**
重新设置样式的

## 摘要

在本节课中，你快速概述了 Windows Presentation Foundation 及其允许你执行的操作。你创建了一个简单的 WPF 应用程序，并添加代码以响应用户事件。最后，你学习了如何为你的应用程序创建样式，从而相对轻松地完全改变其外观。

此时，应用程序运行良好且外观不错，但实际上尚未执行任何操作。在下一节课中，当更详细地了解 WPF 提供的数据绑定功能时，你将学习如何将剩余部分整合在一起。

## 问答

问：*Windows Presentation Foundation 是什么？*

答：Windows Presentation Foundation (WPF) 是一种表示技术，提供统一的编程模型，使你能够构建包含用户界面元素、媒体和文档的 Windows 应用程序。

问：*采用标记和代码后置样式开发有什么好处？*

答：这实现了外观与行为之间的清晰分离，提供了以下好处：
- a. 降低开发和维护成本。
- b. 开发效率更高，允许应用程序的外观与实现应用程序行为的其他开发人员同时创建。
- c. 可以使用多种设计工具来创建和共享标记。

## 工作坊

### 测验

1.  Grid 中列和列的星号大小调整是什么？
2.  什么是路由事件？

