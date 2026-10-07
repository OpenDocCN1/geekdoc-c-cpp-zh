
```cs
br.GradientStops.Add(new GradientStop(Colors.Lime, 0.75));
br.GradientStops.Add(new GradientStop(Colors.Blue, 1.00));
grdGradientBackground.Background = br;
```

这段代码创建了一个 `RadialBrush`。然后，它将 `GradientStop` 对象添加到画笔的 `GradientStops` 集合中。

## 不需要类型转换器

注意传递给 `GradientStop` 对象构造函数的值是一个颜色和一个数值。由于这两个值都不像 XAML 文件中那样字符串，因此它们不需要类型转换器。

属性元素（Property elements）允许您在 XAML 代码中构建复杂对象。之前的示例中使用的其他常见属性元素包括：

- Grid.ColumnDefinitions：`ColumnDefinition` 对象的集合，决定了 Grid 列的宽度。
- Grid.RowDefinitions：`RowDefinition` 对象的集合，决定了 Grid 行的高度。
- BitmapEffect：控件的 `Bitmap` 属性决定控件是否显示阴影、浮雕表面、斜角或其他特殊效果。`BitmapEffect` 必须是一个对象，因此 XAML 代码必须将其设置为属性元素。

## 高效效果

> Microsoft 本可以为 `BitmapEffect` 定义一个简单的类型转换器。例如，它可以将字符串 "Bevel" 转换为 `BevelBitmapEffect` 对象。遗憾的是，他们没有这样做，你只能使用属性元素。

- Header：项在 `MenuItem` 中的显示、作为 `GroupBox` 的标题或在 `TabItem` 标签上由 `Header` 属性定义。如果您想使用属性将 `Header` 设置为字符串值；如果您想显示其他内容（如 `Image` 或 `StackPanel`），则您需要使用属性元素。
- ContextMenu：控件的 `ContextMenu` 属性定义了右键点击时出现的菜单。在对象上，您必须使用属性元素来定义它。
- LayoutTransform：控件的 `LayoutTransform` 属性决定控件在布局和绘制之前如何移动、拉伸或旋转。这些变换是复杂的对象，您必须使用属性元素来定义它们。

## 属性元素语法 157

图 9-3 所示的 `PropertyElements` 示例程序演示了这些属性元素。

以下 XAML 代码展示了 `PropertyElements` 程序是如何工作的。代码后的讨论介绍了每个属性元素的功能。在阅读讨论时，请参考图 9-3 以查看结果。

```xml
<Window
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  x:Class="Window"
  x:Name="PropertyElements"
  Width="400" Height="300"
  FontWeight="Bold" FontSize="16">
  <Background>
    <LinearGradientBrush EndPoint="0.5,1" StartPoint="0.5,0">
      <GradientStop Color="Red" Offset="0"/>
      <GradientStop Color="Black" Offset="1"/>
    </LinearGradientBrush>
  </Background>
  <Grid>
    <Grid.ColumnDefinitions>
      <ColumnDefinition Width="*"/>
      <ColumnDefinition Width="*"/>
      <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
    <Grid.RowDefinitions>
      <RowDefinition Height="*"/>
      <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    <Image.Row="0" Width="100" Height="Auto"
      Source="Lighthouse.jpg">
      <BevelBitmapEffect BevelWidth="10"/>
    </Image>
    <Image.ContextMenu>
      <ContextMenu>
        <MenuItem Header="Header">
          <StackPanel Orientation="Horizontal">
            <TextBlock Text="Phone" VerticalAlignment="Center"/>
            <Image Width="30"
              Source="cellphone.ico">
              <DropShadowBitmapEffect/>
            </Image>
          </StackPanel>
        </MenuItem>
        <MenuItem Header="Exit"/>
      </ContextMenu>
    </Image.ContextMenu>
  </Grid>
</Window>
```

```xml
</Image.ContextMenu>
</Image>
<GroupBox Grid.Row="0" Grid.Column="1" Grid.ColumnSpan="2" Margin="10">
  <GroupBox Header>
    <StackPanel Orientation="Horizontal">
      <Label Content="Keys"/>
      <Image Width="30" Source="Keys.ico">
        <Image.BitmapEffect>
          <DropShadowBitmapEffect/>
        </Image.BitmapEffect>
      </Image>
    </StackPanel>
  </GroupBox>
  <Image Grid.Row="1" Grid.Column="0" Width="75" Source="Fog.jpg">
    <Image.LayoutTransform>
      <RotateTransform Angle="-10"/>
    </Image.LayoutTransform>
  </Image>
  <Label Content="Stretched Text" FontSize="25" Foreground="Yellow" HorizontalAlignment="Center" VerticalAlignment="Top" Margin="0, -40" Grid.Row="1" Grid.Column="1" Grid.ColumnSpan="2">
    <Label.RenderTransform>
      <TransformGroup>
        <ScaleTransform ScaleY="3"/>
        <SkewTransform Angle="20"/>
        <RotateTransform Angle="20"/>
      </TransformGroup>
    </Label.RenderTransform>
  </Label>
</Grid>
```

## 158 | 第 9 章 属性

## PropertyElements

图 9-3 所示的 `PropertyElements` 示例程序演示了这些属性元素。

以下 XAML 代码展示了 `PropertyElements` 程序是如何工作的。代码后的讨论介绍了每个属性元素的功能。在阅读讨论时，请参考图 9-3 以查看结果。

*(注：原文后续存在大量重复和 OCR 错误，此处已合并核心内容并进行翻译)*
