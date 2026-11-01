+   - Animation storyboarding that can be used in all manner of situations, including user-triggered events such as mouse clicks on buttons
+   - Reusable resources that you can use to dynamically style controls

# Separation of Concerns

One problem that exists with maintaining Windows applications that has been written over the years is that they very often mix the code that generates the user interface and the code that executes based on users' actions. This makes it difficult for multiple developers and designers to work on the same project. WPF solves this in two ways. First, by using XAML to describe the GUI rather than C#, the GUI becomes platform independent, and you can in fact render XAML without any code whatsoever. Second, this means that it feels natural to place the C# code in a different file than you place the GUI code. Visual Studio utilizes something called code-behind files, which are C# files that are dynamically linked to the XAML files.

Because the GUI is separated from the code, it is possible to create tailor-made applications for designing the GUI, and this is exactly what Microsoft has done. The design tool Blend for Visual Studio is the favored tool used by designers when creating GUIs for WPF. This tool can load the same projects as Visual Studio, but where Visual Studio targets the developer more than the designer, the opposite is true in Expression Blend. This means that on large projects with designers and developers, everyone can work together on the same project, using their preferred tool without fear of inadvertently influencing the others.

# XAML in Action

As stated, XAML is XML, which means that as long as the files are fairly small, it is possible to see immediately what it is describing. Take a look at this small example and see if you can tell what it does:

```
<Window x:Class="Ch14Ex01.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:local="clr-namespace:WpfApplication1"
    mc:Ignorable="d"
    Title="Hello World" Height="350" Width="525">
    <Grid>
        <Button Content="Hello World"
            HorizontalAlignment="Left"
            Margin="220,151,0,0"
            VerticalAlignment="Top"
            Width="75"/>
    </Grid>
</Window>
```

The XAML in this example creates a window with a single button on it. Both the window and the button display the text "Hello World". XML allows you to place tags inside other tags as long as