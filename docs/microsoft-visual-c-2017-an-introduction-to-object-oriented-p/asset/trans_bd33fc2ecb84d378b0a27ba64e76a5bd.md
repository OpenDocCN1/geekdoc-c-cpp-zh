

（续）

| 事件 |  |
| --- | --- |
| Leave | 当控件失去焦点时触发 |
| LocationChanged | 当 Location 属性值发生变化时触发 |
| LostFocus | 当控件失去焦点时触发 |
| MouseDown | 当鼠标指针悬停在控件上并按下鼠标键时触发 |
| MouseEnter | 当鼠标指针进入控件时触发 |
| MouseHover | 当鼠标指针悬停在控件上时触发 |
| MouseLeave | 当鼠标指针离开控件时触发 |
| MouseMove | 当鼠标指针在控件上移动时触发 |
| MouseUp | 当鼠标指针悬停在控件上并释放鼠标键时触发 |
| MouseWheel | 当控件具有焦点时滚动鼠标轮时触发 |
| Move | 当控件移动时触发 |
| Resize | 当控件大小发生变化时触发 |
| TextChanged | 当 Text 属性值发生变化时触发 |
| VisibleChanged | 当 Visible 属性值发生变化时触发 |

表 13-1 某些控件公共实例事件

你已经使用 IDE 创建了事件处理方法。这些方法是在 IDE 中双击控件时生成的事件。例如，你为 Button 创建了 `Click()` 方法，并为 LinkLabel 创建了 `LinkClicked()` 方法。Form 可以包含任意数量的控件，这些控件可能关联有事件。此外，单个控件可能会触发任意数量的事件。例如，除了创建按钮的默认 `Click` 事件外，你可能还想在用户鼠标滑过按钮时定义各种操作。表 13-1 仅列出了控件支持的许多事件中的少数几个；理论上，任何控件都可以触发任何可用事件。

假设你想创建一个项目，该项目在鼠标悬停在按钮上和点击按钮时具有不同的操作集。图 13-18 显示了一个在 IDE 中启动的项目。已经执行了以下操作：

- * Form 调整了大小。*
- Form 的 Text 属性被更改了。
- 将一个 Button 拖到 Form 上，并将其 Text 设置为 "Click me"。
- 向 Form 中添加了一个 Label，将其 Text 设置为 "Hello"，并增大了字体。

## 句控件组件事件

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_649_0.png)

图 13-1 在 IDE 中启动 ButtonTwoEvents 项目

当你在 IDE 中双击 Form 上的 Button时，你会生成一个 `Click()` 方法的骨架。你可以更改方法的标识符使其以大写字母开头，然后添加语句，在用户点击按钮时更改 Label 的文本和颜色，如下所示：

```sharp
private void Button1_Click(object sender, EventArgs e)
{
    label1.Text = "Button was clicked";
    label1.BackColor = Color.CornflowerBlue;
}
```

> Color.CornflowerBlue 是 C# 的预定义颜色属性之一。完整列表见第 12 章的表 12-5。

当屏幕右侧选中 Button 时，你可以点击属性窗口中的 Events 图标。Events 图标看起来像一个闪电符号。图 13-19 显示属性窗口显示的是事件而不是属性，并且 Click 事件关联有一个方法。

## 第 13 章 处理事件

如果你滚动查看属性窗口中列出的事件，你可以看到各种事件选择。如果你向下滚动到 MouseEnter 并双击，你可以查看到 Form1.cs 文件中的事件处理程序代码，如下：

```sharp
private void button1_MouseEnter(object sender, EventArgs e)
{
}
```

你在属性窗口中查看事件时，可以通过点击 Properties 图标返回属性列表。该图标位于 Events 图标的左侧。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_650_0.png)

图 13-19 显示事件的属性窗口

你可以重命名方法使其以大写字母开头，并在此方法内输入任何你需要的语句：例如，你可能会编写以下方法：

```sharp
private void Button1_MouseEnter(object sender, EventArgs e)
{
  label1.Text = "Go ahead";
  button1.BackColor = Color.Red;
}
```

当你运行带有这两个新方法的程序时，会发生不同的事件：

- 当鼠标进入按钮（即鼠标滑过按钮）时，Label 的 Text 更改为 "Go ahead"，按钮变为红色，如图 13-20 左侧所示。
- 点击按钮后，Label 的 Text 再次更改为 "Button was clicked"，Label 变为蓝色，如图 13-20 右侧所示。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_650_1.png)

图 13-20 鼠标进入按钮和在点击按钮后的 OneEvents 程序

Copyright 2018 Cengage Learning. 版权所有。未经许可不可全部或部分复制、扫描或复制。WCN-02-200-252.

