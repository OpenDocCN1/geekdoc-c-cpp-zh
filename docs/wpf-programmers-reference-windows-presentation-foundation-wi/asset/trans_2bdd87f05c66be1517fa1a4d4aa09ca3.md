

# 变换技巧

Storyboard 可以更改变换的属性，但它不能从零开始创建一个新的变换。在旋转按钮的示例中，Storyboard 可以更改 `RenderTransform` 的旋转角度，但它不能凭空产生 `RenderTransform`，因此 Button Style 创建了一个初始的 `RenderTransform`，将按钮旋转 0 度。

在通常情况下，如果你想旋转、拉伸或其他更改控件的变换，你必须为它提供一个初始变换，以便 Storyboard 进行修改。

`sbSpin` Storyboard 也被定义为资源以进一步简化 Button 的代码。你甚至可以在 Button Style 中定义 `EventTrigger`，使 Button 的代码变得非常简单。在某些情况下，定义相同或相似的触发器是有意义的：例如，考虑图 14-2 所示的 `CentralizedTriggers` 示例程序。该程序在左侧显示了一系列缩略图。当你点击其中一张时，图像会展开并移动以填充右侧区域。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_275_0.png)

图 14-2

在这个示例中，所有缩略图的操作都大同相同：它们都会展开自己的图像。在像显示一系列具有相似用途控件的程序中，如果它们的触发器都放在一起，可能会让程序的逻辑更容易理解。这对于一系列缩略图、按钮、菜单项、单选按钮或任何执行大致相同操作的控件组都是意义意义。

当路由事件（routed event）被触发时，它会在包含启动它的控件层次结构中移动。`CentralizedTriggers` 示例控件显示在 `Canvas` 上，当用户点击其中一个缩略图（一个 `Image` 控件）时，`MouseLeftDown` 事件从缩略图开始，移动到 `Canvas`，然后再次移动到 `Window`。程序代码可以在任何级别捕捉事件。

以下代码片段显示了 `CentralizedTriggers` 程序 `Canvas` 控件的结构：

```
<Canvas Margin="5">
  <Canvas.Resources>
    <!-- 定义一个未命名的 Image Style。 -->
    <Style TargetType="Image">
      <Setter Property="Opacity" Value="0.5"/>
      <Setter Property="Width" Value="100"/>
      <Setter Property="Height" Value="100"/>
      <Setter Property="Stretch" Value="Uniform"/>
      <Setter Property="BitmapEffect">
        <DropShadowBitmapEffect/>
      </Setter>
    </Style>
  </Canvas.Resources>
```

```
<!-- 为每个 Image 定义一个 Storyboard. -->
<Storyboard x:Key="sbImg1">
  Code omitted ...
</Storyboard>
定义其他 Storyboards
</Canvas.Resources>
```

```
<!-- 处理 MouseLeftDown 事件。 -->
<Canvas.Triggers>
  <EventTrigger SourceName="RoutedEvent" Tag="Image.MouseLeftDown">
    <EventTrigger.Actions>
      <RemoveStoryboard StoryName="sbImg1"/>
      <RemoveStoryboard StoryName="sbImg2"/>
      <RemoveStoryboard StoryName="sbImg3"/>
      <RemoveStoryboard StoryName="sbImg4"/>
    </EventTrigger.Actions>
  </EventTrigger>
```

```
<BeginStoryboard Name="sbImg1">
  <StaticResource sbImg1/>
</BeginStoryboard>
</EventTrigger.Actions>
</EventTrigger>
为其他 Images 定义 EventTriggers
</Canvas.Triggers>
```

```
<!-- 构建控件。 -->
```

