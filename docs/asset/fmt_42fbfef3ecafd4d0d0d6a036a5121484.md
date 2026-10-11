
例如，假设一个 `Window` 包含一个带有 `Label` 的 `StackPanel`，而 `Label` 使用了名为 `LabelValue` 的资源。当它构建 `Label` 时，WPF 首先检查 `Label` 的资源字典（如果存在）以寻找 `LabelValue`。如果没找到，WPF 将移动到 `StackPanel` 并搜索其资源。如果仍然找不到，WPF 将继续向上到 `Window` 并检查其资源。

如果在逻辑树顶部的 `Window` 中仍未找到 `LabelValue` 资源，WPF 将检查 `App.xaml` 文件查看其是否定义了该资源。

如果经过这一切之后 WPF 仍然找不到该资源，应用程序将以多种方式失败。例如，Expression Blend 窗口设计器不会渲染需要资源的控件，如果你尝试运行应用程序，它会失败。相反，Visual Studio 的窗口设计器会显示错误消息且不绘制任何控件。

## 20 | 第 12 章：资源

`ResourceHierarchy` 示例程序演示了资源的查找。下面的代码显示了程序的 `App.xaml` 文件。该文件定义了名为 `String1`、`String2`、`String3` 和 `String4` 的字符串资源。

```xml
<Application
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:sys="clr-namespace:System;assembly=mscorlib"
    x:Class="App"
    StartupUri="Window.xaml">
    <Application.Resources>
        <!-- 应用程序级别的资源应该定义在这里在这里 -->
        <sys:String x:Key="String1">String1 in App.Resources.</sys:String>
        <sys:String x:Key="String2">String2 in App.Resources.</sys:String>
        <sys:String x:Key="String3">String3 in App.Resources.</sys:String>
        <sys:String x:Key="String4">String4 in App.Resources.</sys:String>
    </Application.Resources>
</Application>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_239_0.png)

下面的代码显示了程序的主 XAML 文件：

```xml
<Window
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:sys="clr-namespace:System;assembly=mscorlib"
    x:Name="Window"
    Title="ResourceHierarchy"
    Width="150" Height="180"
    FontSize="16" FontWeight="Bold">
    <Window.Background>
        <LinearGradient EndPoint="0.5,0.5" StartPoint="0.5,0.0">
            <GradientStop Color="#FFFFFFFF" Offset="0"/>
            <GradientStop Color="#FFA6009F" Offset="1"/>
        </LinearGradient>
    </Window.Background>
    <Window.Resources>
        <sys:String x:Key="String2">String2 in Window.Resources.</sys:String>
        <sys:String x:Key="String3">String3 in Window.Resources.</sys:String>
        <sys:String x:Key="String4">String4 in Window.Resources.</sys:String>
    </Window.Resources>
    <StackPanel Margin="5">
        <StackPanel.Resources>
            <sys:String x:Key="String3">
                String3 in StackPanel.Resources.
            </sys:String>
            <sys:String x:Key="String4">
                String4 in StackPanel.Resources.
            </sys:String>
        </StackPanel.Resources>
        <Label Content="{StaticResource String1}"/>
        <Label Content="{StaticResource String2}"/>
        <Label Content="{StaticResource String3}"/>
        <Label>
            <Label.Resources>
                <sys:String x:Key="String4">
                    String4 in Label.Resources.
                </sys:String>
            </Label.Resources>
        </Label>
    </StackPanel>
</Window>
```

`ResourceHierarchy`

在这段代码中，`Window` 定义了资源 `String2`、`String3` 和 `String4`；`StackPanel` 定义了资源 `String3` 和 `String4`；而最后一个 `Label` 定义了资源 `String4`。

第一个 `Label` 使用了资源 `String1`。WPF 采样了逻辑树，在包含它的 `StackPanel` 或 `Window` 中没有找到名为 `String1` 的资源。它最终在 `App.xaml` 的应用程序资源字典中找到了该资源。

同样，第二个 `Label` 在 `Window` 的资源中找到了它的资源 `String2`，而第三个 `Label` 在 `StackPanel` 的资源中找到了它的资源 `String3`。

第四个 `Label` 略有不同，因为它定义了自己的 `String4` 资源。它的内容被设置为一个 `StaticResource` 对象，该对象提供了资源的键 `String4`。

## 缺失的属性

在在下面的代码中，使用属性而不是 `StaticResource` 的内容是很有诱惑力的：

```xml
<Label Content="{StaticResource String4}">
  <Label.Resources>
    <sys:String x:Key="String4">
      String4 in Label.Resources.
    </sys:String>
  </Label.Resources>
</Label>
```

遗憾的是，当 WPF 读取 `Label` 的 `Content` 属性时，`Label` 的资源字典尚未准备绪。Expression Blend 的 Window 设计器似乎能正确找到该值，但在运行时和 Visual Studio 设计器中，`Label` 无法找到它自己的资源，并向上逻辑树移动到 `StackPanel` 版本的 `String4`。

## 合并资源字典

合并资源字典允许多个控件、窗口或应用程序共享相同的值。要合并字典，请创建一个以 `ResourceDictionary` 对象为根元素的 XML 文件。像处理 `Window` 一样给该元素添加命名空间属性，并将资源放在字典内部。

## 准备就绪字典

你可以将 `Window` 的命名空间声明复制并粘贴到资源字典中。Visual Studio 和 Expression Blend 可以添加带有默认命名空间声明的资源字典。在 Visual Studio 中，打开“项目”菜单，选择“新建项”命令，选择“资源字典”命令并点击“添加”。在 Expression Blend 中，打开“文件”菜单，选择“新建项”命令，选择“资源字典”项并点击“确定”。

下面的代码显示了一个名为 `RectangleResources.xaml` 的资源字典。该文件定义了 `MultiWindow` 示例程序使用的资源（为了节省空间，我省略了一些资源）。

```xml
<ResourceDictionary
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:sys="clr-namespace:System;assembly=mscorlib">
    <!-- 资源字典项应该定义在这里 -->
    <sys:Double x:Key="rectWidth">140</sys:Double>
    <sys:Double x:Key="rectHeight">50</sys:Double>
    <sys:Double x:Key="rectRadX">5</sys:Double>
    <sys:Double x:Key="rectRadY">20</sys:Double>
    <!-- 其他资源省略 ...
