
```cpp
setAcceptDrops(true);
}
```

在构造函数中，我们启用了列表部件（list widget）的拖放功能。

```cpp
void ProjectListWidget::mouseEvent(QMouseEvent *event)
{
    if (event->button() == Qt::LeftButton)
        startPos = event->pos();
    QListWidget::mousePress(event);
}
```

当用户按下鼠标左键时，我们将鼠标位置存储在私有变量 `startPos` 中。我们调用 QListWidget 对 mouseEvent 的实现，以确保 `QListWidget` 能够像往常处理鼠标事件。

```cpp
void ProjectListWidget::moveEvent(QMouseEvent *event)
{
    if (event->buttons() & Qt::LeftButton) {
        int distance = (event->pos() - startPos).manhattanLength();
        if (distance >= QApplication::startDragDistance())
            performDrag();
    }
    QListWidget::moveEvent(event);
}
```

当用户按住左键并移动鼠标光标时，我们考虑开始拖拽。我们计算当前鼠标位置与按下左键位置之间的距离——“曼哈顿长度”（Manhattan length）是起点原点向量长度的快速计算近似值。如果距离大于或等于 QApplication 推荐的拖拽开始距离（通常为四个像素），我们调用私有函数 `performDrag()` 来开始拖拽。这可以避免在用户手抖时意外触发拖拽。

```cpp
void ProjectListWidget::performDrag()
{
  QWidgetItem *item = currentItem();
  if (item) {
    QMimeData *mimeData = new QMimeData;
    mimeData->setText(item->text());
```

```cpp
QDrag *drag = new QDrag(this);
drag->setMimeData(mimeData);
drag->setPixmap(QPixmap(":/images/person.png"));
if (drag->exec(Qt::MoveAction) == Qt::MoveAction)
    delete item;
}
```

在 `performDrag()` 中，我们创建了一个以当前为父对象的 `QDrag` 类型对象。`QDrag` 将数据存储在 `QMimeData` 对象中。对于此示例，我们通过 `QMimeData::setText()` 以 text/plain 字符串的形式提供数据。`QMimeData` 为处理最常见的类型（图像、URL、颜色等）提供了若干项功能，并可以处理表示为 `QByteArray` 的任意 MIME 类型。调用 `QDrag::setPixmap()` 设置在拖拽过程中跟随光标的图标。

`QDrag::exec()` 启动拖拽操作并阻塞，直到用户释放或取消拖拽。它接受一组“拖拽动作”作为参数（`Qt::CopyAction`, `Qt::MoveAction`, `Qt::LinkAction`），并返回执行的拖拽动作（如果没有执行，则返回 `Qt::IgnoreAction`）。执行哪个动作取决于源部件允许、目标支持以及发生释放时按下了哪些修饰键。在调用 `exec()` 后，Qt 会接管拖拽对象的所有权，并在完成后对其将其删除。

```cpp
void ProjectListWidget::dragEnterEvent(QDragEnterEvent *event)
{
    ProjectListWidget *source =
        q_cast<ProjectListWidget>(event->source());
    if (source && source != this) {
        event->setDropAction(Qt::MoveAction);
        event->accept();
    }
}
```

`ProjectListWidget` 不仅发起拖拽，如果拖拽来自同一应用程序中的另一个 `ProjectListWidget`，它也会接受此类拖拽。`QDragEnterEvent::source()` 返回发起拖拽部件的指针（如果它是同一应用程序的一部分）；否则返回空指针。我们使用 `q_cast<T>()` 来确保拖拽来自 `ProjectListWidget`。

```cpp
void ProjectListWidget::dragEnterEvent(QDragEnterEvent *event)
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

## 支持自定义类型

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

