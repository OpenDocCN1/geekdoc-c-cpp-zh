# ListBox Event Handlers

One of the properties of the ListBox class is SelectedItem. It returns an object representing the selected string item. If you retrieve the selection using this property, the object must be converted to a string object to display it in the Result TextBox. The Text property of the txtBoxResult object is used to display the selection. The statement in Example 10-10 is added to the body of the lstBoxEvents_SelectedIndexChanged() method so that when the event is fired, the selection is displayed.

# Example 10-10

```
private void lstBoxEvents_SelectedIndexChanged(object sender,
                                             System.EventArgs e)
{
        this.txtBoxResult.Text =
                this.lstBoxEvents.SelectedItem.ToString( );
}
```

The ToString( ) method was used to convert the item object to a string for displaying; the Text property can also be used to retrieve the data from a ListBox control object. If you use the Text property as opposed to the SelectedItem property, there is no requirement of adding the ToString( ) method. Thus, the body of the lstBoxEvents_SelectedIndexChanged method could read as shown in Example 10-11.

# Example 10-11

```
private void lstBoxEvents_SelectedIndexChanged(object sender,
                                             System.EventArgs e)
{
        this.txtBoxResult.Text = this.lstBoxEvents.Text;
}
```

Figure 10–3 shows the output generated from Example 10–11 after the SelectedIndexChanged event is fired. Notice that the items appear in alphabetical order. The Sorted property rearranged the items.