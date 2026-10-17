
请注意，如果一组中的所有行或列具有相同的高度或宽度，则无需指定其大小。

6. 将 `customersTabularView` `Grid` 控件中的 `ID`、`Title`、`First Name` 和 `Last Name` `TextBlock` 控件的 XAML 标记复制到新的 `Grid` 控件中，放在刚刚添加的行定义之后。将 `ID` 控件放在第 0 行，将 `Title` 控件放在第 1 行，将 `First Name` 控件放在第 2 行，将 `Last Name` 控件放在第 3 行。将所有控件放在第 0 列。

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

7. 将 `customersTabularView` `Grid` 控件中的 `id`、`title`、`firstName` 和 `lastName` `TextBox` 和 `ComboBox` 控件的 XAML 标记复制到新的 `Grid` 控件中，放在 `TextBox` 控件之后。将 `id` 控件放在第 0 行，将 `title` 控件放在第 1 行，将 `firstName` 控件放在第 2 行，将 `lastName` 控件放在第 3 行。将四个控件全部放在第 1 列。此外，通过在控件名称前加上字母 `c`（表示列）来更改控件的名称。此最终更改是必要的，以避免与 `customersTabularView` `Grid` 控件中现有控件的名称冲突。

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

8. 将 `customersTabularView` `Grid` 控件中的电子邮件地址和电话号码的 `TextBlock` 和 `TextBox` 控件复制到新的 `Grid` 控件中，放在 `cTitle` `ComboBox` 控件之后。将 `TextBlock` 控件放在第 0 列，第 4 行和第 5 行，将 `TextBox` 控件放在第 1 列，第 4 行和第 5 行。将电子邮件 `TextBox` 控件的名称更改为 `cEmail`，将电话 `TextBox` 控件的名称更改为 `cPhone`。删除 `cEmail` 和 `cPhone` 控件的 `Width` 属性，并将它们的 `HorizontalAlignment` 属性设置为 `Stretch`。

Click here to view code image

```
<ComboBox ...>

    ...

</ComboBox>

<TextBlock Grid.Row="4" Grid.Column="0"

HorizontalAlignment="Center" TextWrapping="Wrap"

Text="Email" VerticalAlignment="Center" FontSize="20"/>
```

```
<TextBox Grid.Row="4" Grid.Column="1" x:Name="cEmail"
HorizontalAlignment="Stretch"
TextWrapping="Wrap" Text="" VerticalAlignment="Center"
FontSize="20"/>
<TextBlock Grid.Row="5" Grid.Column="0"
HorizontalAlignment="Center" TextWrapping="Wrap"
Text="Phone" VerticalAlignment="Center" FontSize="20"/>
<TextBox Grid.Row="5" Grid.Column="1" x:Name="cPhone"
HorizontalAlignment="Stretch"
TextWrapping="Wrap" Text="" VerticalAlignment="Center"
FontSize="20"/>
```

Design View 窗口应显示如下的列式布局：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_744_0.png)

9. 返回 `customersTabularView` `Grid` 控件的 XAML 标记，并将 `Visibility` 属性设置为 `Visible`。

Click here to view code image

```
<Grid x:Name="customersTabularView" Margin="10,20,10,20"

Visibility="Visible">
```

10. 在 `customersColumnarView` `Grid` 控件的 XAML 标记中，将 `Visibility` 属性设置为 `Collapsed`。

Click here to view code image

```
<Grid x:Name="customersColumnarView" Margin="10,20,10,20"

Visibility="Collapsed">
```

Design View 窗口应显示 Customers 表单的原始表格布局。这是应用将使用的默认视图。

您现在已定义了在窄视图中出现的布局。您可能会担心，本质上您所做的只是复制了许多控件并以不同方式布局它们。如果运行表单并在视图之间切换，数据如何在一种视图中传输到另一种视图？例如，如果在应用全屏运行时输入客户详细信息，然后切换到窄视图，新显示的控件将不包含您刚刚输入的相同数据。UWP 应用通过使用数据绑定来解决此问题。这是一种将同一数据关联到多个控件的技术，并且随着数据的更改，所有控件都会显示更新后的信息。您将在第 26 章看到其工作原理。目前，您只需要考虑如何使用 Visual State Manager 在视图更改时在布局之间切换。

