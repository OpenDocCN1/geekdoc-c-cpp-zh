# Chapter 24

# Customising widgets

Change the properties of widgets
alter how they look

In all the examples we've seen so far, we have used widgets in their default state; we've just created the widget with the gtk_<widget name>_new function call and used it. However, GTK does allow a degree of customisation of widgets by setting the properties for each.
As an example, we are going to look at some of the properties of the basic GtkButton widget. Try this example:

```
void main (int argc, char *argv[]) {
  gtk_init(&argc, &argv);

  GtkWidget *win = gtk_window_new(GTK_WINDOW_TOPLEVEL);
  GtkWidget *btn = gtk_button_new_with_label("clicked");
  g_signal_connect(btn, "clicked", G_CALLBACK(end_program),
  NULL);
  g_signal_connect(win, "delete_event", G_CALLBACK(end_program),
  NULL);

  GtkWidget *btn2 = gtk_button_new_with_label("exit");
  g_object_set(S_OBJECT(btn2), "relief", GTK_RELIEF_NONE, NULL);

  GtkWidget *box = gtk_box_new(FALSE, 5);
  gtk_pack_start(GTK_BOX(box), btn2, TRUE, TRUE, 0);
  gtk_pack_start(GTK_BOX(box), btn, TRUE, TRUE, 0);
  gtk_container_add(GTK_CONTAINER(win), box);
  gtk_widget_show_all(win);

  gtk_main();
}
```

This is familiar code from previous examples, but the highlighted line is new.
g_object_set takes as arguments the name of a widget, followed by a NULL terminator.