</ResourceDictionary>
```

`MultiWindowResources`

下面的代码显示了 `MultiWindow` 程序如何使用此字典。`Window` XAML 文件使用了 `ResourceDictionary.MergedDictionaries` 元素，该元素包含了对字典文件的引用。

```xml
<Window.Resources>
  <ResourceDictionary>
    <ResourceDictionary.MergedDictionaries>
      <ResourceDictionary Source="Rectangle.xaml"/>
    </ResourceDictionary.MergedDictionaries>
  </ResourceDictionary>
</Window.Resources>
```

下面的代码显示了 `Window` 如何使用这些资源。此代码创建了一个引用外部字典中资源的 `Rectangle`。

```xml
<Grid MouseDown="AddUser_MouseDown">
    <Rectangle
        Margin="{StaticResource rectMargin}"
        Width="{StaticResource rectWidth}"
        Height="{StaticResource rectHeight}"
        RadiusX="{StaticResource rectRadX}"
        RadiusY="{StaticResource rectRadY}"
        Fill="{StaticResource rectFill}"
        Stroke="{StaticResource rectStroke}"
        StrokeThickness="{StaticResource rectStrokeThickness}"
        BitmapEffect="{StaticResource rectBitmapEffect}"/>
    />
    <Label HorizontalAlignment="Center" VerticalAlignment="Center"
           Content="Add User"
           FontSize="{StaticResource rectFontSize}"
           FontWeight="{StaticResource rectWeight}"/>
    />
</Grid>
```

`MultiWindowResources`

`MultiWindowResources` 示例使用类似的代码在其四个窗口 中包含资源字典。由于每个表单都引用相同的资源，它们具有共同的外。如果你决定更改外观，只需修改资源字典，所有表单都会自动更新。

图 12-8 显示了 `MultiWindowResources` 程序显示了几个类似按钮的表单。除了允许多个表单或应用程序共享资源外，合并字典允许单个窗口加载多个资源字典。如果你希望分开字典来存储资源组，这将非常有用。例如，你可能会分开字典来存储按钮资源、标签资源列表资源。

## 被覆盖的资源

当程序加载资源字典时，它的值将覆盖从其他资源字典加载的同名资源，因此最后加载的值是控件使用的值。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_239_0.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_241_0.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_241_1.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_242_0.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_242_1.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_243_0.png)

由于加载了 `ResRed.xml` 文件，该中的资源值具有优先级。图 12-9 显示了 `ResourceDictionaries` 程序使用了该资源字典中的值。

通过简单地切换这些资源字典的顺序，你就可以完全改变应用程序的外观。图 12-10 显示了 `ResourceDictionaries` 程序使用了 `ResBlue.xaml` 资源字典中的值。

第 16 章中的“Skins”节解释了如何以类似的方式在运行时切换应用程序的外观。

## 动态资源

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_244_0.png)

图 12-9

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_244_1.png)

图 12-10

为止，本章只使用了静态资源。如果 WPF 遇到 XAML 文件，它会查找资源的值并将其赋值给当前正在读取的属性。一旦属性值被设置，WPF 就不会再次查找。

这就是为什么本章较早“资源层次结构”节中描述的后续代码不起作用。属性 `Content="StaticResource String4"` 位于 `Label` 资源之前，当需要该资源时，资源尚未准备绪。

```xml
<Label Content="StaticResource String4">
<Label.Resources>
  <sys x:Key="String4">
    String4 in Label.Resources.
  </sys>
</Label.Resources>
</Label>
```

动态资源与静态资源类似，不同在于它不是在第一次遇到时就读取。WPF 并不是立即设置属性的值，而是等待并在实际需要时再查找属性的值。

例如，以下代码（使用 `DynamicLabelResource` 示例程序）可以正常工作。代码记录了 `Content` 使用资源值 `String4` 的事实，但在准备渲染 `Label` 之前不会查找值。到那时，资源已经存在了。

```xml
<Label Content="DynamicResource String4">
<Label.Resources>
  <sys x:Key="String4">
    String4 in Label.Resources.
  </sys>
</Label.Resources>
</Label>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_244_2.png)

## 资源密集资源

```xml
</sys:String>
</Label.Resources>
</Label>
```

`DynamicLabelResource`

对于 WPF 来说，实现动态资源比实现静态资源要得多；因此，通常情况下，在可行的情况下最好使用静态资源。在上一个示例中，你可以在 `Label` 的容器而不是 `Label` 中使用 `String4` 资源。这样你就可以使用静态资源而不是动态资源了。

除了延迟查找外，WPF 还准备了动态资源，以便能够检测其值的变化。例如，如果上一个示例中的资源 `String` 在程序运行时发生了变化，WPF 将检测到该变化并更新 `Label` 以显示新值。

这种检测能力通常用于系统定义的资源，如系统颜色。如果用户打开系统配置应用程序并更改系统颜色，程序会自动重新加载任何修改过的资源。

`SimpleClock` 示例演示了两种变化的资源——由程序更改的资源和更改的系统颜色。

程序使用以下资源声明创建一个名为 `TimeNow` 的简单字符串：
