
```cpp
FindFileDialog::FindFileDialog(QWidget *parent)
: QDialog(parent)
{
    namedLabel->setGeometry(9, 9, 50, 25);
    namedLineEdit->setGeometry(65, 9, 200, 25);
    lookInLabel->setGeometry(9, 40, 50, 25);
    lookInLineEdit->setGeometry(65, 40, 200, 25);
    subfoldersCheckBox->setGeometry(9, 40, 50, 25); // 原文如此
}
```

# 第二部分：进阶 Qt

## 6. 布局管理

![](img/5a524abdf0b0d58fa99d30abb4463611_225_0.png)

- 在表单上布局部件
- 堆叠布局 `Stacked Layouts`
- 分隔器 `Splitters`
- 滚动区域 `Scrolling Areas`
- 停靠窗口和工具栏 `Dock Windows and Toolbars`
- 多文档界面 `Multiple Document Interface`

放置在表单上的每个部件都必须赋予适当的大小和位置。Qt 几个在表单上布局部件的类：`QHBoxLayout`、`QVBoxLayout`、`QGridLayout` 和 `QStackedLayout`。这些类如此方便易用，几乎每个 Qt 开发者都会通过源代码或通过 Qt Designer 使用它们。

使用 Qt 布局类的另一个原因是它们确保表单能够自动适应不同的字体、语言和平台。如果用户更改系统字体设置，应用程序的表单将立即响应，并在必要时调整自身大小。如果你将应用程序的用户界面翻译成其他语言，布局类会考虑部件翻译后的内容以避免文本截断。

其他执行布局管理的类还包括 `QSplitter`、`QScrollArea`、`QMainWindow` 和 `QMdiArea`。所有这些类都提供了用户可以操作的灵活布局。例如，`QSplitter` 提供了一个分隔条，用户可以拖动它来调整部件的大小，而 `QMdiArea` 提供对 MDI（多文档界面，一种在应用程序主窗口内同时显示多个文档的方法）的支持。由于它们经常作为正式布局的替代方案，我们在本章中介绍了它们。

# 在表单上布局部件

管理表单部件布局有三种基本方法：绝对定位、手动布局和布局管理器。我们将查看每一个：

在子部件上。如果子部件的尺寸提示 `size hint` 发生变化，布局将自动重新生成，并考虑新的尺寸提示。此外，布局管理器根据表单子部件的最小尺寸和尺寸提示，自动为整个表单设置最小尺寸。

在目前为止介绍的示例中，我们简单地将部件放入布局中，并使用间隙器 `stretches` 来消耗任何额外的空间。在某些情况下，这不足以让布局看起来完全符合我们的预期。在这些情况下，我们可以通过更改正在布局部件的尺寸策略和尺寸提示来调整布局。

部件的尺寸策略 `size policy` 告诉布局系统如何拉伸或收缩。Qt 为所有内置部件提供了合理的默认尺寸策略，但由于没有一个默认值可以兼顾所有可能的布局，开发者更改表单上一两个部件的尺寸策略仍然很常见。`QSizePolicy` 包含水平和垂直两个部分。以下是最有用的值：

- **Fixed** `Fixed` 意味着部件不能增大或缩小。部件始终保持其尺寸提示的大小。
- **Minimum** `Minimum` 意味着部件的尺寸提示是其最小尺寸。部件不会缩小到尺寸提示以下，但必要时它可以增大以填充可用空间。
- **Maximum** `Maximum` 意味着部件的尺寸提示是其最大尺寸。部件可以缩小到其最小尺寸提示。
- **Preferred** `Preferred` 意味着部件的尺寸提示是其首选尺寸，但必要时部件仍可以缩小或增大。
- **Expanding** `Expanding` 意味着部件的尺寸提示可以缩小或增大，并且它特别倾向于增大。

图 6.4 总结了不同尺寸策略的含义，并以一个显示文本“Some Text”的 `QLabel` 为例。

## 图 6.4. 不同尺寸策略的含义

| | 最小尺寸提示 | 尺寸提示 | |
|---|---|---|---|
| Fixed | | Some Text | |
| Minimum | | Some Text | Some Text |
| Maximum | Some | Some Text | |
| Preferred | Some | Some Text | Some Text |
| Expanding | Some | Some Text | Some Text |

`Expanding` 的方式相同。当一个同时包含 `Preferred` 和 `Expanding` 部件的表单被调整大小时，额外的空间会分配给 `Expanding` 部件，而 `Preferred` 部件保持其尺寸提示大小。

还有两种尺寸策略：`MinimumExpanding` 和 `Ignored`。前者在 Qt 的某些版本中是必要的，但现在不再需要了；首选的方法是使用 `Expanding` 并重新实现 `minimumSizeHint()`。后者与 `Expanding` 类似，但它忽略了部件的尺寸提示和最小尺寸提示。

除了尺寸策略的水平和垂直部分外，`QSizePolicy` 类还存储了水平和垂直的拉伸因子 `stretch factor`。这些拉伸因子可以用于指示当表单扩展时，不同的子部件以不同的速率增长。例如，如果我们在一个 `QTextEdit` 上方有一个 `Qtree`，并且我们希望 `QTextEdit` 的高度是 `Qtree` 的两倍，我们可以将 `QTextEdit` 的垂直拉伸因子设为 2，将 `Qtree` 的垂直拉伸因子设为 1。

影响布局的另一种方法是在子部件上设置最小尺寸、最大尺寸或固定尺寸。布局管理器在布局部件时将遵守这些约束。如果这还不够，我们始终可以派生子部件的类并重新实现 `sizeHint()` 来获取所需的尺寸提示。
