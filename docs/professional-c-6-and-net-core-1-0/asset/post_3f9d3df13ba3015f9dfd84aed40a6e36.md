
Dictionary1.xaml defines two resources: LinearGradientBrush with the CyanGradientBrush key, and a style for a Button that can be referenced with the PinkButtonStyle key (code file download ResourcesLib[WPF|UWP]/Dictionary1.xaml):

```
<ResourceDictionary
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
    <LinearGradientBrush x:Key="CyanGradientBrush" StartPoint="0,0" EndPoint="0.3,1">
        <LinearGradientBrush.GradientStops>
            <GradientStop Offset="0.0" Color="LightCyan" />
            <GradientStop Offset="0.14" Color="Cyan" />
            <GradientStop Offset="0.7" Color="DarkCyan" />
        </LinearGradientBrush.GradientStops>
    </LinearGradientBrush>

    <Style x:Key="PinkButtonStyle" TargetType="Button">
        <Setter Property="FontSize" Value="22" />
        <Setter Property="Foreground" Value="White" />
        <Setter Property="Background">
            <Setter.Value>
                <LinearGradientBrush StartPoint="0,0" EndPoint="0,1">
                    <LinearGradientBrush.GradientStops>
                        <GradientStop Offset="0.0" Color="Pink" />
                        <GradientStop Offset="0.3" Color="DeepPink" />
                        <GradientStop Offset="0.9" Color="DarkOrchid" />
                    </LinearGradientBrush.GradientStops>
                </LinearGradientBrush>
            </Setter.Value>
        </Setter>
    </Style>
</ResourceDictionary>
```

With the target project, the library needs to be referenced, and the resource dictionary needs to be added to the dictionaries. You can use multiple resource dictionary files that you can add by using the MergedDictionaries property of the ResourceDictionary. You can add a list of resource dictionaries to the merged dictionaries.

How the reference to the library is handled is different between WPF and UWP apps. With WPF, the pack URI syntax is used. The pack URI can be assigned as absolute, which means the URI begins with pack://, or as relative, as it is used in this example. With relative syntax, the referenced assembly ResourceLibWPF, which includes the dictionary, is first after the / followed by ;component. Component means that the dictionary is included as a resource in the assembly. After that, you add the name of the dictionary file Dictionary1.xaml. If the dictionary is added into a subfolder, the folder name must be declared as well (code file StylesAndResourcesWPF/App.xaml):

```
<Application x:Class="StylesAndResourcesWPF.App"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
```

background and dark foreground, and for the dark theme a dark background and light foreground. The key for the style is the same within both dictionaries: SampleButtonStyle (code file StylesAndResourcesUWP/Styles/SampleThemes.xaml):

```
<ResourceDictionary
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:local="using:StylesAndResourcesUWP">
<ResourceDictionary.ThemeDictionaries>
<ResourceDictionary x:Key="Light">
<Style TargetType="Button" x:Key="SampleButtonStyle">
<Setter Property="Background" Value="LightGray" />
<Setter Property="Foreground" Value="Black" />
</Style>
</ResourceDictionary>
<ResourceDictionary x:Key="Dark">
<Style TargetType="Button" x:Key="SampleButtonStyle">
<Setter Property="Background" Value="Black" />
<Setter Property="Foreground" Value="White" />
</Style>
</ResourceDictionary>
</ResourceDictionary.ThemeDictionaries>
</ResourceDictionary>
```

You can assign the style using the ThemeResource markup extension. Other than using a different markup extension, everything else is the same as with the StaticResource markup extension (code file StylesAndResourcesUWP/ThemeDemoPage.xaml):

```
<Button Style="{ThemeResource SampleButtonStyle}" Click="OnChangeTheme" Content="Change Theme" />
```

Depending on the theme that is selected, the corresponding style will be used.

## Selecting a Theme

