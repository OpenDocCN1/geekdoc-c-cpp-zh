
`void ProjectListWidget::dragEnterEvent(QDragEnterEvent *event)`

```cpp
{
    ProjectListWidget *source =
        q_cast<ProjectListWidget>(event->source());
    if (source && source != this) {
        event->setDropAction(Qt::MoveAction);
        event->accept();
    }
}
```

```cpp
void ProjectListWidget::dragMoveEvent(QMouseEvent *event)
{
    if (event->mimeData()->hasText()) {
        ProjectListWidget *source =
        // ... logic logic (event for this 
        event->setDropAction(Qt::MoveAction);
        event->accept();
    }
}
```

`ProjectListWidget` 不仅发起拖拽，如果拖拽来自同一应用程序中的另一个 `ProjectListWidget`，它也会接受此类拖拽。`QDragEnterEvent::source()` 返回发起拖拽部件的指针（如果它是同一应用程序的一部分）；否则返回空指针。我们使用 `q_cast<T>()` 来确保拖拽来自 `ProjectListWidget`。

```cpp
void ProjectListWidget::dragMoveEvent(QMouseEvent *event)
{
    if (event->mimeData()->hasText()) {
        ProjectListWidget *source =
        // ...
    }
}
```

```cpp
void ProjectListWidget::dropEvent(QDropEvent *event)
{
    if (event->mimeData()->hasText()) {
        QString text = event->mimeData()->text();
        // ... handle drop
        event->setDropAction(Qt::MoveAction);
        event->accept();
    }
}
```

### 支持自定义类型

在示例中，我们依赖于 `QMimeData::setText()`。但如果我们想拖拽自定义类型，必须为 `QMimeData` 子类。为了展示这些方法的工作原理：

- 第一种方法没有子类，但有缺点：我们需要存储多次数据（每种 MIME 类型存储一次）。
- 第二种方法是 `QMimeData` 的子类，并赋予我们完全的控制权。
- 第三种方法是 `QMimeData` 的子类以尽可能减少这些问题。

第一种方法所示：

```cpp
void ProjectListWidget::moveEvent(QMouseEvent *event)
{
    if (event->buttons() & Qt::LeftButton) {
        int distance = (event->pos() - startPos).manhattanLength();
        if (distance >= QApplication::startDragDistance()) {
            performDrag();
        }
    }
    QListWidget::moveEvent(event);
}
void ProjectListWidget::performDrag()
{
    QString plainText = selectionAsString();
    if (plainText.isEmpty()) {
        return;
    }
    QMimeData *mimeData = new QMimeData;
    mimeData->setText(plainText);
    mimeData->setHtml(toHtml(plainText));
    mimeData->setData("text/csv", toCsv(plainText).toUtf8());
    QDrag *drag = new QDrag(this);
    drag->setMimeData(mimeData);
    if (drag->exec(Qt::CopyAction | Qt::MoveAction) == Qt::MoveAction) {
        deleteSelection();
    }
}
```

The `toCsv()` 和 `toHtml()` 函数将“制表符和换行符”字符串转换为一个

CSV（逗号分隔值）或 HTML 字符串。例如，数据：

| 红色 | 绿色 | 蓝色 |
| 青色 | 黄色 | 品红色 |

转换为：

"Red", "Green", "Blue"
"Cyan", "Yellow", "Magenta"

或转换为：

```html
<table>
<tr><td>Red</td><td>Green</td><td>Blue</td></tr>
<tr><td>Cyan</td><td>Yellow</td><td>Magenta</td></tr>
</table>
```

该转换是以尽可能简单的方式执行的，使用了 `QString::replace()`。为了转义 HTML 特殊字符，我们使用 `QString::escape()`。

```cpp
void MyTable::dropEvent(QDropEvent *event) {
  if (event->mimeData()->hasFormat("text/csv")) {
    QByteArray csvData = event->mimeData()->data("text/csv");
    QString csvText = QString::fromUtf88(csvData);
    ...
    event->acceptProposedAction();
  } else if (event->mimeData()->hasFormat("text/plain")) {
    QString plainText = event->mimeData()->text();
    ...
    event->acceptProposedAction();
  }
}
```

