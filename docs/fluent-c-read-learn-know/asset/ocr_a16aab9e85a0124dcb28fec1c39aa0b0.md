![](bbox=[0.085, 0.055, 0.205, 0.165])

# # XAML FUNDAMENTALS

Let's start our examination of XAML with a comparison of XAML markup with something you're already familiar with, C#. The following code snippets produce the same window:

```
```
<Window x:Class="MainWindow" Title="My Window" Name="MyWindow">
<Grid name="LayoutRoot">
<!-- The button is inside the grid -->
<Button name="FirstButton" Height="74" Width="229">
Click Me, Please
</Button>
</Grid>
</Window>
```
```

```
```
Window MyWindow = new MainWindow();
MyWindow.Title = "My Window";
Grid LayoutRoot = new Grid();
MyWindow.Content = LayoutRoot;
// The button is inside the grid
Button FirstButton = new Button();
Button.Height = 74;
Button.Width = 229;
Button.Content = "Click Me, Please";
LayoutRoot.Children.Add(FirstButton);
```
```

![](bbox=[0.105, 0.67, 0.23, 0.83])

# ## PUT ON YOUR THINKING HAT

If C# can do everything XAML can do, and a lot more besides, can you think of some reasons why using both languages in the application development process is a good idea?