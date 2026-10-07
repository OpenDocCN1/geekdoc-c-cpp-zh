
```xml
<Label Content="Mercury" HorizontalAlignment="Center"
    Foreground="Green"/>
</StackPanel>
<ComboBoxItem>
    ... OtherComboBoxItems omitted ...
</ComboBox>
```

UseComboBox

The ComboBox's Background property sets the background used for the ComboBox itself, not the items. You can see in Figure 7-3 the right ComboBox's background is black.

A ComboBoxItem's Background property sets the background used for the ComboBoxItem. For example, in Figure 7-4, you can see that the background behind the Earth, Jupiter, and Saturn items is black.

Notice the blue background Mars in Figure 7-4 when the mouse hovers over an item in the dropdown list (Mars in Figures 7-3 and 7-4), the ComboBox changes its background color so the user can see that it is selected.

The ComboBox can only change the background color of an item where it is not covered by its contents. For example, in the previous code, if you set the ComboBoxItem's StackPanel's Background property to blue, then all of the dropdown items would have a blue background. The ComboBox would only be able to change the color of two small slices to the left and right of the dropdown item, so the user would have very little clue when the item is selected.

The morale of the story is to not try to fill the dropdown completely but make sure that some background shows through.

The following table summarizes the ComboBox's most useful properties:

| PROPERTY | PURPOSE |
| --- | --- |
| Background | The background used to draw the ComboBox itself |
| IsEditable | Determines whether the user can type a new value into the ComboBox. (This works best if the items are plaintext values as on the left in Figure 7-3.) |
| MaxDropdownHeight | The maximum height of the dropdown list |
| SelectedIndex | The index of the currently selected item |
| SelectedItem | The currently selected ComboBoxItem |

# CONTEXTMENU

The ContextMenu controls a pop-up menu associated with a control. For example, the ContextMenu example shown in Figure 7-5 contains a ListBox with an associated ContextMenu. When you right on the ListBox, the ContextMenu automatically appears, as shown in the figure.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_161_0.png)

FIGURE 7-5

Strangely, neither Expression Blend nor Visual Studio has a ContextMenu in its Control Toolboxes. Fortunately, a ContextMenu is easy to build for XAML.

The following XAML code shows how the UseContextMenu program builds its ListBox and ContextMenu. After the ListBox's Background element, a ListBox.ContextMenu elements define the ContextMenu. Each must contain a ContextMenu object that contains MenuItem objects.

```xml
<ListBox Name="WebSites" Grid.Row=1 HorizontalAlignment="Stretch" Width="Auto" IsSynchronizedWithCurrentItem="True" Margin="5">
<ListBox.Background>
  <LinearGradientBrush EndPoint="0.5,0.5" StartPoint="0.5,0">
    <GradientStop Color="#FFFFFF" Offset="0"/>
    <GradientStop Color="#FFFF00" Offset="1"/>
  </LinearGradientBrush>
  </ListBox.Background>
  <ListBox.ContextMenu>
    <ContextMenu>
      <MenuItem Name="mnuAddNewSite" Header="Add New Site"/>
      <MenuItem Name="mnuDeleteSite" Header="Delete Site"/>
    </ContextMenu>
  </ListBox.ContextMenu>
  <ListBox.ItemTemplate>
    <StackPanel Orientation="Horizontal">
      <Label Content="VB Helper" Width="150"/>
      <Label Content="www.vb-helper.com" Width="150"/>
    </StackPanel>
  </ListBox.ItemTemplate>
  ... Other ListItems omitted
</ListBox>
```

You can easily create submenus in a ContextMenu by simply adding MenuItems inside other MenuItems. For example, the following ContextMenu contains a submenu with Items Copy, Cut, and Paste:

```xml
<ContextMenu>
  <MenuItem Name="mnuAddNewSite" Header="Add New Site"/>
  <MenuItem Name="mnuDeleteSite" Header="Delete Site"/>
  <MenuItem Header="Submenu">
    <MenuItem Name="mnuCopy" Header="Copy"/>
    <MenuItem Name="mnuCut" Header="Cut"/>
    <MenuItem Name="mnuPaste" Header="Paste"/>
  </MenuItem>
</ContextMenu>
```

# HANDLING MENUITEMS

When the user selects an item, the MenuItem object raises a Click event just as a Button does. You can catch it and handle it in the same way.

ContextMenus are one kind of Menu object. The “Menu” section later in this chapter has more about Menu and MenuItem objects.

# FRAME

The Frame control displays content and provides a simple navigation model. It can display web pages or XAML files and follow links in those files.

The control's Source property determines the web page or XAML file that the control should display. A program can also call the control's Navigate method to make it display a new page. For example, the C# code makes the Frame named fraGo open the web page www.vb-helper.com/index_categories.html:

```csharp
fraGo.Navigate(new Uri("http://www.vb-helper.com/index_categories.html"));
```

When the Frame navigates to a new page, because its Source changed or the program called the Navigate method, the Frame stores its previous location in its navigation history. The user can click on the control's forward and backward buttons to move through the history.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_163_0.png)

The UseFrame example program shown in Figure 7-6 contains a ComboBox and a Frame. When you select a web page from the ComboBox, the control displays the page.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_163_1.png)

In Figure 7-6, you can see the navigations in the Frame control's upper-left corner. If you click on the small dropdown to the right of the buttons, the control displays a list of the pages in the navigation history so so you can quickly jump to one of them.

# GRIDSPLITTER

The GridSplitter controls the user adjust the widths of the rows and columns in a Grid. To use a GridSplitter, you add it to a cell in a Grid. To use a GridSplitter, you add it to a cell in a Grid. At time, the user can grab the GridSplitter and drag it to resize rows or columns.

FIGURE 7-7 shows the GridSplitter.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_164_0.png)

The GridSplitter controls the user adjust the widths of the rows and columns in a Grid. To use a GridSplitter, you add it to a cell in a Grid. To use a GridSplitter, you add it to a cell in a Grid. At time, the user can grab the GridSplitter and drag it to resize rows or columns.

The following XAML code shows how UseSplitter program makes its GridSplitter:

```xml
<GridSplitter Column="1" RowSpan="2"
    HorizontalAlignment="Left"
    VerticalAlignment="Stretch"
    Background="Blue"
    ShowsPreview="False"
    Width="5"/>
```

The following list explains each of the property values:

- Column="1" — The GridSplitter in column 1.
- RowSpan="2" — This makes the GridSplitter span both rows.
- HorizontalAlignment="Left" — This puts the GridSplitter on the left.
- VerticalAlignment="Stretch" — This makes the control fill vertically.
- Background="Blue" — This makes the control stand out.
- ShowsPreview="False" — If this is True, the control shows a ghost of itself as the user drags. If this is False, the control resizes columns.
- Width="5" — This determines the control's width.

To make a GridSplitter that lets the user resize rows instead of columns, switch the roles of rows and columns and the vertical and horizontal alignment. The following XAML code shows how Splitter program makes its GridSplitter:

```xml
<GridSplitter Row="1" ColumnSpan="2"
    HorizontalAlignment="Stretch"
    VerticalAlignment="Top"
    Background="Red"
    ShowsPreview="True"
    Height="5"/>
```

![](img/c9b2d34f4fc2f7e276f6a0a6fa9c2f6_165_0.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_165_1.png)

# 128 | CHAPTER 7 USER INTERACTION CONTLS
