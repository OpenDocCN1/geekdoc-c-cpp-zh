

![](img/5a524abdf0b0d58fa99d30abb4463611_200_0.png)

![](img/5a524abdf0b0d58fa99d30abb4463611_200_1.png)

在构造函数中，我们创建了两个 QToolButton，每个按钮带有一个图标。这些按钮允许用户进行放大和缩小。按钮的图标存储在资源文件中，因此任何使用 Plotter 控件的应用程序都需要在其 .pro 文件中包含此项。

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

按钮上的 `adjustSize()` 调用将它们的大小设置为其尺寸提示（size hints）的大小。按钮没有被放入布局中；相反，我们将在 Plotter 的 `resizeEvent` 事件中手动对它们的位置。由于我们没有使用任何布局，我们必须通过将此传递给 QToolButton 构造函数来显式指定按钮的父对象。

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

`setPlotSettings()` 函数用于指定用于绘制图表的 PlotSettings。它由 Plotter 构造函数调用，也可以由该类的用户调用。Plotter 从默认缩放级别开始。用户每次缩放，都会创建一个新的 PlotSettings 实例并放入栈中。缩放栈由两个成员变量表示：

- `zoomStack` 以 `QVector<PlotSettings>` 的形式存储当前的缩放状态
- `curZoom` 存储当前 PlotSettings 在 `zoomStack` 中的索引。

在调用 `setPlotSettings()` 之后，缩放栈只包含一个项目，放大和缩小按钮被隐藏。在我们在 `zoomIn()` 和 `zoomOut()` 槽对它们调用 `show()` 之前，这些按钮不会显示。（通常情况下，对顶层控件调用 `show()` 即可显示所有子控件。当我们显式对子控件调用 `hide()` 时，它会被隐藏，直到我们调用 `show()` 为止）。

调用 `refreshPixmap()` 对于更新显示是必要的。通常我们调用 `update()`，但在这里我们的处理方式不同，因为我们希望保持 QPixmap 始终是最新的。在重新生成像素图后，`refreshPixmap()` 调用 `update()` 将像素拷贝到控件上。

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

如果用户之前放大过后又缩小了，那么下一个缩放级别的 PlotSettings 将位于缩放栈中，我们可以再次放大。（否则，仍然可以使用橡皮胶框进行缩放）。

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

`minimumSizeHint()` 函数与 `sizeHint()` 类似。就像 `sizeHint()` 指定控件的理想大小一样，`minimumSizeHint()` 指定控件的理想最小大小。我们返回的值 300 x 200（因为 Margin 等于 50），以便为四周留出边距并为图表本身留出空间。

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

