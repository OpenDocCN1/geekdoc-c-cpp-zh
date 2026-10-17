
每当用户将对象拖到控件上方时，`dragEnterEvent()` 就会被调用。如果我们在事件上调用 `acceptProposedAction()`，则表示用户可以将拖动对象投放到此控件上。默认情况下，控件不会接受拖动。Qt 会自动更改光标，以指示用户该控件是否为有效的投放目标。

在这里，我们希望允许用户拖动文件，但不允许其他内容。为了实现，我们检查拖动的 MIME 类型。`text/uri-list` MIME 类型用于存储统一资源标识符 URI 列表，这些可以是文件名、URL（如 HTTP/FTP 路径或其他资源标识符）。拖放系统由 IANA 定义，由不同类型组成。当用户在控件上方释放鼠标按钮时，会调用 `dropEvent()`。

```cpp
void MainWindow::dropEvent(QDropEvent *event)
{
    QList<QUrl> urls = event->mimeData()->urls();
    if (!urls.isEmpty()) {
        QString fileName = urls.first().toLocalFile();
        if (readFile(fileName)) {
            textEdit->append(fileName);
        }
    }
    event->acceptProposedAction();
}
```

### 图 9.1 选择器应用程序

![](img/5a524abdf0b0d58fa99d30abb4463611_354_0.png)

（注：由于您提供的文本在此处中断，以上翻译已涵盖了文本中所有可见的完整内容。）

```cpp
QDrag *drag = new QDrag(this);
drag->setMData(mimeData);
drag->setPixmap(QPixmap(":/images/person.png"));
if (drag->exec(Qt::MoveAction) == Qt::MoveAction)
    delete item;
```

在 `performDrag()` 中，我们创建了一个 `QDrag` 类型的对象并将 `this` 作为它的父对象。`QDrag` 将数据存储在 `QMimeData` 对象中。在本示例中，我们通过 `QMimeData::setText()` 提供 `text/plain` 字符串格式的数据。`QMimeData` 提供了多种处理最常见类型（图像、URL、颜色等）的功能，并可以处理表示为 `QByteArray` 的任意 MIME 类型。调用 `QDrag::setPixmap()` 会设置拖拽过程中跟随光标的图标。

`QDrag::exec()` 开始拖拽操作并阻塞，直到用户释放或取消拖拽。它接受一组“拖动动作”作为参数（`Qt::CopyAction`、`Qt::MoveAction`、`Qt::LinkAction`），并返回执行的拖动动作（如果没有执行，则返回 `Qt::IgnoreAction`）。执行哪种动作取决于源控件允许的操作、目标支持的操作以及在释放时按下了哪些修饰键。在调用 `exec()` 后，Qt 将接管拖拽对象的所有权并在完成后将其删除。

```cpp
void ProjectListWidget::dragEnterEvent(QDragEnterEvent *event)
{
    ProjectListWidget source =
        object_cast<ProjectListWidget>(event->source());
    if (source && source != this) {
        event->setDropAction(Qt::MoveAction);
        event->accept();
    }
}
```

`ProjectListWidget` 不仅能源自拖拽，如果拖拽源自同一应用程序中的另一个 `ProjectListWidget`，它也能接受此类拖拽。`QDragEnterEvent::source()` 如果发起拖拽的控件属于同一个应用程序，则返回该控件指针；否则返回空指针。我们使用 `q_cast<T>()` 来确保拖拽来自 `ProjectListWidget`。如果一切正确，我们告诉 Qt 我们已准备好接受该动作作为操作。

```cpp
void ProjectListWidget::dragMoveEvent(QDragMouseEvent *event)
{
    ProjectListWidget source =
    qobject_cast<ProjectListWidget>(event->source());
    if (source && source != this) {
        event->setDropAction(Qt::MoveAction);
        event->accept();
    }
}
```

`dragMoveEvent()` 中的代码与我们在 `dragEnterEvent()` 中做的完全相同。这是有必要的，因为我们需要重写 `QList`（实际上是 `QAbstractListView`）对该函数的实现。

```cpp
void ProjectListWidget::dropEvent(QDropEvent *event)
{
    ProjectListWidget source =
    qobject_cast<ProjectListWidget>(event->source());
    if (source && source != this) {
        addItem(event->mimeData()->text());
        event->setDropAction(Qt::MoveAction);
        event->accept();
    }
}
```

在 `dropEvent()` 中，我们使用 `QMimeData::text()` 获取被拖拽的文本并使用该文本创建一个项。我们还需要接受该事件作为“移动动作”，以告诉源控件它现在可以移除被拖拽项的原始版本。

拖放和释放是应用程序之间传输数据的一种强大机制。但在某些情况下，也可以不使用 Qt 的拖放功能来实现拖放和释放。如果我们只是想在一个应用程序中的一个控件内移动数据，我们可以简单地重新实现 `mousePressEvent()` 和 `mouseReleaseEvent()`。

