
内容区域对话的额外内容，可以通过 `gtk_dialog_get_content_area` 函数访问。

像如下所示修改上面的处理函数：

```
void open_dialog(Gtkwidget *wid, gpointer ptr) {
  Gtkwidget *dlg = gtk_dialog_new_with_buttons("My dialog",
      GTK_WINDOW (ptr),
      GTK_DIALOG_MODAL | GTK_DIALOG_DESTROY_WITH_PARENT,
      "Cancel", 0, "OK", NULL);

  Gtkwidget *lbl = gtk_label_new (
    gtk_container_add(
      GTK_CONTAINER (gtk_dialog_get_content_area (GTK_DIALOG (dlg))),
      lbl
    );
    gtk_widget_show (lbl);
}
```

```
int result = gtk_dialog_run (GTK_DIALOG (dlg));
g_widget_destroy (dlg);
printf("Return code: %d\n", result);
```

我们使用了熟悉的 `gtk_container_add` 函数将标签添加到对话框的内容区域。请注意，我们还需要对添加的标签调用 `gtk_widget_show` —— `gtk_dialog_run` 会自动显示对话框本身的组件（如背景和按钮），但你需要显式地显示你添加的所有其他内容。

![](img/6a7eee5b22417c3d49170130a20b16f2_121_0.png)

向内容区域添加了标签的 GtkDialog
与主应用程序窗口一样，如果我们想向内容区域添加多个组件，首先需要添加一个框或一个表格，然后将组件放入其中。

## 第 23 章

## 内置对话框

GTK 包含了一些用于常用函数的预制对话框。

在许多桌面应用程序中都有常用的对话框；例如，用于选择加载或保存的文件，或者选择颜色。GTK 包含了这些常用对话框的预制版本，可以轻松地包含在应用程序中，无需从头创建对话框的每个方面。对于大多数此类对话框，有一个 GTK 按钮可以启动对话框；最简单的方法是在应用程序中包含相应的按钮，剩下的工作都会为你完成。

## 文件选择器对话框

让我们来看一个文件选择器对话框的示例，它用于获取文件的名称和路径，这些路径可以在后续的文件读取操作中使用。

```
static void label(GtkFileFileChooser *btn, gpointer ptr)
{
    char *filename = gtk_file_chooser_get_filename(GTK_FILE_CHOOSER(btn));
    // ... ...
}

void main (int argc, char *argv[])
{
    gtk_init(&argc, &argv);

    GtkWidget *win = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_window_set_title(win, "FileChooser");
    GtkWidget *btn = gtk_button_new_with_label("Open");
    g_signal_connect(btn, "clicked", G_CALLBACK(end_program), NULL);

    g_signal_connect(win, "delete_event", G_CALLBACK(end_program), NULL);

    GtkWidget *vbox = gtk_vbox_new(FALSE, 5);

    gtk_container_add GTK_CONTAINER (win, bbox);
    GtkWidget *fc_btn = gtk_file_choose_button_new (
  GTK_FILE_CHOOSER_ACTION_OPEN);
    gtk_signal_connect (fc_btn,
      CALLBACK (file_selected), NULL);
    gtk_box_pack_start (GTK_BOX, vbox), fc_btn, TRUE, TRUE, 0);
    gtk_box_pack_start (GTK_BOX, vbox), btn, TRUE, TRUE, 0);
    gtk_widget_show_all (win);
    gtk_main ();
```

创建了一个类型为 FileFileChooser 的组件并将其添加到窗口中。`gtk_file_chooser_button_new` 函数接受两个参数。第一个是应用于文件选择器窗口的标题。在这种情况下，我们想要打开一个现有文件，因此使用了 `GTK_FILE_CHOOSER_ACTION_OPEN`。另一种是选择一个现有文件夹，对应的代码为 `GTK_FILE_CHOOSER_ACTION_SELECT_FOLDER`。

`file-set` 信号连接到按钮上 —— 当用户做出选择时触发触发 —— 在该信号的处理函数中，调用了 `gtk_file_chooser_get_filename` 函数来读取文件名。

运行这段代码时，你会看到一个像这样的窗口：

![](img/6a7eee5b22417c3d49170130a20b16f2_123_0.png)

一个 GtkFileChooser

顶部按钮右侧的文件夹图标表示它是文件选择器；按钮的标题是当前选定的文件名，当程序首次运行时显示为“(None)”。如果你点击该按钮，将打开一个文件选择对话框：

## C 语言与 GUI 编程简介

![](img/6a7eee5b22417c3d49170130a20b16f2_124_0.png)

从 GtkFileChooserButton 打开的对话框用于选择现有文件提供了一个标准文件浏览器，因为我们是以“打开”模式打开窗口的，它只允许你选择系统中已存在的文件。使用浏览器选择文件并点击 Open。当窗口关闭时，按钮的标题将更新为选定的文件，并打印到启动终端。

