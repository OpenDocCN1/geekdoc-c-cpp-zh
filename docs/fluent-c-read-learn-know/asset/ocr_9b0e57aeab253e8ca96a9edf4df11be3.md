# HOW'D YOU DO?

Remember, there are different ways to express the same thing in both C# and XAML, so don't worry if your code is a little different than mine, so long as the syntax is correct.

```
```csharp
Window MainWindow = new MainWindow();
MainWindow.Title = "Sample";
MainWindow.Height = 300;
MainWindow.Width = 500;
DockPanel LayoutRoot = new DockPanel();
Menu MainMenu = new Menu();
MenuItem FileMenu = new MenuItem();
FileMenu.Header = "File";
MainMenu.AddChild(FileMenu);
LayoutRoot.Children.Add(MainMenu);
MainWindow.Content = LayoutRoot;
```
```

```
```xml
<Window x:Class="MainWindow" Title="Sample" Height="300" Width="500">
<DockPanel Name="LayoutRoot">
<Menu Name="MainMenu">
<MenuItem Name="FileMenu" Header="File" />
</Menu>
</DockPanel>
</Window>
```
```

This one was a little tricky. Did you get it right? You don't need to explicitly add the MenuItem to the Menu because that's implicit in the structure of the XAML.

Did you have a problem figuring out what to call the variables here? Unlike C# variables, XAML elements don't have to have names unless you're going to reference them in code, but it's a good idea to give them one using the name attribute.

```
```csharp
MainWindow mywindow = new MainWindow();
Grid LayoutRoot = new Grid();
Button myButton = new Button();
myButton.Height = 50;
myButton.Width = 75;
LayoutRoot.Children.Add(myButton);
myWindow.Content = LayoutRoot;
```
```

```
```xml
<Window x:Class="MainWindow" Height="Auto" Width="Auto">
<Grid Name="LayoutRoot">
<Button Height="50" Width="75">
Cancel
</Button>
</Grid>
</Window>
```
```