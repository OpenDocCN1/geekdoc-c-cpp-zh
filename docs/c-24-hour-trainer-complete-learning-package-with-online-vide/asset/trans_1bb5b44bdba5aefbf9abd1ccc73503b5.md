

- 使用两个 ScrollBar 控件，其中一个的 `Orientation = Horizontal`。

- 使用 Canvas 代替 Panel，并使用 Image 代替 PictureBox。

- 不要捕获窗体的 Load 和 Resize 事件，而是捕获 Canvas 控件的 SizeChanged 事件，并为其提供以下事件处理程序：

```csharp
// Set the scrollbar maximums to fit the Canvas.
private void fieldCanvas_SizeChanged(object sender, SizeChangedEventArgs e)
{
    mouseHScrollBar.Maximum = e.NewSize.Width;
    mouseVScrollBar.Maximum = e.NewSize.Height;
}
```

- 为 Canvas 的 MouseMove 事件处理程序使用以下代码：

```csharp
// Move the scrollbars to track the mouse.
private void Canvas_MouseMove(object sender, MouseEventArgs e)
{
    Point location = Mouse.GetPosition(fieldCanvas);
    mouseHScrollBar.Value = location.X;
    mouseVScrollBar.Value = location.Y;
}
```

- 最初将 Image 控件定位在 Canvas 控件的左上角。然后使用以下 MouseDown 事件处理程序：

```csharp
// Move the mouse Image to the point clicked.
private void fieldCanvas_MouseDown(object sender, MouseButtonEventArgs e)
{
    Point location = Mouse.GetPosition(fieldCanvas);
    mouseImage.Margin = new Thickness(location.X, location.Y, 0, 0);
}
```

3. 生成图 4-3 所示的 DynamicEvents 示例程序。如果单击 Attach 两次会发生什么？三次呢？如果随后单击 Detach 一次会发生什么？五次呢？

4. [WPF] 使用 WPF 应用程序重复练习 3。

5. 创建一个窗体，其中包含一个标有“Stop”的 Button 和两个名为 leftTimer 和 rightTimer 的 Timer。将 Timer 的 Interval 属性设置为 1000。在设计时，将 leftTimer 的 Enabled 属性设置为 True。

    - 在每个 Timer 的 Tick 事件处理程序中，禁用该 Timer 并启用另一个 Timer。
    - 让一个 Timer 的 Tick 事件处理程序还通过设置 Button 的 Left 和 Top 属性将其移动到 (10, 10)。
    - 让另一个 Timer 的 Tick 事件处理程序将 Button 移动到 (200, 200)。
    - 在 Button 的 Click 事件处理程序中，将两个 Timer 的 Enabled 都设置为 false。

    运行程序。尝试为 Timer 的 Interval 属性设置不同的值。如果 Interval = 10 会发生什么？

6. 复制你为练习 1 生成的 FollowMouse 程序。修改副本，使用户可以调整滚动条来移动 PictureBox。

7. [WPF] 复制你为练习 2 生成的程序。修改副本，使用户可以调整滚动条来移动图像。（提示：为节省代码，对两个滚动条使用同一事件处理程序。为防止鼠标图像出现在滚动条上方以及窗口右下角的小区域中，将 Canvas 控件的 ClipToBounds 属性设置为 True。）

8. 制作一个类似于图 4-5 所示的程序。当用户取消选中 Breakfast、Lunch 或 Dinner 复选框时，程序应禁用相应的 GroupBox。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_107_0.png)

**图 4-5**

**提示：**

- 使 OK 按钮成为窗体的接受按钮。使 Cancel 按钮成为窗体的取消按钮。
- 清空 GroupBox 的 Text 属性。然后将 CheckBox 放置在 GroupBox 上原来文本所在的位置。（确保不要将 CheckBox 放在 GroupBox 内部。试一下就会明白为什么不行。你可能需要先定位 CheckBox，然后再将 GroupBox 移到相应位置。）
- 要启用或禁用 GroupBox，请将其 Enabled 属性设置为相应 CheckBox 的 Checked 属性，如下代码所示：

```csharp
// Enable or disable the corresponding GroupBox.
private void breakfastCheckBox_CheckedChanged(object sender, EventArgs e)
{
    breakfastGroupBox.Enabled = breakfastCheckBox.Checked;
}
```

9. [WPF] 使用 WPF 应用程序重复练习 8。提示：

- WPF CheckBox 不显示背景，因此此程序中的复选框不会覆盖其下方 GroupBox 的边框。要解决该问题，请将每个 CheckBox 放在 Canvas 中，并让 Canvas 使用白色背景。
- GroupBox 只能有一个子元素。为每个 GroupBox 提供一个包含 RadioButton 的 StackPanel。使用 RadioButton 的 Margin 属性在选项之间添加一些间距。
- WPF `CheckBox` 控件没有 `CheckedChanged` 事件。请改用 `Click` 事件。
- 要启用或禁用 `GroupBox`，请将其 `IsEnabled` 属性设置为相应 `CheckBox` 的 `IsChecked.Value` 属性，如下代码所示：