你可以使用 GtkFileChooserButton 打开选择现有文件或文件夹的浏览器，但 GTK 的设计者认为你不能使用这种方法来选择保存新文件的地方。为此，你需要自己创建一个 Gtk 对话框。修改代码如下：

```
static void func(GtkWidget *btn, gpointer *ptr) {
    GtkWidget *sch = gtk_file_chooser_dialog_new ("Save",
        GTK_WINDOW(ptr), GTK_FILE_CHOOSER_ACTION_SAVE,
        "Cancel", GTK_RESPONSE_CANCEL, "Open", GTK_RESPONSE_ACCEPT);
    if (gtk_dialog_run(GTK_DIALOG(sch)) == GTK_RESPONSE_ACCEPT) {
        char *filename = gtk_file_chooser_get_filename(GTK_FILE_CHOOSER(sch));
        printf("Saved to %s\n", filename);
    }
    gtk_widget_destroy(sch);
}
```

```c
void main (int argc, char *argv[]) {
    gtk_init(&argc, &argv);

    GtkWidget *win = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_window_set_title(win, "FileChooser");
    GtkWidget *btn = gtk_button_new_with_label("Open");
    g_signal_connect(btn, "clicked", G_CALLBACK(end_program), NULL);

    g_signal_connect(win, "delete_event", G_CALLBACK(end_program), NULL);

    GtkWidget *vbox = gtk_vbox_new(FALSE, 5);
    GtkWidget *bbox = gtk_get_border_width(vbox);
    gtk_container_add(GTK_CONTAINER(win), vbox);
    gtk_container_set_border_width(GTK_CONTAINER(vbox), 10);

    GtkWidget *fc_btn = gtk_file_choose_button_new(
      GTK_FILE_CHOOSER_ACTION_OPEN);
    gtk_signal_connect(fc_btn,
      CALLBACK (file_selected), NULL);
    gtk_box_pack_start(GTK_BOX(vbox), fc_btn, TRUE, TRUE, 0);
    gtk_box_pack_start(GTK_BOX(vbox), btn, TRUE, TRUE, 0);
    gtk_widget_show_all(win);
    gtk_main();
}
```

创建了一个类型为 FileFileChooser 的组件并将其添加到窗口中。`gtk_file_chooser_button_new` 函数接受两个参数。第一个是应用于文件选择器窗口的标题。在这种情况下，我们想要打开一个现有文件，因此使用了 `GTK_FILE_CHOOSER_ACTION_OPEN`。另一种是选择现有文件夹，对应的代码为 `GTK_FILE_CHOOSER_ACTION_SELECT_FOLDER`。

`file-set` 信号连接到按钮上 —— 当用户做出选择时触发 —— 在该信号的处理函数中，调用了 `gtk_file_chooser_get_filename` 函数来读取文件名。

运行这段代码时，你会看到一个像这样的窗口：

![](img/6a7eee5b22417c3d49170130a20b16f2_123_0.png)

一个 GtkFileChooser

顶部按钮右侧的文件夹图标表示它是文件选择器；按钮的标题是当前选定的文件名，当程序首次运行时显示为“(None)”。如果你点击该按钮，将打开一个文件选择对话框：

在这种情况下，我们创建一个按钮来打开对话框，然后必须手动创建并打开对话框。

通过 `gtk_file_chooser_dialog_new` 创建对话框，其参数与 `gtk_dialog_with_buttons` 非常相似。首先提供对话框的标题，接着是父窗口指针，然后是一个决定对话框行为的标志（在这种情况下，被设置为提供一个可以保存文件的位置）。剩余的参数是对话框底部按钮的标签和返回值列表，以 NULL 结尾。

当按下按钮时，通过调用 `gtk_dialog_run` 创建对话框：按钮处理函数等待对话框返回：然后我们像处理文件打开对话框一样，使用 `gtk_file_chooser_get_filename` 从文件选择器中读取文件路径。

![](img/6a7eee5b22417c3d49170130a20b16f2_125_0.png)

## C 语言 GUI 编程简介

如果你运行这段代码并点击“Save file”按钮，你会发现文件保存选择器与文件打开选择器有不同，因为它有一个允许输入新文件名的框：

![](img/6a7eee5b22417c3d49170130a20b16f2_126_0.png)

用于选择新文件的 GtkFileChooserDialog

输入新文件名并选择新文件的位置，当你按下“OK”时，新文件的路径将打印到终端。

有时你需要允许用户选择一种颜色来决定如何高亮显示，例如：使用 GtkColorButton 可以轻松实现这一点

颜色在 GTK 中存储在 GdkColor 结构中，包含红、绿、蓝分量的独立值。因此，GtkColorButton 操作的是存储为 GdkColor 格式的数据。
