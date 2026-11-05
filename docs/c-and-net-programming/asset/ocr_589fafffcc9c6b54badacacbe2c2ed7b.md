+   - As with any XML document, one element can be nested inside another. A button element inside a Grid element means a Grid that contains a button inside. However, Nesting is usually a way to express containment.
+   - The properties of each class can be set through attributes.

# ### Programming Example

Create a blank WPF page, visual studio adds up few lines of code by default as shown below,

```
    <Window x:Class="TireControl.Window1"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Window1" Height="300" Width="300">
    <Grid>
    </Grid>
    </Window>
```

+   1. This XAML includes only two elements-the top-level Window element, which represents the entire window, and the Grid, in which all controls will be placed. Although any top-level element can be used, WPF applications rely on just a few, that is,
+      **Window Page (which is similar to Window, but used for navigable applications) and**
+      **Application (which defines application resources and startup settings)**
+   2. In all XML documents, there can only be one top-level element. In the current example, that means as soon as the Window element is closed with the </Window> tag, the document ends. No more content can follow.

# ### 27.1.6 XAML Namespaces

It's not enough to supply just the name of any class being used, the XAML parser also needs to know the .Net namespace where this class is located. As in window can exist in several places, it might refer to system.windows.window class or it could refer to a window class in a third party component. To figure out which class is really required, the XAML parser examines the XML namespace that's applied to the element.

Below code lines declare XAML namespace,

```
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x=http://schemas.microsoft.com/winfx/2006/xaml
```

**XMLNS** - The xmlns attribute is a specialized attribute in XML that is reserved for declaring namespaces. This snippet of markup declares two namespaces that one can find in every WPF XAML document created,

```
    xmlns=http://schemas.microsoft.com/winfx/2006/xaml/presentation ,
```