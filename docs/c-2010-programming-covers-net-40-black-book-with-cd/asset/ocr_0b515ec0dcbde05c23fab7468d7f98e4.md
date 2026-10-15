```
System.Object
    System.Windows.Threading.DispatcherObject
        System.Windows.DependencyObject
            System.Windows.Media.Visual
                System.Windows.UIElement
                    System.Windows.FrameworkElement
                        System.Windows.Controls.Control
                            System.Windows.Controls.ItemsControl
                                System.Windows.Controls.HeaderedItemsControl
                                    System.Windows.Controls.TreeViewItem
```

You can add a TreeViewItem control to a WPF application by using the following code snippet:

```
<TreeViewItem>
    <!--Items-->
</TreeViewItem>
```

Table 10.40 describes the noteworthy properties of the TreeViewItem class:

| Table 10.40: Noteworthy Property of the TreeViewItem Class |
| Property | Description |
| IsExpanded | Determines whether the nested items in a TreeViewItem control are expanded or collapsed |
| IsSelected | Determines whether a TreeViewItem control is selected or not |

The TreeViewItem control cannot be added from the Toolbox. You can add the control through XAML code.

# The MenuItem Control

The MenuItem control in WPF represents the selectable menu items contained in the Menu control. The menu classes, Menu and ContextMenu, include the items of the MenuItem control. The content properties of the MenuItem control are Items and ItemsSource. The header property of the MenuItem control is Header. The MenuItem control can have submenus, which are made up of objects within the ItemsCollection property of the MenuItem control. The default value of the HorizontalAlignment property of a MenuItem control is set to Stretch.

The inheritance hierarchy of the MenuItem class is as follows:

```
System.Object
    System.Windows.Threading.DispatcherObject
        System.Windows.DependencyObject
            System.Windows.Media.Visual
                System.Windows.UIElement
                    System.Windows.FrameworkElement
                        System.Windows.Controls.Control
                            System.Windows.Controls.ItemsControl
                                System.Windows.Controls.HeaderedItemsControl
                                    System.Windows.Controls.MenuItem
```

You can add the MenuItem control to a WPF application by using the following code snippet:

```
<MenuItem>
    <!-- Items -->
</MenuItem>
```

Table 10.41 describes the noteworthy properties of the MenuItem class:

| Table 10.41: Noteworthy Properties of the MenuItem Class |
| Property | Description |
| Command | Gets or sets the command associated with a MenuItem control |
| CommandParameter | Gets or sets the parameter to pass the Command property of a MenuItem control |
| CommandTarget | Gets or sets the control on which to raise the specified command |
| Icon | Gets or sets the icon that appears in a MenuItem control |