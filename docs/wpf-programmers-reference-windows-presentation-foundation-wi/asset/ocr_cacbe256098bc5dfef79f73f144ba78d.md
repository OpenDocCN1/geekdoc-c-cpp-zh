# MAKE ROOM

Be sure to allow room for the splitters when you place other objects inside the Grid. For example, if you place a 5-pixel-wide GridSplitter on the left edge of the second-column, then any other controls in column should have a left margin of at least 5 so they don't overlap with the splitter.

# LISTBOX

The ListBox displays a list of items and lets the user select one or more

The control should contain ListBoxItems that holds the choices. The SelectedIndex, SelectedItem, and SelectedValue properties let you get and set the currently selected item.

**TABLE D-14**: Key Properties of ListBox

| PROPERTY | PURPOSE |
| --- | --- |
| HorizontalContentAlignment | Determines the ListboxItems are aligned. This can be Center, Left, Right, or Stretch. |
| SelectedIndex | Determines the index of the currently selected item. |
| SelectedItems | Returns the currently selected items. (You cannot use SelectedIndex, SelectedItem, or other selection properties to see which items are selected if more than one is.) |
| SelectionMode | Determines how many items the user can select. This can be Single (one item only), Multiple (can select multiple items by clicking on them individually), or Extended (can use [Shift]+click and [Ctrl]+click to select multiple items). |

**TABLE D-15**: Key Events for ListBox

| EVENT | PURPOSE |
| --- | --- |
| SelectionChanged | Occurs when the selected items change. |

The ListBox objects inside a ListBox also provide some useful events (see Table D-16).