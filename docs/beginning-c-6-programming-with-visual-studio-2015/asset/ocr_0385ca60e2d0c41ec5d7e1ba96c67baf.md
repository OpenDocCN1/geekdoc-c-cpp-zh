The code used here is as follows (you can find it in the downloaded code at LayoutExamples\ StackPanels.xaml):

```
```xml
<Window x:Class="LayoutExamples.StackPanels"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:local="clr-namespace:LayoutExamples"
mc:Ignorable="d"
Title="StackPanel" Height="300" Width="300">
    <Grid>
        <StackPanel HorizontalAlignment="Left" Height="128" VerticalAlignment="Top" Width="284" Orientation="Horizontal">
            <Button Content="Button" Height="128" VerticalAlignment="Top" Width="75"/>
            <Button Content="Button" Height="128" VerticalAlignment="Top" Width="75"/>
            <Button Content="Button" Height="128" VerticalAlignment="Top" Width="75"/>
        </StackPanel>
        <StackPanel HorizontalAlignment="Left" Height="128" VerticalAlignment="Top" Width="284" Margin="0,128,0,0" Orientation="Vertical">
            <Button Content="Button" HorizontalAlignment="Left" Width="284"/>
            <Button Content="Button" HorizontalAlignment="Left" Width="284"/>
            <Button Content="Button" HorizontalAlignment="Left" Width="284"/>
        </StackPanel>
    </Grid>
</Window>
```
```

# WrapPanel

WrapPanel is essentially an extended version of StackPanel; controls that “don’t fit” are moved to additional rows (or columns). Figure 14-6 shows a WrapPanel control containing multiple shapes, with the window resized to two sizes.

![](bbox=[0.15, 0.73, 0.55, 0.84])

FIGURE 14-6

The code to achieve this effect is shown here (you can find it in the downloaded code at LayoutExamples\WrapPanel.xaml):

```
```xml
<Window x:Class="LayoutExamples.WrapPanel"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
```
```