We then added the renderer we just created to the cell layout of the combo box - this means that the renderer will be called when the combo box wants to display some data (The final parameter, set to FALSE is whether or not the data is expanded to fill free space in the layout; this has no effect on a combo box).

```
gtk_cell_layout_set_attribute(GTK_CELL_LAYOUT (comb), rend,
```

Finally, we set the text attribute of the cell renderer to the data from the supplied column number of the list store - this causes the renderer to display the data in column 0 as text in the combo box.

Try building and running the code, and satisfy yourself that it does the same thing as the previous example with GtkComboBoxText.

![](bbox=[0.046, 0.415, 0.715, 0.595])

A GtkComboBoxinstead of the GtkComboBoxText - don't worry, they are supposed to look like the same!

Some of the code above probably looks a bit like black magic, and in truth it is a complicated way to put some text in a combo box, cell renderers make more sense in some other circumstances, which we will look at in the next chapter. But they are a necessary complication when using list stores to provide data for combo boxes, and that can be very useful, because we can process the data in a list store and have the combo box automatically reflect that processing.

For example, in the code above, we have put the three text strings into the list store in alphabetical order, but in the real world, we can't guarantee that data will come in in a nice tidy order like that. With a list store, it is easy to sort the data, by replacing the line:

```
Gtkwidget *comb = gtk_combo_box_new_with_model (
GTK_TREE_MODEL (ls));
```