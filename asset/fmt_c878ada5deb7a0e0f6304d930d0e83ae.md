
`QTableWidgetSelectionRange selectedRange() const;`

`void clear();`

`bool readFile(const QString &fileName);`

`bool writeFile(const QString &fileName);`

`void sort(const SpreadsheetCompare &compare);`

```cpp
`autoRecalculate()` 函数被内联实现，因为它返回了是否强制执行自动重新计算。
```

在第 3 章中，我们在实现 `MainWindow` 时，依赖了 `Spreadsheet` 中的一些公共函数。例如，我们在 `MainWindow::newFile()` 中调用了 `clear()` 来重置表格。我们还使用了继承自 `QTableWidget` 的函数，特别是 `setCurrentCell()` 和 `setShowGrid()`。

+ public slots:
`void cut();`
`void copy();`
`void paste();`
`void del();`
`void selectCurrentRow();`
`void selectCurrentColumn();`
`void recalculate();`
`void setAutoRecalculate(bool recalc);`
`void findNext(const QString &str, Qt::CaseSensitivity cs);`
`void findPrevious(const QString &str, Qt::CaseSensitivity cs);`

+ signals:
`void modified();`

`Spreadsheet` 提供了许多实现了“编辑”、“工具”和“选项”菜单动作的槽，并提供了一个信号 `modified()`，用于通告任何发生的更改。

+ private slots:
`void somethingChanged();`

我们定义了一个供 `Spreadsheet` 类内部使用的私有槽。

```cpp
enum MagicNumber = 0x7F51C883, RowCount = 999, ColumnCount = 26

Cell *cell(int row, int column) const;

QString text(int row, int column) const;

QString formula(int row, int column) const;

void setFormula(int row, int column, const QString &formula);

bool autoRecalc;

};
```

在类的私有部分，我们声明了三个常量、四个函数和一个变量。

```cpp
class SpreadsheetCompare

{

public:

    bool operator()(const QStringList &row1,

                   const QStringList &row2) const;

    enum { KeyCount = 3 };

    int keys[KeyCount];

    bool ascending[KeyCount];

};

#endif
```

头文件以 `SpreadsheetCompare` 类定义结束。我们将在回顾 `Spreadsheet::sort()` 时解释这一点。

现在我们来看实现部分：

```cpp
#include <QtGui>
#include "cell.h"
#include "spreadsheet.h"
```

```cpp
Spreadsheet::Spreadsheet(QWidget parent)
: QTableWidget(parent)
{
    autoRecalc = true;
    setItemPrototype(new Cell);
    setSelectionMode(ContiguousSelection);
connect(this, SIGNAL(itemChanged(QTableWidgetItem*)),
    this, SLOT(somethingChanged()));
clear();
}
```

通常，当用户在空单元格中输入某些文本时，`QWidget` 会自动创建一个 `QTableWidgetItem` 来持有文本。在我们的电子表中，我们允许创建 `Cell` 项来代替它。这是通过构造函数中的 `setItemPrototype()` 调用实现的。在内部，`QWidget` 每当需要新项时，都会将该项作为原型进行隆。

同样在构造函数中，我们将选择模式设置为 `QAbstractItemView::ContiguousSelection`，以允许单次矩形选择。我们将表格的 `itemChanged()` 信号连接到私有的槽 `somethingChanged()`；这确保了当用户编辑单元格时，调用 `somethingChanged()` 槽。最后，我们调用 `clear()` 来调整表格大小并设置列标题。

```cpp
void Spreadsheet::clear()
{
    setRowCount(0);
    setColumnCount(0);
    setRowCount(RowCount);
    setColumnCount(ColumnCount);
    for (int i = 0; i < ColumnCount; ++i) {
        QTableWidgetItem *item = new QTableWidgetItem;
        item->setText(QString(QChar('A') + i));
        setHorizontalHeader(i, item);
    }
    setCurrentCell(0, 0);
}
```

`clear()` 函数在 `Spreadsheet` 构造函数中调用以初始化电子表。它也被 `MainWindow::newFile()` 调用。

