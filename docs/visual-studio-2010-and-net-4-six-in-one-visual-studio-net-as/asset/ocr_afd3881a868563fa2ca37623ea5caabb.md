# LISTING 5-2 (continued)

```
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.xmlformats.org/markup-compatibility/2006"
d:DesignWidth="600"
d:DesignWidth="800">

<Grid.Resources>
  <ResourceDictionary>
    <MergedDictionaries>
      <ResourceDictionary Source="Microsoft.VisualStudio.Shell.StartPage;component=Styles/startpageresources.xaml" />
    </MergedDictionaries>
  </ResourceDictionary>
</Grid.Resources>
n<Grid x:Name="LayoutRoot"
Background="DynamicResource {x:Static vs:Brushes.StartPageBackgroundColor}"
Style="DynamicResource StartPage.OuterGridStyle">
  <!-- Grid omitted -->
</Grid>
</Grid>
```

*Code file [StartPage.xml] available for download at Wrox.com*

The most eye-catching thing in this list is its root element is a Grid and not a Window, Page, or a UserControl. This Grid is a container holding the resources and defining the layout of the Start. As you can see from the attributes of the Grid tag, it defines xmlns for a namespaces used by the referenced assemblies summarized in Table 5-4, and also a tag for the SimpleStartPageControl assembly.

The Start Page uses resources in a resource assembly of Visual Studio. The <Grid.Resources> element make them available for the page.
The Nested Grid with the LayoutRoot defines the content of the Start Page. Visual Studio nests this UIElement into the Start Page. You can see how the StartPageBackgroundColor property of the VsBrushes (defined in the Microsoft.VisualStudio.Shell.10.0 assembly) is used to set up the background of the grid.

![](bbox=[0.12, 0.755, 0.803, 0.828])

The LayoutRoot grid contains more than 200 lines defining the UI of the page. It is worth taking a look at a few details of this XAML code, because this will help you understand how the Start Page is composed.