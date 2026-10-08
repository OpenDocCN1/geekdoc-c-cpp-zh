
controls are wrapped to the next column when there are more controls than will display in the available space.

Figure 17.3 shows an example of using a DockPanel. The XAML for this layout is shown in Listing 17.4.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_388_0.png)

## LISTING 17.4 XAML Creating a Layout Using DockPanel

```xml
<Window x:Class="WpfApplication1.Layouts"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Layouts" Height="182" Width="272">
    <Grid>
        <DockPanel>
            <Border DockPanel.Dock="Top" BorderThickness="1" BorderBrush="Black">
                <TextBlock Height="35">Dock = "Top"</TextBlock>
            </Border>
            <Border DockPanel.Dock="Bottom" BorderThickness="1" BorderBrush="Black">
                <TextBlock Height="31" >Dock = "Bottom"</TextBlock>
            </Border>
            <Border DockPanel.Dock="Left" BorderThickness="1" BorderBrush="Black">
                <TextBlock Width="93">Dock = "Left"</TextBlock>
            </Border>
            <Border BorderThickness="1" BorderBrush="Black">
                <TextBlock>Fill</TextBlock>
            </Border>
        </DockPanel>
    </Grid>
</Window>
```

Like all WPF elements, layouts can be nested inside each other, allowing you to create complex layouts.

## Using Graphics, Animation, and Media

WPF provides a flexible and rich graphics environment featuring resolution- and device-independent graphics, improved precision, advanced graphics and animation support, and support for hardware acceleration. All graphics measurements in WPF use pixels (1/96th of an inch), no matter what the actual screen resolution might be.

WPF provides support for

- 2-D shapes, like rectangles and ellipses
- 2-D geometries to create custom shapes
- 2-D effects, such as gradients, painting with videos, rotation, and scaling
- 3-D rendering, which integrates with 2-D graphics enabling you to show 2-D images rendered onto 3-D shapes

In addition to the 2-D and 3-D graphics capabilities, WPF also provides animation support. This enables you to make controls grow, shake, spin, or fade, creating unique and interesting transition effects.

WPF directly supports using media, such as images, video, and audio, to convey information. Many controls, including an Image control, implicitly know how to display images. Audio and video are both supported through the MediaElement control, which is powerful enough to be the basis for a custom media player.

## Understanding Text, Typography, and Documents

High-quality text rendering and manipulation is supported through OpenType font support and ClearType enhancements. WPF also has intrinsic support for working with flow documents, fixed documents, and XML Paper Specification (XPS) documents.

Flow documents optimize viewing and readability by dynamically reflowing content as the window size and display settings change. Fixed documents can be used when a precise presentation is required, such as in desktop publishing applications. XPS is an open, cross-platform document format, and support for XPS documents in WPF is built on the support for fixed documents.

## Data Binding

Data binding in WPF is handled through a sophisticated and flexible binding engine that enables you to bind a control (the target) to data (the source). This binding engine provides a simple and consistent way to present and interact with data. Many controls have built-in support for displaying single data items or collections of data items, and controls can be bound to a variety of data sources, including .NET objects and XML. The data binding support in WPF is so powerful that many things that were previously only possible in code are now possible directly in XAML.

# Creating a WPF Application

In the rest of this hour, you start creating a photo viewer application by creating a new project, laying out the form, and adding controls.

First, create a new WPF Application project using the New Project dialog, as shown in Figure 17.4. In the Name field, enter **PhotoViewer**.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_390_0.png)

Just as it does with Console applications, Visual Studio creates a solution and project for you. This time, instead of displaying the generated *C#* class file, Visual Studio displays the visual designer for the application's main window, the Controls toolbox, and the Properties window. Figure 17.5 shows what Visual Studio should look like after having just created the project.

The visual designer for XAML-based user interfaces is split into two sections. By default, the top half shows the visual representation of the layout and the bottom half shows the XAML. You can make changes in both portions, and changes made in one will be reflected in the other. Figure 17.6 shows a more detailed view of the XAML designer.

You can easily switch between the XAML and Design panes, including swapping them, using the tabs and the Swap Panes button (shown circled), as shown in Figure 17.7.

You can also change the orientation of the panes, switching between a horizontal (which is the default) or vertical layout, and collapse the XAML pane entirely using the buttons on the right side of the Design and XAML tabs, as shown in Figure 17.8.

At the bottom of the editing window is the selected element outline, as shown in Figure 17.9. This shows you visually what element you have selected (shown in bold) and the path of visual elements that contain the currently selected element.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_391_0.png)

**FIGURE 17.5**
Visual Studio after creating a WPF application

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_391_1.png)

**FIGURE 17.6**
Detailed view of the XAML editing surface

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_391_2.png)

**FIGURE 17.7**
Design and XAML tabs

# HOUR 17: Building a Windows Application

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_392_0.png)

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_392_1.png)

The button on the far left displays a tree-oriented view, called the document outline, showing all the visual elements in the window and their relationships to each other (see Figure 17.10). In this example, the document outline is not interesting because the window has no other elements. However, when you start adding controls and creating complex layouts, the document outline and selected element outline both become helpful for navigating through your layout.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_392_2.png)

If you look at the XML generated by Visual Studio, the `x:Class` attribute specifies the fully qualified name of the class that implements the window. In this case, the class is **MainWindow** in the **PhotoViewer** namespace. The window **Title**, **Width**, and **Height** are also specified. These can be changed directly in the XML or using the Properties window, as shown in Figure 17.11.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_392_3.png)

The `xml:ns` namespace attributes define the schemas used by WPF. These schemas include definitions for all the controls and other items you can incorporate into a WPF application.

Change the window title to be **WPF Photo Viewer**, either through the Properties window or directly in the XAML.

## Creating the Layout

You are now ready to start creating the layout for the photo viewer application. If you look at the XAML again, you notice that the `Window` already includes a child element named `Grid`. In this case, the `Grid` doesn't explicitly define any rows or columns, so it is a 1x1 table. For the photo viewer application, you need a grid structure containing two rows and two columns.

If you click on the large area of whitespace in the Design tab, click on the blank line between the `Grid` element in the XAML, or click the `Grid` in the document outline, the `Grid` becomes the selected element. You can visually design the table structure using the mouse by moving the mouse cursor over the blue-shaded edge of the grid in the Design pane. This displays a light blue guideline across the grid showing where the row or column will be created. When the guideline is in the correct place, you can click the left mouse button to create the row or column. An example of what this would look like is shown in Figure 17.12.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_393_0.png)

You can also edit the structure using the `ColumnDefinitions` and `RowDefinitions` properties of the `Grid` through the Properties window, as shown in Figure 17.13.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_393_1.png)

This displays a Collection Editor dialog, shown in Figure 17.14, enabling you to easily add rows and columns and configure their properties at the same time. Using the collection editor is generally the easiest, particularly if you are adding a lot of rows or columns. In fact, if you need to change anything about an existing row or column you must do so using either the Collection Editor or directly in the XAML.
