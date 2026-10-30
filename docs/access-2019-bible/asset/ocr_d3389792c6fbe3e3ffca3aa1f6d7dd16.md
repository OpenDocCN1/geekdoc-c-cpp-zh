This indicates to Access that you want the first column to be invisible and sets explicit column widths for the other columns.

The second column—in this case, the organization name—is the one against which the user’s text input is matched. The first visible column in the combo box is always used for this purpose. Figure 19.5 shows the resulting drop-down list. Although this is a rather extreme example of loading a combo box with data, it effectively illustrates the power of the Access Combo Box control.

# FIGURE 19.5

The drop-down list for the Organization combo box.

![](bbox=[0.21, 0.47, 0.9, 0.8])

When working with combo boxes, if you set the Limit To List property to Yes, the user is required to choose from only the entries in the drop-down list. You can then construct an event procedure for the control’s NotInList event to handle what should happen if a user enters a value not in the list. You might want to open a form into which the user can enter new information; or perhaps you want to display a message box that instructs the user what procedure to follow to add data.