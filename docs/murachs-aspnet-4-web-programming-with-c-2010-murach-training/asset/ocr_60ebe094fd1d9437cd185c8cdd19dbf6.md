# Common members of list item collection objects

| Property | Description |
|---|---|
| Count | The number of items in the collection. |
| Indexer | Description |
| [integer] | A ListItem object that represents the item at the specified index. |
| Method | Description |
| Add(string) | Adds a new item to the end of the collection, and assigns the specified string value to both the Text and Value properties of the item. |
| Add(ListItem) | Adds the specified list item to the end of the collection. |
| Insert(integer, string) | Inserts an item at the specified index location in the collection, and assigns the specified string value to the Text property of the item. |
| Insert(integer, ListItem) | Inserts the specified list item at the specified index location in the collection. |
| Remove(string) | Removes the item from the collection whose Text property is equal to the specified string value. |
| Remove(ListItem) | Removes the specified list item from the collection. |
| RemoveAt(integer) | Removes the item at the specified index location from the collection. |
| Clear() | Removes all the items from the collection. |
| FindByValue(string) | Returns the list item whose Value property has the specified value. |
| FindByText(string) | Returns the list item whose Text property has the specified value. |

# Code that loads items into a list box using strings

```
lstColor.Items.Add("Black");
lstColor.Items.Add("Red");
lstColor.Items.Add("Blue");
lstColor.Items.Add("Green");
```

# Code that loads items into a drop-down list using ListItem objects

```
ddlDay.Items.Add(New ListItem("Sunday", "1"));
ddlDay.Items.Add(New ListItem("Monday", "2"));
ddlDay.Items.Add(New ListItem("Tuesday", "3"));
ddlDay.Items.Add(New ListItem("Wednesday", "4"));
ddlDay.Items.Add(New ListItem("Thursday", "5"));
ddlDay.Items.Add(New ListItem("Friday", "6"));
ddlDay.Items.Add(New ListItem("Saturday", "7"));
```

# Description

+   - The ListItemCollection object is a collection of ListItem objects. Each ListItem object represents one item in the list.
+   - Items in a ListItemCollection object are numbered from 0. So the index for the first item in the list is 0, the index for the second item is 1, and so on.
+   - When you load items into a list box using strings, both the Text and Value properties of the list item are set to the string value you specify. To set the Text and Value properties of a list item to different values, you must create a list item object and then add that item to the collection.

Figure 6-13    Members for working with list item collections