```
<Image Canvas.Left="0" Canvas.Top="0" Name="img1" Source="Canon01.jpg"/>
<Image Canvas.Left="0" Canvas.Top="100" Name="img2" Source="Canon02.jpg"/>
<Image Canvas.Left="0" Canvas.Top="200" Name="img3" Source="Canon03.jpg"/>
<Image Canvas.Left="0" Canvas.Top="300" Name="img4" Source="Canon04.jpg"/>
</Canvas>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_276_0.png)

`Canvas.Resources` 部分定义了一个未命名的 Style（Width, Height, Stretch 等）以及链接并移动缩略图以填充视图区域的 storyboards。

`Canvas.Triggers` 部分定义了 Images 的 EventTriggers。之前的代码只详细显示了第一个触发器。它的 `SourceName` 和 `RoutedEvent` 属性指示该触发器捕获由名为 img1 的 Image 控件引发的 `MouseLeftDown` 事件。

`Trigger.Actions` 部分使用 `Remove` 对象来取消任何之前正在运行的 Storyboards，将缩略图恢复到原始位置。（本章稍后的“控制 Storyboards”部分将介绍更多关于 `RemoveStoryboard` 等对象的内容。）它随后使用 `BeginStoryboard` 运行 `sbImg` Storyboard，将 Image 控件 img1 移动到视图区域。

定义了资源和触发器后，定义 Image 控件的程序代码非常简单且于理解。

将触发器与引发事件的控件放在一起通常是有意义的，但有时将代码段组合在一起会使代码更易读。这使得各个代码部分（样式、storyboard、触发器、控件）更容易理解。

# 属性元素中的 Storyboards

代码不需要引用资源中定义的 storyboard，可以直接在 `BeginStoryboard` 元素内部包含一个 storyboard。以下代码显示了一个包含 storyboard 的 Button：

```
<Button Width="100" Height="50" Content="Click Me">
  <Button.Triggers>
    <EventTrigger RoutedEvent="Button.MouseEnter">
      <EventTrigger.Actions>
        <BeginStoryboard>
          <Storyboard>
            Place animations here
          </Storyboard>
        </BeginStoryboard>
      </EventTrigger.Actions>
    </EventTrigger>
  </Button.Triggers>
</Button>
```

#  中的 Storyboards

在控件中构建 storyboard 会导致定义非常长且需要一些嵌套元素，因此你可能希望在资源中定义它们。例如，以下代码定义了一个包含事件触发器的 Button Style：

```
<Style x:Key="btnEventSize" TargetType="Button">
  <Setter Property="Width" Value="100"/>
  <Setter Property="Height" Value="50"/>
  <Triggers>
    <EventTrigger RoutedEvent="Button.MouseEnter">
      <EventTrigger.Actions>
        <Storyboard Storyboard="StaticResource BigSize"/>
      </EventTrigger.Actions>
    </EventTrigger>
    <EventTrigger RoutedEvent="Button.MouseLeave">
      <EventTrigger.Actions>
        <Storyboard Storyboard="StaticResource SmallSize"/>
      </EventTrigger.Actions>
    </EventTrigger>
  </Triggers>
</Style>
```

程序可以使用以下代码定义使用该样式的按钮：

<Button Style="StaticResource btnEventSize" Content="New Size"/>

# 属性触发器动画

通常，属性触发器使用 setter 来立即更改属性值，但你可以使用属性触发器来运行 storyboard。属性触发器应用 storyboard 的方式与其应用 setter 的方式不同，因为它们的目的不同。

setter 在另一个属性具有特定值时更改属性。例如，只要该属性为 True，Setter 会将 Width 更改为 150。如果 MouseOver 不再为 True，Setter 返回到正常尺寸，例如 100。在这里，Setter 在 IsMouseOver 为 True 时将 Width 属性设置为 150。

相比之下，动画随时间平滑地从一个值变为另一个值。例如，动画可能会让 Button 的 Width 在 1 秒内从原始值 100 变化到 150。在这种情况下，只要 IsMouseOver 属性为 True 就运行动画是没有意义的。即使 IsMouseOver 持续了 10 分钟，动画也会在 1 秒内完成。现在动画会反复播放，但在本示例中这可能有点奇怪。

为了合理地应用动画，属性触发器除了普通的 setter 之外还提供了两个可以执行动画的额外部分：EnterActions 和 ExitActions。

