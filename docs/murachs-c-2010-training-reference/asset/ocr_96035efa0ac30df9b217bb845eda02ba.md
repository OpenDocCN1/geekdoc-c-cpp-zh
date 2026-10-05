# 284 Section 2 The C# language essentials

After you add a combo box or list box to form and set its properties the you want, you can use code like that in figure 10-3 to work with the control. Here, the first example uses a foreach loop to load the name of each month in an array to a combo box. Each time through the loop, the Add method is used to add a name to the items collection for this combo box.

The first item in the array that's loaded into the list indicates that the user should select a month from the list. This is a common technique that's used to provide instructions to the user. As you'll see later in this chapter, though, you'll need to include additional code when you use this technique to be sure that the user selects any other item than the one that provides instructions.

The second example is similar, but it uses a loop to load integer values into a combo box. The first value is the current year, and the next values are the seven years from that. Like the combo box that contains the names of the months, the first entry in this combo box provides instructions for the user.

The third example shows how you can load a list box like the one shown in figure 10-1. To make sure that no items have already been loaded into this list box, this example begins by calling the Clear method to clear all the items. Then, it adds three items to the list box. Finally, it sets the SelectedIndex property to 0, which causes the first item in the list to be selected.

Although it's not shown here, it's common to put code that loads a combo box or list box in the Load event of the form. That way, the control is loaded when the form is loaded. After that, the user can select an item from the combo box or list box and other methods can get information about that.

The statements in the fourth example show four ways that you can get information from a combo box or list box. The first statement uses the SelectedIndex property to get the index of the item that's currently selected in the Years combo box. The second statement shows how to get the value's displayed in the text box property of this combo box. The third statement shows how to get the value of the item's currently selected in this combo box. Notice that the GetSelectedItem property returns an object type, which you can cast this object to the appropriate data type to get the value of it. Finally, the fourth statement uses an index to get the second item in the Months combo box. Since the value of this item is a string type, the ToString method is used to get the value of this item. However, you could also cast the object to a string type like this:

```
string expMonthValue = (string) cboExpirationMonth.Items[1];
```

The fifth example shows how to use the Add, Insert, and RemoveAt to work with the items in a combo box list. This example begins with a foreach loop that adds three names to the list. Then, the Insert method inserts a new name at the beginning of the list, and the RemoveAt method removes the last item from the list. When you use these methods, you indicate the index where you want the item inserted or removed. Finally, the last statement shows how you can initialize a combo box so that no value is selected. To do that, you set the SelectedIndex property of the control to -1.