我们使用了 `QWidget::clear()` 来清除所有项和选择，但这会留下表头保持当前的大小。相反，我们将表格缩减为 0 x 0。这清空了整个电子表，包括表头。然后我们将表格调整为 `ColumnCount` x `RowCount` (26 x 999)，并使用包含列 "A"、"B"..."Z" 的 `QTableWidgetItem` 设置水平表头。我们不需要设置垂直表头标签，因为这些被用于识别 "1"..."2"..."999"。最后，我们将光标移动到 A1 单元格。

`QTableWidget` 由几个子组件组成。它顶部有一个水平 `QHeaderView`，左侧有一个垂直 `QHeaderView`，以及两个 `QScrollBar`。该区域由一个特殊的子组件占据，该组件通过继承自 `QTableView` 和 `QAbstractScrollArea` 的函数（图 4.2）提供一个可滚动的视口和两个滚动条，可以开启或关闭。我们将在第 6 章中介绍 `QScrollBar` 类。

### 图 4.2. QTableWidget 的组成组件

![](img/5a524abdf0b0d58fa99d30abb4463611_143_0.png)

```cpp
Cell *Spreadsheet::cell(int row, int column) const
{
    return static_cast<Cell *>(item(row, column));
}
```

`cell()` 私有函数返回给定行和列的 `Cell` 对象。如果它返回 `null`，则单元格为空。

```cpp
QString Spreadsheet::text(int row, int column) const
{
    Cell *c = cell(row, column);
    if (c) {
        return c->text();
    } else {
        return "";
    }
}
```

```cpp
QString Spreadsheet::formula(int row, int column) const
{
    Cell *c = cell(row, column);
    if (c) {
        return c->formula();
    } else {
        return "";
    }
}
```

将公式转换为值的任务由 `Cell` 类执行。此时，需要注意的是，单元格中显示的文本是计算公式的结果，而不是公式本身。

- 如果公式是数字，它被解释为数字。例如，公式 "1.50" 解析为双精度数值 1.5，在电子电子表中右对齐。
- 如果公式以单引号开头，剩余部分被解释为文本。例如，公式 '12345' 解析为字符串 "12345"。
- 如果公式以等号 ('=') 开头，它被解释为算术公式。例如，如果 A1 包含 "12"，单元格 A2 包含 "6"，公式 "=A1+A2" 解析为 18。

![](img/5a524abdf0b0d58fa99d30abb4463611_144_png)

## 存储数据

在电子表中，每个非空单元格都作为独立的 `WidgetItem` 存储在内存中。这种存储数据的方法也被 `ListWidget` 和 `QTreeWidget` 使用，它们分别操作 `ListItem` 和 `TreeWidgetItem`。

Qt 的项类可以即箱用作数据头。例如，`TableWidgetItem` 已经存储了一些属性，包括字符串、字体、颜色和指向表格的指针。项还可以持有数据（`QVariant`），通过子类项类可以提供额外功能。

旧的工具包在项中提供 `void` 来存储自定义数据。在 Qt 中，更自然的方法是使用 `setData()` 配合 `QVariant`，但如果需要 `void`，则可以通过子类项类并添加 `void` 成员变量轻松实现。

对于更有挑战性的数据处理需求，例如大数据、复杂数据项、数据库集成和多数据视图，Qt 提供了一套模型/视图类，将数据与其视觉表示分离离开。这些将在第 10 章中介绍。

```cpp
void Spreadsheet::setFormula(int row, int column, const QString &formula)
{
    Cell *c = cell(row, column);
    if (!c) {
        c = new Cell;
        setItem(row, column, c);
    }
    c->setFormula(formula);
}
```

`setFormula()` 是私有函数，用于为指定的单元格设置公式。如果单元格已经有一个 `Cell` 对象，否则我们将创建一个新的 `Cell` 对象并使用 `QWidgetItem::setItem()` 将其插入到表中。最后，我们调用单元格的 `setFormula()` 函数，如果单元格在屏幕外，这将导致单元格重绘。我们不需要担心以后删除 `Cell`；`QWidgetItem` 会接管单元格的所有权，并在适当的时间自动删除它。

```cpp
QString Spreadsheet::currentLocation() const {
  return QChar('A' + currentColumn())
  + QString::number(currentRow() + 1);
}
```

`currentLocation()` 按常用的电子表格格式（列字母后跟行号）返回当前单元格的位置。`MainWindow::updateStatusBar()` 使用它在状态栏中显示位置。

```cpp
QString Spreadsheet::currentFormula() const {
  return formula(currentRow(), currentColumn());
}
```

