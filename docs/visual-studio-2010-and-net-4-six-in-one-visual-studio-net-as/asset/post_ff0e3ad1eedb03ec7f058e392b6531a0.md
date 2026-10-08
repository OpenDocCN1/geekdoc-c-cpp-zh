
![](img/b5597c749e848b27b0d305153ae16106_377_0.png)

Here is the code snippet for the *Focused* state:

```
<VisualState x:Name="Focused">
<Storyboard>
  <DoubleAnimationUsingKeyFrames Storyboard.TargetProperty="Shape.StrokeThickness" Storyboard.TargetName="Ellipse">
<EasingDoubleKeyFrame Time="0" Value="2"/>
</DoubleAnimationUsingKeyFrames>
</Storyboard>
</VisualState>
```

This code snippet simply sets the StrokeThickness property for the Ellipse within the Button to 2, in the Focused state. The properties are set via Storyboards. A Storyboard is an animation feature, so it may seem like an overkill for setting properties, but Storyboards allow for advanced (and, if misused, varying) features — such as pulsating the color of the button within the MouseOver state indefinitely.

The XAML for the MouseOver and Pressed states look pretty similar to the previous one. The difference is that there is a transition for the entire state group:

```xml
<VisualStateGroup.Transitions>
<VisualTransition GeneratedDuration="0:0:0.3"/>
</VisualStateGroup.Transitions>
```

This illustrates that when the properties change within the VisualStateGroup, the change should occur as a smooth linear animation, and last 0.3 seconds. Easings can also be applied to make the transition non-linear, or even bouncy. Visual states can also have more specific transitions. Separate transitions can be defined for entering or exiting a state, or between two specific states.

> Visual states can also be used to represent the states of a user control, or even an entire application.

A Style can also be defined to apply this template to all Buttons. After all, the ControlTemplate is nothing more than a property, and properties can be set from styles:

```xml
<Style TargetType="Button">
  <Setter Property="Template" Value={StaticResource ButtonControlTemplate}/>
</Style>
```

After including this code snippet in the Resources part of an external resource, along with the referenced ButtonControlTemplate resource, the Template attributes of the Buttons can be removed. This style applies for all Buttons, so the look and feel of your application will stay the same, with the additional benefit of new buttons automatically skinned.

# Templates for Data Binding

Templates are cool for re-skinning controls, but where they really shine is data binding. For example, apart from its control template, a ListBox has three templates to define:

- Template: This defines how a ListBox should look.
- ItemsPanel — This defines the layout panel that contains the items.
- ItemContainerStyle — Although it is not strictly a template, the style (and, therefore, the template) of the ListItems can be changed via ItemContainerStyle.

Suppose you want to list the authors from the earlier data binding sample in a nice horizontal ListBox. The code-behind is the same as the Author sample we saw earlier (Listdatabinding)—the only difference is that time will be displayed in a ListBox, so the ItemsSource of the ListBox must be set at the end of the constructor.

```csharp
myListBox.ItemsSource = authors;
```

The XAML is pretty simple so far, as shown in 8-13.

| LISTING 18: DataBindingTemplates.xaml |
| :--- |
| Available for Download at Wrox.com | `<UserControl x:Class="DataBindingTemplates.DataBindingTemplates" xmlns="http://schemas.microsoft.com/winx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winx/2006/xaml" xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.microsoft.com/openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" d:DesignHeight="300" d:DesignWidth="400"><Grid Name="LayoutRoot" Background="White"><ListBox Name="myListBox" Height="88" Margin="8,8,8,0" VerticalAlignment="Top"/></Grid></UserControl>` |

Code file [DataBindingTemplates.xaml] available for download at Wrox.com

However, running the code results in a rather disappointing screen, as shown in Figure 8-21.

What happened? The ListBox had no idea what to display for each Author, so it called (via the ContentPresenter control) the ToString() method for each Author object, and displayed all the results of each other. To display the Authors themselves, the ItemTemplate must be defined. 8-14 shows how one may do to it.

![](img/b5597c749e848b27b0d305153ae16106_379_0.png)

# LISTING 8-14: BindingTemplates.xml

```xml
<UserControl x:Class="TemplateDememos.BindingTemplates"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2006"
xmlns:mc="http://schemas.microsoft.com/openxmlformats/markup-compatibility/2006"
c:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="400">

<Grid Name="LayoutRoot" Background="White">
  <ListBox Name="myListBox" Height="88" Margin="8,8,8,0"
VerticalAlignment="Top"/>
</Grid>
</UserControl>
```

However, running the code results in a rather disappointing screen, as shown in Figure 8-21.

What happened? The ListBox had no idea what to display for each Author, so it called (via the ContentPresenter control) the ToString() method for each Author object, and displayed all the results of each other. To display the Authors themselves, the ItemTemplate must be defined. 8-14 shows how one may do to it.

![](img/b5597c749e848b27b0d305153ae16106_379_1.png)

Code file [BindingTemplates.xaml] available for download at Wrox.com

The items look okay now, but they are still arranged vertically. This is where if nothing is defined, the ListBox uses a VirtualizingPanel to arrange its items. VirtualizingPanel is like a StackPanel, except that it performs better with high-item count by creating the visual tree for those items that are visible in the current scroll window. Redefining the ItemsTemplate, the default VirtualizingPanel can be replaced with any container item — such as a WrapPanel, or even a RadialPanel that arranges the items in a circle. However, for this example, a StackPanel with a horizontal layout will do.

```xml
<UserControl.Resources>
<DataTemplate x:Key="AuthorTemplate">
  <StackPanel Width="100">
    <TextBlock Text="Binding Name" x:Name="tbName" />
    <TextBlock Text="Binding Cycles" TextTrimming="Ellipsis" />
  </StackPanel>
</DataTemplate>
<ItemsPanelTemplate x:Key="ItemsPanelTemplate">
  <StackPanel Orientation="Horizontal"/>
</ItemsPanelTemplate>
</UserControl.Resources>
```

And to reference the newly created ItemsPanelTemplate, the declaration of the ListBox changes to the following:

```xml
<ListBox x:Name="MyListBox" Height="160" Margin="8,8,8,0" VerticalAlignment="Top"
  ItemTemplate={StaticResource AuthorTemplate}
  ItemsPanel={StaticResource ItemsPanelTemplate}">
```

The result. This is where the ItemsContainer style comes into the scene. The default style defines the
VisualStateGroups:

- CommonStates for mouseover and focused/unfocused loop
- FocusStates
- LayoutStates for adding transitions when an item is loaded or unloaded (that is, removed)
- SelectionStates for handling selections

The sample to demonstrate ItemContainerStyle rotates the selected items with a little bounce effect. It is fun, but not something to use in a business application. Listing 8-15 shows the final XAML illustrating ItemTemplate, ItemsPanelTemplate, and ItemContainerStyle.

![](img/b5597c749e848b27b0d305153ae16106_380_0.png)

# LISTING 8-15: DatabindingTemplates.xaml

```xml
<UserControl x:Class="Templateemos.DatabindingTemplates"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
```
