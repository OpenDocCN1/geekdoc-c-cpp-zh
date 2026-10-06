
these use built-in brush patterns (Qt::SolidPattern, Qt::NoBrush). In modern applications, gradients are a popular alternative to monochrome fill patterns. Gradients rely on interpolation to obtain smooth transitions between two or more colors. They are frequently used to produce 3D effects; for example, the Plastique and Cleanlooks styles use gradients to render QPushButton.

Qt supports three types of gradients: linear, conical, and radial. The Oven Timer example in the next section combines all three of gradients in a single widget to make it look like the real thing.

- Linear gradients are defined by two control points and by a series of "color stops" on the line that connects these two points. For example, the linear gradient in Figure 8.6 is created using the following code:

```
QLinearGradient gradient(50, 100, 300, 350);
grad.setColorAt(0.0, Qt::white);
grad.setColorAt(0.2, Qt::green);
grad.setColorAt(1.0, Qt::black);
```

# Figure 8.6. QPainter's gradient brushes

![](img/5a524abdf0b0d58fa99d30abb4463611_292_0.png)

We specify three colors at three different positions between the two control points. Positions are specified as floating-point values between 0 and 1, where 0 corresponds to the first control point and 1 to the second control point. Colors between the specified stops are linearly interpolated.

- Radial gradients are defined by a center point (xc, yc), a radius r, and a focal point (xf, yf), in addition to the color stops. The center point and the radius specify a circle. The colors spread outward from the focal point, which can be Conical or any other point inside the circle.

Conical gradients are defined by a center point (xc, yc) and an angle a. The colors spread around the center point like the sweep of a watch's second hand.

So far, we have mentioned QPainter's pen, brush, and font settings. In addition to these, QPainter has other settings that influence the ways shapes and text are drawn:

- The background brush is used to fill the background of geometric shapes (underneath the brush pattern), text, and bitmaps when the background mode is Qt::OpaqueMode (the default is Qt::TransparentMode).

- The brush origin is the starting point for brush patterns, normally the top-left corner of the widget.

- The clip region is the area of the device that can be painted. Painting outside the clip region has no effect.

- The viewport, window, and world transform determine how logical QPainter coordinates map to physical device coordinates. By default, these are set up so that the logical and physical coordinate systems coincide. We cover coordinate systems in the next section.

- The composition mode specifies how the newly drawn pixels should interact with the pixels already present on the paint device. The default is "source over", where drawn pixels are alpha-blended on top of existing pixels. This is supported only on certain devices and covered later in this chapter.

At any time, we can save the current state of a painter on an internal stack by calling save() and restore it later by calling restore(). This can be useful if we want to temporarily change some painter settings and then reset them to their previous values, as we will see in the next section.

## 2. 2D Graphics

![](img/5a524abdf0b0d58fa99d30abb4463611_294_0.png)

- Painting with QPainter
- Coordinate System Transformations
- High-Quality Rendering with QImage
- Item-Based Rendering with Graphics View
- Printing

Qt's 2D graphics engine is based on the QPainter class. QPainter can draw geometric shapes (points, lines, rectangles, ellipses, arcs, chords, pie segments, polygons, curves), as well as pixmaps, images, and text. QPainter supports advanced features such as antialasing (for text and shape edges), alpha blending, gradient filling, and vector paths. QPainter supports linear transformations, such as translation, rotation, shearing, and scaling.

QPainter can be used to draw on a "paint device", such as a QWidget, a QPixmap, a QImage, or a QSvgGenerator. QPainter can also be used in conjunction with QPrinter for printing and generating PDF documents. This means that we can use the same code to display data onscreen and produce printed reports.

By reimplementing QWidget::paintEvent(), we can create custom widgets and exercise complete control over their appearance, as we saw in Chapter 5. For customizing the look and feel of predefined Qt widgets, we can also specify a style sheet or create a QStyle subclass; we cover both of these approaches in Chapter 19.

A common requirement is the need to display large numbers of lightweight items that the user can interact with on a 2D canvas. Qt 4.2 introduced a new "graphics view" architecture centered on the QGraphics, QGraphicsScene, and QGraphicsItem classes. This architecture offers a high-level interface for designing item-based graphics, and supports standard user actions on items, including moving, selecting, and grouping. The items themselves are drawn using QPainter as usual and can be transformed individually. We cover this architecture later in the chapter.

An alternative to QPainter is to use OpenGL commands. OpenGL is a standard library for drawing 3D graphics. In Chapter 20, we will see how to use the QtOpenGL module, which makes it easy to integrate OpenGL code into Qt applications.

### Painting with QPainter

To start painting to a paint device (typically a widget), we simply create a QPainter and pass a painter to the device. For example:

```cpp
void MyWidget::paintEvent(QPaintEvent *event)
{
    QPainter painter(this);
}
```

We can draw various shapes using QPainter's draw... functions. Figure 8.1 lists the most important. The way the drawing is performed is influenced by QPainter's settings. Some of these are adopted from the device, whereas others are initialized to default values. The three main settings are the pen, the brush, and the font. Figure 8.1. QPainter's most frequently used draw... functions:

![](img/5a524abdf0b0d58fa99d30abb4463611_296_0.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_1.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_2.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_3.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_4.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_5.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_6.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_7.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_8.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_9.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_10.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_11.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_12.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_13.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_14.png)

- The pen is used for drawing lines and shape outlines. It consists of a color, a width, a line style, a cap style, and a join style. The pen styles are shown in Figures 8.2 and 8.3.

### Figure 8.2. Cap and join styles

![](img/5a524abdf0b0d58fa99d30abb4463611_296_15.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_16.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_17.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_18.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_19.png)
![](img/5a524abdf0b0d58fa99d30abb4463611_296_20.png)

# Figure 8.3. Line width

| | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| SolidLine | | | | |
| DashLine | --- | ---- | ---- | ---- |
| DotLine | --- | --- | --- | --- |
| DashDotLine | ---- | ---- | ---- | ---- |
| DashDotDotLine | | | | | |
| NoPen | | | | | |

- The brush is the pattern used for filling geometric shapes. It normally consists of a color and a style, but it can also be a texture (a pixmap that is repeated infinitely) or a gradient. The brush styles are shown in Figure 8.4.

# Figure 8.4. Predefined brush styles

![](img/5a524abdf0b0d58fa99d30abb4463611_297_0.png)
