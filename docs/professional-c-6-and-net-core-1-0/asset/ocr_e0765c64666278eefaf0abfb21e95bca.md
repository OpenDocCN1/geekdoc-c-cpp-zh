| Template Type | Description |
|---|---|
| ControlTemplate | Enables you to specify the visual structure of a control and override its look. |
| ItemsPanelTemplate | For an ItemsControl you can specify the layout of its items by assigning an ItemsPanelTemplate. Each ItemsControl has a default ItemsPanelTemplate. For the MenuItem, it is a WrapPanel. The StatusBar uses a DockPanel, and the ListBox uses a VirtualizingStackPanel. |
| DataTemplate | These are very useful for graphical representations of objects. When styling a ListBox, by default the items of the ListBox are shown according to the output of the ToString method. By applying a DataTemplate you can override this behavior and define a custom presentation of the items. |
| HierarchicalDataTemplate | Used for arranging a tree of objects. This control supports HeaderedItemsControls, such as TreeViewItem and MenuItem. This template class is only available with WPF. |

> **NOTE** *The HierarchicalDataTemplate is discussed with the TreeControl in Chapter 34, “Windows Desktop Applications with WPF.”*

# Control Templates

Previously in this chapter you’ve seen how you can style the properties of a control. If setting simple properties of the controls doesn’t give you the look you want, you can change the Template property. With the Template property, you can customize the complete look of the control. The next example demonstrates customizing buttons, and later in the chapter list views are customized step by step so you can see the intermediate results of the changes.

You customize the Button type in a separate resource dictionary file: ControlTemplates.xaml. Here, a style with the key name RoundedGelButton is defined. The style RoundedGelButton sets the properties Background, Height, Foreground, and Margin, and the Template. The Template is the most interesting aspect with this style. The Template specifies a Grid with just one row and one column.

Inside this cell, you can find an ellipse with the name GelBackground. This ellipse has a linear gradient brush for the stroke. The stroke that surrounds the rectangle is very thin because the StrokeThickness is set