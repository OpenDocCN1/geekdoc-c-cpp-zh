

Segoe Print 字体比默认字体更大。

13. 切换回 MainPage.xaml 文件并找到 customersTabularView Grid 控件中 Adventure Works Customers 标签的 TextBlock 控件的 XAML 标记：

Click here to view code image

```
<TextBlock Grid.Row="0" HorizontalAlignment="Center"
TextWrapping="Wrap"
Text="Adventure Works Customers" VerticalAlignment="Center"
FontSize="50"/>
```

14. 将此控件的属性更改为引用 TabularHeaderStyle 样式，如以下代码中以粗体所示：

Click here to view code image

```
<TextBlock Grid.Row="0" Style="{StaticResource TabularHeaderStyle}"
Text="Adventure Works Customers"/>
```

Design View 窗口中显示的标题应更改颜色、大小和字体，看起来像这样：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_753_0.png)

15. 找到 customers-ColumnarView Grid 控件中 Customers 标签的 TextBlock 控件的 XAML 标记：

Click here to view code image

```
<TextBlock Grid.Row="0" HorizontalAlignment="Center"
TextWrapping="Wrap"
Text="Customers" VerticalAlignment="Center" FontSize="30"/>
```

修改此控件的标记以引用 ColumnarHeaderStyle 样式，如此处以粗体所示：

Click here to view code image

```
<TextBlock Grid.Row="0" Style="{StaticResource ColumnarHeaderStyle}"
Text="Customers"/>
```

请注意，由于 customers-ColumnarView Grid 控件默认情况下是折叠的，因此您在 Design View 窗口中看不到此更改。但是，当您稍后在本练习中运行该应用程序时，您将看到此更改的效果。

16. 返回 Code and Text Editor 窗口中的 AppStyles.xaml 文件。修改 HeaderStyle 样式，添加以下示例中以粗体显示的附加属性 Setter 元素：

Click here to view code image

```
<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn="{StaticResource FontStyle}">
    <Setter Property="HorizontalAlignment" Value="Center"/>
    <Setter Property="TextWrapping" Value="Wrap"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="Foreground" Value="SteelBlue"/>
    <Setter Property="RenderTransformOrigin" Value="0.5,0.5"/>
    <Setter Property="RenderTransform">
        <Setter.Value>
            <CompositeTransform Rotation="-5"/>
        </Setter.Value>
    </Setter>
</Style>
```

这些元素通过使用转换将标题中显示的文本绕其中点旋转 5 度角。

### Note

此示例显示了一个简单的转换。使用 RenderTransform 属性，您可以对项目执行各种其他转换，并且可以组合多个转换。例如，您可以在 x 和 y 轴上平移（移动）项目，使项目倾斜（使其倾斜），并缩放元素。

您还应注意到 RenderTransform 属性的值本身就是另一个属性/值对（属性为 Rotation，值为 −5）。在这种情况下，您使用 <Setter.Value> 标签指定值。

17. 切换到 MainPage.xaml 文件。在 Design View 窗口中，标题现在应以俏皮的角度显示：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_754_0.png)

18. 在 AppStyles.xaml 文件中，添加以下样式：

Click here to view code image

```
<Style x:Key="LabelStyle" TargetType="TextBlock" BasedOn="{StaticResource FontStyle}">
    <Setter Property="FontSize" Value="30"/>
    <Setter Property="HorizontalAlignment" Value="Center"/>
    <Setter Property="TextWrapping" Value="Wrap"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="Foreground" Value="AntiqueWhite"/>
</Style>
```

您将把此样式应用于为用户输入客户信息而使用的各种 TextBox 和 ComboBox 控件提供标签的 TextBlock 元素。该样式引用与标题相同的字体样式，但将其他属性设置为更适合标签的值。

19. 返回 MainPage.xaml 文件。在 XAML 窗格中，修改 customersTabularView 和 customersColumnarView Grid 控件中每个标签的 TextBlock 控件的标记。删除 HorizontalAlignment、TextWrapping、VerticalAlignment 和 FontSize 属性，并引用 LabelStyle 样式，如此处以粗体所示：

Click here to view code image

```
<Grid x:Name="customersTabularView" Margin="10,20,10,20" Visibility="Visible">
    ...
    <Grid Grid.Row="2">
        ...
        <TextBlock Grid.Row="0" Grid.Column="1" Style="{StaticResource LabelStyle}" Text="ID"/>
        <TextBlock Grid.Row="0" Grid.Column="3" Style="{StaticResource LabelStyle}" Text="Title"/>
        <TextBlock Grid.Row="0" Grid.Column="5" Style="{StaticResource LabelStyle}" Text="First Name"/>
        <TextBlock Grid.Row="0" Grid.Column="7" Style="{StaticResource LabelStyle}" Text="Last Name"/>
        ...
        <TextBlock Grid.Row="3" Grid.Column="1" Style="{StaticResource LabelStyle}" Text="Email"/>
        ...
        <TextBlock Grid.Row="5" Grid.Column="1" Style="{StaticResource LabelStyle}" Text="Phone"/>
        ...
    </Grid>
</Grid>
<Grid x:Name="customersColumnarView" Margin="10,20,10,20" Visibility="Collapsed">
```

```
...
<Grid Grid.Row="1">
...
<TextBlock Grid.Row="0" Grid.Column="0" Style="{StaticResource LabelStyle}"
Text="ID"/>
<TextBlock Grid.Row="1" Grid.Column="0" Style="{StaticResource LabelStyle}"
Text="Title"/>
<TextBlock Grid.Row="2" Grid.Column="0" Style="{StaticResource LabelStyle}"
Text="First Name"/>
<TextBlock Grid.Row="3" Grid.Column="0" Style="{StaticResource LabelStyle}"
Text="Last Name"/>
...
<TextBlock Grid.Row="4" Grid.Column="0" Style="{StaticResource LabelStyle}"
Text="Email"/>
...
<TextBlock Grid.Row="5" Grid.Column="0" Style="{StaticResource LabelStyle}"
Text="Phone"/>
...
</Grid>
</Grid>
```

表单上的标签应更改为 Segoe Print 字体，并以白色显示，字体大小为 30 磅：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_756_0.png)

20. 在 Debug 菜单上，单击 Start Debugging 以构建并运行应用程序。

### Note

如果您在分辨率小于 1366 × 768 的显示器上运行，请使用 Simulator。

Customers 表单应出现并以与 Visual Studio 中的 Design View 窗口中显示的方式相同的样式进行样式设置。请注意，如果您在表单上的各个字段中输入任何文本，它们将使用 TextBox 控件的默认字体和样式。

### Note

虽然 Segoe Print 字体适用于标签和标题，但不建议将其用作数据输入字段的字体，因为其中一些字符可能难以区分。例如，小写字母 l 与数字 1 非常相似，大写字母 O 与数字 0 几乎无法区分。因此，对于 TextBox 控件坚持使用默认字体是有意义的。

21. 调整窗口大小使其变窄，并验证样式是否已应用于 customersColumnarView 网格中的控件。表单应如下所示：

# Customers

ID

Title

First Name

Last Name

Email

Phone

22. 返回 Visual Studio 并停止调试。

为完整起见，以下图像显示了 Customers 应用程序在 Windows Phone 10 模拟器上运行：

# Customers

ID

Title

First Name

Last Name

Email

Phone

您可以看到，通过使用样式，您可以轻松实现许多很酷的效果。此外，仔细使用样式可以使您的代码比在单个控件上设置属性时更易于维护。例如，如果您想更改 Customers 应用程序中标签和标题使用的字体，您只需对 *FontStyle* 样式进行一次更改。一般来说，您应该尽可能使用样式；除了有助于可维护性之外，使用样式还有助于保持表单的 XAML 标记干净整洁，并且表单的 XAML 只需指定控件和布局，而无需指定控件在表单上应如何显示。您还可以使用 Visual Studio 2015 的 Microsoft Blend 来定义可集成到应用程序中的复杂样式。专业图形艺术家可以使用 Blend 开发自定义样式并以 XAML 标记的形式提供这些样式供开发人员构建应用程序使用。开发人员需要做的就是将适当的 *Style* 标签添加到用户界面元素以引用相应的样式。

## Summary

在本章中，您学习了如何使用 *Grid* 控件来实现可扩展到不同设备形态和方向的用户界面。您还学习了如何使用 Visual State Manager 在用户更改显示应用程序的窗口大小时调整控件的布局。最后，您学习了如何创建自定义样式并将其应用于表单上的控件。现在您已经定义了用户界面，下一个挑战是为应用程序添加功能，使用户能够显示和更新数据，这就是您将在最后几章中要做的事情。

- 如果您想继续下一章，请保持 Visual Studio 2015 运行并转到第 26 章。
- 如果您现在想退出 Visual Studio 2015，请在 File 菜单上单击 Exit。如果出现 Save 对话框，请单击 Yes 并保存项目。

## Quick reference

