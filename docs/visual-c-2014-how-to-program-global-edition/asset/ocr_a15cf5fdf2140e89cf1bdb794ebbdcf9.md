# 15.6 ListBox Control 657

| ListBox properties, methods and an event | Description |
| --- | --- |
| SelectionMode | Determines the number of items that can be selected and the means through which multiple items can be selected. Values are None (the default), MultiSimple (multiple selection allowed) or MultiExtended (multiple selection allowed using a combination of arrow keys and mouse clicks and Shift and Ctrl keys). |
| Sorted | Indicates whether items are sorted alphabetically. Setting this property's value to true sorts the items. The default value is false. |
| Common Methods | |
| ClearSelected | Deselects every item. |
| GetSelected | Returns true if the item at the specified index is selected. |
| Common Event | |
| SelectedIndexChanged | Generated when the selected index changes. This is the default event when the control is double clicked in the designer. |

Fig. 15.16 | ListBox properties, methods and an event. (Part 2 of 2. )

Both ListBox and Checked have properties Items, SelectedItem and SelectedIndex. Property Items returns a collection of the list items. Collections are a common way to manage lists of objects in the .NET framework. Many .NET GUI components (e.g., List) use collections to expose lists of internal objects (e.g., items in a ListBox). We discuss collections in Chapter 21. The collection returned by Items is an object of type ListBox.ObjectCollection. Property SelectedItem returns the currently selected item. If the user can select multiple items, use SelectedItems to return all the selected items as a ListObjectCollection. Property SelectedIndex returns the index of the selected item—if there could be more than one, use property SelectedIndices, which returns a ListBox.SelectedIndexCollection. If no items are selected, property SelectedIndex returns -1. Method GetSelected takes an index and returns true if the corresponding item is selected.

Adding Items to ListBoxes and CheckedListBoxnTo add items to a ListBox or a CheckedList, we must add items to its collection. This can be achieved by calling method Add a string to the ListBox's or CheckedListBox's Items. For example, we could write

```
myListBox.Items.Add(myListItem);
```

to string myListItem to myListBox. To add multiple objects, you can either call method Add multiple times or call AddRange to an array of objects. Classes ListBox and CheckedListBox each call the submitted object's ToString method to determine the Label for the corresponding object's entry in the list. You can add different objects to a ListBox or a CheckedListBox that later be returned through properties SelectedItem and SelectedItems.