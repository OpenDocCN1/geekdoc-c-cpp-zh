

![](img/16f6e3fe08f01ddadb2741a92c392b0e_738_0.png)

+   21. 在模拟器中，单击“开始”按钮，单击“设置”，单击“电源”，然后单击“断开连接”。
+   模拟器关闭，你返回到 Visual Studio。

+   22. 在 Visual Studio 工具栏中，在“调试目标”下拉列表框中，选择“本地计算机”。

## 通过使用 Visual State Manager 来调整布局

Customers 应用的用户界面可针对不同的分辨率和设备形态进行缩放，但如果减小视图的宽度，其工作效果仍然不佳，而且在智能手机上看起来可能也不太好，智能手机的宽度甚至更窄。如果仔细想想，在这些情况下解决问题的办法与其说是缩放控件，不如说是以不同的方式布局它们。例如，在窄视图中，Customers 表单最好看起来像这样：

### Customers

ID

Title

First Name

Last Name

Email

Phone

你可以通过以下几种方式实现此效果：

+   你可以为每种设备系列创建 MainPage.xaml 文件的多个版本。每个 XAML 文件都可以链接到同一个代码后置文件（MainPage.xaml.cs），这样它们都运行相同的代码。例如，要为智能手机创建 XAML 文件，请向项目中添加一个名为 DeviceFamily-Mobile 的文件夹（此名称很重要），然后使用“添加新项”菜单命令向该文件夹添加一个名为 MainPage.xaml 的新 XAML 视图。在此页面文件夹上按智能手机上应显示的方式布局控件。XAML 视图将自动链接到现有的 MainPage.xaml.cs 文件。运行时，UWP 将根据应用程序运行的设备类型选择适当的视图。

+   - 你可以使用 Visual State Manager 在运行时修改页面的布局。所有 UWP 应用都实现了一个 Visual State Manager，用于跟踪应用的视觉状态。它可以检测窗口的高度和宽度何时发生变化，你可以添加 XAML 标记，根据窗口大小定位控件。此标记可以移动控件或显示和隐藏控件。
+   - 你可以使用 Visual State Manager 根据窗口的高度和宽度在视图之间切换。这种方法是对前面描述的两种选项的混合组合，但它是混乱最少的方法（你不需要大量复杂的 XAML 代码来计算每个控件的最佳位置），也是最灵活的方法（如果在同一设备上缩小窗口，它也能工作）。

你将在接下来的练习中遵循这第三种方法。第一步是为窄视图中应出现的客户数据定义一个布局。

## 定义窄视图的布局

+   1. 在 Customers 应用的 XAML 面板中，将下面以粗体显示的 x:Name 和 Visibility 属性添加到 Grid 控件中：

Click here to view code image

```
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Grid x:Name="customersTabularView" Margin="10,20,10,20" Visibility="Collapsed">
        ...
    </Grid>
</Grid>
```

此 Grid 控件将保存表单的默认视图。你将在本练习集中后面的其他 XAML 标记中引用此 Grid 控件，因此需要为其命名。Visibility 属性指定控件是显示（Visible）还是隐藏（Collapsed）。默认值是 Visible，但暂时你将隐藏此 Grid，以便在定义另一个用于以列格式显示数据的 Grid 时使用。

+   2. 在 customersTabularView Grid 控件的结束 </Grid> 标签之后，添加另一个 Grid 控件。将 x:Name 属性设置为 customersColumnarView，将 Margin 属性设置为 10,20,10,20，并将 Visibility 属性设置为 Visible。

### Tip

你可以通过单击 Design View 窗口的 XAML 面板中 XAML 标记左侧边缘出现的 + 和 – 符号来展开和收缩 XAML 面板中的元素，使结构更易于阅读。

Click here to view code image

```
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Grid x:Name="customersTabularView" Margin="10,20,10,20" Visibility="Collapsed">
        ...
    </Grid>
    <Grid x:Name="customersColumnarView" Margin="10,20,10,20" Visibility="Visible">
    </Grid>
</Grid>
```

此 Grid 控件将保存表单的“窄”视图。此网格中的字段将按前面所述以列方式布局。

3. 在 customersColumnarView Grid 控件中，添加以下行定义：

Click here to view code image

```
<Grid x:Name="customersColumnarView" Margin="10,20,10,20" Visibility="Visible">
    <Grid.RowDefinitions>
        <RowDefinition Height="*"/>
        <RowDefinition Height="10*"/>
    </Grid.RowDefinitions>
</Grid>
```

你将使用顶部行显示标题，并使用第二行、更大的行来显示用户输入数据的控件。

4. 在行定义之后立即添加下面以粗体显示的 TextBlock 控件。此控件在 Grid 控件的第一行中显示截断的标题 Customers。将 FontSize 设置为 30。

Click here to view code image

