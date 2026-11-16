# # PUT ON YOUR THINKING HAT

Time to get your feet wet. Can you translate the C# snippet below into XAML, and the XAML code into C#? [Don't worry about what all the elements are. We'll be examining them in later chapters.

![](bbox=[0.09, 0.05, 0.2, 0.21])

```
Window MainWindow = new MainWindow();
MainWindow.Title = "Sample";
MainWindow.Height = 300;
MainWindow.Width = 500;

DockPanel LayoutRoot = new
DockPanel();

Menu MainMenu = new Menu();
MenuItem FileMenu = new MenuItem();
FileMenu.Header = "File";

MainMenu.AddChild(FileMenu);
LayoutRoot.Children.Add(MainMenu);
MainWindow.Content = LayoutRoot;
```

> Notice that you call AddChild() on the Menu, but Add() on the LayoutRoot. You'll find out why when we examine WPF controls in the next chapter.

```
<Window x:Class="MainWindow" Height="Auto" Width="Auto">
<Grid name="LayoutRoot">
<Button Height="50" Width="75">
Cancel
</Button>
</Grid>
</Window>
```