## 9. 拖放和释放

![](img/5a524abdf0b0d58fa99d30abb4463611_358_0.png)

- 启用拖放
- 支持自定义拖拽类型
- 剪贴板处理

拖放和释放是在应用程序内部或不同应用程序之间传输信息的现代且直观的方式。除了用于移动和复制数据的剪贴板支持外，它通常会被提供。

在本章中，我们将看到如何为应用程序添加拖放支持，以及如何处理自定义格式。然后，我们将展示如何重用拖放代码来添加剪贴板支持。这种代码重用是可能的，因为这两种机制都基于 `QMimeData`，该类可以提供多种格式的数据。

### 启用拖放

拖放涉及两个不同的动作：拖拽和释放。Qt 控件可以作为拖拽源、释放源或两者兼具。

我们的第一个示例展示了如何让 Qt 应用程序接受由另一个应用程序发起的拖拽。该 Qt 应用程序是一个主窗口，以 `QTextEdit` 作为其中心控件。当用户从桌面或文件管理器拖拽文本文件并将其释放到应用程序上时，应用程序会将文件加载到 `QTextEdit`。

这里是示例中 `MainWindow` 类的定义：

```cpp
class MainWindow : public QMainWindow
{
    Q_OBJECT
public:
    MainWindow();
protected:
    void dragEnterEvent(QDragEnterEvent event);
    void dropEvent(QDropEvent event);
private:
    bool readFile(const QString &fileName);
    QTextEdit *textEdit;
};
```

`MainWindow` 类重写了 `QWidget` 的 `dragEnterEvent()` 和 `dropEvent()`。由于示例的目的是为了展示拖放，许多功能被省略了。

```cpp
MainWindow::MainWindow()
{
    textEdit = new QTextEdit();
    setCentralWidget(textEdit);
    textEdit->setAcceptDrops(false);
    setAcceptDrops(true);
    setWindowTitle(tr("Text Editor"));
}
```

在构造函数中，我们创建了 `QTextEdit` 并将其设置为中心控件。通过禁用 `textEdit` 的接受释放并启用主窗口的接受释放，当用户从桌面或文件管理器拖拽文本文件并将其释放到应用程序上时，应用程序会将文件加载到 `QTextEdit`。

```cpp
void MainWindow::dragEnterEvent(QDragEvent *event)
{
    if (event->mimeData()->hasFormat("text/uri-list"))
        event->acceptProposedAction();
}
```

`dragEnterEvent()` 是当用户将对象拖入控件时调用的。通过对事件调用 `acceptProposedAction()`，我们指示控件可以接受释放。

```cpp
void MainWindow::dropEvent(QDropEvent *event)
{
  List<QUrl> urls = event->mimeData()->urls();
  if (urls.isEmpty())
    return;
  QString fileName = urls.first().toLocalFile();
  if (fileName.isEmpty())
    return;
  if (readFile(fileName))
    setWindowTitle(tr("%1 - %2")).arg(fileName).arg(tr("Drag File")));
}
```

`dropEvent()` 是当用户将对象释放到控件时调用的。我们调用 `QMimeData::urls()` 获取 `QUrl` 列表。通常用户一次只拖一个文件，但他们也可以通过拖拽选择来拖拽多个文件。

`QWidget` 也提供了 `dragMoveEvent()` 和 `dragLeaveEvent()`，但大多数应用程序不需要重新实现。第二个示例说明了如何发起拖拽并接受释放。我们将创建一个支持拖放的 `QListWidget` 子类，并将其作为图 9.1 所示项目选择应用程序的组件。

#### 图 9.1. 项目选择应用程序

![](img/5a524abdf0b0d58fa99d30abb4463611_361_0.png)

项目选择应用程序向用户展示两个填充了名称的列表控件。每个列表控件代表一个项目。用户可以通过拖列表控件中的名称将人员从一个项目移动到另一个项目。

所有的拖放代码都位于 `QListWidget` 子类中。这里是类的定义：

```cpp
class ProjectListWidget : public QListWidget
{
    Q_OBJECT
public:
    ProjectListWidget(QWidget *parent = 0);
protected:
    void mousePressEvent(MouseEvent event);
    void mouseMoveEvent(MouseEvent event);
    void dragEnter(DragEnterEvent *event);
    void dragMoveEvent(DragMoveEvent event);
    void dropEvent(QDropEvent event);
private:
    void performDrag();
    QPoint startPos;
};
```

`ProjectListWidget` 类重写了 `QWidget` 中声明的五个事件处理器。

```cpp
ProjectListWidget::ProjectListWidget(QWidget *parent)
: QListWidget(parent)
{
```

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
