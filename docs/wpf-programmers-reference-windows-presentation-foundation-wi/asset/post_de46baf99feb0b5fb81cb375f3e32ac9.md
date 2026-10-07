
# Normal Property Values

As the previous examples show, you can make resources that are LinearGradientBrushes, RadialGradientBrushes, and BitmapEffectGroups. You can also make resources that are SolidColorBrushes, Thicknesses (for Margins), DashStyles, Colors (although that is less useful than you might think instead — you probably want a Brush, FontFamilies, FontStyles, and just about any other property type you want to use.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_234_0.png)

These “normal” property values are fairly easy to understand and make good intuitive sense. For example, it seems reasonable that you might want several controls to share the same Background, Margin, or DashStyle.

The examples in the previous section demonstrated this kind of simple property type.

# Controls

Resources often contain “normal” property values but they can also hold controls. For example, the following XAML control defines a TextBox that contains some text in two different styles:

```xml
<TextBlock x:Key="txtName" TextAlignment="Center">
  <Run>Click Me</Run><LineBreak/>
  <Run TextBlock.Foreground="Red"
        TextBlock.FontSize="20"
        TextBlock.FontStyle="Italic"
        TextBlock.FontWeight="Bold">
    PLEASE!
  </Run>
</TextBlock>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_234_1.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_234_2.png)

The ContentResource program uses the following code to set a Button’s Content property to the TextBlock resource so it displays the:

```xml
<Button Width="125" Height="75" Content="{StaticResource txtButton}"/>
```

Figure 12-3 shows

In this example, making the TextBox a resource doesn’t save you much trouble. It requires about the same amount of code that you would use if the Button defined its content and you are unlikely to have lots of buttons with the exact same content, you probably won’t use the resource to save duplication.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_234_3.png)

FIGURE 12-3

This technique is much more useful on the few occasions upon which you do want multiple copies of the same content. For example, suppose an application displays a series of pictures of people and you want to provide each with the same menu context: Details, Email, Phone, and Delete. Deleting the code defines a ContextMenu that includes these commands and a BitmapEffect that drops shadows:

```xml
<Window.Resources>
  <ContextMenu x:Key="ctxPerson">
    <MenuItem Header="Details" Click="mnuDetails_Click"/>
    <MenuItem Header="Email" Click="mnuEmail_Click"/>
    <MenuItem Header="Phone" Click="mnuPhone_Click"/>
    <Separator/>
    <MenuItem Header="Delete" Click="mnuDelete_Click"/>
  </ContextMenu>
  <BitmapEffectGroup x:Key="bmePerson">
    <DropShadowBitmapEffect/>
  </BitmapEffectGroup>
</Window.Resources>
```

The following code shows how an Image can use the resources:

```xml
<Image Name="imgClaude" Width="100" Height="100" Stretch="Uniform"
MouseDown="img_MouseDown"
Source="Claude.jpg" Tag="Claude"
BitmapEffect="{StaticResource bmePerson}"
ContextMenu="{StaticResource ctxPerson}"/> own```

A series of Buttons can use similar code to display the same ContextMenu. 
The program uses code-bind to respond when the user selects a context menu MenuItem.
Unfortunately the Click event handler raised by the MenuItem doesn't know which Image control the user clicked. The MenuItem's parameters tell which MenuItem was clicked but not which Image displayed the Context.

One way to figure out which Image displayed the menu is to save a reference to Image when the menu is displayed. The ContextMenu example program assigns the following event handler to all of its Image controls' MouseDown event handlers. If the user is pressing the right button over the Image, then the code saves a reference to the Image control for use when the user selects a menu item.

```csharp
// Remember the image clicked.
private Image m_ImageClicked = null;
private void img_MouseDown(Object sender, MouseButtonArgs e)
{
  if (e.RightButton == MouseButtonState.Pressed)
  {
    m_ImageClicked = (Image)sender;
  }
}
```

# Resource Types

```csharp
// Display details for the person clicked.
private void mnuDetails_Click(object sender, RoutedEventArgs e)
{
    if (m_ImageClicked != null)
        MessageBox.Show("Display details for " + m_ImageClicked.ToString());
}
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_236_0.png)

