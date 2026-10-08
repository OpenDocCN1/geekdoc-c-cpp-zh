

当运行此应用程序时，任务栏外观如图 8-45 所示。矩形是图标覆盖层（icon overlay），缩略图上的黑白小脸是预览按钮（ThumbButton）。可以有多个缩略按钮。例如，Windows Media Player 使用缩略按钮来快速访问上一个、下一个和暂停功能。

![](img/b5597c749e848b27b0d305153ae16106_406_0.png)

在 Windows 7 上执行耗时操作并运行任务栏的程序，可以在任务栏上显示其进度状态。这允许用户通过查看任务栏而无需将应用程序置于前台，即可确定操作状态。

要在你的应用程序中使用此功能，请将 `TaskItemInfo.ProgressValue` 设置为 0 到 1 之间的值，并将 `TaskItemInfo.ProgressState` 设置为 `Normal`。`ProgressState` 还可以设置为 `Indeterminate`（显示不确定动画）、`Error`（使进度条变为红色，表示进度出现错误）、`None`（清除任何进度条）以及 `Paused`（使进度条变为黄色）。

## 不同的控制模板模型

WPF 直到在 WPF 4 中才引入了 Silverlight 的视觉状态管理器（VSM）。正因如此，控件使用的模板模型与 Silverlight 不同。以下是 WPF TextBox 模板的一段代码：

```xml
<Setter Property="Template">
<Setter>
  <ControlTemplate TargetType={x:Type TextBox} Name="Bd">
  <Microsoft_Windows_Themes:ListBoxChrome x:Name="
    SnapsToDevicePixels="true" Background={TemplateBinding Background}
    BorderBrush={TemplateBinding BorderBrush}
    BorderThickness={TemplateBinding BorderThickness}
    Focused={TemplateBinding IsKeyboardFocusWithin}
    MouseOver={TemplateBinding IsMouseOver}>
  <ScrollView x:Name="PART_ContentHost">
    SnapsToDevicePixels={TemplateBinding SnapsToDevicePixels}/>
  </ScrollView>
  <Microsoft_Windows_Themes:ListBoxChrome>
  <Triggers>
    <Trigger Property="IsEnabled" Value="false">
      <Setter Property="Background" TargetName="Bd"
      Value="DynamicResource (x:Static SystemColors.ControlBrushKey)"/>
      <Setter Property="Foreground"
      Value="DynamicResource (x:Static SystemColors.GrayTextBrushKey)"/>
    </Trigger>
  </Triggers>
  </ControlTemplate>
</Setter>
</Setter>
```

图 45：图标覆盖层和预览按钮

此模板中有几个有趣的地方。其是 WPF 控件的外观和感受与当前的 Windows 窗口保持一致。另一个是基于触发器（triggers）运行。例如，`IsEnabled` 属性会自动触发两个设置器以相应地更改颜色——在 VSM 模型中，你通过逻辑来定义一组控件。

同样，鼠标悬停状态可以表示为基于 `MouseOver` 属性的属性触发器。WPF 4 控件也为了兼容 Silverlight 实现了 VSM 状态，但默认控件是基于触发器模型的。

## 视觉画刷 (VisualBrush)

VisualBrush 与早期引入的 Silverlight VideoBrush 非常相似，但它的源不是视频，可以是任何 WPF 控件。这允许实现酷炫的效果，例如非常流行的反射效果，且性能开销极小。

## WPF 3D

WPF 拥有一个相当复杂的三维引擎，该引擎与视觉树的其他部分集成，对于一个 UI 框架来说已经非常先进——不要尝试使用 WPF 3D 编写你的下一个 CAD 或游戏。WPF 3D 支持模型、光照、材质和颜色。二维元素也可以映射到三维模型。

例如，可以在球体上放置一个 DataGrid，它将是交互式的。然而，WPF 中的维度（dimension）不支持球体、立方体或茶壶等三维原始几何体——仅支持最基础的形状。