```csharp
// Enable or disable the appropriate GroupBox.
private void breakfastCheckBox_Click(object sender, RoutedEventArgs e)
{
    breakfastGroupBox.IsEnabled = breakfastCheckBox.IsChecked.Value;
}
```

- 要设置 WPF 窗口的接受按钮，请将 Button 的 `IsDefault` 属性设置为 `True`。
- 要设置 WPF 窗口的取消按钮，请将 Button 的 `IsCancel` 属性设置为 `True`。

10. 制作一个类似于图 4-6 所示的程序。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_108_0.png)

**图 4-6**

- 创建一个 `PictureBox` 并向其中加载图像。将其大小设置为与图片大小匹配，并将其 `SizeMode` 属性设置为 `StretchImage`。（另请查看将其设置为 `Normal` 时会发生什么。）
- 将滚动条放在 `PictureBox` 旁边。设置它们的 `Maximum` 属性，使用户可以选择介于 0 与图片宽度/高度之间的值。
- 最初将滚动条的 `Value` 属性设置为等于图像的宽度/高度。
- 让滚动条的 `Scroll` 事件处理程序将 `PictureBox` 的宽度/高度设置为等于滚动条的值。

11. [WPF] 使用 WPF 应用程序重复练习 10。提示：

- 将 Image 控件的 Stretch 属性设置为 Fill。（另请查看将其设置为 None 时会发生什么。）
- 在 WPF 程序中，用户可以将 ScrollBar 设置为其 Maximum 值。

12. [WPF, Games, Hard] 在 Windows Forms 应用程序中很难做到、而在 WPF 应用程序中却很容易做到（至少如果设置得当）的一件事是变换对象。例如，缩放、旋转和倾斜控件相对容易。对于本练习，制作一个类似于图 4-7 所示的程序。当用户调整底部的滚动条时，程序应旋转图像，并在右下角的 Label 中显示旋转角度。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_109_0.png)

**图 4-7**

**提示：**

- 布局窗口及其控件。将图片放入 Image 控件中。将标签控件命名为 degreesLabel。

- 使用“属性”窗口的 Transform 部分将 Image 旋转 360 度。

- 编辑 XAML 代码，为 rotateTransform 提供一个名为 x:Name 的属性，其值为 rotateTransform。Image 控件的代码应类似如下：

```xml
<Image x:Name="image" HorizontalAlignment="Left"
VerticalAlignment="Top" Source="ScienceGirl.png"
Stretch="None" Grid.ColumnSpan="2"
Margin="10,10,0,0" RenderTransformOrigin="0.5,0.5">
<Image.RenderTransform>
<TransformGroup>
<ScaleTransform/>
<SkewTransform/>
<RotateTransform x:Name="rotateTransform" Angle="360"/>
<TranslateTransform/>
</TransformGroup>
</Image.RenderTransform>
</Image>
```

- 使 ScrollBar 的 ValueChanged 事件处理程序如下所示：

```csharp
// Rotate the Image.
private void degreesScrollBar_ValueChanged(object sender,
    RoutedPropertyChangedEventArgs<double> e)
{
    rotateTransform.Angle = degreesScrollBar.Value;
    degreesLabel.Content = degreesScrollBar.Value.ToString("0");
}
```

13. [WPF] 生成一个 WPF 应用程序，其中的 Grid 包含一个 Image。为 Grid 提供一个 MouseMove 事件处理程序，将 Image 移动到鼠标位置。（提示：默认情况下，窗口的主 Grid 具有透明背景，因此无法正确接收鼠标事件。要解决此问题，请设置其 Background 画笔。只要不是透明，可以使用任何画笔。）

14. 生成一个显示 TrackBar 和 HScrollBar 的 Windows Forms 程序。将它们的 Maximum 属性设置为 10，并将滚动条的 LargeChange 属性设置为 1。当控件的值在运行时更改时，在 Label 中显示新值。

15. [WPF] 制作一个 WPF 应用程序，显示两个 Slider 和一个 ScrollBar，它们的 Maximum 都设置为 10。将其中一个 Slider 的 IsSnapToTickEnabled 设置为 True。当控件的值在运行时更改时，在 Label 中显示新值。

16. 制作一个类似于图 4-8 所示的条形图。单击按钮时，应为条形分配随机值。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_110_0.png)

**图 4-8**

**提示：**

- 对于条形，使用多列 TableLayoutPanel 中的 Label。

- 要使 Label 显示在 TableLayoutPanel 的底部，请将其 Anchor 属性设置为 Bottom、Left、Right。

- 要使 Label 彼此接触，请将其 Margin 属性设置为 0, 0, 0, 0。

- 使用类似以下的代码为 Label 指定随机高度。请注意，**加粗的语句**位于事件处理程序之外。

```csharp
// Make a random number generator.
private Random Rand = new Random();

// Pick random values for the Labels.
private void pickValuesButton_Click(object sender, EventArgs e)
```

