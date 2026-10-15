```
RadiusX="1" RadiusY="1">
<GradientStop Color="LightPink" Offset="0.25" />
<GradientStop Color="DeepPink" Offset="0.5" />
<GradientStop Color="Pink" Offset="1" />
</RadialGradientBrush>
</TextBlock.Foreground>
Hello WPF
</TextBlock>
</Border>
</StackPanel>
</StackPanel>
</Window>
```

In Listing 12.32, a Button control is added to the window. When you run the application, by pressing the F5 key on the keyboard, and click the Button control, a TextBlock appears on the window with a scrolling effect. This effect is possible with the help of the transforming effect of the DoubleAnimation class. After clicking the Button control, the output of the code is shown in Figure 12.35:

![](bbox=[0.31, 0.335, 0.65, 0.58])

Figure 12.35: Transforming Control using the DoubleAnimation Class

# Creating Local Animations

You have learned to create animations by using the Storyboard timeline, either through the XAML code or the code of the code-behind file. There can be instances when you can create animations without using a Storyboard object. This type of animation is termed as local animation. You can use the BeginAnimation method to apply local animation that cannot be created in the XAML code. You can create local animations in the code-behind file. You should add the System.Windows.Media.Animation namespace in your code file for creating local animation. Let's create animations which are locally created. To do this, create a WPF application named LocalAnimation (also available in CD) and add the code, given in Listing 12.33, to the MainWindow.xaml file:

# Listing 12.33: Creating Local Animation

```
<Window x:Class="LocalAnimation.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="300" Width="300">
<Grid>
<Button Height="23" HorizontalAlignment="Left" Margin="25,31,0,0" Name="Button1" VerticalAlignment="Top" Width="91" Click="button1_Click">One Rotation</Button>
<Rectangle Margin="131,0,0,50" Name="rectangle1" Stroke="Black" Fill="Aqua" Height="66" VerticalAlignment="Bottom" HorizontalAlignment="Left" Width="72" />
<Button Height="23" HorizontalAlignment="Right" Margin="0,31,23,0" Name="button2" VerticalAlignment="Top" Width="75" Click="button2_Click">Forever</Button>
```