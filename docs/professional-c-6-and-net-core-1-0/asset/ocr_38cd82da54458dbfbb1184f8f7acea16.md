![](bbox=[0.1, 0.06, 0.9, 0.17])

# Figure 30.10

# SolidColorBrush

The first button in Figure 30.10 uses the SolidColorBrush, which, as the name suggests, uses a solid color. The complete area is drawn with the same color.

You can define a solid color just by setting the Background attribute to a string that defines a solid color. The string is converted to a SolidColorBrush element with the help of the BrushValueSerializer (code file Brushes [WPF|UWP]/Main [Window|Page].xaml):

```
<Button Height="30" Background="#FFC9659C">Solid Color</Button>
```

Of course, you will get the same effect by setting the Background child element and adding a SolidColorBrush element as its content (code file BrushesDemo/MainWindow.xaml). The first button in the application uses a hexadecimal value for the solid background color:

```
<Button Content="Solid Color" Margin="10">
<Button.Background>
<SolidColorBrush Color="#FFC9659C" />
</Button.Background>
</Button>
```

# LinearGradientBrush

For a smooth color change, you can use the LinearGradientBrush, as the second button in Figure 30.10 shows. This brush defines the StartPoint and EndPoint properties. With this, you can assign two-dimensional coordinates for the linear gradient. The default gradient is diagonal linear from 0,0 to 1,1. By defining different values, the gradient can take different directions. For example, with a StartPoint of 0,0 and an EndPoint of 0,1, you get a vertical gradient. The StartPoint and EndPoint value of 1,0 creates a horizontal gradient.

With the content of this brush, you can define the color values at the specified offsets with the GradientStop element. Between the stops, the colors are smoothed (code file Brushes [WPF|UWP]/Main [Window|Page].xaml):

```
<Button Content="Linear Gradient Brush" Margin="10">
<Button.Background>
<LinearGradientBrush StartPoint="0,0" EndPoint="0,1">
<GradientStop Offset="0" Color="LightGreen" />
<GradientStop Offset="0.4" Color="Green" />
<GradientStop Offset="1" Color="DarkGreen" />
```