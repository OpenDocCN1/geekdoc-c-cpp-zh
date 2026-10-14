

window，展开 Common 属性类别（如果尚未展开）。然后，单击 Items 属性旁边的省略号按钮。
对象集合编辑器窗口打开。
9. 在窗口左下方的列表中，选择 ComboBoxItem，然后单击 Add。在显示该项属性的右窗格中，如果尚未展开，请展开 Common 部分，然后在 Content 属性中输入 Mr。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_718_0.png)

10. 单击 OK。

对象集合编辑器关闭。如果检查 title ComboBox 的 XAML 标记，它现在应该如下所示：

Click here to view code image

```
<ComboBox x:Name="title" HorizontalAlignment="Left"
Margin="420,240,0,0"
    VerticalAlignment="Top" Width="100" FontSize="20"/>
    <ComboBoxItem Content="Mr"/>
</ComboBox>
```

这里有两个需要注意的地方。第一个是 ComboBox 标记已被拆分为一个开始的 <ComboBox> 标签和一个结束的 </ComboBox> 标签。第二个是，在这些标签之间，Visual Studio 添加了一个 ComboBoxItem 元素，其 Content 属性设置为 Mr。当应用程序运行时，
该项将在下拉列表中显示。

11. 向 *title* ComboBox 添加值 *Mrs*、*Ms* 和 *Miss*。你可以使用对象集合编辑器或手动输入 XAML 标记。 resulting 标记应如下所示：

Click here to view code image

```
<ComboBox x:Name="title" HorizontalAlignment="Left"
    Margin="420,240,0,0"
    VerticalAlignment="Top" Width="75" FontSize="20">
    <ComboBoxItem Content="Mr"/>
    <ComboBoxItem Content="Mrs"/>
    <ComboBoxItem Content="Ms"/>
    <ComboBoxItem Content="Miss"/>
</ComboBox>
```

## Note

*ComboBox* 控件可以显示简单的元素，例如显示文本的一组 *ComboBoxItem* 控件，但它也可以包含更复杂的元素，例如按钮、复选框和单选按钮。如果要添加简单的 *ComboBoxItem* 控件，手动输入 XAML 标记可能更容易，但如果要添加更复杂的控件，对象集合编辑器会非常有用。然而，你应避免在组合框中过于聪明；最好的应用程序是提供最直观的 UI 的应用程序，而在组合框中嵌入复杂控件可能会让用户感到困惑。

12. 在表单中添加另外两个 *TextBox* 控件和两个 *TextBlock* 控件。使用 *TextBox* 控件，用户将能够为客户输入电子邮件地址和电话号码，而 *TextBlock* 控件为文本框提供标签。使用下表中给出的值设置控件的属性。

| Control | Property | Value |
|---|---|---|
| First TextBlock | HorizontalAlignment | Left |
|  | Margin | 300,390,0,0 |
|  | TextWrapping | Wrap |
|  | Text | Email |
|  | VerticalAlignment | Top |
|  | FontSize | 20 |
| First TextBox | x:Name | email |
|  | HorizontalAlignment | Left |
|  | Margin | 450,390,0,0 |
|  | TextWrapping | Wrap |
|  | Text | Leave Empty |
|  | VerticalAlignment | Top |
|  | Width | 400 |
|  | FontSize | 20 |
| Second TextBlock | HorizontalAlignment | Left |
|  | Margin | 300,540,0,0 |
|  | TextWrapping | Wrap |
|  | Text | Phone |
|  | VerticalAlignment | Top |
|  | FontSize | 20 |
| Second TextBox | x:Name | phone |
|  | HorizontalAlignment | Left |
|  | Margin | 450,540,0,0 |
|  | TextWrapping | Wrap |
|  | Text | Leave Empty |
|  | VerticalAlignment | Top |
|  | Width | 200 |
|  | FontSize | 20 |

这些控件的 XAML 标记应如下所示：

Click here to view code image

