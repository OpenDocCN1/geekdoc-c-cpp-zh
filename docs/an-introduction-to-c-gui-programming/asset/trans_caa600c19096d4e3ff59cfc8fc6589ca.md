
```c
gtk_list_store_insert_with_values (ls, NULL, pos++, 0,
  "Option 1", 1, icon, -1);
gtk_list_store_insert_with_values (ls, NULL, pos++, 0,
  "Option 2", 1, icon, -1);
gtk_list_store_insert_with_values (ls, NULL, pos++, 0,
  "Option 3", 1, icon, -1);
```

GtkWidget *tv = gtk_tree_view_new_with_model (
  GTK_TREE_MODEL (ls));

GtkCellRenderer *prend = gtk_cell_renderer_pixbuf_new ();
GtkCellRenderer *trend = gtk_cell_renderer_text_new ();

```c
gtk_tree_view_insert_column_with_attributes (
  GTK_TREE_VIEW (tv), -1, "Icon", prend, "pixbuf", 1, NULL);
gtk_tree_view_insert_column_with_attributes (
  GTK_TREE_VIEW (tv), -1, "Option", trend, "text", 0, NULL);
```

```c
GtkWidget *tbl = gtk_table_new (2, 2, FALSE);
gtk_table_attach_defaults (GTK_TABLE (tbl), tv, 0, 2, 0, 1);
gtk_table_attach_defaults (GTK_TABLE (tbl), btn, 0, 1, 1, 2);
gtk_container_add (GTK_CONTAINER (win), tbl);
gtk_widget_show_all (win);
gtk_main();
```

首先，我们调用 `gtk_list_store_new` 创建一个包含2列的列表存储；列 0 包含一个如上一章所示的文本字符串；列 1 包含一个 pixbuf（pixel buffer 的缩写），用于存储图像。

```c
GtkListStore *ls = gtk_list_store_new (2, G_TYPE_STRING,
  GTK_TYPE_PIXBUF);
```

我们创建了一个包含小图像的 `GdkPixbuf` ——在这种情况下，我们从当前项加载一个图标到其中，通过 `GdkPixbuf` 可以存储任何你选择要显示的图像。

```c
GdkPixbuf *icon = gtk_icon_theme_load_icon (
  gtk_icon_theme_get_default (), "dialog-ok-apply", 32, 0,
  NULL);
```

在每个情况下，我们都向列表存储添加了三行；我们在行的第 0 列放入一个文本字符串，并在第 1 列放入我们创建的 pixbuf。

# C语言与 GTK 编程简介

```c
gtk_list_store_insert_with_values (ls, NULL, pos++, 0, icon, \
1, icon, -1);
gtk_list_store_insert_with_values (ls, NULL, pos++, 0, icon, \
1, icon, -1);
gtk_list_store_insert_with_values (ls, NULL, pos++, 0, icon, \
1, icon, -1);
```

我们需要创建一个 `GtkTreeView` 来显示列表存储。这一步与上一章中创建 `GtkListStore` 类似 —— 将新的 `GtkTreeView` 与我们创建的 `GtkListStore` 关联。

```c
GtkWidget *tv = gtk_tree_view_new_model (
GTK_TREE_MODEL (ls));
```

与组合框一样，我们需要为想要在此显示的所有数据类型创建单元渲染器，在这种情况下，我们有两个 —— 一个文本渲染器和一个 pixbuf 渲染器。

```c
GtkCellRenderer *prend = gtk_cell_renderer_pixbuf_new();
GtkCellRenderer *trend = gtk_cell_renderer_text_new();
```

最后，我们将想要查看的列插入树视图中。

```c
gtk_tree_view_insert_column_with_attributes (
  GTK_TREE_VIEW (tv), -1, "Icon", prend, "pixbuf", 1, NULL);
gtk_tree_view_insert_column_with_attributes (
  GTK_TREE_VIEW (tv), -1, "Option", trend, "text", 0, NULL);
```

