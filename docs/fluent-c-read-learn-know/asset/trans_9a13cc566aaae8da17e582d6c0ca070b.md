
## 应用变换

UIElement 定义了两个属性，LayoutTransform 和 RenderTransform，你可以使用它们来转换元素。你可以将这些属性设置为 TransformGroup，以便应用多个变换。

### 布局变换

布局变换在面板排列其子元素之前应用，因此其他元素会移开。

```xml
<Button>
    Third Button
    <Button.LayoutTransform>
        <RotateTransform ... />
    </Button.LayoutTransform>
</Button>
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_762_0.png)

### 变换组

变换组允许你向对象应用多个变换。

```xml
<Button Width="200" Height="50">
    Third Button
    <Button.LayoutTransform>
        <TransformGroup>
            <RotateTransform CenterX="1" CenterY="1"
                Angle="15" />
            <ScaleTransform CenterX="1" CenterY="1"
                ScaleX="0.75" ScaleY="0.75" />
        </TransformGroup>
    </Button.LayoutTransform>
</Button>
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_762_1.png)

### 呈现变换

呈现变换在面板排列其子元素之后应用，因此转换后的元素可能会与其他元素重叠或被其他元素遮挡。

```xml
<Button>
Third Button
<Button.RenderTransform>
<RotateTransform ... />
</Button.RenderTransform>
</Button>
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_763_0.png)

## 动动脑筋

按照示例在窗体中添加第二个按钮，并使其在鼠标悬停时晃动。以下是一些入门提示：

- 还记得 NaN 问题吗？为了在为变换制作动画时避免该问题，在声明按钮时给它一个空变换：
  `<RotateTransform />`
  你还可以设置动画中所有变换共享的属性：
  `<RotateTransform CenterX="100" CenterY="25"/>`
- 你不希望所有按钮都晃动，因此创建一个带有键的新按钮样式，并将该样式作为 StaticResource 分配给按钮。
- 你可以在 Storyboard 本身中设置 TargetProperty。你将要为 Angle 属性制作动画，它实际上是 UIElement 中声明的附加属性：
  `TargetProperty="(UIElement.RenderTransform).(RotateTransform.Angle)"`
- 你实际上需要四个 DoubleAnimation 实例来使按钮晃动。向一个方向旋转（我将角度更改为 15 度，但你可以自行决定），返回到原始（未转换）值，然后向另一个方向旋转并返回。
- 你需要调整 BeginTime 和 Duration 属性，以便动画按顺序运行：
  `<DoubleAnimation Duration="0:0:0.25" ... />`
  `<DoubleAnimation BeginTime="0:0:0.25" Duration="0:0:0.25" />`

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_763_1.png)

此动画在上一个动画结束后开始。

## 做得怎么样？

如果你没有偷看就让这个功能正常工作，你应该为自己感到骄傲。你几乎准备好开始发送简历了。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_764_0.png)

## 这是我编写的 Button 元素版本。

```xml
<Button Grid.Column="1" Width="200" Height="50" Style="{StaticResource Wiggle}">
Transformed Button
<Button.RenderTransform >
<RotateTransform CenterX="100" CenterY="25" />
</Button.RenderTransform>
</Button>
```

这是按钮内容。你认为如果我明确指定 `<Button.Content> Transformed Button </Button.Content>` 会更清晰吗？

设置变换的默认属性可以节省事件触发器中的一些代码，并确保 WPF 创建 RenderTransform 属性。

## 休息一下

这是一个困难的练习，你可能花了一些时间才完成。那么，在完成复习并进入下一章（我们将使用模板完全重新定义控件的外观）之前，为什么不先休息一下呢？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_764_1.png)

## 动画样式如下：

我们知道 RotateTransform 属性存在，因为它已在 XAML 中声明。

```xml
<Style TargetType="Button" x:Key="Wiggle">
<Style.Triggers>
<EventTrigger RoutedEvent="Button.MouseEnter">
<BeginStoryboard>
<Storyboard>
Storyboard.TargetProperty="(UIElement.RenderTransform).(RotateTransform.Angle)">
<DoubleAnimation Duration="0:0:0.25" To="15" />
<DoubleAnimation BeginTime="0:0:0.25" Duration="0:0:0.25" />
<DoubleAnimation BeginTime="0:0:0.5" Duration="0:0:0.25" To="-15" />
<DoubleAnimation BeginTime="0:0:0.75" Duration="0:0:0.25" />
</Storyboard>
</BeginStoryboard>
</EventTrigger>
</Style.Triggers>
</Style>
```

BeginTime 属性是错开的，因此它们按顺序发生。

你可能将持续时间设置得更长或更短。这无关紧要，只要你的 BeginTime 属性反映你选择的实际持续时间即可。

## 复习

通常有三个地方可以定义资源。它们是什么？

引用资源有两种方式？你会在什么情况下使用每种方式？

以下两个声明有什么区别：

```xml
<Style x:Key="MyStyle" TargetType="Button" >
<Style TargetType="Button" >
```

哪两个集合允许你在属性触发器中放置 EventAction？

什么逻辑运算符组合 MultiTrigger 中的 Condition 元素？

为什么 System.Windows.Media.Animation 命名空间中有这么多类？

如果在动画时间轴中不指定 By、To 或 From，会发生什么？

## 恭喜！你已完成本章。在进入下一章之前，花一分钟思考一下你取得了哪些成就...

列出你在本章中学到的三件事：

- 1
- 2
- 3

你认为为什么需要知道这些才能成为一名 C# 程序员？

本章中有什么你觉得需要更详细理解的内容吗？如果有，你打算怎么做？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_768_0.png)

## 模板

在上一章中，我们了解了如何使用资源、样式和触发器来简化定义 WPF 控件的外观和视觉行为，但元素的基本结构保持不变——我们更改了按钮的大小和颜色，并使其移动，但它看起来仍然像一个按钮。在本章中，我们还将使用 WPF 模板来控制该结构，以重新定义任何 FrameworkElement 或 FrameworkContentElement 的可视化树。

希望你的按钮是三角形的？没问题。你的应用程序真的需要椭圆窗口吗？你可以使用模板实现这一点。

我们将先检查一些可用于构建控件新版本的基本元素，然后探讨重新定义控件外观的非常简单的过程。我们还将探讨使新模板反映你在设计时和运行时设置的控件属性的技术。最后，我们将探讨一种新的指定视觉行为的方法，类似于触发器，但仅在控件模板中可用。

## 如何融入

在整本书中，你一直通过为应用程序的主窗口定义逻辑树来构建应用程序。

```xml
<Window ... />
<Grid>
    <StackPanel>
        <Label>This is a label</Label>
        <TextBox Margin="10">Textbox</TextBox>
        <Button Margin="10">Button</Button>
    </StackPanel>
</Grid>
</Window>
```

此 XAML 创建了此窗口...

...来自此逻辑树。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_770_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_770_1.png)

但每个元素也有一个可视化树，它定义了元素本身的组成方式。可视化树位于 XAML 控件模板中，该模板定义为资源或作为控件样式的一部分。

Border 是装饰器之一：它有点像面板，因为它显示一段内容。

VisualStateManager 执行与事件触发器相同的功能。

VisualStates 类似于事件触发器，而 VisualTransitions 包含在状态之间移动时激活的事件操作。

内容呈现器（PRESENTERS）显示控件的内容。它们有自己的模板（称为 ContentTemplate）。WPF 中处处都有模板。

```xml
<Style TargetType="Button"
    ...
    <Setter Property="Template">
    <ControlTemplate TargetType="Button">
    <Border ...>
    <VisualStateManager>
    <VisualStateGroup x:Name="CommonStates">
    <VisualState ...>
    <VisualTransition ...>
    </VisualStateGroup>
    </VisualStateManager>
    <ContentPresenter ...>
    </Border>
    </ControlTemplate>
    </Setter>
    ...
    </Style>
```
