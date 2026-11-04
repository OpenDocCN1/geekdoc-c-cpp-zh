# 15.10 ListView Control

The ListView control is similar to a ListBox in that both display lists from which the user can select one or more items (an example of a ListView can be found in Fig. 15.31). ListView is more versatile and can display items in different formats. For example, a ListView can display icons next to the list items (controlled by its SmallImageList, LargeImageList or StateImageList properties) and show the details of items in columns. Property MultiSelect (a bool) determines whether multiple items can be selected. CheckBoxes can be included by setting property CheckBoxes (a bool) to true, making the ListView's appearance similar to that of a CheckedListBox. The View property specifies the layout of the ListBox. Property Activation determines the method by which the user selects a list item. The details of these properties and the Click and ItemActivate events are explained in Fig. 15.29.

| ListView properties and events | Description |
| --- | --- |
| *Common Properties* | |
| Activation | Determines how the user activates an item. This property takes a value in the ItemActivation enumeration. Possible values are OneClick (single-click activation), TwoClick (double-click activation, item changes color when the mouse moves over the item) and Standard (the default; double-click activation, item does not change color). |
| CheckBoxes | Indicates whether items appear with CheckBoxes. true displays CheckBoxes. The default is false. |
| LargeImageList | Specifies the ImageList containing large icons for display. |
| Items | Returns the collection of ListViewItems in the control. |
| MultiSelect | Determines whether multiple selection is allowed. The default is true, which enables multiple selection. |
| SelectedItems | Returns the collection of selected items as a ListView.SelectedListViewItemCollection. |
| SmallImageList | Specifies the ImageList containing small icons for display. |
| View | Determines appearance of ListViewItems. Possible values are LargeIcon (the default; large icon displayed, items can be in multiple columns), SmallIcon (small icon displayed, items can be in multiple columns), List (small icons displayed, items appear in a single column), Details (like List, but multiple columns of information can be displayed per item) and Tile (large icons displayed, information provided to right of icon). |
| *Common Events* | |
| Click | Generated when an item is clicked. This is the default event. |
| ItemActivate | Generated when an item in the ListView is activated (clicked or double clicked). Does not contain the specifics of which item is activated—you can use SelectedItems or SelectedIndices to determine this. |

**Fig. 15.29** | ListView properties and events.