每次对 `tree_view` 的调用都将树本身作为第一个参数。该参数是列的位置 —— 这可以是实际位置（从表格左侧的 0 开始编号），也可以在这里是 -1，这表示该列应作为下一列添加；即表格中已存在的最右侧列的右侧。下一个参数是列标题（可以显示在表格顶部），然后是我们创建的用于该列的渲染器。

最后的参数被传递给单元渲染器本身，并将渲染器的属性设置到列表存储中某列的数据上 —— 在第一个实例，我们使用 pixbuf 渲染器的 'pixbuf' 属性设置到第 1 列的数据上，在第二种情况下，我们把文本渲染器的 'text' 属性设置到第 0 列的数据上（由于某些渲染器可以设置多个属性，因此最后一个参数是 `NULL`，表示没有更多需要设置的属性了）。

构建并运行代码，并观察发生了什么 —— 你应该会看到类似图像叠加的效果：

![](img/6a7eee5b22417c3d49170130a20b16f2_110_0.png)

![](img/6a7eee5b22417c3d49170130a20b16f2_111_0.png)

具有两列（一个 pixbuf 和一些文本）的 GtkTreeView

# 从树视图获取输入

树视图作为信息显示非常有用，但也可以用于读取用户的选择。如果你点击表格中的某一行，它会被高亮 —— 你也可以通过键盘上的箭头键在表格中上下移动高亮部分。

![](img/6a7eee5b22417c3d49170130a20b16f2_111_1.png)

一个被用户选了行的 GtkTreeView

每当选中的行改变时，树视图就会产生 `cursor-changed` 信号，因此可以用此调用相应的回调函数：

```c
g_signal_connect(tv, "cursor-changed", G_CALLBACK
(row_selected), NULL);
```

回调函数应该如下：

```c
void row_selected (GtkWidget *wid, gpointer ptr)
{
    GtkTreeSelection *sel;
    GtkTreeModel *model;
    GtkTreeIter iter;
    char *option;

    sel = gtk_tree_view_get_selection (GTK_TREE_VIEW (wid));
    if (gtk_tree_selection_get_selected (sel, &model, &iter))
    {
        gtk_tree_model_get(model, &iter, 0, &option, -1);
        printf ("The selected row contains the text %s\n", option);
    }
}
```

确定哪些行被选中需要一个迭代器（iterator），它是一个存储列表存储中某行位置的数据结构。

首先，我们需要获取树视图的 `GtkTreeSelection` —— 它存储了当前被高亮的行（或哪些行）。

```c
sel = gtk_tree_view_get_selection (GTK_TREE_VIEW (tv));
```

从 `GtkTreeSelection` 获取 `GtkTreeIter` 和关联的 `GtkTreeModel`。模型是提供树数据的列表存储，迭代器是当前被高亮的行。

```c
if (gtk_tree_selection_get_selected (sel, &model, &iter))
```

（此函数返回 `FALSE` 则表示没有选中项 —— 否则下一行会导致崩溃。）

最后，我们可以从模型和迭代器获取实际值。

```c
gtk_tree_model_get (model, &iter, 0, &option, -1);
```

当设置列表存储中的值时，传递给函数的模型和迭代器之后的参数是一对值，每对第一个是要读取的列，第二个是要写入数据的指针。在这种情况下，第一列的文本指针作为 `option` 返回。`-1` 表示没有更多要设置的属性。

# 第21 章

# 菜单

带有下拉菜单和弹出菜单的菜单栏

应用程序顶部都有菜单栏。GTK 提供了许多创建菜单栏或弹出菜单的控件。菜单的构建块是 `GtkMenuItem`。菜单中的每个项都是 `GtkMenuItem`，它关联有一个文本标签。使用 `GtkWidget` 来包含一个或多个 `GtkMenuItem`；创建一个类型在应用程序菜单栏项被选中时看到的弹出菜单。

# 菜单栏

`GtkMenuBar` 可以显示在应用程序顶部；它包含许多 `GtkMenuItem`；每个项为 `GtkMenu` 提供名称，如上所述，认为 `GtkMenuItem` 既是菜单的成员又是整个菜单的名称可能有些困惑，但希望示例会让情况更清晰。这是带有菜单栏应用程序的代码：

```c
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
}
```

