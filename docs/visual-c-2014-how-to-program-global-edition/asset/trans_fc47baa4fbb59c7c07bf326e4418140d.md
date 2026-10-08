
## 第 2 章 Visual Studio 简介与视觉编程

在表单上添加按钮。添加三个 `Text` 属性分别为“New User”、“Login”和“Forgot password”的按钮。按图所示更改它们的 `BackColor` 和 `ForeColor` 属性。
（计算器 GUI）如图图 2.38 所示创建 GUI。

2.9

![](img/57baed2319be0bb1b5f98674846f2711_102_0.png)

图 2.38 计算器 GUI。

- a) 操作表单属性。将表单的 `Text` 属性更改为 Calculator。将 `Font` 属性更改为 9pt Segoe UI。将表单的 `Size` 属性更改为 258, 210。
- b) 在表单上添加 TextBox。在属性窗口中将 TextBox 的属性设置为 0。拉伸 TextBox 并按图 2.38 所示的位置放置。将 `TextAlign` 属性设置为 Right 以使 TextBox 中显示的文本右对齐。
- c) 在表单上添加第一个 Panel。Panel 控件用于分组其他控件。向表单添加一个 Panel1。将 Panel 的 `BorderStyle` 属性更改为 Fixed3d，使 Panel 的尺寸呈现凹陷效果。将 `size` 属性更改为 90, 120。此 Panel1 将包含计算器的数字键。
- d) 在表单上添加第二个 Panel1。将 Panel 的 `BorderStyle` 属性更改为 Fixed3d。将 `size` 属性更改为 62, 120。此 Panel 将包含计算器的运算符。
- e) 在表单上添加第三个（最后一个）Panel。将 Panel 的 `BorderStyle` 属性更改为 Fixed3d。将 `size` 属性更改为 54, 62。此 Panel 将包含计算器的 C（清除）键和 C/A（全部清除）键。
- f) 在表单上添加按钮。计算器上有 20 个按钮。通过将按钮拖放到 Panel 上来向表单添加按钮。将按钮的 `Text` 属性更改为它所代表的计算器字符。你在 `Text` 中输入的值将显示在按钮表面。最后，使用 `Size` 属性调整按钮大小。标记为 0-9、*、/、-、和. 的按钮尺寸均为 23, 23。00 按钮尺寸为 52, 23。OFF 按钮尺寸为 54, 23。+ 按钮尺寸为 23, 21。C（清除）和 C/A（全部清除）按钮尺寸为 44, 23。

2.10

（闹钟 GUI）如图 2.39 所示创建闹钟 GUI。

![](img/57baed2319be0bb1b5f98674846f2711_102_1.png)

图 2.39 闹钟 GUI。

*

# 练习 103

- a) 操作表单属性。将表单的 `Text` 属性更改为 Alarm Clock，将 `Font` 属性更改为 9pt Segoe UI。将表单的大小更改为 430, 170。
- b) 在表单上添加按钮。向表单添加七个按钮。将每个按钮的 `Text` 属性更改为相应的文本。按所示对齐按钮。
- c) 在表单上添加 GroupBox。GroupBox 类似于 Panel，不同之处在于 GroupBox 有标题。将 `Text` 属性更改为 AM/PM，并将尺寸设置为 100, 50。在表单上水平居中 GroupBox。
- d) 在 GroupBox 中添加 RadioButton。在 GroupBox 中放置两个 RadioButton。将其中一个 RadioButton 的 `Text` 属性更改为 AM，另一个更改为 PM。按所示对齐 RadioButton。
- e) 在表单上添加 Label。向表单添加一个 Label 并将其 `Text` 属性更改为 00:00:00。将 `BorderStyle` 属性更改为 Fixed3d并将 `BackColor` 更改为黑色。使用 `Font` 属性使文本固定为 12pt。将 `Foreground` 更改为 Silver-1，使文本在黑色背景下脱颖。按所示位置放置 Label。

2.11（收音机 GUI）如图 2.40 所示创建 GUI。[注：本练习使用的图像位于本章的示例文件夹中]。

![](img/57baed2319be0bb1b5f98674846f2711_103_0.png)

- a) 操作表单属性。将 `Font` 属性更改为 9pt Segoe UI。将 `Text` 属性更改为 Radio 并 `Size` 更改为 427, 194。
- b) 添加预设电台组和按钮。设置 GroupBox 的 `Size` 及其 `Text` 为 Pre-Stations。向组添加六个按钮。将每个按钮的 `Size` 设置为 23, 23。分别将按钮的 `Text` 改为 1, 2, 3, 4, 5, 6。
- c) 添加扬声器组和选择框。设置 GroupBox 的 `Size` 为 120, 55，其 `Text` 为 Speakers。向 GroupBox 中添加两个 Checkbox。将 Checkbox 的属性设置为 Rear 和 Front。
- d) 添加电源/关闭按钮。向表单添加一个按钮。将其 `Text` 设置为 Power/off，`Size` 设置为 75。
- e) 添加电源/关闭按钮。（注：OCR 文本不完整/重复）。
