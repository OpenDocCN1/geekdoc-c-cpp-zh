# Chapter 21

# # Men

Create menu bars with drop-down menus and also pop-up menus

any applications have a menu bar at the top of the main window. GTK provides a number of widgets which can be used to create either menu bars or pop-up menus.
The building block of menus is the GtkMenuItem widget. Each entry in a menu is a GtkMenuItem, which has a text label associated with it. A GtkWidget is used to hold one or more GtkMenuItem widgets; creating a single menu of the sort seen as a pop-up or when an item on an application menu bar is selected.

# Menu bars

A GtkMenuBar can be displayed at the top of an application's window; this contains a number of GtkMenuItems; each of which provides the name for a GtkMenu, as described above it be slightly confusing to consider that a GtkMenuItem is both a member of a menu and the name of the entire menu but hopefully an example will make things a bit clearer. Here's the code for an application with a menu bar:

```
void main (int argc, char *argv[]) {
    int init;
    gtk_init (&argc, &argv);
    GtkWidget *win = gtk_window_new (GTK_WINDOW_TOPLEVEL);
    GtkWidget *btn = gtk_button_new_with_label ("Close");
    g_signal_connect (btn, "clicked", G_CALLBACK (end_program), NULL);
    g_signal_connect (win, "delete_event", G_CALLBACK (end_program), NULL);
    GtkWidget *mbar = gtk_menu_bar_new ();
    GtkWidget *hbox = gtk_box_new (FALSE, FALSE, 5);
    gtk_box_pack_start (GTK_BOX (hbox), mbar, TRUE, TRUE, 0);
    gtk_container_add (GTK_CONTAINER (win), hbox);
```