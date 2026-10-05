
将两个控件的 `VerticalAlignment` 属性都设置为 `Center`（居中），并移除 `Margin` 属性。

以下 XAML 代码显示了控件的完整定义：

点击此处查看代码图像

```
<Grid Grid.Row="2">
  <Grid.RowDefinitions>
    ...
  </Grid.RowDefinitions>
  <Grid.ColumnDefinitions>
    ...
  </Grid.ColumnDefinitions>
  <TextBox ... x:Name="email" />
  <TextBox Grid.Row="5" Grid.Column="1"
    HorizontalWrapping="Wrap" Text="Phone" VerticalAlignment="Center"
    FontSize="20"/>
  <TextBox Grid.Row="5" Grid.Column="3" Grid.ColumnSpan="3"
    x:Name="phone"
    HorizontalAlignments="Left" TextWrapping="Wrap" Text=""
    VerticalAlignments="Center"
    Width="200" FontSize="20"/>
</Grid>
```

在下一个练习中，你将运行应用程序以查看布局如何适应不同的分辨率和表单因子。

# 测试应用程序

- 1. 在“调试”（Debug）菜单上，选择“开始调试”（Start Debugging）。应用程序看起来应该与下面的图片相似：

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_989_0.png)

- 2. 调整窗口大小使其变窄。控件应该调整它们位置和大小。然而，在某个时刻，窗口将变得太窄，无法正确显示文本和固定宽的控件（email 和 phone），导致文本换行和截断。这就是应用程序在小型平板电脑或手机上可能的外：

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_990_0.png)

- 3. 返回 Visual Studio 并停止调试。

- 4. 在设计视图（Design View）窗口顶部的下拉列表中，选择 **Phone**（手机）布局。

设计视图窗口会调整显示，并确认应用程序在手机设备上的可能外观。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_991_0.png)

- 5. 尝试其他设备尺寸和方向。注意网格如何导致控件调整它们的位置。

- 6. 在继续之前，切换回 **13.3” Desktop**（桌面）布局。

# 使用视觉状态管理器（Visual State Manager）调整布局

Customers 应用程序的用户界面针对不同的分辨率和因子进行缩放，但如果你缩小视图宽度，它仍然运行得不好，而且在手机或其他窄设备上看起来可能不太好。如果你仔细考虑，这些情况下问题的解决方案与其说是缩放控件，不如说是实际上以不同的方式布局它们。例如，如果 Customers 表单在窄视图下看起来像下面的图片，将更有意义。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_992_0.png)

你可以通过几种方式实现这种效果：

- **通过为 MainPage.xaml 文件创建多个版本，每个设备族一个**：这些 XAML 文件中的每一个都可以链接到相同的底层代码（MainPage.xaml.cs），以便它们都运行相同的代码。例如，要为智能手机创建一个 XAML 文件，请向项目添加一个名为 `DeviceFamily-Mobile`（此名称很重要）的文件夹，然后使用“添加新项”菜单向该文件夹添加名为 `MainPage.xaml` 的新 XAML 视图。在此页面上按照它们在智能手机上显示的方式布局控件。XAML 视图将自动链接到现有 MainPage.xaml.cs 文件。在运行时，UWP 将根据运行应用程序的设备类型选择合适的视图。

- **通过视觉状态管理器在运行时修改页面布局**：所有 UWP 应用程序都实现了一个视觉状态管理器，用于跟踪应用程序的视觉状态。它可以检测窗口高度和宽度的变化，你可以添加 XAML 代码，根据窗口的大小对控件进行定位。这些代码可以移动控件，或显示和隐藏控件。

- **通过视觉状态管理器根据窗口的高度和宽度在视图之间切换**：这种方法是这里描述的前两种方案的混合，但它是最不混乱的（你不需要编写许多复杂的代码来计算每个控件的最佳位置），而且是最灵活的（如果在同一设备上收窄窗口，它仍然有效）。

你将在下一个练习中使用第三种方法。第一步是为应该在窄视图中显示的客户数据定义布局。

# 为窄视图定义布局

- 1. 在 Customers 应用程序的 XAML 格中，为第一个嵌套 Grid 控件添加此处所示 `x:Name` 和 `Visibility` 属性：

点击此处查看代码图像

```
<Grid>
  <Grid x:Name="customersTabularView" Margin="10,20,10,20" Visibility="Collapsed">
    ..
  </Grid>
</Grid>
```

此 Grid 将包含表单的默认视图。你将在其他练习中引用此 Grid。`Visibility` 属性指定控件是显示还是隐藏。

- 2. 在 `customersTabularView` 的 `</Grid>` 标签之后，添加另一个 Grid。将 `x:Name` 属性设置为 `customersView`，`Margin` 属性设置为 `10,20,10,20`，并将 `Visibility` 属性设置为 `Visible`。此 Grid 将包含表单的“窄”视图。

点击此处查看代码图像

```
<Grid>
  <Grid x:Name="customersTabularView" Margin="10,20,10,20" Visibility="Collapsed">
    ..
  </Grid>
  <Grid x:Name="customersView" Margin="10,20,10,20" Visibility="Visible">
  </Grid>
</Grid>
```

- 3. 在 `customersColumnView` Grid 中，添加以下行定义：

点击此处查看代码图像

```
<Grid x:Name="customersColumnView" Margin="10,20,10,20" Visibility="Visible">
  <Grid.RowDefinitions>
    <RowDefinition Height="*"/>
    <RowDefinition Height="10"/>
  </Grid.RowDefinitions>
</Grid>
```

你将使用第一行显示第一项，并使用较大的第二行显示用户输入数据的控件。

- 4. 紧接行定义之后，添加此处**加粗**所示的 TextBlock 控件。该控件在 Grid 的第一行显示截断的标题 "Customers"。将 `FontSize` 设置为 30。

点击此处查看代码图像

```
<Grid x:Name="customersColumnView" Margin="10,20,10,20" Visibility="Visible">
  <Grid.RowDefinitions>
    <RowDefinition Height="*"/>
    <RowDefinition Height="10"/>
  </Grid.RowDefinitions>
  <TextBlock Grid.Row="0" HorizontalAlignment="Center"
    TextWrapping="Wrap" Text="Customers" VerticalAlignment="Center" FontSize="30"/>
</Grid>
```

- 5. 在 `customersColumnView` Grid 的第 1 行添加另一个 Grid，直接跟在包含 Customers 标题的 TextBlock 控件之后。此 Grid 将以两列显示标签和数据输入控件，将后续代码示例中**加粗**所示的行和列定义添加到此 Grid 中：

点击此处查看代码图像

```
<TextBlock Grid.Row="0" ... />
<Grid Grid.Row="1">
  <Grid.ColumnDefinitions>
    <ColumnDefinition/>
    <ColumnDefinition/>
  </Grid.ColumnDefinitions>
  <Grid.RowDefinitions>
    <RowDefinition/>
    <RowDefinition/>
    <RowDefinition/>
    <RowDefinition/>
    <RowDefinition/>
    <RowDefinition/>
  </Grid.RowDefinitions>
</Grid>
```

> **注意**
> 如果一组行或列具有相同的高度或宽度，则不需要指定它们的大小。

- 6. 从 `customersTabularView` Grid 复制 ID、Title、First Name 和 Last Name TextBlock 控件的 XAML 代码到新的 Grid 控件中，紧接在你刚刚添加的行定义之后。将 ID 控件放在第 0 行，Title 控件放在第 1 行，First Name 控件放在第 2 行，Last Name 控件放在第 3 行。将所有控件放在第 0 列。