```
<Grid x:Name="customersColumnarView" Margin="10,20,10,20" Visibility="Visible">
    <Grid.RowDefinitions>
        ...
    </Grid.RowDefinitions>
    <TextBlock Grid.Row="0" HorizontalAlignment="Center" TextWrapping="Wrap" Text="Customers" VerticalAlignment="Center" FontSize="30"/>
</Grid>
```

5. 在 customersColumnarView Grid 控件的第 1 行中添加另一个 Grid 控件，直接放在包含 Customers 标题的 TextBlock 控件之后。此 Grid 控件将以两列显示标签和数据输入控件，因此请将以下代码示例中以粗体显示的行和列定义添加到此 Grid。

Click here to view code image

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

请注意，如果一组中的所有行或列具有相同的高度或宽度，则无需指定其大小。

6. 将 customersTabularView Grid 控件中的 ID、Title、First Name 和 Last Name TextBlock 控件的 XAML 标记复制到新的 Grid 控件中，放在刚刚添加的行定义之后。将 ID 控件放在第 0 行，将 Title 控件放在第 1 行，将 First Name 控件放在第 2 行，将 Last Name 控件放在第 3 行。将所有控件放在第 0 列。

Click here to view code image

```
<Grid.RowDefinitions>
    ...
</Grid.RowDefinitions>
<TextBlock Grid.Row="0" Grid.Column="0"
HorizontalAlignment="Center"
TextWrapping="Wrap" Text="ID" VerticalAlignment="Center"
FontSize="20"/>
<TextBlock Grid.Row="1" Grid.Column="0"
HorizontalAlignment="Center"
TextWrapping="Wrap" Text="Title" VerticalAlignment="Center"
FontSize="20"/>
<TextBlock Grid.Row="2" Grid.Column="0"
HorizontalAlignment="Center"
TextWrapping="Wrap" Text="First Name" VerticalAlignment="Center"
FontSize="20"/>
<TextBlock Grid.Row="3" Grid.Column="0"
HorizontalAlignment="Center"
TextWrapping="Wrap" Text="Last Name" VerticalAlignment="Center"
FontSize="20"/>
```

7. 将 customersTabularView Grid 控件中的 id、title、firstName 和 lastName TextBox 和 ComboBox 控件的 XAML 标记复制到新的 Grid 控件中，放在 TextBox 控件之后。将 id 控件放在第 0 行，将 title 控件放在第 1 行，将 firstName 控件放在第 2 行，将 lastName 控件放在第 3 行。将四个控件全部放在第 1 列。此外，通过在控件名称前加上字母 c（表示列）来更改控件的名称。此最终更改是必要的，以避免与 customersTabularView Grid 控件中现有控件的名称冲突。

Click here to view code image

```
<TextBlock Grid.Row="3" Grid.Column="0"
HorizontalAlignment="Center"
TextWrapping="Wrap" Text="Last Name" .../>
<TextBox Grid.Row="0" Grid.Column="1" x:Name="cId"
HorizontalAlignment="Stretch"
TextWrapping="Wrap" Text="" VerticalAlignment="Center"
FontSize="20" IsReadOnly="True"/>
<TextBox Grid.Row="2" Grid.Column="1" x:Name="cFirstName"
HorizontalAlignment="Stretch"
TextWrapping="Wrap" Text="" VerticalAlignment="Center"
FontSize="20"/>
<TextBox Grid.Row="3" Grid.Column="1" x:Name="cLastName"
HorizontalAlignment="Stretch"
TextWrapping="Wrap" Text="" VerticalAlignment="Center"
FontSize="20"/>
<ComboBox Grid.Row="1" Grid.Column="1" x:Name="cTitle"
HorizontalAlignment="Stretch"
VerticalAlignment="Center" FontSize="20">
    <ComboBoxItem Content="Mr"/>
    <ComboBoxItem Content="Mrs"/>
    <ComboBoxItem Content="Ms"/>
    <ComboBoxItem Content="Miss"/>
</ComboBox>
```

8. 将 customersTabularView Grid 控件中的电子邮件地址和电话号码的 TextBlock 和 TextBox 控件复制到新的 Grid 控件中，放在 cTitle ComboBox 控件之后。将 TextBlock 控件放在第 0 列，第 4 行和第 5 行，将 TextBox 控件放在第 1 列，第 4 行和第 5 行。将电子邮件 TextBox 控件的名称更改为 cEmail，将电话 TextBox 控件的名称更改为 cPhone。删除 cEmail 和 cPhone 控件的 Width 属性，并将它们的 HorizontalAlignment 属性设置为 Stretch。

Click here to view code image

```
<ComboBox ...>
    ...
</ComboBox>
<TextBlock Grid.Row="4" Grid.Column="0"
HorizontalAlignment="Center" TextWrapping="Wrap"
Text="Email" VerticalAlignment="Center" FontSize="20"/>
```

