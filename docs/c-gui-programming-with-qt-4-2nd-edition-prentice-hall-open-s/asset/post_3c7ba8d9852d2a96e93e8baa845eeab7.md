
![](img/5a524abdf0b0d58fa99d30abb4463611_200_0.png)

![](img/5a524abdf0b0d58fa99d30abb4463611_200_1.png)

Still in the constructor, we create two QToolButton, each with an icon. These buttons allow the user to zoom in and out. The buttons' icons are stored in a resource file, so any application that uses the Plotter widget will need this entry in its .pro file.

```
RESOURCES = plotter.qrc
```

The resource file is similar to the one we have used for the Spreadsheet application:

```
<RCC>
<resource>
  <file>images/zoomin.png</file>
  <file>images/zoomout.png</file>
</resource>
</RCC>
```

The adjustSize() calls on the buttons set their sizes to be that of their size hints. The buttons are not put in a layout; instead, we will position them manually in the Plotter's resize event. Since we are not using any layouts, we must specify the buttons' parent explicitly by passing this to the QToolButton constructor.

The call to setPlotSettings() at the end completes the initialization.

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

setPlotSettings() function is used to specify PlotSettings to use for displaying the plot. It is called by the Plotter constructor and can be called by users of the class. The Plotter starts out at its default zoom level. Each time the user zooms, in a new PlotSettings instance is created and put onto the zoom. The zoom stack is represented by two member variables:

- zoomStack holds the current zooms as a QVector<PlotSettings>
- curZoom holds the current PlotSettings's index in the zoomStack.

After the call to setPlotSettings(), the zoom stack contains only one entry, and the Zoom In and Zoom Out buttons are hidden. These buttons will not be shown until we show() on them in the zoomIn() and zoomOut() slots. (Normally, it is sufficient to call show() on the top-level widget to show all the children. When we explicitly call hide() on a child widget, it is hidden until we call show().).

The call to refreshPixmap() is necessary to update the display. Usually, we call update(), but here we do things differently because we want to keep a QPixmap up-to-date at all times. After regenerating the pixmap, refreshPixmap() calls update() to copy the pixmap onto the widget.

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

The zoomOut() slot zooms out if the graph is zoomed in. It decrements the current zoom level and enables the Zoom Out button depending on whether the graph can be zoomed out or not. The Zoom In button is enabled and shown, and the display is updated with a call to refreshPixmap().

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

If the user has previously zoomed in and then out again, the PlotSettings for the next zoom level will be in the zoom stack, and we can zoom in. (Otherwise, it is still possible to zoom using a rubber band).

The slot increments curZoom to move one level deeper into the zoom stack, sets the Zoom button enabled or disabled depending on whether it is possible to zoom in any further, and enables and shows the Zoom Out button. Again, we call refreshPixmap() to make the plotter use the latest zoom settings.

```cpp
void Plotter::setCurveData(int id, const QVector<QPoint> &data)
{
  curveMap[id] = data;
  refreshPixmap();
}
```

The setData() function sets the curve data for a given curve ID. If a curve with the same ID already exists in curveMap, it is replaced with the new data; otherwise, the new curve is simply inserted. The curveMap member variable is of type QMap<int, QVector<QPoint>>.

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

The minimumSizeHint() function is similar to sizeHint(). Just as sizeHint() specifies a widget's ideal size, minimumSizeHint() specifies a widget's ideal size the value we return is 300 x 200 (since Margin equals 50) to allow for the margin on all four sides and some space for the plot itself.

```cpp
QSize Plotter::sizeHint() const
{
    return QSize(12 * Margin, 8 * Margin);
}
```

This finishes the review of Plotter's public functions. Now let's review the protected functions.

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
