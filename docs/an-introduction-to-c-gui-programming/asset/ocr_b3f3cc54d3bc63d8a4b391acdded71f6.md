you type a value that isn't a number, or is outside the range specified in the GtkAdjustment, it will be corrected to a value within a range when one of these buttons – or ‘Copy button’ – is pressed.

# Toggle buttons

One easy way to get input from the user is by the use of buttons to select an option. GTK offers several widgets for this purpose, two of the more useful are check buttons – boxes that can be ticked or unt – and radio buttons – selectors in which only one member of a group can be active at a time. These are both children of the GtkToggleButton widget, which is itself a child of the GtkButton widget we have already used several times, toggle button is a button which can be in either a selected or an unselected condition.

# Check buttons

Check buttons are the simplest of the two, so we’ll look at those first. A GtkCheckButton is a box which can be empty or have a tick mark in it; clicking on it toggles between those two states. Creating one is as easy as:

```
GtkWidget *chk = gtk_check_button_new_with_label ("My check");
```

This creates a check button and a label to its left with the supplied text in it. (There is also a function gtk_check_button_new, which creates the check box without the label – this makes things tidier if you have a label for it elsewhere in your window.) Try replacing btn2 in the previous example with a checkbox like chk – it should look like this:

![](bbox=[0.118, 0.597, 0.574, 0.725])

A GtkCheckButton at the top-right of the window

By default, a check button which has just been created is in the unchecked state. To check the button, you call

```
gtk_toggle_button_set_active(GTK_TOGGLE_BUTTON (chk), TRUE);
```

Setting the button’s active state to TRUE checks the box, setting it to FALSE unchecks it. There is a corresponding function to read the active state of a toggle button – to read whether a check button is currently checked into a variable, do: