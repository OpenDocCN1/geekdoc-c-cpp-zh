
按照习惯，`numXTicks` 和 `numYTicks` 偏移了一个值；如果 `numXTicks` 为 5，Plotter 将在 x 轴上绘制刻度线。这简化了后续的计算。

现在让我们回顾实现文件：

```cpp
Plotter::Plotter(QWidget *parent)
    : QWidget(parent)
{
    setBackgroundRole(QPalette::Dark);
    setAutoFillBackground(true);
    setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding);

    setFocusPolicy(Qt::StrongFocus);
    rubberBandIsShown = false;

zoomInButton = new QToolButton(this);
zoomInButton->setIcon(QIcon(":/images/zoomin.png"));
zoomInButton->adjustSize();
connect(zoomInButton, SIGNAL(clicked()), this, SLOT(zoomIn()));

zoomOutButton = new QToolButton(this);
zoomOutButton->setIcon(QIcon(":/images/zoomout.png"));
zoomOutButton->adjustSize();
connect(zoomOutButton, SIGNAL(clicked()), this, SLOT(zoomOut()));

setPaletteSettings(setPaletteSettings());
}
```

`setBackgroundRole()` 调用 `QWidget` 使用调色板中的“深色”组件。这为 Qt 提供了一个默认颜色，当控件调整到更大尺寸时，在 `paintEvent()` 有机会绘制像素之前，该颜色可填充任何新暴露的像素。（默认情况下，控件继承其父控件的背景。）

`setFocusPolicy(Qt::StrongFocus)` 允许控件通过点击或按下 Tab 键获取焦点。当 Plotter 获得焦点时，它将接收按键事件。Plotter 理解几个按键：`+` 放大；`-` 缩小；以及使用方向键向上、向下、向左和向右滚动。

## 图 5.9. 滚动 Plotter 控件

![](img/5a524abdf0b0d58fa99d30abb4463611_200_0.png)

![](img/5a524abdf0b0d58fa99d30abb4463611_200_1.png)

在构造函数中，我们创建了两个 `QToolButton`，每个按钮带有一个图标。这些按钮允许用户进行放大和缩小。按钮的图标存储在资源文件中，因此任何使用 Plotter 控件的应用程序都需要在其 `.pro` 文件中包含此项。

```
RESOURCES = plotter.qrc
```

该资源文件与我们之前在 Spreadsheet 应用程序中使用的类似：

```
<RCC>
<resource>
  <file>images/zoomin.png</file>
  <file>images/zoomout.png</file>
</resource>
</RCC>
```

按钮上的 `adjustSize()` 调用将它们的大小设置为其尺寸提示（size hints）的大小。按钮没有被放入布局中；相反，我们将在 Plotter 的 `resizeEvent` 事件中手动对它们的位置。由于我们没有使用任何布局，我们必须通过将此传递给 `QToolButton` 构造函数来显式指定按钮的父对象。

结尾处的 `setPlotSettings()` 调用完成了初始化。

```cpp
void Plotter::setPlotSettings(const PlotSettings &settings)
{
  zoomStack.clear();
  zoomStack.append(settings);
  curZoom = 0;
  zoomInButton->hide();
  zoomOutButton->hide();
  refreshPixmap();
}
```

`setPlotSettings()` 函数用于指定用于绘制图表的 `PlotSettings`。它由 Plotter 构造函数调用，也可以由该类的用户调用。Plotter 从默认缩放级别开始。用户每次缩放，都会创建一个新的 `PlotSettings` 实例并放入栈中。缩放栈由两个成员变量表示：

- `zoomStack` 以 `QVector<PlotSettings>` 的形式存储当前的缩放状态
- `curZoom` 存储当前 `PlotSettings` 在 `zoomStack` 中的索引。

在调用 `setPlotSettings()` 之后，缩放栈只包含一个项目，放大和缩小按钮被隐藏。在我们在 `zoomIn()` 和 `zoomOut()` 槽对它们调用 `show()` 之前，这些按钮不会显示。（通常情况下，对顶层控件调用 `show()` 即可显示所有子控件。当我们显式对子控件调用 `hide()` 时，它会被隐藏，直到我们调用 `show()` 为止）。

调用 `refreshPixmap()` 对于更新显示是必要的。通常我们调用 `update()`，但在这里我们的处理方式不同，因为我们希望保持 `QPixmap` 始终是最新的。在重新生成像素图后，`refreshPixmap()` 调用 `update()` 将像素拷贝到控件上。

```cpp
void Plotter::zoomOut()
{
    if (curZoom > 0) {
        --curZoom;
        zoomOutButton->setEnabled(curZoom > 0);
        zoomInButton->setEnabled(true);
        zoomInButton->show();
        refreshPixmap();
    }
}
```

`zoomOut()` 槽在图表放大时执行缩小。它递减当前的缩放级别，并根据图表是否可以缩小来启用或禁用缩小按钮。放大按钮被启用并显示，通过调用 `refreshPixmap()` 更新显示。

```cpp
void Plotter::zoomIn()
{
    if (curZoom < zoomStack.count() - 1) {
        ++curZoom;
        zoomInButton->setEnabled(curZoom < zoomStack.count() - 1);
        zoomOutButton->setEnabled(true);
        zoomOutButton->show();
        refreshPixmap();
    }
}
```

如果用户之前放大过后又缩小了，那么下一个缩放级别的 `PlotSettings` 将位于缩放栈中，我们可以再次放大。（否则，仍然可以使用橡皮胶框进行缩放）。

该槽函数增加 `curZoom` 以移动到缩放栈中更深一层，根据是否可以进一步放大来启用或禁用放大按钮，并启用且显示缩小按钮。同样，我们调用 `refreshPixmap()` 让绘图器使用最新的缩放设置。

```cpp
void Plotter::setCurveData(int id, const QVector<QPoint> &data)
{
  curveMap[id] = data;
  refreshPixmap();
}
```

`setData()` 函数为给定的曲线 ID 设置曲线数据。如果 `curveMap` 中已存在相同 ID 的曲线，它将被新数据替换；否则，新曲线将直接插入。`curveMap` 成员变量类型为 `QMap<int, QVector<QPoint>>`。

```cpp
void Plotter::clearCurve(int id)
{
  curveMap.remove(id);
  refreshPixmap();
}
```

```cpp
QSize Plotter::minimumSizeHint() const
{
  return QSize(6 * Margin, 4 * Margin);
}
```

`minimumSizeHint()` 函数与 `sizeHint()` 类似。就像 `sizeHint()` 指定控件的理想大小一样，`minimumSizeHint()` 指定控件的理想最小大小。我们返回的值 300 x 200（因为 `Margin` 等于 50），以便为四周留出边距并为图表本身留出空间。

```cpp
QSize Plotter::sizeHint() const
{
    return QSize(12 * Margin, 8 * Margin);
}
```

Plotter 公有函数的审查结束。现在让我们查看保护函数。

```cpp
void Plotter::paintEvent(QEvent *event)
{
    QStylePainter painter(this);
    painter.drawPixmap(0, 0, pixmap);

    if (rubberBandVisible) {
        QStyleOption지역 option(rect);
        style()->drawPrimitive(QStyle::SolarBand, &option, &painter);
    }

    if (hasFocus()) {
        QStyleOptionRect option;
        option.initFrom(this);
        style()->drawPrimitive(QStyle::FrameFocus, &option, &painter);
    }
}
```

```cpp
void Plotter::resizeEvent(QResizeEvent *event)
{
```

```cpp
x = width() - (zoomInButton->width() + zoomInButton->width() + 10);
zoomInButton->move(x, 5);
zoomOutButton->move(x + zoomInButton->width() + 5, 5);
refreshPixmap();
```

当 Plotter 小部件触发 `resizeEvent()` 时，Qt 会生成一个“resize”（大小调整）事件。在这里，我们重新实现了 `resizeEvent()`，以便将放大按钮和缩小按钮放置在 Plotter 小部件的右上角。

我们将放大按钮和缩小按钮移动到并排位置，它们之间有 5 像素的间距，并且距离父部件的顶边缘和右边缘有 5 像素的偏移。

如果我们想让按钮固定在左上角（坐标为 (0, 0)），我们只需要在 Plotter 构造函数中将它们移动到那里即可。但我们想要跟踪右上角，因为那里的坐标取决于部件的大小。因此，我们需要重新实现 `resizeEvent()` 并设置按钮的位置。

我们没有在 Plotter 构造函数中为按钮设置任何位置。这并不是问题，因为 Qt 在小部件首次显示之前总是会生成大小调整事件。

重新实现 `resizeEvent()` 并手动布局子小部件的替代方案是使用布局管理器（例如 `QGridLayout`）。使用布局会稍微复杂一些，并消耗更多资源；另一方面，它能够优雅地处理阿拉伯语和希伯来语等语言的从右向左布局。

最后，我们调用 `refreshPixmap()` 在新的尺寸下重绘 pixmap。

