
these styles to the controls on the Customers form.

## Define styles for the Customers form

- 1. In Solution Explorer, right-click the Customers project, point to Add, and then click New Item.
- 2. In the Add New Item – Customers dialog box, click Resource Dictionary. In the Name box, type AppStyles.xaml, and then click Add.
- 3. In Solution Explorer, right-click the Customers project, point to Add, and then click New Folder. Change the name of the new folder to Images.
- 4. Right-click the Images folder, point to Add, and then click Existing Item.
- 5. In the Add Existing Item – Customers dialog box, browse to the \Microsoft Press\VCSBS\Chapter 25\Resources folder in your Documents folder, click wood.jpg, and then click Add.
- 6. In the Code and Text Editor window displaying the AppStyles.xaml file, add the following XAML markup shown in bold:

The AppStyles.xaml file appears in the Code and Text Editor window. A resource dictionary is a XAML file that contains resources that the app can use. The AppStyles.xaml file looks like this:

Click here to view code image

```
<ResourceDictionary
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Customers">

</ResourceDictionary>
```

Styles are one example of a resource, but you can also add other items. In fact, the first resource that you will add is not actually a style but an ImageBrush that will be used to paint the background of the outermost Grid control on the Customers form.

The wood.jpg file is added to the Images folder in the Customers project. This file contains an image of a tasteful wooden background that you will use for the Customers form.

Click here to view code image

```
<ResourceDictionary
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Customers">

    <ImageBrush x:Key="WoodBrush" ImageSource="Images/wood.jpg"/>
</ResourceDictionary>
```

This markup creates an ImageBrush resource called WoodBrush that is

based on the wood.jpg file. You can use this image brush to set the background of a control, and it will display the image in the wood.jpg file.

## 7. Underneath the ImageBrush resource, add the following style shown in bold to the AppStyles.xaml file:

Click here to view code image

```
<ResourceDictionary
    ...>

    <ImageBrush x:Key="WoodBrush" ImageSource="Images/wood.jpg"/>
    <Style x:Key="GridStyle" TargetType="Grid">
        <Setter Property="Background" Value="{StaticResource WoodBrush}"/>
    </Style>
</ResourceDictionary>
```

This markup shows how to define a style. A Style element should have a name (a key that enables it to be referenced elsewhere in the app), and it should specify the type of control to which the style can be applied. You are going to use this style with the Grid control.

The body of a style consists of one or more Setter elements. In this example, the Background property is set to the WoodBrush ImageBrush resource. The syntax is a little curious, though. In a value, you can either reference one of the appropriate system-defined values for the property (such as “Red” if you want to set the background to a solid red color) or specify a resource that you have defined elsewhere. To reference a resource defined elsewhere, you use the StaticResource keyword and then place the entire expression in curly braces.

## 8. Before you can use this style, you must update the global resource dictionary for the app in the App.xaml file by adding a reference to the AppStyles.xaml file. In Solution Explorer, double-click App.xaml to display it in the Code and Text Editor window. The App.xaml file looks like this:

Click here to view code image

```
<Application
    x:Class="Customers.App"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Customers"
    RequestedTheme="Light">

</Application>
```

Currently, the App.xaml file defines only the app object and brings a few namespaces into scope; the global resource dictionary is empty.

## 9. Add to the App.xaml file the code shown here in bold:

Click here to view code image

```
<Application
    x:Class="Customers.App"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Customers"
    RequestedTheme="Light">
    <Application.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <ResourceDictionary Source="AppStyles.xaml"/>
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

This markup adds the resources defined in the AppStyles.xaml file to the list of resources available in the global resource dictionary. These resources are now available for use throughout the app.

10. Switch to the MainPage.xaml file displaying the UI for the Customers form.

In the XAML pane, find the outermost Grid control:

Click here to view code image

```
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
```

In the XAML markup for this control, replace the Background property with a Style property that references the GridStyle style, as shown in bold in the following code:

Click here to view code image

```
<Grid Style="{StaticResource GridStyle}">
```

The background of the Grid control in the Design View window should switch and display a wooden panel, like this:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_751_0.png)

### Note

Ideally, you should ensure that any background image that you apply to a page or control maintains its aesthetics as the device form factor and orientation change. An image that looks cool on a 30-inch monitor might appear distorted and squashed on a Windows phone. It might be necessary to provide alternative backgrounds for different views and orientations and use the Visual State Manager to modify the Background property of a control to switch between them as the visual state changes.

11. Return to AppStyles.xaml in the Code and Text Editor window and add the following FontStyle style after the GridStyle style:

Click here to view code image

```
<Style x:Key="GridStyle" TargetType="Grid">
...
</Style>
<Style x:Key="FontStyle" TargetType="TextBlock">
    <Setter Property="FontFamily" Value="Segoe Print"/>
</Style>
```

This style applies to TextBlock elements and changes the font to Segoe Print. This font resembles a handwriting style.

At this stage, it would be possible to reference the FontStyle style in every TextBlock control that required this font, but this approach would not provide any advantage over simply setting the FontFamily directly in the markup for each control. The real power of styles occurs when you combine multiple properties, as you will see in the next few steps.

Click here to view code image

```
Add the HeaderStyle style shown here to the AppStyles.xaml file:
<Style x:Key="FontStyle"
TargetType="TextBlock">
...
</Style>
<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn="{StaticResource FontStyle}">
    <Setter Property="HorizontalAlignment" Value="Center"/>
    <Setter Property="TextWrapping" Value="Wrap"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="Foreground" Value="SteelBlue"/>
</Style>
```

This is a composite style that sets the HorizontalAlignment, TextWrapping, VerticalAlignment, and Foreground properties of a TextBlock. Additionally, the HeaderStyle style references the FontStyle style by using the BasedOn property. The BasedOn property provides a simple form of inheritance for styles.

You will use this style to format the labels that appear at the top of the customersTabularView and customersColumnarView controls. However, these headings have different font sizes (the heading for the tabular layout is bigger than that of the columnar layout), so you will create two more styles that extend the HeaderStyle style.

## 12. Add the following styles to the AppStyles.xaml file:

Click here to view code image

```
<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn="{StaticResource FontStyle}">
...
</Style>
<Style x:Key="TabularHeaderStyle" TargetType="TextBlock"
BasedOn="{StaticResource HeaderStyle}">
    <Setter Property="FontSize" Value="40"/>
</Style>

<Style x:Key="ColumnarHeaderStyle" TargetType="TextBlock"
BasedOn="{StaticResource HeaderStyle}">
    <Setter Property="FontSize" Value="30"/>
</Style>
```

Note that the font sizes for these styles are slightly smaller than the font sizes currently used by the headings in the Grid controls. This is because
