
that the end result of the measure-arrange process is different depending on the type of layout container performing the process.

For example, the elements contained within a Grid control are laid out according to the row-and-column layout defined by column and row definitions and the assignment of UI elements to specific rows and columns. Elements contained within a StackPanel are laid out sequentially, either horizontally or vertically. A single element (which can itself be a layout panel) contained within a Border simply appears surrounded by a border.

Regardless of the layout mechanism used by the parent panel, the measure-arrange process is still invoked in the same fashion.

To recap, the Measure pass is where the desired size of each element is determined, and the Arrange pass is where each child element's size and position are finalized.

Take a look at the following XAML (don't worry if it doesn't make much sense to you yet; it will as you progress throughout the book). Pay close attention to the order in which the child elements appear and how each element is nested within a parent panel. Figure 5.1 shows how these elements are measured and then arranged to produce a rich display.

```
<Grid x:Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
<Border BorderBrush="AliceBlue" BorderThickness="2">
    <StackPanel>
        <TextBlock Text="Hello"/>
        <TextBlock Text="World"/>
        <StackPanel Orientation="Horizontal">
            <TextBlock Foreground="Yellow" Text="Hello "/>
            <TextBlock Foreground="Yellow" Text=" World"/>
        </StackPanel>
        <Grid>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="150"/>
                <ColumnDefinition Width="200"/>
            </Grid.ColumnDefinitions>
            <Grid.RowDefinitions>
                <RowDefinition Height="150"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
            <Button Grid.Row="0" Grid.Column="0">
                <TextBlock Text="Button"/>
            </Button>
            <Button Grid.Row="0" Grid.Column="1">
                <StackPanel>
                    <TextBlock Text="Other Button"/>
                    <TextBlock Text="hi"/>
                </StackPanel>
            </Button>
        </Grid>
    </StackPanel>
</Border>
</Grid>
```

```
<TextBlock Text="Goodbye World"/>
</StackPanel>
</Border>
</Grid>
```

![](img/04a00d46bb1059867d95707babd62ee7_69_0.png)

Figure 5.1  Nested layout panels.

In the preceding example, the outermost element is a Grid. Inside that Grid, we’ve got a Border. Within that Border is a StackPanel with several child controls, including other StackPanels, another Grid, and a TextBlock. Figure 5.1 shows you how all those nested layout panels are measured and arranged to produce an output. It’s also worth noting that you can set the content of a Button to a StackPanel, which can contain multiple child elements. As you progress throughout this book you’ll see more tricks and incredible things you can do with Silverlight and XAML and controls, but for the purposes of this chapter, the important thing to note here is how the measure-and-arrange process is used on layout panels to produce output in a uniform, predictable fashion.

## Summary

In this chapter I provided a brief introduction to the layout and rendering system used in Silverlight. Deliberately brief, this chapter provides just enough information to get you ready to start building full-featured Silverlight user interfaces. Knowing the recursive, hierarchical nature of Silverlight layout panels will go a long way toward helping you build amazing user interfaces in the future and as you read though this book.

## From Xcode to Visual Studio

> *A tool is usually more simple than a machine; it is generally used with the hand, whilst a machine is frequently moved by animal or steam power.*
> 
> Charles Babbage

This chapter is all about tools. As much as we might like to think otherwise, developers can’t produce applications without the aid of modern tools such as Xcode, Visual Studio, Eclipse, or any number of other IDEs.

This chapter covers the IDE used for developing iOS applications, Xcode, and the IDE used for building Windows Phone 7 applications, Visual Studio.

Developers need to know some basic things about Visual Studio so that they can move around within that environment smoothly and efficiently and write their applications without the tools getting in their way. In addition to a tour of Visual Studio 2010, I also provide a high-level overview of Xcode and its fundamentals.

### Xcode and iOS Application Development

Xcode is the IDE used by developers for building Mac desktop applications as well as iOS applications. It is an incredibly configurable tool, allowing you to change everything from the window layout, whether it does all of its editing in a single window, the colors, and hundreds of other preferences.

The main output of an Xcode project can be found under the Targets folder. When you use Xcode to build an application, that application is a target. Each target is composed of a bunch of source code files, statically linked libraries, and Frameworks that are referenced as part of the project. For example, if you’re going to build an iOS application that uses Core Data for persisting data on the phone, you’ll have to add `CoreData.framework` to the Frameworks configuration of your Xcode project.

## Chapter 6 From Xcode to Visual Studio

To further add power, functionality, and potential confusion for new developers, a single Xcode project can have multiple targets. Indeed, developers create targets for unit testing (I'll mention unit testing again in a later chapter), and a very common scenario is using a single Xcode project to produce different targets for iPhone and iPad. This is because the iPad's UI is so different from the iPhone's (and it includes controls that don't exist on the iPhone). Developers will build different UIs but share the same controller and back-end code within the same Xcode project.

The Xcode UI is much like any other IDE, such as Eclipse, MonoDevelop, or Visual Studio. In the layout (my personal preference) shown in Figure 6.1, the left side of the view is a navigation pane. This pane shows you the main node, the project root. Double-clicking this (called FortuneBuilders in the screenshot because that's the name of the project I was working on at the time) brings up the project settings dialog. Below the project node you have a bunch of folders, some of which are created for you by Xcode. One thing that iOS developers are familiar with is that the folder structure within Xcode does not necessarily match the folder structure on disk. Files sitting in the Classes folder are often sitting in the main project directory alongside the files sitting in the Controllers directory. This often confuses developers familiar with Visual Studio, which actually does have a 1:1 mapping between project folders and disk folders.

![](img/04a00d46bb1059867d95707babd62ee7_72_0.png)

The right side of the window shown in Figure 6.1 is the code editor. At the top of this window there is occasionally a separate navigation pane that I have hidden by using the Shift+Command+E macro. The color scheme is my own personal preference and not the Xcode default. Because developers are often very particular about the syntax highlighting colors in their IDE, I wanted you to see that Xcode can be made to mimic virtually any developer’s favorite colors and fonts.

If you’re curious, the code you’re looking at in that screenshot is from a table view controller that displays a list of YouTube videos that were downloaded by accessing the Google Data feed for a particular YouTube user’s uploaded videos. The code in the screenshot shows some of the code necessary to crack open the Google Data feed information and populate a custom table view cell that was loaded from an Interface Builder file. We’ll talk about Interface Builder and Microsoft’s Design tool, Expression Blend, in the next chapter.

When you want to run your application, you can select the environment in which you want the application to run. You can choose either Debug or Release mode, whether the application will run on the device or in the emulator, and even the particular base SDK under which to run the application. This gives you tremendous flexibility to quickly and easily run your application under all the possible environments you’re planning to support. Figure 6.2 shows what it looks like when you run the application under the iOS 4.0 emulator.

![](img/04a00d46bb1059867d95707babd62ee7_73_0.png)

Figure 6.2 The iOS 4 emulator running an iOS application.
