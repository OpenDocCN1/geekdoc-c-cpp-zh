![](bbox=[0.36, 0.06, 0.58, 0.24])

# Figure 10.56: Changing the Appearance of a Control

# Using ControlTemplate

The ControlTemplate template specifies the structure of a control that can be shared across multiple instances of the control. Let’s use the Control template in a WPF application. Create a WPF application named UsingControlTemplate (available in the CD) and add the following code to the MainWindow.xaml file, as shown in Listing 10.26:

# Listing 10.26: Showing the Code for Implementing ControlTemplate

```
<Window x:Class="UsingControlTemplate.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="350" Width="525">
<Window.Resources>
<Style x:Key="ButtonStyle" TargetType="{x:Type Button}">
<Setter Property="Template">
<Setter.Value>
<ControlTemplate>
<Grid>
<Grid.RowDefinitions>
<RowDefinition Height="2*"/>
<RowDefinition Height="*"/>
</Grid.RowDefinitions>
<Rectangle RadiusX="4" RadiusY="8" Margin="2">
<Rectangle.Fill>
<LinearGradientBrush StartPoint="0,0" EndPoint="0,1">
<GradientStop Offset="0" Color="LightBlue"/>
<GradientStop Offset="0.5" Color="Gold"/>
<GradientStop Offset="1" Color="PaleGreen"/>
</LinearGradientBrush>
</Rectangle.Fill>
</Rectangle>
</Grid>
</ControlTemplate>
</Setter.Value>
</Setter>
</Style>
</Window.Resources>
<StackPanel>
<Button Name="Button1" Height="41" />
<Button Name="Button2" Height="41" />
<Button Name="Button3" Style="{StaticResource ButtonStyle}" Height="71">TemplateButton</Button>
</StackPanel>
</Window>
```