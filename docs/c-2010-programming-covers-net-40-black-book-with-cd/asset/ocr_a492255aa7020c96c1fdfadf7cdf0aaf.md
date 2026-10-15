# Setting Styles through Resources

Resources are helpful in setting styles in WPF because resources enable the styles to be reused in applications. If you declare the style in the root element of an application, the style can be used anywhere in the application. If you declare the style in one of the application’s XAML files, then the style can be used in that XAML file only. Let’s learn to set the styles in a WPF application through resources. Create a WPF application named SettingStyle_Resources (available in the CD) and add the code to the MainWindow.xaml file, as shown in Listing 10.22:

# Listing 10.22: Showing the Code for Setting Styles

```
<Window x:Class="SettingStyle_Resources.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="350" Width="525">
<Grid>
<StackPanel x:Name="ButtonPanel" Background="PeachPuff">
<StackPanel.Resources>
<Style x:Key="MyButton">
<Setter Property="Button.Background" Value="Pink"/>
<Setter Property="Button.Foreground" Value="Blue"/>
<Setter Property="Button.MinWidth" Value="50"/>
<Setter Property="Button.MinHeight" Value="50"/>
<Setter Property="Button.Margin" Value="12"/>
</Style>
</StackPanel.Resources>
<Button Style="{StaticResource MyButton}">Button1</Button>
<Button Style="{StaticResource MyButton}">Button2</Button>
<Button Style="{StaticResource MyButton}">Button3</Button>
</StackPanel>
</Grid>
</Window>
```

In Listing 10.22, there are three Button controls, which are added inside a StackPanel control. All the Button controls have the same style. The style of the Button control is commonly defined through a resource. You just need to reference the style in all of the Button controls. Now, run the application by pressing the F5 key. Figure 10.54 shows the output of Listing 10.22:

![](bbox=[0.33, 0.59, 0.67, 0.78])

Figure 10.54: Style Applied to Controls

# Extending an Existing Style

There are some cases where you want two controls to share the same style. You can do this by creating a new style that is based on the first style. Let’s learn how to do this in a WPF application. Create an application named ExtendingStyle (available in the CD) and add the code to the MainWindow.xaml file, as shown in Listing 10.23: