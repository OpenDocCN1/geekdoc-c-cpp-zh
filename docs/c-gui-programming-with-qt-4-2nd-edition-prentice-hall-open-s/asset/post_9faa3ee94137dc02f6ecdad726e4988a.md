
Now comes the world transform. The world transform is a transformation matrix that is applied in addition to the window–viewport conversion. It allows us to translate, scale, rotate, or shear the items we are drawing. For example, if we wanted to draw text at a 45° angle, we would use this code:

```
QTransform transform;
transform.rotate(+45.0);
painter.setWorldTransform(transform);
painter.drawText(pos, tr("Sales"));
```

The logical coordinates we pass to `drawText()` are converted by the world transform, then mapped to physical coordinates using the window–viewport settings.

If we specify multiple transformations, they are applied in the order in which they are given. For example, if we want to use the point (50, 50) as the rotation's pivot point, we can do so by translating the window by (+50, +50), performing the rotation, and then translating the window back to its original position:

```
QTransform transform;
transform.translate(+50.0, +50.0);
transform.rotate(+45.0);
transform.translate(-50.0, -50.0);
painter.setWorldTransform(transform);
painter.drawText(pos, tr("Sales"));
```

A simpler way to specify transformations is to use `QPainter`'s `translate()`, `scale()`, `rotate()`, and `shear()` convenience functions:

```
npainter.translate(-50.0, -50.0);
painter.rotate(+45.0);
painter.translate(+50.0, +50.0);
painter.drawText(pos, tr("Sales"));
```

if we want to use the same transformations repeatedly, it is more efficient to store them in a QTransform object and set the world transform on the painter whenever the transformations are needed.

To illustrate painter transformations, we will review the code of the OvenTimer widget shown in Figures 8.11 and 8.12. The OvenTimer widget is modeled after the kitchen timers that were used before it was common to have ovens with clocks built-in. The user can click a notch to set the duration. The wheel automatically turns counterclockwise until 0 is reached, at which point OvenTimer emits the timeout() signal.

# Figure 8.11. The OvenTimer widget

![](img/5a524abdf0b0d58fa99d30abb4463611_304_0.png)

# Figure 8.12. The OvenTimer widget at three different sizes

![](img/5a524abdf0b0d58fa99d30abb4463611_304_1.png)

```
class OvenTimer : public QWidget
{
    Q_OBJECT
public:
    OvenTimer(QWidget parent = 0);

    void setDuration(int secs);

```
int duration() const;
void draw(QPainter painter);
```

signals:
void timeout();

protected:
void paintEvent(QPaintEvent event);
void mousePressEvent(QMouseEvent event);

private:
QDateTime finishTime;
QTimer updateTimer;
QTimer finishTimer;
};
```

OvenTimer class is derived from QWidget and reimplements two virtual functions: paintEvent() and mousePressEvent().

```
const double DegreesPerMinute = 7.0;
const double DegreesPerSecond = DegreesPerMinute / 60;
const int MaxMinutes = 45;
const int MaxSeconds = MaxMinutes * 60;
const int UpdateInterval = 5;
```

In oventimer.cpp, we start by defining a few constants that control the oven timer's look and feel.

OvenTimer::OvenTimer(QWidget *parent)
: QWidget(parent)

```
{
finishTime = QDateTime::currentDateTime();
updateTimer = new QTimer(this);
connect(updateTimer, SIGNAL(timeout()), this, SLOT(update));
```

```
finishTimer = new QTimer(this);
finishTimer->setSingleShot(true);
connect(finishTimer, SIGNAL(timeout()), this, SIGNAL(timeout()));
connect(finishTimer, SIGNAL(timeout()), updateTimer, SLOT(stop));
```

```
QFont font;
font.setPointSize(8);
setFont(font);
```
}

In the constructor, we create two QTimer objects: updateTimer is used to refresh the appearance of the widget every five seconds, finishTimer emits the widget's timeout() signal when the oven timer reaches 0. The finishTimer needs to time out only, so we call setSingleShot(true); by default, timers fire repeatedly until they are stopped or destroyed. The last connect() call is an optimization to stop updating the widget when the timer is inactive.

At the end of the constructor, we set the point size of the font used for drawing the widget to 9 points. At the end, this is done to ensure that the numbers displayed on the widget have approximately the same size everywhere.

```
void OvenTimer::setDuration(int secs)
{
    secs = qBound(0, secs, MaxSeconds);

    finishTime = QDateTime::currentDateTime().addSecs(secs);

    if (secs > 0)
        updateTimer->start(UpdateInterval 1000);
        finishTimer->start(secs 1000);
    } else {
        updateTimer->stop();
        finishTimer->stop();
    }
    update();
}
```

The setDuration() function sets the duration of the oven timer to the given number of seconds. Using Qt's qBound() function means that we can avoid writing code such as this:

```
if (secs < 0) {
    secs = 0;
} else if (secs > MaxSeconds) {
    secs = MaxSeconds;
}
```

We compute the finish time by adding the duration to the current time (obtained from QDateTime::currentDateTime()) and store it in the finishTime private variable. At the end, we call update() to redraw the widget with the new duration.

The finishTime variable is of type QDateTime. Since the variable holds both a date, we avoid a wrap-around bug when the current time is before midnight and the finish time is after midnight.

```
int OvenTimer::duration() const
{
    int secs = QDateTime::currentDateTime().secsTo(finishTime);
    if (secs < 0)
        secs = 0;
    return secs;
}
```

The duration() function returns the number of seconds left before the timer expires. If the timer is inactive, we return 0.

```
void OvenTimer::mouseEvent(MouseEvent event)
{
    QPoint point = event.pos() - rect().center();
    double theta = std::atan2(-point.x(), point.y()) * 180.0 / M_PI;
    setDuration(int(theta / DegreesPerSecond));
}
```

```
void OvenTimer::paintEvent(QPaintEvent *event)
{
    QPainter painter(this);
    painter.setRenderHint(QPainter::Antialasing, true);

    int side = qMin(width(), height());

    painter.setViewport((width() - side) / 2, (height() - side) / 2, side, side);
    painter.setWindow(-50, -50, 100, 100);

    draw(&painter);
}
```

In paintEvent(), we set the viewport to be the largest square that fits inside the widget. we set the window to the 100x100 rectangle extending from (-50, -50) to (+50, +50). The draw() function actually performs the drawing.

```
void OvenTimer::draw(QPainter *painter)
{
    static const int triangle[3][2] = {
        {-2, -49}, {2, -49}, {0, -47}
    };
    QPen thickPen(palette().foreground(), 1.5);
    QPen thinPen(palette().foreground(), 0.5);

    painter->setPen(thinPen);
    painter->setBrush(palette().foreground());
    painter->drawPolygon(QPolygon(3,&triangle[0][0]));
}
```

We start by drawing the tiny triangle that marks the 0 position at the top of the widget. The triangle is specified by three hard-coded coordinates, and we use drawPolygon() to render it.

What is so convenient about the window–viewport mechanism is that we can hardcode the coordinates we use in the draw commands and still get good resizing behavior.

```
QConicalGradient coneGradient(0, 0, -90.0);
coneGradient.setColorAt(0.0, Qt::darkGray);
coneGradient.setColorAt(0.2, niceBlue);
coneGradient.setColorAt(0.5, Qt::white);
coneGradient.setColorAt(1.0, Qt::darkGray);

painter->setBrush(coneGradient);
painter->drawEllipse(-46,-46, 92, 92);
```

We draw the outer circle and fill it using a conical gradient. The gradient's center point is located at (0, 0), and the angle is -90°.
