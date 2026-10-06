Here's an example of using GtkColorButton:

```
static void (GtkButton *btn, gpointer ptr)
{
  GdkColor col;
  gtk_color_button_get_color(btn, &col);
  printf("%d %d %d\n", col.red, col.green, col.blue);
}
```

```
void main (int argc, char *argv[])
{
  gtk_init(&argc, argv);

  GtkWidget *win = gtk_window_new(GTK_WINDOW_TOPLEVEL);
  GtkWidget *btn = gtk_button_new_label("Close window");
  g_signal_connect(btn, "clicked", G_CALLBACK(end_program), NULL);
  g_signal_connect(win, "destroy", G_CALLBACK(end_program), NULL);

  GtkWidget *vbox = gtk_vbox_new(FALSE, 5);
  gtk_container_add(vbox, btn);

  GtkWidget *col_btn = gtk_color_button_new(0);
  g_signal_connect(col_btn, "changed", G_CALLBACK(col_selected), NULL);

  gtk_box_pack_start(GTK_BOX(vbox), col_btn, TRUE, TRUE, 0);
  gtk_box_pack_start(GTK_BOX(vbox), btn, TRUE, TRUE, 0);
  gtk_widget_show_all(win);
  gtk_main();
}
```

We create the picker button in the same way as the file chooser button, and we connect to the color-set signal on it to detect when the user has made a selection. The handler for this signal calls gtk_color_button_get_color to read the selected value back into a GdkColor structure, and then prints out the red, green, and blue values.
If you run this, you'll see that the colour button shows a small rectangle of the currently selected colour.