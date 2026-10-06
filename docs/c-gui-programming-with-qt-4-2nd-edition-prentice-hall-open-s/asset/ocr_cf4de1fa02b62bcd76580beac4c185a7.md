# # Subclass QStyle

The QStyle class was introduced with Qt 2.0 to provide a means of encapsulating an application's look and feel. Classes such as QAnimationStyle, QMotifStyle, QCDStyle implemented the look and feel for the platforms and desktop environments on which Qt ran. Qt 4.3 provides eight styles, in addition to the QStyle abstract base class and the base class QCommonStyle. Figure 19.16 shows how they relate to each other.

**Figure 19.16. Inheritance tree for Qt's built-in styles**

![](bbox=[0.01, 0.23, 0.58, 0.41])

For Qt developers, the QStyle architecture makes it possible to develop a custom look and feel by subclassing QStyle or one of the existing styles. We can perform minor customizations on an existing style (e.g., QAnimationStyle), or we can develop an entire custom style from scratch.

The QStyle API provides functions for drawing graphical elements (such as drawPrimitive(), drawControl(), drawComplexControl(), etc.) and for querying the style (pixelMetrics(), styleHint(), hitTest(), etc.). The QStyle member functions typically take a QStyleOption object that holds both general information about the widget being drawn (such as its palette) and widget-specific information (e.g., the text of a button). The functions also take an optional pointer to a QWidget, to situations where the QStyleOption doesn't provide all the necessary information.

Suppose we want to create a MyPushButton class, which would look like a standard Qt button but without deriving from QPushButton. (This example is rather convoluted, but it will help us to clarify the relationship between widgets and styles.) In the MyPushButton event handler, we would set up a QStyleOption (actually, a QStyleOptionButton) and call QStyle::drawControl() as follows:

```
void MyPushButton::paintEvent(QPaintEvent * /* event */)
{
    QPainter painter(this);

    QStyleOptionButton option;
    option.initFrom(this);
```