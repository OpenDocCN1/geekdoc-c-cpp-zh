checks whether the event source was the Small, Medium, Large, or Extra Large button. All we care about is the desired size of the font.

User data provide a convenient mechanism for transferring arbitrary data from a control to a shared handler. You can set arbitrary objects as user data of a control. We will set the desired font sizes:

```
small.setUserData(8);
medium.setUserData(14);
. . .
```

In the shared event handler, we retrieve the user data from the currently selected button in the toggle group:

```
int size = (int) group.getSelectedToggle().getUserData();
```

If you look again at Figure 13.17, you will note that the appearance of the radio buttons differ from that of checkboxes. Checkboxes are square and contain a checkmark when selected. Radio buttons are round and contain a dot when selected.

If you have more than a handful of alternatives, radio buttons are not a good choice because they take up too much screen space. Instead, use a combo box. When the user clicks on this control, a list of choices drops down, and the user can then select one of them (see Figure 13.18).

If the drop-down list box is set to be editable, you can edit the current selection as if it were a text field. For that reason, this control is called a combo box—it combines the flexibility of a text field with a set of predefined choices. The ComboBox class provides a combo box control.

Call the setEditable method to make the combo box editable. Note that editing affects only the selected item. It does not change the list of choices in any way.

In the example program, the user can choose a font family from a list of all available families. We add all choices to the list returned by getItems:

```
ComboBox<String> families = new ComboBox<>();
families.getItems().addAll(Font.getFamilies());
```

> **NOTE:** `ComboBox<T>` is a generic class. The type parameter denotes the type of the items. If the item type is not String, then a converter needs to convert between them type and the strings that the user views and potentially edits. We take up that issue in Chapter 11 of Volume II.