您可以使用触发器，当显示的某些方面（如高度或宽度）发生变化时提醒 Visual State Manager。您可以在应用的 XAML 标记中定义这些触发器执行的视觉状态转换。这就是您将在下一个练习中要做的事情。

## 使用 Visual State Manager 修改布局

- 1. 在 Customers 应用的 XAML 面板中，在 `customersColumnarView` `Grid` 控件的结束 `</Grid>` 标签之后，添加以下标记：

Click here to view code image

```
<Grid x:Name="customersColumnarView" Margin="10,20,10,20" Visibility="Visible">

...

</Grid>

<VisualStateManager.VisualStateGroups>

    <VisualStateGroup>

        <VisualState x:Name="TabularLayout">

        </VisualState>

    </VisualStateGroup>

</VisualStateManager.VisualStateGroups>
```

您通过实现一个或多个视觉状态组来定义视觉状态转换。每个视觉状态组指定在 Visual State Manager 切换到此状态时应发生的转换。每个状态应被赋予有意义的名称以帮助您识别其用途。

- 2. 将以下以粗体显示的视觉状态触发器添加到视觉状态组：

Click here to view code image

```
<VisualStateManager.VisualStateGroups>

    <VisualStateGroup>

        <VisualState x:Name="TabularLayout">

            <VisualState.StateTriggers>

                <AdaptiveTrigger MinWindowWidth="660" />

            </VisualState.StateTriggers>

        </VisualState>

    </VisualStateGroup>

</VisualStateManager.VisualStateGroups>
```

此触发器将在窗口宽度降至 660 像素以下时触发。这是 Customers 表单上的控件和标签开始换行并变得难以使用时的宽度。

3. 在触发器定义之后，将以下以粗体显示的代码添加到 XAML 标记中：

Click here to view code image

```
<VisualStateManager.VisualStateGroups>

    <VisualStateGroup>

        <VisualState x:Name="TabularLayout">

            <VisualState.StateTriggers>

                <AdaptiveTrigger MinWindowWidth="660"/>

            </VisualState.StateTriggers>

            <VisualState.Setters>

                <Setter Target="customersTabularView.Visibility" Value="Visible"/>

                <Setter Target="customersColumnarView.Visibility" Value="Collapsed"/>

            </VisualState.Setters>

        </VisualState>

    </VisualStateGroup>

</VisualStateManager.VisualStateGroups>
```

此代码指定触发器被触发时发生的操作。在此示例中，操作是通过使用 `Setter` 元素定义的。`Setter` 元素指定要设置的属性和应设置该属性的值。对于此视图，`Setter` 命令更改指定属性的值；`customersTabularView` `Grid` 控件变为可见，而 `customersColumnarView` `Grid` 控件被折叠（变为不可见）。

4. 在 `TabularLayout` 视觉状态定义之后，添加以下以粗体显示的标记，该标记为窄视图定义了等效功能：

Click here to view code image

```
<VisualStateManager.VisualStateGroups>

    <VisualStateGroup>

        <VisualState x:Name="TabularLayout">

            ...

        </VisualState>

        <VisualState x:Name="ColumnarLayout">

            <VisualState.StateTriggers>

                <AdaptiveTrigger MinWindowWidth="0"/>

            </VisualState.StateTriggers>

            <VisualState.Setters>

                <Setter Target="customersTabularView.Visibility" Value="Collapsed"/>

                <Setter Target="customersColumnarView.Visibility" Value="Visible"/>

            </VisualState.Setters>

        </VisualState>

    </VisualStateGroup>

</VisualStateManager.VisualStateGroups>
```

```
</VisualStateGroup>

</VisualStateManager.VisualStateGroups>
