
```c
sigprocmask ( SIG_BLOCK, &block, NULL);

while ( strcmp ( buffer,"\n") != 0 )
{
    printf ("Enter a String: ");
    gets ( buffer);
    puts (buffer);
}
sigprocmask ( SIG_UNBLOCK, &block, NULL);
while ( 1 )
    printf ("\rProgram running\n" );
return 0; }
```

在这个程序中，我们为 `SIGINT`、`SIGTERM` 和 `SIGCONT` 注册了一个通用处理器。接下来，我们想在缓冲区中反复接受字符串并在屏幕上显示它们，直到用户从键盘输入“\n”。此外，我们希望这种输入活动不会被 `SIGINT` 或 `SIGTERM` 信号中断。然而，`SIGCONT` 应该是允许的。因此，在继续循环之前，我们必须阻塞 `SIGINT` 和 `SIGTERM` 信号。当我们通过循环后，取消这些信号的阻塞。这种信号的阻塞和取消可以通过 `sigprocmask()` 库来实现。

`sigprocmask()` 函数的第一个参数指定是阻塞还是取消阻塞一组信号。下一个参数是一个结构（`typedef sigset_t`）的地址，描述了我们要阻塞/取消阻塞的信号集。最后一个参数是在阻塞/取消阻塞之前设置现有信号集的变量。

有一些函数可以帮助我们填充 `sigset_t` 结构。`sigemptyset` 清空 `sigset_t` 变量，使其不引用任何信号。该函数接受的唯一参数是 `sigset_t` 变量的地址。我们使用这个函数来快速初始化空集。为了阻塞 `SIGINT` 和 `SIGTERM`，我们将它们添加到空信号集中。这可以通过 `sigaddset()` 库函数来实现。

这些信号。结果，任何挂挂的信号都会被立即传递给程序。因此，如果我们在接收输入的循环尚未结束时按下 Ctrl + C 或使用 `kill` 命令，这些信号将保持挂起状态。一旦我们完成循环，信号处理程序就会被调用。

# Let Us C

## 事件驱动编程

在理解了信号处理机制后，让我们看看 Linux 库如何利用信号来创建事件驱动的 GUI 程序。如你所知，在 GUI 程序中，事件通常发生在我们点击窗口、输入字符、关闭窗口、重绘窗口等时候。我们选择了 GTK 库 2.0 版本来创建 GUI 应用。这里，GTK 代表 Gimp Tool Kit。安装此工具包请参考附录 H。以下是使用该工具包在屏幕上创建一个窗口的第一个程序。

```c
/* mywindow.c */
#include <gtk/gtk.h>
int main ( int argc, char *argv[]) {
    GtkWidget *p;
    gtk_init (&argc, &argv);
    p = gtk_window_new (GTK_WINDOW_TOPLEVEL);
    gtk_window_set_title(p, "Sample Window");
    g_signal_connect (p, "destroy", gtk_main_quit, NULL);
    gtk_widget_set_size_request(p, 300, 300) ;
    gtk_widget_show (p);
    gtk_main();
    return 0;}
```

### 第 21 章：更多 Linux 编程

我们需要按照如下方式编译此程序：

```bash
gcc mywindow.c `pkg-config gtk+-2.0 --cflags --libs`
```

在这里，我们正在编译 `mywindow.c` 程序并将其与 GTK 工具包中必要的库进行链接。注意我们在命令中使用的引号。

以下是程序的输出...

![](img/0a2b9a1d8482fa3ff7aa8a4a25b7ce2b_702_0.png)

图 21.1

GTK 库提供了大量的函数，使我们能够很容易地创建 GUI 程序。GTK 下的每个窗口被称为小部件（widget）。要创建一个简单的窗口，我们必须执行以下步骤：

- (a) 通过调用 `gtk_init()` 函数初始化 GTK 库。该函数需要 `main()` 中接收到的命令行参数的地址。
- (b) 接下来，调用 `gtk_window_new()` 函数创建一个顶窗口。该函数取的唯一参数是要要创建的窗口类型。可以通过指定 `GTK_WINDOW_TOPLEVEL` 值来创建一个顶窗口。这会在内存中创建一个窗口并返回指向小部件对象的指针。小部件对象是一个结构体变量 `GtkWidget`，存储了包括它代表的窗口属性在内的信息。我们将此指针收集在一个名为 `p` 的 `GtkWidget` 结构指针中。
- (c) 通过调用 `gtk_window_set_title()` 函数为窗口设置标题。该函数的第一个参数是指向要设置标题窗口的 `GtkWidget` 指针。第二个参数是描述要在窗口标题中显示的文本的字符串。
- (d) 为 `destroy` 信号注册信号处理程序。每当我们尝试关闭窗口时，就会接收到 `destroy` 信号。`destroy` 信号处理器应该执行清理工作然后关闭应用程序。GTK 提供了一个名为 `gtk_main_quit()` 的现成函数来完成这项工作。我们只需要将此函数与 `destroy` 信号关联。这可以通过 `g_signal_connect()` 函数实现。该函数的第一个参数是要注册 `destroy` 信号处理程序的小部件指针。第二个参数是指定信号名称的字符串。第三个参数是信号处理例程的地址。我们没有使用第四个参数。
- (e) 使用 `gtk_widget_set_size_request()` 函数将窗口调整为所需的大小。第二个和第三个参数分别指定窗口的高度和宽度。
- (f) 使用 `gtk_widget_show()` 函数在屏幕上显示窗口。
- (g) 在循环中等待以接收窗口的事件。这可以通过 `gtk_main()` 函数完成。

另一个在窗口中绘制几个形状的程序又如何？这里是该程序...

```c
/* myshapes.c */
#include <gtk/gtk.h>
int expose_event ( GtkWidget *widget, GdkEventExpose *event )
{
  GdkGC *p;
  GdkPoint arr[5] = {250, 150, 250, 300, 350, 400, 400, 320, 190 };
  p = gdk_gc_new ( window ->window );
  gdk_draw_line ( window ->window, p, 10, 10, 200, 100 );
  gdk_draw_rectangle ( window ->window, p, TRUE, 10, 20, 200, 100 );
  gdk_draw_arc ( window ->window, p, TRUE, 200, 10, 200, 200, 2880, -2880 );
  gdk_draw_polygon ( window ->window, p, TRUE, arr, 5 );
  gdk_gc_unref ( p );
  return TRUE;
}
int main( int argc, char *argv[])
{
  GtkWidget *p;
  gtk_init (&argc, &argv );
  p = gtk_window_new ( GTK_WINDOW_TOPLEVEL );
  gtk_window_set_title ( p, "Sample Window" );
  g_signal_connect ( p, "destroy", gtk_main_quit, NULL );
  g_signal_connect ( p, "expose_event", expose_event, NULL );
  gtk_widget_set_size_request ( p, 500, 500 );
  gtk_widget_show ( p );
  gtk_main( );
  return 0; }
```
