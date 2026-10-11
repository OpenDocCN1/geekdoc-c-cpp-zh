
`gtk_box_pack_start` 的第三个参数称为 `expand`。如果设置为 `TRUE`，那么当窗口增大时，分配给此小部件的空间也会按比例增大。如果设置为 `FALSE`，分配给此小部件的空间永远不会超过所需的最小空间。

第四个参数称为 `fill`。如果 `expand` 设置为 `FALSE`，则它没有作用；但如果 `expand` 设置为 `TRUE`，它将控制是分配给小部件的空间还是小部件本身增长。如果 `expand` 为 `TRUE` 且 `fill` 为 `FALSE`，小部件本身的大小保持不变；如果 `expand` 和 `fill` 均为 `TRUE`，小部件本身将增长以填满增加的空间。

写下来这些可能很难理解，但几个例子将有助于理清思路。在上面的示例中，将 `GtkHB` 改回 `GtkVBox`，然后将示例中三个 `gtk_box_pack_start` 调用的 `expand` 和 `fill` 都设置为 `FALSE`。如果你调整窗口大小，标签和两个按钮将保持在窗口顶部相同的高度。

![](img/6a7eee5b22417c3d49170130a20b16f2_91_0.png)

所有小部件的 `expand` 和 `fill` 均设置为 `FALSE` 的布局

现在尝试相同的操作，但将 `btn` 的 `gtk_box_pack_start` 中的 `expand` 参数设置为 `TRUE`：

![](img/6a7eee5b22417c3d49170130a20b16f2_92_0.png)

“关闭窗口”按钮 `expand` 设置为 `TRUE` 且 `fill` 设置为 `FALSE` 的布局

按钮现在向下移动以适应增加空间的中间部分，额外空间已分配给按钮，但按钮本身的大小保持不变。

最后，尝试将 `btn` 的 `expand` 和 `fill` 都设置为 `TRUE`，查看与上方图片类似的结果。

![](img/6a7eee5b22417c3d49170130a20b16f2_93_0.png)

“关闭窗口”按钮 `expand` 和 `fill` 均设置为 `TRUE` 的布局

现在增大窗口会导致整个按钮填满额外空间。

我们可以看到，这些参数只影响小部件的垂直尺寸；这是因为它们被使用在 `GtkVBox` 中。如果我们也想控制小部件的水平尺寸，我们需要创建一个包含一组 `GtkBoxes` 的 `GtkBox`，然后用这些容器来包含小部件本身。

`gtk_box_pack_start` 调用中的最后一个参数称为 `padding` —— 这是在小部件两端插入的自由空间（以像素为单位），这是在 `gtk_box_new_call` 中请求的所有小部件之间的 `spacing` 之外的。

通过仔细调整 `expand`、`fill` 和 `padding` 参数，你可以创建一个整齐显示所有小部件并完全按照你的预期调整大小的窗口。

# 表格

你可能好奇如何在一个每两行的窗口中放置四个项目。嗯，将一个 `GtkHBox` 作为 `GtkVBox` 内部的项目之一是完全可以的，反之亦然。将一个 `GtkHBox` 作为 `GtkHBox` 内部的项目也是可以的（但通常没什么意义）。通过使用嵌套 `GtkHBoxes` 和 `GtkVBoxes` 的组合，你可以按照想要的方式布局窗口中的所有小部件。

嵌套 `GtkBoxes` 和 `GtkVBoxes` 在两个维度上布局小部件的效果非常好，并且实际上能让你对它们的外观拥有最好的控制。其实有一种更简单的替代方案：`GtkTable` 小部件。

`GtkTable` 是一个二维框，在创建时定义为具有特定数量的行和列。小部件可以位于各种行列坐标。这不如使用嵌套的 `GtkBoxes` 和 `GtkVBoxes` 灵活，因为每个小部件必须在行和列上对齐——这意味着任何一行的高度至少与该行中最高的小部件一样，任何一列的宽度至少与该列中最宽的小部件一样，这可能导致大量的空间浪费。但很多时候，这种简单的布局就足够了，`Table` 的工作得良好。

如果我们使用 `GtkTable` 来定位标签和按钮，我们的示例将更改如下：

```c
void main (int argc, char *argv[])

{

    gtk_init(&argc, &argv);

    GtkWidget *win = gtk_window (GTK_WINDOW_TOPLEVEL);

    GtkWidget *btn = gtk_button_with_label ("Click me");

    g_signal_connect(btn, G_CALLBACK (end_program), NULL);

    g_signal_connect(win, G_CALLBACK (end_program), NULL);

    GtkWidget *lbl = gtk_label_new ("My label");

    GtkWidget *btn2 = gtk_button_with_label ("Button 2");

    g_signal_connect(btn2, G_CALLBACK (count_button), lbl);

    GtkWidget *table = gtk_table_new (2, 2, TRUE);

    gtk_table_attach_defaults (GTK_TABLE (table), lbl, 0, 1, 0, 1);

    gtk_table_attach_defaults (GTK_TABLE (table), btn2, 1, 2, 0, 1);

    gtk_table_attach_defaults (GTK_TABLE (table), btn, 0, 2, 1, 2);

    gtk_container_add (GTK_CONTAINER (win), table);

    gtk_widget_show_all (win);

    gtk_main ();

}
```

我们通过以下代码创建一个新的 `GtkTable`：

```c
GtkWidget *tbl = gtk_table_new (2, 2, TRUE);
```

`gtk_table_new` 函数的参数是行数和列数。要向表格中插入小部件，我们使用：

```c
gtk_table_attach_defaults (GTK_TABLE (tbl), lbl, 0, 1, 0, 1);
```

我们将表格和要放入其中的小部件作为参数传递。接下来的数字是小部件附加到表格上的坐标——按顺序它们是左边缘和右边缘的位置，然后是顶部和底部边缘。这把小部件放置在第一列（在 x 0 到 1 之间）和第一行（在 y 0 到 1 之间）。注意，你可以让小部件跨越多行或多列，就像 `btn` 放置的方式：

```c
gtk_table_attach_defaults (GTK_TABLE (tbl), btn, 0, 2, 1, 2);
```

在这种情况下，小部件跨越了第一列和第二列，因为它在左侧附加于 0，右侧附加于 2。为了完整性，请注意 `gtk_table_attach_defaults` 是函数 `gtk_table_attach` 的简化版本，后者具有许多其他选项。这些其他选项包括为每个小部件提供扩展、填充和设置 `padding` 的功能，就像上一章描述的 `gtk_box_pack` 函数一样。但这些函数写起来很麻烦——使用 `gtk_table_attach_defaults` 会将每个小部件的 `padding` 设置为 0 并将 `expand` 设置为 `TRUE`。如果你编译并运行此代码，你将得到一个像下面的窗口。注意，“关闭窗口”按钮如上所述跨越了表格的两个列。

img/6a7eee5b22417c3d49170130a20b16f2_95_0.png)

`GtkTable` 允许小部件在行列中对齐，使用户可以使用选择框和单选按钮输入文本并选择选项。我们已经看到可以使用标签在窗口上显示文本，但如果我们想读取用户输入的某些文本怎么办？GTK 提供了 `GtkEntry` 小部件来实现。

# 文本输入

修改上面的示例代码，在表格中添加带有 `GtkEntry` 小部件的新单元格，如下所示：

```c
#include <gtk/gtk.h>

GtkWidget *txt;

void end_program(GtkWidget *wid, gpointer ptr)

{

    gtk_main_quit();

}

void edit(GtkWidget *wid, gpointer ptr)

{

    const char *input = gtk_entry_get_text(GTK_ENTRY(txt));

    gtk_label_set_text(GTK_LABEL(ptr), input);

}

void main(int argc, char *argv[])

{

    gtk_init(&argc, &argv);

    GtkWidget *win = gtk_window_new(GTK_WINDOW_TOPLEVEL);

    GtkWidget *btn = gtk_button_new_with_label("edit");

    gtk_signal_connect(btn, "clicked", G_CALLBACK(end_program), NULL);

    gtk_signal_connect(win, "delete_event", G_CALLBACK(end_program), NULL);

}
```

```c
GtkWidget *lbl = gtk_label_new ("My label");
```

```c
GtkWidget *btn2 = gtk_button_new_with_label ("Button 2");

g_signal_connect(btn2, "clicked", G_CALLBACK(edit), lbl);
```

```c
txt = gtk_entry_new();
```

```c
GtkWidget *tab = gtk_table_new (2, 2, TRUE);

gtk_table_attach_defaults (GTK_TABLE (tab), lbl, 0, 0, 1, 1);

gtk_table_attach_defaults (GTK_TABLE (tab), btn2, 1, 0, 0, 1);

gtk_table_attach_defaults (GTK_TABLE (tab), win, 0, 1, 1, 2); // 注意：此处原文误为win

gtk_table_attach_defaults (GTK_TABLE (tab), txt, 1, 1, 1, 1);
```

在这个示例中，我们将 `GtkEntry` 小部件的指针 `txt` 声明为全局变量。这是因为我们需要从按钮处理程序访问它，而在这种情况下处理程序也需要访问标签小部件。我们之前使用 `g_signal_connect` 函数中的通用指针将小部件信息传递给处理程序，但对于两个独立的小部件，我们只有一个指针（有很多方法可以使用单个指针，但使用全局变量更容易理解）。

我们添加了一个新函数 `copy_text`，它使用函数 `gtk_entry_get_text` 获取指向文本缓冲区的指针，缓冲区存储了用户在输入框中输入的任何内容。注意这个字符缓冲区带有 `const` 修饰符——这表示程序员无法更改它。然后我们将此缓冲区传递给 `gtk_label_set_text`，它会将 `GtkEntry` 的内容复制到 `GtkLabel`。

最后，我们通过 `gtk_entry_new` 创建 `GtkEntry` 本身，并将其添加到表格中（注意我们移动了 `btn` 的附加点，使其只占据表格的一个单元格而不是两个，以便为 `GtkEntry` 留出足够的空间）。

编译并运行代码；在输入框中输入内容并按下“复制”按钮，看看会发生什么。

img/6a7eee5b22417c3d49170130a20b16f2_97_0.png)

添加到表格右下角的 `GtkEntry`

## 数字调节旋按钮 (Spin buttons)

用户有多种输入数据的方式。通常，他们需要从多个选项中选择一个，而不是被给一个框并要求输入内容。GTK 为此目的提供了许多控件，它们与 `GtkEntry`、`GtkSpinButton` 密切相关。

数字调节旋按钮用于在特定范围内输入数值值。你可以指定最小值、最大值，以及每次按下按钮时数值变化的步长。这提供了一个文本输入控件——用户仍然可以向其中输入——同时也提供了一种更改值的方便方法。如果用户输入了超出你设置的范围的值，当你尝试读取它时，它会自动舍入到范围内最接近的值。

在上面的示例中，我们只需要更改一行代码即可将 `GtkEntry` 转换为 `GtkSpinButton`。将：

```c
txt gtk_entry_new ();
```

替换为：

```c
GtkObject *adj = gtk_adjustment_new (0, -10, 10, 1, 0, 0);

txt gtk_spin_button_new (GTK_ADJUSTMENT (adj), 0, 0);
```

这使得 `txt` 从 `GtkEntry` 变为 `GtkSpinButton`。我们可以看到 `gtk_spin_button_new` 函数的参数之一被称为 `GtkAdjustment` 的东西——它是什么？

`GtkAdjustment` 用于设置数字调节旋按钮（以及其他具有类似行为的控件）可以取值的值范围。`gtk_adjustment_new` 函数的参数按顺序指定了默认值（在本例中为 0）、最小值（-10）、最大值（10）和步长（1）。（最后两个参数指定“页增量”，用于那些有两组不同的按钮来更改值的情况——数字调节旋按钮不使用这些，因此它们可以设置为 0）。

`GtkAdjustment` 作为参数传递给 `gtk_spin_button_new` 函数。

另外两个参数是爬升速率——即按住按钮时值变化的速度——以及数值上显示的小数位数。

![](img/6a7eee5b22417c3d49170130a20b16f2_98_0.png)

-   用 `GtkSpinButton` 代替 `GtkEntry`

编译并运行新版本的代码，文本输入框现在右侧有两个小按钮；这些按钮可以用来更改值。你仍然可以向框内输入内容，如果你输入的值不是数字，或者超出了 `GtkAdjustment` 指定范围，当按下其中一个按钮（或“复制按钮”）时，它将被纠正为范围内的一个值。

## 切换按钮 (Toggle buttons)

获取用户输入的一种简单方法是使用按钮来选择选项。GTK 为此目的提供了几个控件，其中两个比较有用的是复选按钮（check buttons——可以被勾选或取消勾选的框）和单选按钮（radio buttons——在一组中同时只有一个成员处于激活状态的选择器）。它们都是 `GtkToggleButton` 控件的子控件，而该控件本身是我们已经使用过几次的 `GtkButton` 控件的子控件。切换按钮是一种处于已选中或未选中状态之一的按钮。

## 复选按钮 (Check buttons)

复选按钮是两者中最简单的，所以我们先看它们。一个 `GtkCheckButton` 是一个可以是空框也可以带有勾选标记的框；点击它可以在这两种状态之间切换。创建一个复选按钮就像这样简单：

```c
GtkWidget *chk = gtk_check_button_new_with_label ("My check");
```

这创建了一个复选按钮以及其左侧一个带有提供文本的标签。（还有一个函数 `gtk_check_button_new`，它会创建一个不带标签的复选框——如果你在窗口的其他地方有它的标签，这会让事情更整洁。）尝试将上一个示例中的 `btn2` 替换为像 `chk` 的复选框——它看起来应该是这样：

![](img/6a7eee5b22417c3d49170130a20b16f2_99_0.png)

窗口右上角的复选按钮

默认情况下，新建的复选按钮处于未勾选状态。要勾选按钮，你调用：

```c
gtk_toggle_button_set_active(GTK_TOGGLE_BUTTON (chk), TRUE);
```

将按钮的激活状态设置为 `TRUE` 会勾选方框，设置为 `FALSE` 则会取消勾选。有一个相应的函数来读取切换按钮的激活状态——要将复选按钮当前是否被勾选读取到一个变量中，请执行：

# C语言编程入门

```c
int state = gtk_toggle_button_get_active(GTK_TOGGLE_BUTTON (chk));
```

如果按钮被勾选，`state` 的值将为1，否则为 0。

你也可以通过 `signal_connect` 为复选按钮的 `toggled` 信号连接一个处理函数——这等于我们在之前的示例中看到的连接到普通 `GtkButton` 的 `clicked` 信号：

```c
g_signal_connect(chk, "toggled", G_CALLBACK(check_toggle), NULL);
```

`toggled` 用的处理函数如下：

```c
void check_toggle(GtkWidget *wid, gpointer ptr)

{

    printf("The state of the button is %d", gtk_toggle_button_get_active(GTK_TOGGLE_BUTTON (wid)));

}
```
