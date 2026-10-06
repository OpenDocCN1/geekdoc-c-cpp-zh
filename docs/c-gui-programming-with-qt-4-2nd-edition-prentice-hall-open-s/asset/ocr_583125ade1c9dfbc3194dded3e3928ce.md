# High-Quality Rendering with QImage

When drawing, we may be faced with a trade-off between speed and accuracy. For example, X11 and Mac OS X, drawing on a Widget Qpixmap relies on the platform's native paint engine. On X11, this ensures that communication with the X server is kept to a minimum; only paint commands are sent rather than actual image data. The main drawback of this approach is that Qt is limited by the platform's native support:

+   - On X11, features such as antialiasing and support for fractional coordinates are available only if the X Render extension is present on the X server.
- On Mac OS, the native aliased graphics engine uses different algorithms for drawing polygons than X11 and Windows, with slightly different results.

When accuracy is more important than efficiency, we can draw to QImage and copy the result onto the screen. This always uses Qt's internal paint engine, giving identical results on all platforms. The only restriction is that the QImage on which we paint must be created with an argument of QImage::Format_RGB32 or QImage::Format_ARGB32_Premultiplied.

Let's suppose we want to use antialiasing for drawing a widget, and we want to get good results on X11 systems with no X Render extension. The original paintEvent() handler, which relies on X Render for the antialiasing, might look like this:

```
void MyWidget::paintEvent(QPaintEvent *event)
{
    QPainter painter(this);
    painter.setRenderHint(QPainter::Antialiasing, true);
    draw(&painter);
}
```

Here's how to rewrite the widget's paintEvent() function to use Qt's platform-independent graphics engine:

```
void MyWidget::paintEvent(QPaintEvent *event)
{
```