

![](img/d99870e80390742f93963da7be0b2e61_667_0.png)

## 图 17-18

在结束设计讨论之前，有必要简要介绍一下样式。可能不太明显，但如果你不覆盖样式，每个 WPF 应用程序都有一个隐式的样式定义。例如，当你向窗体添加按钮时，它如何知道其背景应为渐变银色？那些悬停和鼠标按下效果又是从哪里来的？

## 样式

样式本质上利用了资源的概念。使用样式时，你可以选择引用所有公共类型的对象并为该控件类型设置默认样式，也可以创建自定义样式，专门用于引用它的那些控件实例。简而言之，样式提供了一种机制，让你可以在整个应用程序中应用主题，并在需要覆盖主题的特定实例中覆盖该主题。如果之后另一位开发人员向你的应用程序添加新元素，默认样式会自动应用。

样式的定义方式与资源类似；实际上，它们定义在 XAML 文件中资源所在的同一部分。与资源一样，当你在应用程序级别定义样式时，该样式可以应用于应用程序中的所有窗口。相反，如果样式仅针对给定窗口、页面或用户控件中的对象，那么在该级别定义它们就很有意义。

与其提供一个简单的样式示例，不如看一个复杂的样式，它专注于标准按钮的悬停效果。此效果在默认样式内定义，以下代码块为类型为 Button 的控件提供了默认样式。请注意，以 XAML 格式生成此样式信息最好使用 Expression Blend 完成，如第 18 章所述。

```
```xml
<Style x:Key="ButtonFocusVisual">
    <Setter Property="Control.Template">
        <Setter.Value>
            <ControlTemplate>
                <Rectangle SnapsToDevicePixels="true" Stroke="Black" StrokeDashArray="1 2"
StrokeThickness="1" Margin="2"/>
```
```

```
</ControlTemplate>
    </Setter.Value>
</Setter>
</Style>
<LinearGradientBrush x:Key="ButtonNormalBackground" EndPoint="0,1" StartPoint="0,0">
    <GradientStop Color="#F3F3F3" Offset="0"/>
    <GradientStop Color="#EBEBEB" Offset="0.5"/>
    <GradientStop Color="#DDDDDD" Offset="0.5"/>
    <GradientStop Color="#CDCDCD" Offset="1"/>
</LinearGradientBrush>
<SolidColorBrush x:Key="ButtonNormalBorder" Color="#FF707070"/>
<Style x:Key="ButtonStyle1" TargetType="{x:Type Button}">
    <Setter Property="FocusVisualStyle" Value="{StaticResource ButtonFocusVisual}"/>
    <Setter Property="Background" Value="{StaticResource ButtonNormalBackground}"/>
    <Setter Property="BorderBrush" Value="{StaticResource ButtonNormalBorder}"/>
    <Setter Property="BorderThickness" Value="1"/>
    <Setter Property="Foreground" Value="{DynamicResource {x:Static SystemColors.ControlTextBrushKey}}"/>
    <Setter Property="HorizontalContentAlignment" Value="Center"/>
    <Setter Property="VerticalContentAlignment" Value="Center"/>
    <Setter Property="Padding" Value="1"/>
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type Button}">
                <Microsoft_Windows_Themes:ButtonChrome SnapsToDevicePixels="true" x:Name="Chrome" Background="{TemplateBinding Background}" BorderBrush="{TemplateBinding BorderBrush}" RenderDefaulted="{TemplateBinding IsDefaulted}" RenderMouseOver="{TemplateBinding IsMouseOver}" RenderPressed="{TemplateBinding IsPressed}">
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

    <Style x:Key="ButtonStyle1" TargetType="{x:Type Button}">

这一行在代码块中以粗体突出显示，表示这组资源定义了一个键为 ButtonStyle1 的样式。由于此样式是使用键定义的，因此它不是应用于目标类型所有控件的默认样式。样式总是定义目标类型，因为不同的控件类型期望在样式的所有详细元素中定义不同的特定值。

要让每个控件按钮都使用相同的样式，可以不提供 ButtonStyle1 样式的键，而只提供类型定义。如果在某个时候你希望不同类型的对象共享某些特征，可以通过定义资源并将其应用于每种类型的样式来实现。如果随后这些样式在没有键的情况下被指定，那么它们默认应用于该类型的每个对象。

接下来，如果你想找到一种方法来移除鼠标悬停在按钮上时出现的默认高亮效果，那么你需要确定样式是如何指定该效果的。好消息是导致该行为的钩子实际上包含在此文件中；坏消息是它引用了一个模板，然后该模板被分配给该行为。下面的 XAML 行显示了 RenderMouseOver 属性正在与模板的 IsMouseOver 关联：

```
RenderMouseOver="{TemplateBinding IsMouseOver}"
```

正是这个模板导致按钮改变其外观以反映此状态。因此，要获得没有此默认行为的按钮，你需要定义一个新模板，或者从自定义样式中删除此 XAML 元素。

当然，你可以获取前面的代码块，进行必要的更改，并将其粘贴到应用程序的 XAML 中。如果你还执行了其他需要执行的步骤，这当然会奏效。然而，从长远来看，前面的 XAML 块是特定于 Button 类型控件的。此外，前面所有代码实际上都是生成的。如果你需要自定义另一种控件类型的运行时行为，则需要为该控件生成默认样式。Expression Blend 虽然不再是必需的，但仍然是执行此操作的一个不错选择。

## 数据绑定到数据源

本章要讨论的最后一项是绑定到数据源。为简洁起见，此示例使用一个简单的 XML 文件 People.xml，它是 ProVB_WPF_Step3 项目的一部分。该文件的内容如下：

```
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
```

![](img/d99870e80390742f93963da7be0b2e61_669_0.png)

该文件的内容相当简单，代表了一个人力资源风格的应用程序。每个条目都有一个内部 ID 和一系列字段。working_folder 节点是特定于机器的，因此当你考虑运行此应用程序时，需要将其映射到本地机器上存在的文件夹。否则，你将看不到任何图像。

虽然此文件将在主窗口中进行数据绑定，但第一步是更新 ImageRotator 控件。其转换的第一部分涉及获取只读的 ImageURI 属性，并将其转换为可读写的依赖属性。如前所述，先前引用的只读属性在示例下载代码中已被注释掉并折叠在一个区域中。最终代码的开始方式与原始代码类似，它定义了一个标准类属性。然而，在这种情况下，该属性支持一个 Set 方法，该方法调用本地方法来更新 Image 控件中显示的图像。

