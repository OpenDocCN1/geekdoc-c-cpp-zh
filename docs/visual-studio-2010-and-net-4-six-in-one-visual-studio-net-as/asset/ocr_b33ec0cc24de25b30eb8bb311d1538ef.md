![](bbox=[0.095, 0.093, 0.545, 0.372])

**FIGURE 19-7:** Handling events within a template

As you can see, the same unordered list is used as before. The only difference is that the user can click on any item to select it. This selectivity feature is added to the li element with the sys="Select" attribute, and the cursor is changed with the style attribute to provide a visual cue for the user.

The ViewData is able to automatically add a CSS class to the currently selected element if the name of this class is defined in the selectedItemClass property. You can use this CSS class to highlight the selected data item. Even if you use the sys:command and the style attributes to a child element inside the template, the selectedItemClass will be added to the whole list item. This means although you can raise the Select event from any part of the data item, only the whole data item can be selected, not parts of it.

This code also shows that you can specify the item when the control is first rendered by setting its zero-based index in the dv:selectedIndex property.

After the user successfully selects a record, he or she can click on the "Get details" link that calls the getDetails JavaScript function. Note that this function is outside the template, and because no context parameters are passed to the function, the selection must be queried from the ViewData.

The following code snippet shows the implementation of the getDetails method:

```
function getDetails() {
  var dv = $dv("countryList");
  var country = dv.get_selectedData();
  var msg = String.format("You selected %0, (%1) is the capital of %2.",
  dv.selectedIndex());
}
```