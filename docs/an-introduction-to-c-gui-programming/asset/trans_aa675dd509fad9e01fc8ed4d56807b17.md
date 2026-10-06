

## 第15 章

## 按钮

通过添加按钮让你的空窗口变得更有趣且更具交互性

我们在上一章节中看到的简单程序在屏幕上画出了一个窗口，但它看起来非常单调。还有一个问题是，用 X 按钮关闭窗口时，程序仍在运行。我们将通过添加一个关闭窗口的按钮来解决这两个问题。

按钮是另一个标准的 GTK 控件，它支持你预期的所有功能——你可以给它设置一个标签；当你点击它时可以看到它的外观发生变化；你可以使用键盘快捷键激活它；你还可以临时禁用并将其显示为灰色。

第一要工作是将按钮添加到窗口中。完成后，我们就可以考虑让它变得有用。

将上一个示例的代码修改为：

```c
#include <gtk/gtk.h>

void main (int argc, char *argv[])
{
    gtk_init (&argc, &argv);
    Gtkwidget *win = gtk_window_new (GTK_WINDOW_TOPLEVEL);
    GtkWidget *btn = gtk_button_new_with_label ("Click me");
    gtk_container_add (GTK_CONTAINER (win), btn);
    gtk_widget_show_all (win);
    gtk_main();
}
```

让我们来看看这些：

```c
GtkWidget *btn = gtk_button_new_with_label ("Click me");
```

这创建了一个 GtkButton 控件。虽然有一个标准的 `gtk_button_new` 函数，但使用这个版本 `gtk_button_new_with_label` 允许我们能够在创建按钮的同时为按钮添加一个标签。

```c
gtk_container_add (GTK_CONTAINER (win), btn);
gtk_widget_show_all (win);
```

最后，对 `gtk_widget_show` 的调用被替换为 `gtk_widget_show_all` —— 这告诉 GTK 显示该控件以及它包含的任何控件；如果这一行没有更改，窗口将会显示，但按钮将保持隐藏。如果你编译并运行代码，你会发现显示有一个标记为“Click me”按钮的窗口：

![](img/6a7eee5b2241c3d49f0a2b81.png)

## 容器

在示例中，我们使用该行将按钮放入窗口中。正如你可能注意到的，GTK 中的每个函数调用都以 `gtk_` 前缀开头，随后是它所操作的控件类型名称——`gtk_window_new` 创建一个 GtkWindow 类型的控件。因此，此函数调用操作的是 GtkContainer 类型的属性，但我们将其应用于 `win`，而它是一个 GtkWindow。

GTK 内部存在控件类型的层级结构，控件类型继承其在层级中的父类型，该类型可以被描述为上方控件类型的子。因为 GtkContainer 是 GtkWindow 的父类型之一，你可以在 Gtk 控件上使用 gtk_container 函数。这样将一个控件放入另一个控件内部是我们经常需要的操作。你会注意到，当 `win` 作为参数传递给 `gtk_container_add` 函数时，它被封装在 `GTK_CONTAINER()` 函数内部——这会将参数转换为 GTK_CONTAINER 类型的变量，告诉函数将 `win` 视为一个 GtkContainer。如果不包含这个函数，代码仍然可以工作，但编译器会报错！（GTK 为每种类型的控件都提供了一个函数，因为将控件转换为不同的类型是非常常见的。）

## 信号

如果你运行应用程序，你可以用鼠标点击按钮，它会高亮显示已被点击。你也可以按下键盘上的 ENTER 键来执行相同的操作——其行为与我们在应用程序中常见的按钮完全相同，但它实际上仍然没有执行任何操作。下一步是修复这个问题。

这样做的方法是将处理函数连接到按钮被点击时产生的信号上。

这里是添加了处理函数的代码：

```c
#include <gtk/gtk.h>

void end_program(GtkWidget *wid, gpointer ptr) {
    gtk_main_quit();
}

void main (int argc, char *argv[]) {
    gtk_init(&argc, &argv);
    GtkWidget *win = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    GtkWidget *btn = gtk_button_new_with_label("Click");
    g_signal_connect(btn, "clicked", G_CALLBACK(end_program), NULL);
    gtk_container_add(GTK_CONTAINER, win, btn);
    gtk_widget_show_all(win);
    gtk_main();
}
```

处理函数（通常称为回调函数）名为 `end_program`，它所做的只是调用 GTK 函数 `gtk_main_quit` ——如该名称所示的那样，该函数退出 `gtk_main` 内部循环并允许程序结束。

```c
g_signal_connect(btn, "destroy", G_CALLBACK(end_program), NULL);
```

这一行将处理函数（end_program）连接到名为 "clicked" 的信号，该信号在按钮控件被鼠标点击时由其发射。我们使用 `GTK_CALLBACK` 函数来确保编译器知道 `end_program` 函数是一个有效的回调。不过这并不完美——如果我们点击 X 按钮，窗口会关闭但程序不会退出。让我们通过将另一个处理函数连接到点击 X 时产生的信号来修复这个问题。