虽然我们提供了三种不同格式的数据，但我们在 `dropEvent()` 中只接受其中两种。如果用户从 `QTable` 拖动单元格到 HTML 编辑器，我们也希望这些单元格被转换为 HTML 表格。如果用户将任意 HTML 拖入 `QWidgetItem`，我们则不希望接受它。

为了实现这个示例，我们还需要在 `MyTableWidget` 构造函数中设置 `setAcceptDrops(true)` 和 `setSelectedMode(ContiguousSelection)`。

我们重新编写这个示例，但这次我们将派生 `QMimeData` 子类，以推迟或避免（可能开销较大的）`QTableItems` 与 `QByteArray` 之间的转换。以下是我们的子类的定义：

```cpp
class TableMimeData : public QMimeData
{
    Q_OBJECT
public:
    TableMimeData(const QTable *tableWidget,
                  const QTreeWidgetItemSelectionRange &range);
    const QTable *table() const { return myTableWidget; }
    QTreeWidgetItemSelectionRange range() const { return myRange; }
    QStringList formats() const;
protected:
    QVariant retrieveData(const QString &format,
                          QVariant::Type preferredType) const;
private:
    static QString toHtml(const QString &plainText);
    static QString toCsv(const QString &plainText);
    QString text(int row, int column) const;
    QString rangeAsPlainText() const;
    const QTable *myTableWidget;
    QTreeWidgetItemSelectionRange myRange;
    QStringList myFormats;
};
```

我们没有存储实际数据，而是存储了一个指定哪些单元格被拖拽的 `QTableSelectionRange`，并保留了指向 `QTable` 的指针。`formats()` 和 `retrieveData()` 函数是从 `QMimeData` 重新实现的。

```cpp
TableMimeData::TableMimeData(const QTable *tableWidget,
              const QTableSelectionRange &range)
{
    myTableWidget = tableWidget;
    myRange = range;
    myFormats << "text/csv" << "text/html" << "text/plain";
}
```

在构造函数中，我们初始化了私有变量。

```cpp
QStringList TableMimeData::formats() const
{
    return myFormats;
}
```

`formats()` 函数返回由 MIME 数据对象提供的 MIME 类型列表。格式的精确顺序通常并不重要，但将“最佳”格式放在最前面是一种良好的做法。支持许多格式的应用程序有时会使用第一个匹配的格式。

```cpp
QVariant TableMimeData::retrieveData(const QString &format, QVariant::Type preferredType)
{
    if (format == "text/plain") {
        return rangeAsPlainText();
    } else if (format == "text/csv") {
        return toCsv(rangeAsPlainText());
    } else if (format == "text/html") {
        return toHtml(rangeAsPlainText());
    } else {
        return QMimeData::retrieveData(format, preferredType);
    }
}
```

`retrieveData()` 函数以 `QVariant` 形式返回给定给定 MIME 类型的数据。`format` 参数的值通常是 `formats()` 返回的字符串之一，但我们无法假设这一点，因为所有应用程序都会根据 `formats()`  MIME 类型。`QMimeData` 提供的 `text()`、`html()`、`urls()`、`imageData()`、`colorData()` 和 `data()` 获取函数都在 `retrieveData` 中实现。

`preferredType` 参数为我们提供了关于在 `QVariant` 中放入何种类型的提示。在这里，我们忽略了它，并信任 `QMimeData` 在必要时将返回值转换为所需的类型。

```cpp
void MyTableWidget::dropEvent(QDropEvent event)
{
    const TableMimeData *tableData = qobject_cast<const TableMimeData*>(event->mimeData());
    if (tableData) {
      const QTable *otherTable = tableData->table();
      QTableSelectionRange otherRange = tableData->range();
      event->acceptProposedAction();
    } else if (event->mimeData()->hasFormat("text/csv")) {
      QByteArray csvData = event->mimeData()->data("text/csv");
      QString csvText = QString::fromUtf8(csvData);
      event->acceptProposedAction();
    } else if (event->mimeData()->hasFormat("text/plain")) {
      QString plainText = event->mimeData()->text();
      ...
      event->acceptProposedAction();
    }
}
```