There are different ways to select a theme. First, there’s a default for the app itself. The RequestedTheme property of the Application class defines the default theme of the app. This is defined within App.xaml, which is the place where the themes dictionary file is referenced as well (code file StylesAndResourcesUWP/App.xaml):

```
<Application
x:Class="StylesAndResourcesUWP.App"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:local="using:StylesAndResourcesUWP"
RequestedTheme="Light">
<Application.Resources>
<ResourceDictionary>
<ResourceDictionary.MergedDictionaries>
<ResourceDictionary Source="ms-appx:///StylesLib/Dictionary1.xaml" />
```

```
<ResourceDictionary Source="Styles/SampleThemes.xaml" />
</ResourceDictionary.MergedDictionaries>
</ResourceDictionary>
</Application.Resources>
</Application>
```

The RequestedTheme property is defined in the XAML element hierarchy. Every element can override the theme to be used for itself and its children. The following Grid element changes the default theme for the Dark theme. This is now the theme used for the Grid and all its children elements (code file StylesAndResourcesUWP/ThemeDemoPage.xaml):

```
<Grid x:Name="grid1"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}"
    RequestedTheme="Dark">
    <Button Style="{ThemeResource SampleButtonStyle}"
Click="OnChangeTheme"
        Content="Change Theme" />
</Grid>
```

You can also dynamically change the theme by setting the RequestedTheme property from code (code file StylesAndResourcesUWP/ThemeDemoPage.xaml.cs):

```
private void OnChangeTheme(object sender, RoutedEventArgs e)
{
    grid1.RequestedTheme = grid1.RequestedTheme ==
ElementTheme.Dark ?
        ElementTheme.Light: ElementTheme.Dark;
}
```

> NOTE Using the ThemeResource markup extension is useful only in cases where the resource should look different based on the theme. If the resource should look the same, with all themes, keep using the StaticResource markup extension.

## Templates

An XAML Button control can contain any content. The content can be simple text, but you can also add a Canvas element, which can contain shapes; a Grid; or a video. In fact, you can do even more than that with a button! With template-based XAML controls, the functionality of controls is completely separate from their look and feel. A button has a default look, but you can completely customize that look.

WPF and UWP apps provide several template types that derive from the base class FrameworkTemplate.

| Template Type | Description |
|---|---|
| ControlTemplate | Enables you to specify the visual structure of a control and override its look. |
| ItemsPanelTemplate | For an ItemsControl you can specify the layout of its items by assigning an ItemsPanelTemplate. Each ItemsControl has a default ItemsPanelTemplate. For the MenuItem, it is a WrapPanel. The StatusBar uses a DockPanel, and the ListBox uses a VirtualizingStackPanel. |
| DataTemplate | These are very useful for graphical representations of objects. When styling a ListBox, by default the items of the ListBox are shown according to the output of the ToString method. By applying a DataTemplate you can override this behavior and define a custom presentation of the items. |
| HierarchicalDataTemplate | Used for arranging a tree of objects. This control supports HeaderedItemsControls, such as TreeViewItem and MenuItem. This template class is only available with WPF. |

> **NOTE** *The HierarchicalDataTemplate is discussed with the TreeControl in Chapter 34, “Windows Desktop Applications with WPF.”*

## Control Templates

Previously in this chapter you’ve seen how you can style the properties of a control. If setting simple properties of the controls doesn’t give you the look you want, you can change the Template property. With the Template property, you can customize the complete look of the control. The next example demonstrates customizing buttons, and later in the chapter list views are customized step by step so you can see the intermediate results of the changes.

You customize the Button type in a separate resource dictionary file: ControlTemplates.xaml. Here, a style with the key name RoundedGelButton is defined. The style RoundedGelButton sets the properties Background, Height, Foreground, and Margin, and the Template. The Template is the most interesting aspect with this style. The Template specifies a Grid with just one row and one column.

Inside this cell, you can find an ellipse with the name GelBackground. This ellipse has a linear gradient brush for the stroke. The stroke that surrounds the rectangle is very thin because the StrokeThickness is set
