# AN INTRODUCTION TO C AND GUI PROGRAMMING

or vice versa. It's even acceptable to put an GtkHBox as an item inside GtkHBox (but it's
general a bit pointless). Using a combination of nested GtkHBoxes and GtkVBoxes, you can
lay out all the widgets in a window the way you want.

Nesting GtkBoxes and GtkVBoxes works perfectly well for laying out widgets in two
dimens, and actually give you the best control over how they appear, there is a simpler
alternative, the GtkTable widget.

A GtkTable is a two-dimensional box, which is defined as having a certain number of rows and
columns when it is created. Widgets can then be located at various row and column co-ordinates.
This is not as flexible as using nested GtkBoxes and GtkVBoxes, because every
widget has to be aligned in both a row and a column - this means that any row is always
least high as the tallest widget anywhere in it, and any column is at least wide as
t widest widget anywhere in it, this can lead to a lot of wasted space. But often a
simple arrangement like this is all that is needed, a Table works fine.

Here are the changes to our example if we use a GtkTable to position the label and buttons

```
void main (int argc, char *argv[])
{
    gtk_init(&argc, &argv);

GtkWidget *win = gtk_window (GTK_WINDOW_TOPLEVEL);
GtkWidget *btn = gtk_button_with_label ("Click me");
    g_signal_connect(btn, GCALLBACK (end_program),
    NULL);
    g_signal_connect(win, GCALLBACK (end_program),
    NULL);

GtkWidget *lbl = gtk_label_new ("My label");

GtkWidget *btn2 = gtk_button_with_label ("Button 2");
g_signal_connect(btn2, GCALLBACK (count_button),
    lbl);

GtkWidget *table = gtk_table_new (2, 2, TRUE);
gtk_table_attach_defaults (GTK_TABLE (table), lbl, 0, 1, 0, 1);
gtk_table_attach_defaults (GTK_TABLE (table), btn2, 1, 2, 0, 1);
gtk_table_attach_defaults (GTK_TABLE (table), btn, 0, 2, 1, 2);
gtk_container_add (GTK_CONTAINER (win), table);
gtk_widget_show_all (win);
    gtk_main (0
}
```