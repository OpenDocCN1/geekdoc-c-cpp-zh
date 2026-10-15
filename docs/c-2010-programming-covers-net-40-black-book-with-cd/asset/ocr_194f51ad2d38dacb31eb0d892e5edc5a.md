In addition to the exhaustive range of properties to manipulate the look and feel of the controls, the Control class offers a control template for the same tasks. Control templates (instances of the ControlTemplate class) define the look, appearance, and behavior of the respective controls. You can create or modify control templates to suitably change the appearance of the controls.

# The System.Windows.Controls.Panel Class

In WPF 4.0, all the controls that you work with have to be enclosed in a panel, which is a container control that holds other controls as well. A panel allows you to adjust the layout and dimensions of the controls that the panel contains. All the panels are derived from the System.Windows.Controls.Panel class. Some of the panels that inherit the Panel class include Grid, Canvas, and StackPanel.

You can use a particular panel based on your requirements. For example, you can use the Grid panel to arrange the child controls in the form of a grid or the StackPanel panel to position the child controls horizontally or vertically in a straight line. The panels inherit the various properties of the Panel class to allow you to alter the arrangement of the containing or child controls. The properties assist you to change the height and width of the child controls, appropriately align the controls, and position the controls in a layered manner.

> NOTE
> To know more about the controls and panels, refer to Chapter 10, Working with WPF 4.0 Controls, Resources, Styles, Templates, and Commands.

# The System.Windows.Shapes.Shape Class

WPF 4.0 offers extensive support for 2-D graphics to develop WPF applications. One of the frequently used 2-D graphics elements in WPF applications is shape. In WPF 4.0, shapes are derived from the System.Windows.Shapes.Shape class. The Shape class has several derived classes, such as Ellipse, Line, Rectangle, and Polygon, to draw and manipulate different shapes in WPF applications. You can use the properties of the Shape class to perform activities, such as filling the shapes with different colors, adding an outline or border to the shapes, and stretching the shapes. You learn more about shapes in Chapter 12, Using Graphics and Multimedia in Windows Forms and WPF.

# The System.Windows.ContentElement Class

The System.Windows.ContentElement class exists in the PresentationCore assembly and offers some of the core-level functionalities to work with the content of WPF applications. It is responsible for the style and presentation of the content. It also offers features, such as input from mouse and keyboard, focusable elements, and events to indicate various changes in the flow content. In addition, it provides several properties, methods, and events to work with animations and textual content.

Let’s now move on to learn about the application model in WPF 4.0.

# WPF 4.0 Application Model

The application model of a WPF 4.0 provides the essential classes that assist you in collating the different files and resources to develop WPF 4.0 applications. In this topic, you learn about different types of WPF applications supported by Visual Studio 2010. You also learn about the Application class, which is one of the most fundamental classes in WPF 4.0.

# Types of WPF Applications

The types of WPF 4.0 applications supported by Visual Studio 2010 are as follows:

+   - Standalone WPF Applications
+   - XBAP