```
<TextBlock HorizontalAlignment="Left" Margin="300,390,0,0"
TextWrapping="Wrap"
Text="Email" VerticalAlignment="Top" FontSize="20"/>
<TextBox x:Name="email" HorizontalAlignment="Left"
Margin="450,390,0,0"
TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="400"
FontSize="20"/>
<TextBlock HorizontalAlignment="Left" Margin="300,540,0,0"
TextWrapping="Wrap"
Text="Phone" VerticalAlignment="Top" FontSize="20"/>
<TextBox x:Name="phone" HorizontalAlignment="Left"
Margin="450,540,0,0"
TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="200"
FontSize="20"/>
```

设计视图窗口中完成的表单应如下所示：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_721_0.png)

13. 在 Debug 菜单上，单击 Start Debugging 以构建并运行应用程序。
应用程序启动并显示表单。你可以向表单中输入数据并从组合框中选择一个标题，但目前还不能做太多其他事情。
然而，更大的问题是表单看起来很糟糕。显示的右侧已被截断，大量的文本已换行，并且 Last Name 文本框已被截断：

## Adventure Works Customers

ID

First Name

Last Nam

Email

Phone

14. 点击并拖动窗口的右侧以扩展显示，使文本和控件显示为在 Visual Studio 中的设计视图窗口中出现的那样。这是表单作为设计时的最佳大小。

15. 将显示 Customer 应用程序的窗口调整为其最小宽度。这次，大部分表单消失了。一些 TextBlock 内容换行，但表单在这种视图下显然不可用。

16. 返回 Visual Studio，并在 Debug 菜单上单击 Stop Debugging。

这是一个关于在布局应用程序时要小心的好教训。虽然应用程序在运行窗口大小与设计视图相同的情况下看起来不错，但一旦将窗口调整为更窄的视图，它就变得不那么有用（甚至完全无用）。此外，应用程序假定用户将在横向方向上查看屏幕上的设备。如果你暂时将设计视图窗口切换到 12” Tablet 表单因子并单击纵向方向按钮，你可以看到如果用户在支持不同方向的平板电脑上运行应用程序并旋转设备以切换到纵向模式，表单会是什么样子。（之后不要忘记切换回 13.3” Desktop 表单因子。）

问题在于，到目前为止所示的布局技术无法缩放并适应不同的表单因子和方向。幸运的是，你可以使用 Grid 控件的属性和另一个称为 Visual State Manager 的功能来解决这些问题。

## Using the Simulator to test a Universal Windows Platform app

即使你没有平板电脑，你仍然可以使用 Visual Studio 2015 提供的 Simulator 测试你的 UWP 应用程序并查看它们在移动设备上的行为。Simulator 模拟平板设备，提供模拟用户手势（如捏合和滑动对象）以及旋转和更改设备分辨率的能力。

要运行 Simulator 中的应用程序，请打开 Visual Studio 工具栏上的 Debug Target 下拉列表框。默认情况下，调试目标设置为 Local Machine，这会导致应用程序全屏在你的计算机上运行，但你也可以从此列表中选择 Simulator，这将在调试应用程序时启动 Simulator。请注意，你也可以将调试目标设置为不同的计算机，如果需要进行远程调试（选择此选项时将提示你输入远程计算机的网络地址）。以下图像显示了 Debug Target 列表：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_724_0.png)

在选择 Simulator 后，当你从 Visual Studio 中的 Debug 菜单运行应用程序时，Simulator 将启动并显示你的应用程序。Simulator 窗口右侧的工具栏包含一组工具，你可以使用鼠标模拟用户手势。你甚至可以模拟用户的位置，如果应用程序需要有关设备地理位置的信息。然而，对于测试应用程序的布局，最重要的工具是 Rotate Clockwise、Rotate Counterclockwise 和 Change Resolution。以下图像显示了 Customers 应用程序在 Simulator 中运行。应用程序已最大化以占据全屏。标签描述了 Simulator 每个按钮的功能。

