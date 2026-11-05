# 27.1.8 Reading and Writing XAML File - Embed a C# Code into an XAML File

Windows-based WPF applications need to respond to user interface events in very specialized ways. Here is where XAML must be supplemented by real programming code. This code can be put in a CS's separate file or embed it directly in the XAML. It is entirely possible to embed C# code into an XAML file. It's not pretty, but it works. XAML actually supports "code inside" in addition to code behind (somewhat like in ASP.NET).

Below is detailed simple example of embedding C# code into a XAML file.

# Step 1 : Create WPF Window

+   - Create new WPF window in WPF application.
+   - Add a Button in the created window.

```
<Window x:Class="DropBoxIntegration.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006
xmlns:local="clr-namespace:DropBoxIntegration" mc:Ignorable="d"
Title="MainWindow" Height="321" Width="1024" MinHeight="300" MinWidth="600">
<Grid>
<Button x:Name="button" Content="Button" HorizontalAlignment="Left"
Margin="273,3,0,0" Grid.Row="3" VerticalAlignment="Top" Width="7
5" Height="17">
</Button>
</Grid>
</Window>
```

# Step 2 : Messagebox popup on button click.

Add the below mentioned code as it is inside <button> tag.

Bind the Buttonclick event to the below event "Clicked".

```
<x:Code>
<![CDATA[
void Clicked(object sender, RoutedEventArgs e)
{
MessageBox.Show("Hello World");
}
]]>
</x:Code>
```

Combining above two code sets as below,

```
<Window x:Class="DropBoxIntegration.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
```