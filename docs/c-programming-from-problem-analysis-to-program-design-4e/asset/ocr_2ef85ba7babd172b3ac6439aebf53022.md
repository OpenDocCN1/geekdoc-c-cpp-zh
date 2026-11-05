Example 10-15 just touched the surface for what you can do with ListBox objects. You will want to explore this class further. The Items, SelectedItems, and SelectedIndices properties are useful for getting a collection of selected items from the ListBox object. The Count property can also be used with the SelectedItems, and SelectedIndices properties to return the number of items selected. To retrieve that value you would type lstBxEvents.SelectedItems.Count. To reset the listbox or clear all selections, invoke the ClearSelected( ) method.

In addition to being useful for entering values at design time, the ListBox object is a control that can be populated with new values at run time. By including the Add( ) method inside a loop, values entered by the user or read from a file or database table can be added to the control while the application is running. Table 10-2 describes some of the more interesting properties of the ListBox class.

> > **NOTE**
> > The information included in Tables 10-2 and 10-3 was adapted from the MSDN documentation.

# **TABLE 10-2** ListBox properties

| Property | Description |
|---|---|
| Items | Gets the values (items) in the list box |
| MultiColumn | Gets or sets a value indicating whether the list box supports multiple columns |
| SelectedIndex | Gets or sets the zero-based index of the currently selected item |
| SelectedIndices | Gets a collection that contains the zero-based indexes of all currently selected items |
| SelectedItem | Gets or sets the selected item |
| SelectedItems | Gets a collection containing the currently selected items |
| SelectionMode | Gets or sets the method in which items are selected (MultiExtended, MultiSimple, One, None) |
| Sorted | Gets or sets a value indicating whether the items are sorted alphabetically |
| Text | Gets or searches for the text of the currently selected item |