
fill with the widget's eraser color. This is "dark" of the palette, because of the call to setBackgroundRole() in the Plotter constructor. If the background is a non-solid brush, Qpixmap::fill() needs to know the offset to align the brush correctly. Here, the pixmap corresponds to the entire widget, so we position (0, 0).

We create a QPainter to draw on the pixmap. The initComponents() sets the painter's pen, background, and font to the same ones as the Plotter next. We call drawGrid() and drawCurves() to perform the drawing. At the end, we call update() to schedule a paint event for the widget. The pixmap is copied to the widget in the paintEvent() function (p. 12B).

Code View:

```
void Plotter::drawGrid(QPainter *painter)
{
    QRect rect(Margin, Margin,
               width() - 2 * Margin, height() - 2 * Margin);

    if (!rect.isValid())
        return;

    PlotSettings settings = zoomStack()[curZoom];
    QPen quiteDark = palette().dark().color().light();
    QPen light = palette().light().color();

    for (int i = 0; i <= settings.numXTicks; ++i) {
        int x = rect.left() + (i * (rect.width() - 1) / settings.numXTicks);
        double label = settings.minX + (i * settings.spanX / settings.numXTicks);
        painter->setPen(quiteDark);
        painter->drawLine(x, rect.top(), x, rect.bottom());
        painter->setPen(light);
        painter->drawLine(x, rect.bottom(), x, rect.bottom() + 5);
        painter->drawText(x - 5, rect.bottom() + 50, 50, 200, Qt::AlignHCenter | Qt::AlignTop,
                          QString::number(label));
    }
    for (int j = 0; j <= settings.numYTicks; ++j) {
        int y = rect.bottom() - (j * (rect.height() - 1) / settings.numYTicks);
        double label = settings.minY + (j * settings.spanY / settings.numYTicks);
        painter->setPen(quiteDark);
        painter->drawLine(rect.left(), y, rect.right(), y);
        painter->setPen(light);
        painter->drawLine(rect.left() - 5, y, rect.left(), y);
        painter->drawText(rect.left(), Margin, y - 10, Margin - 5, Qt::AlignRight | Qt::AlignVCenter, QString::number(label));
    }
    painter->fillRect(rect.adjusted(0, 0, -1, -1));
}
```

The drawGrid() function draws the grid behind the curves and the axes. The area on which we draw the grid is specified by rect. If the widget isn't large enough to accommodate the graph, we return immediately.

The first for loop draws the grid's vertical lines and the ticks along the x-axis. The second for loop draws the grid's horizontal lines and the ticks along the y-axis. At the end, we draw a rectangle along the margins. The drawText() function is used to draw the numbers corresponding to the text marks on both axes.

The calls to drawText() have the following syntax:

```
painter->drawText(x, y, width, height, alignment, text);
```

where (x, y, width, height) define a rectangle, alignment the position of the text within that rectangle, and text the to draw. In this example, we have calculated the rectangle in which to draw the text manually; a more adaptable alternative would involve calculating the text's bounding rectangle using QMetrics.

Code View:

```
void Plotter::drawCurves(QPainter *painter){
    static const QColor colorForIds[6] = {
        Qt::red, Qt::green, Qt::blue, Qt::cyan, Qt::magenta, Qt::yellow};
    PlotSettings settings = zoomStack[curZoom];
    QRect rect(Margin, Margin, width() - 2 * Margin, height() - 2 * Margin);
    if (!rect.isValid())
        painter->setClipRect(rect.adjusted(+1, +1, -1, -1));
    QMapIterator<int, QVector<QPointF>> i(curveMap);

    while (i.hasNext()) {
        i.next();

        int id = i.key();
        QVector<QPointF> data = i.value();
        QPolygonF poly(data.count());
        for (int j = 0; j < data.count(); ++j) {
            double dx = data[j].x() - settings.minX;
            double dy = data[j].y() - settings.minY;
            double x = rect.left() + (dx * (rect.width() - 1) / settings.spanX());
            double y = rect.bottom() - (dy * (rect.height() - 1) / settings.spanY());
            poly[j] = QPointF(x, y);
        }
        painter->setPen(colorIds[id] % 6);
        painter->drawPolyline(poly);
    }
}
```

The drawCurves() function draws the curves behind the grid and the axes. We start by calling setClipRect() to set the area. If the widget is not large enough to accommodate the graph, we return immediately.

Next, we use a MapIterator to iterate over the curve map. For each curve, we translate the data points from plot coordinate system to widget coordinates. We then set the color based on the curve's ID and draw the curve as a polyline.

The drawCurves() function draws the curves on top of the grid. We start by calling setClipRect() to set the area. If the widget is not large enough to accommodate the graph, we return immediately.

Next, we use a MapIterator to iterate over the curve map. For each curve, we translate the data points from plot coordinate system to widget coordinates. We then set the color based on the curve's ID and draw the curve as a polyline.

The drawCurves() function draws the curves on top of the grid. We start by calling setClipRect() to set the area. If the widget is not large enough to accommodate the graph, we return immediately.
