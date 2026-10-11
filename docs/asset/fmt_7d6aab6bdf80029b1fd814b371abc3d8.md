
```cpp
bool CodeEditor::event(QKeyEvent *event)
{
  if (event->type() == QKeyEvent::KeyPress) {
    QKeyEvent *keyEvent = static_cast<QKeyEvent>(event);
    if (event->key() == Qt::Key_Tab) {
      insertAtCurrentPosition('\t');
      return true;
    }
  }
  return QWidget::event(event);
}
```

如果事件是按键按下，我们将 `QEvent` 对象强制转换为 `QKeyEvent` 并检查按了哪个键。如果键是 `Tab`，我们进行一些处理并返回 `true` 告诉 Qt 我们已经处理了该事件。如果我们返回 `false`，Qt 将将事件传递给父控件。

实现按键绑定的更高层次的方法是使用 `QAction`。例如，如果 `goToBeginningOfLine()` 和 `goToBeginningOfDocument()` 是 `CodeEditor` 中的公共槽，且 `CodeEditor` 被用作 `MainWindow` 类中的中心控件，我们可以通过以下代码添加按键绑定：

```cpp
MainWindow::MainWindow()
{
  editor = new CodeEditor();
  setCentralWidget(editor);

  goToBeginningOfLineAction =
    new QAction(tr("Go to Beginning of Line"), this);
  goToBeginningOfLineAction->setShortcut(tr("Home"));
  connect(goToBeginningOfLineAction, SIGNAL(activated()),
    editor, SLOT(goToBeginningOfLine()));

  goToBeginningOfDocumentAction =
    new QAction(tr("Go to Beginning of Document"), this);
  goToBeginningOfDocumentAction->setShortcut(tr("Ctrl+Home"));
  connect(goToBeginningOfDocumentAction, SIGNAL(activated()),
    editor, SLOT(goToBeginningOfDocument()));
}
```

这使得为控件添加按键绑定变得简单，正如我们在第三章中看到的那样。

```cpp
if (event->timerId == myTimerId) {
    ++offset;
    if (offset >= fontMetrics().width(text)) {
        offset = 0;
        scroll(-1, 0);
    }
} else {
    QWidget::timerEvent(event);
}
```

系统会间隔调用 `timerEvent()` 函数。它将 `offset` 增加 1 以模拟移动，并在文本宽度处回绕。然后，它使用 `QWidget::scroll()` 将部件的内容向左滚动一个像素。调用 `update()` 代替 `scroll()` 就足够了，但 `scroll()` 更高效，因为它只是移动屏幕上现有的像素，并且仅为部件新显示的区域（在本例中为1像素宽的条带）生成绘制事件。

如果定时事件不是我们感兴趣的定时器，我们将其传递给基类。

```cpp
void Ticker::hideEvent(QHideEvent / /* event */)
{
    killTimer(myTimerId);
    myTimerId = 0;
}
```

`hideEvent()` 函数调用 `QObject::killTimer()` 来停止定时器。

定时器是低层的，如果我们需要多个定时器，跟踪所有的定时器 ID 会变得繁琐。在这种情况下，通常为每个定时器创建一个 `QTimer` 对象更简单。`QTimer` 在每个时间间隔都会发射 `timeout()` 信号。`QTimer` 还为单次定时器（仅超时一次的定时器）提供了一个方便的接口，正如我们在第6章（第158页）中所看到的。

## 安装事件过滤器

Qt 事件模型的一个非常强大的特性是，可以设置一个 `QObject` 实例在另一个 `QObject` 实例看到事件之前对其进行监控。

假设我们有一个由多个 `QEdit` 组成的 `CustomerInputDialog` 部件，我们想使用空格键将焦点移动到下一个 `QEdit`。这种非标准行为对于用户接受过相关训练的内部应用程序可能是合适的。一个直接的是子类 `QEdit` 并重新实现 `keyPressEvent()` 来调用 `focusNextChild()`，如下：

```cpp
void MyLineEdit::keyPressEvent(QKeyEvent *event)
{
    if (event->key() == Qt::Key_Space) {
        focusNextChild();
    } else {
        QLineEdit::keyPressEvent(event);
    }
}
```

这种方法有一个主要缺点：如果在表单中使用几种不同类型的部件（例如 `ComboBox` 和 `SpinBoxes`），我们必须对它们进行子类化以产生相同的行为。更好的解决方案是让 `CustomerInputDialog` 监控其子部件的按键事件，并在监控代码中实现所需的行为。可以通过事件过滤器来实现。设置事件过滤器涉及两个步骤：

- 通过在目标对象上调用 `installEventFilter()` 为目标对象注册监控对象。
- 在监控对象的 `eventFilter()` 函数中处理目标对象的事件。

在构造函数中注册监控是一个很好的位置：

```cpp
CustomerInputDialog::CustomerInputDialog(QWidget *parent)
    : QDialog(parent)
{
    ...
    firstNameEdit->installEventFilter(this);
    lastNameEdit->installEventFilter(this);
    cityEdit->installEventFilter(this);
    phoneNumberEdit->installEventFilter(this);
}
```

一旦注册了第一个过滤器，发送到 `firstNameEdit`、`lastNameEdit`、`phoneNumberEdit` 部件的事件在发送到目标位置之前，会首先发送到 `CustomerInfoDialog::eventFilter()` 函数。

这里是接收事件的 `eventFilter()` 函数：

```cpp
bool CustomerInfoDialog::eventFilter(QObject target, QEvent event) {
    if (target == firstNameEdit || target == lastNameEdit
        || target == cityEdit || target == phoneNumberEdit) {
        if (event->type() == QEvent::KeyPress) {
            QKeyEvent *key = static_cast<QKeyEvent>(event);
            if (key->key() == Qt::Key_Space) {
                focusNextChild();
                return true;
            }
        }
    }
    return QDialog::eventFilter(target, event);
}
```

首先，我们检查目标部件是否为 `QLineEdit` 之一。如果事件是按键，我们将其强制转换为 `QKeyEvent` 并检查按了哪个键。

如果按下的键是空格，我们调用 `focusNextChild()` 将焦点传递给焦点链中的下一个部件，并返回 `true` 告诉 Qt 我们已经处理了该事件。如果我们返回 `false`，Qt 将把事件发送到其预期目标，导致 `QLineEdit` 中插入一个多余的空格。

如果目标部件不是 `QLineEdit` 或事件不是空格按键按下，我们将控制权传递给 `eventFilter()` 的基类实现。目标部件也可能是基类 `QDialog` 正在监控的部件。（在 Qt 4.3 中，`QDialog` 并非如此。然而，其他部件类（如 `QScrollArea`）由于各种原因会监控其某些子部件。）

Qt 提供了可以处理和过滤事件的五个级别：

## 1. 我们可以重新实现特定的事件处理器。

重新实现如 `mousePressEvent()` 和 `paintEvent()` 等处理器是处理事件最常用的方法。我们已经见过许多此类例子。

## 2. 我们可以重新实现 `QObject::event()`。

通过重新实现 `event()`，我们可以在事件到达处理器之前拦截它们。这对于没有特定处理器的事件或自定义事件非常有用。

## 3. 我们可以使用事件过滤器。

如所述，事件过滤器是在不对部件进行子类的情况下拦截事件的强大方法。

## 4. 我们可以使用 `QTimer`。

`QTimer` 提供了一种处理基于时间的事件的方便方法。

## 5. 我们可以子类化并重新实现虚方法。

通过对类进行子类化，你可以覆盖它的默认行为并提供虚方法的自己的实现。

```cpp
qApp->processEvents();
```

配合

`qApp->processEvents(QEventLoop::ExcludeUserInputEvents);`

告诉 Qt 忽略鼠标和键盘事件。我们通常希望在执行耗时操作时显示一个 `QProgressDialog`。`QProgressDialog` 有一个进度条，可以向用户告知应用程序的进度。`QProgressDialog` 还提供了一个取消（Cancel）按钮，允许用户中止操作。这里是使用这种方法保存电子文件的代码：

代码视图：

```cpp
bool Spreadsheet::writeFile(const QString &fileName)
{
  QFile file(fileName);
  ..
  QProgressDialog progress(this);
  progress.setLabelText(tr("Saving %1").arg(fileName));
  progress.setRange(0, RowCount);
  progress.setModal(true);

  for (int row = 0; row < RowCount; ++row) {
    progress.setValue(row);
    qApp->processEvents();
    if (progress.wasCancelled()) {
      file.remove();
      return false;
    }
    for (int column = 0; column < ColumnCount; ++column) {
      QString str = formula(row, column);
      if (!str.isEmpty())
        out << quint16(row) << quint16(column) << str;
    }
  }
  return true;
}
```

`QProgressDialog` 将 `NumRows` 作为总步骤数。然后，通过除以每个数值，我们可以 `setValue()` 来更新进度条。`QProgressDialog` 会通过将当前进度值除以总步骤数来自动计算百分比。我们使用 `QApplication::processEvents()` 来处理重绘事件以及用户点击或按键（例如，允许用户点击取消）。如果用户点击取消，我们将中止保存并删除文件。

我们没有对 `QProgressDialog` 调用 `show()`，因为进度对话框会处理自己。如果操作结果不理想（可能是因为要保存的文件很小或者因为机器速度很快），`QProgressDialog` 将检测到这一点并完全不显示。

除了多线程和使用 `QProgressDialog` 之外，还有另一种完全不同的处理耗时操作的方法：不是在用户请求时执行处理，而是将处理推迟到应用程序空闲时。如果处理可以安全地中断和恢复，这种方法就是有效的，因为我们无法预测应用程序将空闲多久。

在 Qt 中，这种方法可以通过使用 0 毫秒定时器来实现。这些定时器在没有待处理事件时就会超时。这是一个显示空闲处理方法的 `timerEvent()` 实现示例：

```cpp
void Spreadsheet::timerEvent(QTimer *event)
{
    if (event->timerId == myTimerId) {
        while (step < MaxStep && !qApp->hasPendingEvents()) {
            performStep(step);
            ++step;
        }
    } else {
        QTableWidget::timerEvent(event);
    }
}
```

当 `hasPendingEvents()` 返回 `true` 时，我们停止处理并将控制权还给 Qt。当 Qt 处理完所有待处理事件后，处理将恢复。

## 2. 二维图形

![](img/5a524abdf0b0d58fa99d30abb4463611_287_0.png)

- 使用 `QPainter` 绘图
- 坐标系变换
- 使用 `QImage` 进行高质量渲染
- 使用 Graphics View 进行基于项的渲染
- 打印

Qt 的二维图形引擎基于 `QPainter` 类。`QPainter` 可以绘制几何形状（点、线、矩形、椭圆、弧、弦、扇形、多边形、曲线），以及位图（pixmaps）、图像和文本。`QPainter` 支持高级功能，如抗锯齿（用于文本和形状边缘）、透明度混合、渐变填充和矢量路径。`QPainter` 支持线性变换，如平移、旋转、倾斜和缩放。

`QPainter` 可用于在“绘图设备”上绘制，例如 `QWidget`、`QPixmap`、`QImage` 或 `QSvgGenerator`。`QPainter` 还可以结合 `QPrinter` 用于打印和生成 PDF 文档。这意味着我们可以使用相同的代码在屏幕上显示数据并生成用于打印的报告。

通过重实现 `QWidget::paintEvent()`，我们可以创建自定义控件并对其外观进行完全控制，正如我们在第 5 章中看到的。。为了自定义预定义 Qt 控件的外观和感受，我们还可以指定样式表（style sheet）或创建一个 `QStyle` 子类；我们在第 19 章将涵盖这两种方法。

一个常见的需求是在二维画布上显示大量用户可以交互的轻量级项。Qt 4.2 引入了一种以 `QGraphicsItem`、`QGraphicsScene` 和 `QGraphics` 类为中心的新“图形视图”架构。这种架构为设计基于项的图形提供了层级接口，并支持对项的标准用户操作，包括移动、选择和分组。项本身像往常一样使用 `QPainter` 绘制，并可以单独进行变换。我们将在章节稍后部分介绍这种架构。

`QPainter` 的替代方案是使用 OpenGL 命令。OpenGL 是一个用于绘制 3D 图形的标准库。在第 20 章，我们将看到如何使用 `QtOpenGL` 模块，它使得将 OpenGL 代码集成到 Qt 中变得简单。

## 使用 QPainter 绘图

要开始在绘图设备（通常是控件）上绘制，我们只需创建一个 `QPainter` 并并将绘制器传递给设备。例如：

```cpp
void MyWidget::paintEvent(QPaintEvent *event)
{
    QPainter painter(this);
}
```

我们可以使用 `QPainter` 的函数绘制各种形状。绘图的方式受到设备、笔（pen）、画刷（brush）和字体的字体。这些设置是默认的。图 8.1 列出了最常用的函数：

```cpp
drawPoint()
drawLine()
drawPolygon()
drawRect()
drawEllipse()
drawArc()
drawChord()
drawPie()
drawText()
drawPixmap()
```

笔用于绘制轮廓。它由颜色、宽度、样式和连接方式组成。样式在图 8.2 和 8.3 中显示。画刷用于填充形状。可以是颜色、渐变或纹理。

# 8.2 Cap 样式

| Cap |

| :--- |

| FlatCap |

| RoundCap |

| SquareCap |

| NoCap |

| Join Style |

| :--- |

| MiterJoin |

| FlatJoin |

| BevelJoin |

| RoundJoin |

字体用于绘制文本。字体有很多属性，包括字体和大小。可以通过调用 `setFont()` 修改这些设置。让我们在实践中看一些示例。这里是绘制图 8.5 (a) 所示椭圆的代码：