```cpp
void Plotter::mousePressEvent(QMouseEvent *event)
{
    QRect rect(Margin, Margin,
               width() - 2 * Margin, height() - 2 * Margin);

    if (event->button() == Qt::LeftButton) {
        if (rect.contains(event->pos())) {
            rubberBandIsShown = true;
            rubberBandRect.setTopLeft(event->pos());
            rubberBandRect.setBottomRight(event->pos());
            updateRubberBandRegion();
            setCursor(Qt::CrossCursor);
        }
    }
}
```

当用户按下左鼠标键时，我们开始显示橡皮筋（rubber band）。这涉及将 `rubberBandShown` 设置为 true，用当前鼠标指针位置初始化 `rubberBandRect` 变量，调度一个画图事件来绘制橡皮筋，并将鼠标光标更改为十字形形状。

`rubberBandRect` 变量的类型为 `QRect`。一个 `QRect` 可以定义为 (x, y, width, height)——其中 (x, y) 是左上角的位置，width 和 height 是矩形的大小——也可以定义为左上角和右下角的坐标对。在这里，我们使用了坐标对表示。我们将用户点击的点同时设置为左上角和右下角。然后，我们调用 `updateRubberBandRegion()` 来强制对橡皮筋覆盖的（微小）区域进行重绘。

Qt 提供了两种控制鼠标光标形状的机制：

- `Widget::Cursor()` 设置鼠标悬停在特定小部件上时使用的光标形状。如果小部件没有设置光标，则使用父小部件的光标。顶层小部件的默认是箭头光标。
- `QApplication::setOverrideCursor()` 设置整个应用程序的光标形状，在调用 `restoreOverrideCursor()` 之前，它会覆盖单个小部件设置的光标。

在第 4 章中，我们使用 `QApplication::setOverrideCursor()` 配合 `Qt::WaitCursor` 将应用程序的光标更改为标准等待光。

```cpp
void Plotter::mouseMoveEvent(QMouseEvent *event)
{
  if (rubberBandIsShown) {
    updateRubberBandRegion();
    rubberBandRect.setBottomRight(event->pos());
    updateRubberBandRegion();
  }
}
```

当用户在按住左键时移动鼠标光标时，我们首先调用 `updateRubberBandRegion()` 调度一个画图事件来重绘橡皮筋所在的区域，然后重新计算 `rubberBandRect` 以考虑鼠标移动，最后再次调用 `updateRubberBandRegion()` 来重绘橡皮筋移动到的新区域。这有效地擦除了（旧的）区域。

如果用户向上或向左移动鼠标，`rubberBandRect` 的名义右下角可能会落到其左上角的上方或左侧。如果发生这种情况，`QRect` 将具有负的宽度或高度。我们在 `paintEvent` 中使用了 `QRect::normalized()` 来确保左上角和右下角坐标经过调整，以获得非负的宽度和高度。

代码视图：

```cpp
void Plotter::mouseReleaseEvent(QMouseEvent *event)
{
    if ((event->button() == Qt::LeftButton) && rubberBandIsShown) {
        rubberBandIsShown = false;
        updateRubberBandRegion();
        unsetCursor();
    }

    QRect rect = rubberBandRect.normalized();
    if (rect.width() < 4 || rect.height() < 4)
        return;
    rect.translate(-Margin, -Margin);

    PlotSettings prevSettings = zoomStack[curZoom];
    PlotSettings settings;
    double dx = prevSettings.spanX() / (width() - 2 * Margin);
    double dy = prevSettings.spanY() / (height() - 2 * Margin);
    settings.minX = prevSettings.minX + dx * rect.left();
    settings.maxX = prevSettings.maxX + dx * rect.right();
}
```

当用户在按住左键时移动鼠标时，我们首先调用 `updateRubberBandRegion()` 调度一个画图事件来重绘橡皮筋所在的区域，然后重新计算 `rubberBandRect` 以考虑鼠标移动，最后再次调用 `updateRubberBandRegion()` 第二次来重绘橡皮筋移动到的新区域。这有效地擦除了（旧的）区域。

如果用户向上或向左移动鼠标，`rubberBandRect` 的名义右下角可能会落到其左上角的上方或左侧。如果发生这种情况， `QRect` 将具有负的宽度或高度。我们在 `paintEvent` 中使用了 `QRect::normalized()` 来确保左上角和右下角坐标经过调整，以获得非负的宽度和高度。

当用户松开左键时，我们会重置橡皮筋。当 `rubberBandShown` 变量，，，，，显示橡皮筋，，重显示橡皮筋的区域。
