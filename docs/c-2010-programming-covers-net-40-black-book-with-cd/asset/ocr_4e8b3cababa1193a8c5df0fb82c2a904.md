# Table 10.35: Showing the Noteworthy Properties of the ComboBox Class

| Property | Description |
|---|---|
| SelectionBoxItemTemplate | Retrieves the item template of the selection box content |
| StaysOpenOnEdit | Determines whether the ComboBox control continues to display the drop-down list of items at the time of editing the item |
| Text | Gets or sets the text of the currently selected item |

Figure 10.26 shows the ComboBox control added to a WPF application:

![](bbox=[0.22, 0.23, 0.8, 0.52])

Figure 10.26: Showing the ComboBox Control

# The ListView Control

The ListView control in WPF provides the infrastructure to display a set of data items in different layouts or views. For example, you can display items in the table format instead of a paragraph and sort the items by using the ListView control. The ListView control is derived from the ListBox control and the members of a data collection are represented as ListViewItem objects. You can use the Items and ItemsSource properties to specify items for the ListView control.

The inheritance hierarchy of the ListView class is as follows:

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.Control
              System.Windows.Controls.ItemsControl
                System.Windows.Controls.Primitives.Selector
                  System.Windows.Controls.ListBox
                    System.Windows.Controls.ListView
```

You can add the ListView control to your application by adding the following code snippet:

```
<ListView>
  <!--Items -->
</ListView>
```

Table 10.36 describes the noteworthy property of the ListView class: