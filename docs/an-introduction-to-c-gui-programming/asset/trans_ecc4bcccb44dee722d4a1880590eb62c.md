

## 数字调节旋按钮 (Spin buttons)

用户有多种输入数据的方式。通常，他们需要从多个选项中选择一个，而不是被给一个框并要求输入内容。GTK 为此目的提供了许多控件，它们与 GtkEntry、GtkSpinButton 密切相关。

数字调节旋按钮用于在特定范围内输入数值值。你可以指定最小值、最大值，以及每次按下按钮时数值变化的步长。这提供了一个文本输入控件——用户仍然可以向其中输入——同时也提供了一种更改值的方便方法。如果用户输入了超出你设置的范围的值，当你尝试读取它时，它会自动舍入到范围内最接近的值。

在上面的示例中，我们只需要更改一行代码即可将 GtkEntry 转换为 GtkSpinButton。将：

```
txt gtk_entry_new ();
```

替换为：

```
GtkObject *adj = gtk_adjustment_new (0, -10, 10, 1, 0, 0);
txt gtk_spin_button_new (GTK_ADJUSTMENT (adj), 0, 0);
```

这使得 txt 从 GtkEntry 变为 GtkSpinButton。我们可以看到 `gtk_spin_button_new` 函数的参数之一被称为 GtkAdjustment 的东西——它是什么？

GtkAdjustment 用于设置数字调节旋按钮（以及其他具有类似行为的控件）可以取值的值范围。`gtk_adjustment_new` 函数的参数按顺序指定了默认值（在本例中为 0）、最小值（-10）、最大值（10）和步长（1）。（最后两个参数指定“页增量”，用于那些有两组不同的按钮来更改值的情况——数字调节旋按钮不使用这些，因此它们可以设置为 0）。

GtkAdjustment 作为参数传递给 `gtk_spin_button_new` 函数。

另外两个参数是爬升速率——即按住按钮时值变化的速度——以及数值上显示的小数位数。

![](img/6a7eee5b22417c3d49170130a20b16f2_98_0.png)

-   用 GtkSpinButton 代替 GtkEntry

编译并运行新版本的代码，文本输入框现在右侧有两个小按钮；这些按钮可以用来更改值。你仍然可以向框内输入内容，如果你输入的值不是数字，或者超出了 GtkAdjustment 指定范围，当按下其中一个按钮（或“复制按钮”）时，它将被纠正为范围内的一个值。

## 切换按钮 (Toggle buttons)

获取用户输入的一种简单方法是使用按钮来选择选项。GTK 为此目的提供了几个控件，其中两个比较有用的是复选按钮（check buttons——可以被勾选或取消勾选的框）和单选按钮（radio buttons——在一组中同时只有一个成员处于激活状态的选择器）。它们都是 GtkToggleButton 控件的子控件，而该控件本身是我们已经使用过几次的 GtkButton 控件的子控件。切换按钮是一种处于已选中或未选中状态之一的按钮。

## 复选按钮 (Check buttons)

复选按钮是两者中最简单的，所以我们先看它们。一个 GtkCheckButton 是一个可以是空框也可以带有勾选标记的框；点击它可以在这两种状态之间切换。创建一个复选按钮就像这样简单：

```
GtkWidget *chk = gtk_check_button_new_with_label ("My check");
```

这创建了一个复选按钮以及其左侧一个带有提供文本的标签。（还有一个函数 `gtk_check_button_new`，它会创建一个不带标签的复选框——如果你在窗口的其他地方有它的标签，这会让事情更整洁。）尝试将上一个示例中的 `btn2` 替换为像 `chk` 的复选框——它看起来应该是这样：

![](img/6a7eee5b22417c3d49170130a20b16f2_99_0.png)

窗口右上角的复选按钮

默认情况下，新建的复选按钮处于未勾选状态。要勾选按钮，你调用：

```
gtk_toggle_button_set_active(GTK_TOGGLE_BUTTON (chk), TRUE);
```

将按钮的激活状态设置为 TRUE 会勾选方框，设置为 FALSE 则会取消勾选。有一个相应的函数来读取切换按钮的激活状态——要将复选按钮当前是否被勾选读取到一个变量中，请执行：

# C语言编程入门

```
int state = gtk_toggle_button_get_active(GTK_TOGGLE_BUTTON (chk));
```

如果按钮被勾选，state 的值将为1，否则为 0。

你也可以通过 `signal_connect` 为复选按钮的 `toggled` 信号连接一个处理函数——这等于我们在之前的示例中看到的连接到普通 GtkButton 的 `clicked` 信号：

```
g_signal_connect(chk, "toggled", G_CALLBACK(check_toggle), NULL);
```

`toggled` 用的处理函数如下：

```
void check_toggle(GtkWidget *wid, gpointer ptr)
{
    printf("The state of the button is %d", gtk_toggle_button_get_active(GTK_TOGGLE_BUTTON (wid)));
}
```

注意，toggled 信号的第一个参数是控件本身，第二个是信号名称，第三个是回调函数。第四个参数用于传递给回调函数的数据。

## 单选按钮 (Radio buttons)

单选按钮可以被视为一组，其中一次只有一个能被选中。单选按钮和复选按钮之间的区别在于，单选按钮需要关联到一个组才能使链接生效。以下是创建一个组并向其中添加单选按钮的方法：

```
GtkButtonGroup *group = gtk_button_group_new();
GtkWidget *rad1 = gtk_radio_button_new_with_label(group, "Button 1");
GtkWidget *rad2 = gtk_radio_button_new_with_label(group, "Button 2");
```

组中的每个按钮都需要与组中的另一个链接。如果你正确链接了它们，那么当你点击“Button 2”时，它会被选中而“Button 1”会被取消选中，反之亦然。

![](img/6a7eee5b22417c3d49170130a20b16f2_101_0.png)

窗口顶部的两个 GtkButton

## 第19章

## 下拉框 (Combo boxes) 与列表存储

创建下拉框并与其关联列表存储

像数字调节旋按钮、单选按钮和复选按钮这样的控件允许用户在较少选项之间进行选择，但有时我们需要提供更多选项。下拉框是为用户提供选择范围而不占用大量空间的好方法；GTK 提供了两种类型的下拉框。

### 文本下拉框

更简单的下拉框类型是 GtkComboBoxText，它允许每个选项仅纯文本。以下是创建它的方法：

```
GtkWidget *comb = gtk_combo_box_text_new ();

gtk_combo_box_text_append_text (comb, "Option 1");
gtk_combo_box_text_append_text (comb, "Option 2");
gtk_combo_box_text_append_text (comb, "Option 3");

gtk_combo_box_set_active (comb, 0);
```

`gtk_combo_box_text_new` 函数创建一个空的下拉框，可以使用 `gtk_combo_box_text_append_text` 向其添加项目（按照它们应该出现的顺序，从上到下）。

最后所示的函数调用 `gtk_combo_box_set_active` 设置了下拉框的初始值——在本例中，设置为 0 选择了第一个添加到下拉框的选项。

