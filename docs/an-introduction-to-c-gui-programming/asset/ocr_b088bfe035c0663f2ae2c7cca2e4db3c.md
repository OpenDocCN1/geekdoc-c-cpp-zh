```
gtk_list_store_insert_with_values (ls, NULL, pos++, 0,
  "Option 1", 1, icon, -1);
gtk_list_store_insert_with_values (ls, NULL, pos++, 0,
  "Option 2", 1, icon, -1);
gtk_list_store_insert_with_values (ls, NULL, pos++, 0,
  "Option 3", 1, icon, -1);
```

GtkWidget *tv = gtk_tree_view_new_with_model (
  GTK_TREE_MODEL (ls));

GtkCellRenderer *prend = gtk_cell_renderer_pixbuf_new (
GtkCellRenderer *trend = gtk_cell_renderer_text_new ();

```
gtk_tree_view_insert_column_with_attributes (
  GTK_TREE_VIEW (tv), -1, "Icon", prend, "pixbuf", 1, NULL);
gtk_tree_view_insert_column_with_attributes (
  GTK_TREE_VIEW (tv), -1, "Option", trend, "text", 0, NULL);
```

```
Gtkwidget *tbl = gtk_table_new (2, 2, FALSE);
gtk_table_attach_defaults (GTK_TABLE (tbl), tv, 0, 2, 0, 1);
gtk_table_attach_defaults (GTK_TABLE (tbl), btn, 0, 1, 1, 2);
gtk_container_add (GTK_CONTAINER (win), tbl);
gtk_widget_show_all (win);
gtk_main();
```

First, we call gtk_list_store_new to create a 2-column list store; column 0 contains a text string as in the previous chapter; column 1 contains a pixbuf (short for pixel buffer), which is used to store an image.

```
GtkListStore *ls = gtk_list_store_new (2, G_TYPE_STRING,
  GTK_TYPE_PIXBUF);
```

We create a GdkPixbuf with a small image in it - in this case, we load an icon from the current item into it, by a GdkPixbuf can store any sort of image you choose to display

```
GdkPixbuf *icon = gtk_icon_theme_load_icon (
  gtk_icon_theme_get_default (), "dialog-ok-apply", 32, 0,
  NULL);
```

We add three rows to the list store in each case; we put a text string into column 0 of the row, and the pixbuf we created in column 1.