```cpp
void Spreadsheet::somethingChanged() {
  if (autoRecalc)
    recalculate();
  emit modified();
}
```

私有槽 `somethingChanged()` 在启用“自动重新计算”时重新计算整个电子表格。它还会发出 `modified()` 信号。

## 加载与保存

现在我们将使用自定义二进制格式实现 `Spreadsheet` 文件的加载和保存。我们将使用 `QFile` 和 `QDataStream`，它们共同提供了与平台无关二进制 I/O 功能。

我们将从写入 `Spreadsheet` 文件开始：

代码视图：

```cpp
bool Spreadsheet::writeFile(const QString &fileName)
{
    QFile file(fileName);
    if (!file.open(QIODevice::WriteOnly)) {
        QMessageBox::warning(this, tr("Spreadsheet"),
            tr("Cannot write file %1:%n2.") .arg(fileName).arg(file.errorString()));
        return false;
    }
    QDataStream out(&file);
    out.setVersion(QDataStream::Qt_4_3);
    out << quint32(MagicNumber);
    QApplication::overrideCursor(Qt::WaitCursor);
    for (int row = 0; row < RowCount; ++row) {
        for (int column = 0; column < ColumnCount; ++column) {
            QString str = formula(row, column);
            if (!str.isEmpty())
                out << quint16(column) << str;
        }
    }
    QApplication::restoreCursor();
    return true;
}
```

`writeFile()` 函数由 `MainWindow::saveFile()` 调用，用于将文件写入磁盘。成功时返回 `true`，错误时返回 `false`。

我们使用给定名称创建一个 `QFile` 对象并调用 `open()` 以写入打开文件。我们还创建一个操作 `QFile` 的 `QDataStream` 对象并使用它来写入数据。

在写入数据之前，我们将应用程序的光标更改为标准（通常是沙漏），并在所有数据写入后恢复正常光标。在函数末尾，文件由 `QFile` 析构函数自动关闭。

`QDataStream` 支持基础 C++ 类型以及 Qt 的许多类型。其语法模仿了标准 C++ 的 `<iostream>` 类。例如，

```
out << x << y << z;
```

将变量 `x`、`y` 和 `z` 写入流，而

```
in >> x >> y >> z;
```

从流中读取。由于 C++ 原始整数类型在不同平台上的大小可能不同，最安全的方法是将这些值强制转换为 `quint8`、`quint16`、`quint32`、`quint64` 或 `qint8` 到 `qint64` 之一，这些类型保证了它们标识的大小（以位为单位）。

`Spreadsheet` 应用程序的文件格式非常简单。`Spreadsheet` 文件以一个识别文件格式的32 位数字开头（`MagicNumber`，在 `spreadsheet.h` 中定义为 0x7F5CC83，这是一个任意数字）。接着是一系列块，每个块包含单个单元格的行、列和公式。为了节省空间，我们不输出空单元格。该格式如图 4.3 所示。

### 图 4.3. Spreadsheet 文件格式

![](img/5a524abdf0b0d58fa99d30abb4463611_148_0.png)

数据类型的精确二进制表示由 `QDataStream` 决定。例如，`quint16` 以大端序存储为两个字节，`QString` 则存储为字符串长度后跟 Unicode 字符。

Qt 类型的二进制表示自 1.0 以来已经发生了很大变化。它在未来的 Qt 版本中可能会继续演进，以跟上现有类型的演进并允许新类型的出现。默认情况下，`QDataStream` 使用最新版本的二进制格式（版本 9），但可以设置为读取旧版本。为了避免在使用较新 Qt 版本重新编译应用程序时出现兼容性问题，我们显式告诉 `QDataStream` 使用我们正在编译的 Qt 版本。

`QDataStream` 非常通用。它可以用于 `QFile`、`QBuffer`、`QProcess`、`TCPSocket` 和 `UDPSocket`。Qt 还提供了 `QTextStream` 可以替代 `QDataStream` 用于读写。第 12 章详细解释了这些类，并描述了处理 `DataStream` 版本的各种方法。

代码视图：

```cpp
bool Spreadsheet::readFile(const QString&fileName)
{
    QFile file(fileName);
    if (!file.open(QIODevice::ReadOnly)) {
        QMessageBox::warning(this, tr("Spreadsheet"),