ContextMenuResource

Figure 12-4 the ContextMenuResource example displaying its shared ContextMenu.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_236_1.png)

FIGURE 12-4

# Simple Data Types

Ironically, some of the simplest types (such as strings, integers, and doubles) are the most confusing to store in resources until you know the trick. The problem is that a XAML file knows only about XAML types such as SolidColorBrush, not system types as Double and Int32. To make the file understand these types, you need to give it a namespace attribute telling it which namespace to look in for these types. For example, the following XAML shows a Window element. The namespace attribute refers to data types defined in mscorlib.

```xml
<Window xmlns="http://schemas.microsoft.com/winfx/2006/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:sys="clr-namespace:System;assembly=mscorlib"
        x:Class="Window"
        Title="ResourceHierarchy"
        Width="350" Height="180"
        FontSize="16" FontWeight="Bold">
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_236_2.png)

ResourceHierarchy

# RESOURCES

Now the following code defines two resources with the Double type. Notice how the code uses the sys prefix to indicate where the Double type is defined.

```xml
<Window.Resources>
  <sys:Double x:Key="dblRadX">5</sys:Double>
  <sys:Double x:Key="dblRadY">20</sys:Double>
</Window.Resources>
```

The following code shows a Rectangle might use these resources for its RadiusX and RadiusY properties:

```xml
<Rectangle Margin="5" Width="175" Height="60"
Fill="Red" Stroke="Black" StrokeThickness="5"
RadiusX={StaticResource dblRadX}
RadiusY={StaticResource dblRadY}/>
```

These simple data types let you place specific values in resources. For example, you can build a resource dictionary containing all of the strings that your application will use for labels, buttons, and other controls. For different buttons (although you might want a button and a menu item to have the same text), placing these values in resources makes it easier to change them in a central location.

The DataTypes example program in Figure 12-5 displays sample resources for each of the simple types defined in the mscorlib library.

| Byte | Object | Char |
| :--- | :--- | :--- |
| 255 | | |
| Char | SByte | -128 |
| DateTime | 4/1/2010 | Single |
| Decimal | 7.9228168528426378938459803 | String | Any text value |
| Double | 1.797693148623187 | UInt16 | 6553 |
| Int16 | 32767 | UInt32 | 429497295 |
| Int32 | 2147483647 | UInt64 | 1844674403709551615 |
| Int64 | 9223372036854775807 | |

Figure 12-5

> DISCOVERING DATA TYPES
> In Visual Studio, you can use the Object Browser to see what data types are available in various libraries like mscorlib.

You can make more than one resource dictionary containing different values for the same resources and then easily switch between them. The section “Skins” in Chapter 16 has more to say about this technique.

# RESOURCE HIERARCHIES

In a WPF tree, many objects might have resource dictionaries. When a control uses a resource, WPF looks upward through the tree until it finds an object that has been defined with the given name and uses it.

For example, suppose a Window contains a StackPanel that holds a Label and the Label uses a resource named LabelValue. When it builds the Label, WPF first checks the Label's resource dictionary (if it exists) for a resource LabelValue. If it doesn't find one, WPF moves up the tree to the StackPanel and searches its resources. If it still doesn't find a LabelValue resource, WPF continues up to the Window and checks its resources.

If it still hasn't found the LabelValue resource in the Window sitting at the top of the logical tree, WPF checks the XAML file App.xaml to see if it defines the resource.

If after all this WPF can't find the resource, the application fails in several ways. For example, the Expression Blend Window Designer doesn't render the control that needs the resource, and if you try to run the application, it fails. In contrast, Visual Studio's Window Designer displays an error message and doesn't draw any of the controls.

# MATCH TYPES

The resource that WPF finds must have the correct data type. For example, suppose you set a ButtonWidth property to the value in the btnWidth resource. Now suppose the first resource WPF finds btnWidth is a String with the value “Big”. WPF tries to assign the Button's Width property the String Big and has a tantrum.
