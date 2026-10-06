
-   这是用户第一次调用查找对话框。
-   查找对话框之前调用过，但用户将其关闭了。
-   查找对话框之前调用过，且目前仍然可见。

如果查找对话框不存在，我们就创建它，并将 `findNext()` 和 `findPrevious()` 信号连接到相应的表格槽（slots）。虽然我们在 `MainWindow` 构造函数中创建了该对话框，但延迟其创建可以使应用程序启动更快。此外，如果从未使用该对话框，它就不会被创建，从而节省了时间和内存。

然后我们调用 `show()`、`raise()` 和 `activateWindow()` 来确保窗口可见并位于其他窗口之上。仅调用 `show()` 就足以让隐藏的窗口显示并置顶，但查找对话框可能在不可见时被调用。在这种情况下，`show()` 将无效，我们必须调用 `raise()` 和 `activateWindow()` 使窗口置顶并处于激活状态。另一种写法是成：

```cpp
if (findDialog->isHidden()) {
    findDialog->show();
} else {
    findDialog->raise();
    findDialog->activateWindow();
}
```

但这在编程上等同于在过单行道之前左右看两侧。

我们现在来看图 3.13 所示的“跳转单元”对话框。我们希望用户弹出它、使用并关闭它，而无法切换到应用程序中的任何其他窗口。这意味着“跳转单元”对话框必须是**模态的**（modal）。模态窗口是在调用时弹出并阻塞应用程序，在窗口关闭之前阻止任何其他处理或交互发生。我们之前使用的文件对话框和消息框都是模态的。

# 图 3.13 表格应用程序的“跳转单元”对话框

![](img/5a524abdf0b0d58fa99d30abb4463611_121_0.png)

如果使用 `show()` 调用（除非我们调用了 `setModal`），则对话框是**非模态**（modeless）：

```cpp
void MainWindow::gotoCell()
{
    GotoCellDialog dialog(this);
    if (dialog.exec()) {
        QString str = dialog.lineEdit->text().toUpper();
        spreadsheet->setCurrentCell(str.mid(1).toInt() - 1,
            str[0].unicode() - 'A');
    }
}
```

`QDialog::exec()` 函数返回真值（`QDialog::Accepted`），否则返回假值（`QDialog::Rejected`）。回想起我们在第 2 章使用 Qt Designer 创建“跳转单元”对话框时，将 OK 连接到 `accept()`，将取消连接到 `reject()`。如果用户选择 OK，我们将当前单元格设置为行编辑器中的中的值。

`QTableWidget::setCurrentCell()` 函数期望两个参数：行索引和列索引。在电子表格应用程序中，单元格 A1 是 (0, 0)，单元格 B27 是 (26, 1)。要从 `QLineEdit::text()` 返回的字符串中获取行索引，我们使用 `QString::mid()`（从起始位置到字符串结束的子字符串）提取行号，使用 `QString::toInt()` 将其转换为整数并减去 1。对于列号，我们从字符串大写后的第一个字符中减去 'A' 的数值。我们知道字符串将具有正确的格式，因为我们为对话框创建的 `QRegValidator` 允许在字母后跟最多三个数字时，OK 按钮才可用。

`gotoCell()` 函数与目前看到的所有代码不同之处在于它在栈上创建了一个小部件（`GotoCellDialog`）。只需多出一行代码，我们同样很容易地使用 `new` 和 `delete`：

```cpp
void MainWindow::gotoCell()
{
    GotoCellDialog *dialog = new GotoCellDialog(this);
    if (dialog->exec()) {
        QString str = dialog->lineEdit->text().toUpper();
        spreadsheet->setCurrentCell(str.mid(1).toInt() - 1,
            str[0].unicode() - 'A');
    }
    delete dialog;
```

这种对话框编程模式是因为我们通常在使用后后不再需要该对话框（菜单），它会在作用域结束时自动销毁。

我们现在转向排序对话框。排序对话框是一个模态对话框，允许用户根据指定的列对当前选择区域进行排序。图 3.14 显示了一个排序示例，以 B 列为主排序键，A 列为次排序键（均为升序）。

# 图 3.14 对电子表格选择区域进行排序

![](img/5a524abdf0b0d58fa99d30abb4463611_123_0.png)

代码视图：

```cpp
void MainWindow::sort()
{
    SortDialog dialog(this);
    QTableWidgetSelection range = spreadsheet->selectedRange();
    dialog.setColumnRange('A' + range.leftColumn(),
                         'A' + range.rightColumn());

    if (dialog.exec()) {
        SpreadsheetCompare compare;
        compare.keys[0] = dialog.primaryColumnCombo->currentIndex();
        compare.keys[1] = dialog.secondaryColumnCombo->currentIndex() - 1;
        compare.keys[2] = dialog.tertiaryColumnCombo->currentIndex() - 1;
        compare.ascending[0] = (dialog.primaryOrderCombo->currentIndex() == 0);
        compare.ascending[1] = (dialog.secondaryOrderCombo->currentIndex() == 0);
        compare.ascending[2] = (dialog.tertiaryColumnCombo->currentIndex() == 0);
        spreadsheet->performSort(compare);
    }
}
```
