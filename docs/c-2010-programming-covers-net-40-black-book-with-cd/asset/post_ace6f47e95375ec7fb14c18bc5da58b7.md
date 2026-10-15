
Now that you have provided all the codes to create and raise the OnMouseHover routed event, you need to use the Frame class and associate a handler for the OnMouseHover event. You can do so by adding the following code snippet in the MainWindow class of the FrameRoutedEvent applications:

```
public void Frame_MouseHover(object sender, RoutedEventArgs e) {
    MessageBox.Show("MouseHover event of Frame handled");
}
```

In the preceding code snippet, a method named Frame_MouseHover() is defined to take two arguments of type object and RoutedEventArgs.

Now, let’s use the Frame class and associate the Frame_MouseHover() method as the handler for the OnMouseHover event in the XAML code.

+   3. Add the code given in Listing 9.13 in the MainWindow.xaml file to use the Frame class:

# Listing 9.13: Associating the Handler for the OnMouseHover Event of the Frame Class

```
<window x:Class="FrameRoutedEvent.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="350" Width="552" xmlns:my="clr-namespace:FrameRoutedEvent">
<Grid>
<Grid.RowDefinitions>
<RowDefinition Height="50*"/>
<RowDefinition Height="50*"/>
</Grid.RowDefinitions>
<my:Frame OnMouseHover="Frame_MouseHover" Grid.Row="0">
<my:Button Name="button1" Height="25" Width="75" Content="InsideFrame"/>
</my:Frame>
<Button Name="button2" Height="25" Width="100" Grid.Row="1" Content="OutsideFrame"/>
</Grid>
</window>
```

In Listing 9.13, the Window element has a reference to the FrameRoutedEvent namespace as it contains the Frame class that is used in the XAML code. The Grid element has two rows of equal height and the Frame element that is prefixed with my. The Frame element appears in the first row of the Grid element and associates the Frame_MouseHover() method with the OnMouseHover routed event. Furthermore, the Frame element has a Button element named button1. This implies that whenever you hover or move the mouse over button1, the OnMouseHover event is raised and handled. There is another Button element named button2 that exists outside the Frame element in the second row of the grid. Note that for button2, the OnMouseHover event is not available.

+   4. Run the FrameRoutedEvent application by pressing F5. At run time, if you move the mouse over button1, a message box appears, as shown in Figure 9.46:

![](img/e073a4882197be4ab61103cbe0bcb394_406_0.png)

Figure 9.46: Handling the OnMouseHover Routed Event of the Frame Class

Now, let’s summarize the main topics discussed in this chapter.

## Summary

In this chapter, you have learned about the fundamentals of WPF in detail. Further, you have also learned about the new features, architecture, class hierarchy, and application model of WPF 4.0. This chapter also covered the basic features of the WPF 4.0 designer and XAML elements used in WPF 4.0. Furthermore, you learned about dependency and attached properties as well as routed and attached events. Finally, we have discussed about dialog boxes and the compilation and execution of WPF applications.

In the next chapter, you learn how to work with the controls, resources, styles, templates, and commands in WPF 4.0.

## 10

## Working with WPF 4.0
Controls, Resources, Styles,
Templates, and Commands

| If you need an Immediate Solution to: | See page: |
|---|---|
| Using WPF Controls | 424 |
| Using the Resources, Styles, and Templates | 437 |
| Using Triggers | 446 |
| Using WPF Commands with Controls | 449 |
| Hosting a Windows Forms Controls in a WPF Application | 450 |
| Hosting a WPF Control in a Windows Forms Application | 451 |

## In Depth

Windows Presentation Foundation (WPF) helps you to separate the design view from the code view; thereby, allowing you to work with one view at a time. Your code can be directly viewed in the design view because WPF is based on what you see is what you get (WYSIWYG) principle. An application in WPF is designed with the help of Extensible Application Markup Language (XAML). This language also defines the hierarchical structure of the controls in a WPF application. You can use XAML to add controls and equip them with additional functionalities. Programming in WPF is very similar to programming in Windows Forms. The only difference between the two is the existence of the WPF design view. The controls in WPF are user-interactive elements and are derived from the System.Windows.Control, Microsoft.Win32, and System.Windows.Document namespaces.

This chapter describes the controls and functions performed in WPF. You also learn about styles, templates, and resources used in WPF. In addition, the chapter discusses triggers, which are needed for the controls to respond to commands.

## WPF 4.0 Controls

WPF has a rich set of controls in which some of the controls are similar to Windows Forms controls. The controls of Windows Forms and WPF applications differ in their look and behavior. You can modify the look of a WPF control by using the XAML code. As you change the XAML code of a control in the XAML view, the look and behavior of the WPF control is automatically changed in the Design view. In a WPF application, the XAML code for the controls is displayed in a tree view. The working of the controls in WPF depends on two base classes, the FrameworkElement and Control classes. The Control class is a public base class derived from the FrameworkElement class.

WPF offers several controls to work with, such as the Grid, TextBox, and RichTextBox controls. Each control in WPF is classified under one of the following categories:

- Container controls
- Simple controls
- Content controls
- Headered content controls
- Items controls
- Headered items controls
- Miscellaneous controls

Let’s look at these categories in detail in the following sections.

## Container Controls

Container controls in WPF include the Grid, UniformGrid, Canvas, DockPanel, StackPanel, and WrapPanel controls. These controls provide built-in layout functionality for child controls. Child controls are controls that are placed inside a container control. For example, a Label control used in a Grid control is the child control of the Grid control. Container controls handle the layout and positioning of child controls.

## The Grid Control

The most common container control is the Grid control. Whenever you add a new window to a WPF application, by default the window automatically includes a Grid control. A Grid control consists of a single cell. You can add additional rows and columns inside the Grid control. The child elements in the Grid control are arranged in columns and rows in the display area. A Grid control can also contain another Grid control as its child element.

The Grid control is represented by the Grid class, which is derived from the Panel class. The inheritance hierarchy of the Grid class is as follows:

```
System.Object
    System.Windows.Threading.DispatcherObject
        System.Windows.DependencyObject
            System.Windows.Media.Visual
                System.Windows.UIElement
                    System.Windows.FrameworkElement
                        System.Windows.Controls.Panel
                            System.Windows.Controls.Grid
```

You can add a Grid control to a WPF application by using the following code snippet:

```
<Grid>
    <!--Child elements-->
</Grid>
```

Table 10.1 describes the noteworthy properties of the Grid class:

| Table 10.1: Showing the Noteworthy Properties of the Grid Class |
| Property | Description |
| ColumnDefinitions | Retrieves a ColumnDefinitionCollection class defined in the Grid control. The ColumnDefinitionCollection class provides access to an ordered collection of columns in the Grid control. |
| RowDefinitions | Retrieves a RowDefinitionCollection class that provides access to an ordered collection of rows in the Grid control. |
| ShowGridLines | Retrieves or specifies a value that indicates the visibility of the grid lines within the Grid control. |

Along with the properties listed in Table 10.1, there are some attached properties of the Grid class. The attached properties in XAML refer to the global properties that can be set on any object.

The attached properties of the Grid class are listed in Table 10.2:

| Table 10.2: Showing the Attached Properties of the Grid Class |
| Property | Description |
| Column | Retrieves or specifies a value to display a specific child content in a particular column within a Grid control |
| ColumnSpan | Retrieves or specifies a value that shows the total number of columns that the child content spans within a Grid control |
| IsSharedSizeScope | Retrieves or specifies a value that shows that multiple Grid elements can share the size information with another Grid elements |
| Row | Retrieves or specifies a value that shows which content should appear in which row within a Grid control |
| RowSpan | Determines how many rows a child content spans within a Grid control |

The Grid control is added to a WPF application by default.

Figure 10.1 shows the default view of a WPF application with the Grid control added to it:
