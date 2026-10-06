
```cpp
if (newImage != image) {
    image = newImage.convertToFormat(QImage::Format_ARGB32);
    update();
    updateGeometry();
}
```

`setImage()` 函数将图像设为带有 Alpha 通道的 32 位，如果它尚未是这样。在代码的其他地方，我们假设图像数据存储为 32 位的 ARGB 值。

在设置图像变量后，我们调用 `QWidget::update()` 来调度使用新图像重绘部件。接下来，我们调用 `QWidget::updateGeometry()` 告诉包含该部件的任何布局部件的大小已更改。布局随后将自动适应新的尺寸提示（size hint）。

```cpp
void IconEditor::setZoomFactor(int newZoom) {
    if (newZoom < 1) {
        newZoom = 1;
    }

    if (newZoom != zoom) {
        zoom = newZoom;
        update();
        updateGeometry();
    }
}
```

`setZoomFactor()` 函数设置图像的缩放因子。为了防止其他地方出现除以零错误，我们修正了任何小于 1 的值。同样，我们调用 `update()` 和 `updateGeometry()` 来重绘部件并通知任何管理布局尺寸提示的更改。

`penColor()`、`iconImage()` 和 `zoomFactor()` 函数在头文件中实现为内联函数。

现在我们查看 `paintEvent()` 函数的代码。该函数是 `IconEditor` 最重要的函数。每当部件需要重绘时，它就会被调用。`QWidget` 中的默认实现什么都不做，让部件为空。

就像我们在第 3 章遇到的 `closeEvent()` 一样，`paintEvent()` 是一个事件处理器。Qt 有许多事件处理器，每个处理器对应一种类型的事件。第 7 章深入涵盖了事件处理。

在许多情况下，会生成绘制事件并调用 `paintEvent()`。例如：

- 当部件首次显示时，系统会自动生成一个绘制事件以强制部件进行自绘。
- 当部件调整大小时，系统会生成一个绘制事件。
- 如果部件被另一个窗口遮挡然后再次显示，将为隐藏的区域生成一个绘制事件（除非窗口系统存储了该区域）。

我们也可以通过调用 `Widget::update()` 或 `Widget::repaint()` 来强制触发绘制事件。这两个函数之间的区别是，`repaint()` 强制立即重绘，而 `update()` 只是在 Qt 处理事件时调度一个绘制事件。（如果部件在屏幕上不可，这两个函数都什么都不做）。如果多次调用 `update()`，Qt 会将连续的绘制事件压缩成单个绘制事件以避免闪烁。在 `IconEditor` 中，我们始终使用 `update()`。

以下是代码：

代码视图：

```cpp
void IconEditor::paintEvent(QPaintEvent event)
{
    QPainter painter(this);
    if (zoom >= 3) {
        painter.setPen(palette().foreground().color());
        for (int i = 0; i <= image.width(); ++i)
            painter.drawLine(i, 0, i, zoom * image.height());
        for (int j = 0; j <= image.height(); ++j)
            painter.drawLine(0, zoom, image.width(), zoom * j);
    }
    for (int i = 0; i < image.width(); ++i) {
        for (int j = 0; j < image.height(); ++j) {
            QRect rect = pixelRect(i, j);
            if (!event->region().intersect(rect).isEmpty()) {
                QColor color = QColor::fromRgba(image.pixel(i, j));
                if (color.alpha() < 255)
                    painter.fillRect(rect, Qt::white);
                painter.fillRect(rect, color);
            }
        }
    }
}
```

我们首先在部件上构造一个 `QPainter` 对象。如果缩放因子为 3 或更多，我们使用 `QPainter::drawLine()` 函数绘制水平和垂直线形成网格。调用 `QPainter::drawLine()` 的语法如下：

```cpp
painter.drawLine(x1, y1, x2, y2);
```

其中 `(x1, y1)` 是线条的一端的位置，`(x2, y2)` 是另一端的位置。还有一个接受两个 `QPoint` 而不是 `float` 的重载版本。

Qt 部件的左上角像素位于 (0,0)，右下角像素位于 (width() - 1, height() - 1)。这与传统的笛卡尔坐标系类似，但方向反相反，如图 5.3 所示。我们可以使用变换（如平移、缩放、旋转和倾斜）更改 `QPainter` 的坐标系。我们将在第 8 章介绍这些内容。

## 图 5.3 使用 QPainter 绘制线条

![](img/5a52abdf0b0d58fa99d30abb446361_185_0.png)
