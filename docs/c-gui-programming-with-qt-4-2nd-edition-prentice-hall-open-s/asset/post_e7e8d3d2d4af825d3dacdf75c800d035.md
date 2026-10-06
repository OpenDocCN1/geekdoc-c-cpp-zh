
button.png as the border image. However, this time, we specify a border width of 16, to scale the image down, and specify a fixed size of the contents of 7 pixels horizontally and 6 pixels vertically. Figure 19.14 shows a schematic of what we have done.

# Figure 19.14. The editable QComboBox's drop-down button's border image

![](img/5a524abdf0b0d58fa99d30abb4463611_743_0.png)

If the combobox is open, we use a different, darker image for the drop-down button:

```
QComboBox::drop-down:editable:open {
  border-image: url(:images/button-pressed.png) 16;
}
```

For editable comboboxes, we specify a right margin of 29 pixels to provide space for the drop-down button, as shown on Figure 19.15:

```
QComboBox::editable {
  margin-right: 29px;
}
```

# Figure 19.15. Structure of an editable QComboBox

![](img/5a524abdf0b0d58fa99d30abb4463611_743_1.png)

We have now finished creating our Candy style sheet. The style sheet is about 100 lines long, and makes use of a few custom images. The result is a highly distinctive dialog.

Creating a custom style using style sheets can involve quite a lot of trial and error, especially for those who have not used CSS before. One of the main challenges with style sheets is that CSS conflict resolution and cascading don't always give intuitive results. For further details, see the online documentation at http://doc.trolltech.com/4.3/stylesheet.html. This describes Qt's style sheet support and provides links to the CSS specification.

## Subclass QStyle

The QStyle class was introduced with Qt 2.0 to provide a means of encapsulating an application's look and feel. Classes such as QAnimationStyle, QMotifStyle, QCDStyle implemented the look and feel for the platforms and desktop environments on which Qt ran. Qt 4.3 provides eight styles, in addition to the QStyle abstract base class and the base class QCommonStyle. Figure 19.16 shows how they relate to each other.

**Figure 19.16. Inheritance tree for Qt's built-in styles**

![](img/5a524abdf0b0d58fa99d30abb4463611_745_0.png)

For Qt developers, the QStyle architecture makes it possible to develop a custom look and feel by subclassing QStyle or one of the existing styles. We can perform minor customizations on an existing style (e.g., QAnimationStyle), or we can develop an entire custom style from scratch.

The QStyle API provides functions for drawing graphical elements (such as drawPrimitive(), drawControl(), drawComplexControl(), etc.) and for querying the style (pixelMetrics(), styleHint(), hitTest(), etc.). The QStyle member functions typically take a QStyleOption object that holds both general information about the widget being drawn (such as its palette) and widget-specific information (e.g., the text of a button). The functions also take an optional pointer to a QWidget, to situations where the QStyleOption doesn't provide all the necessary information.

Suppose we want to create a MyPushButton class, which would look like a standard Qt button but without deriving from QPushButton. (This example is rather convoluted, but it will help us to clarify the relationship between widgets and styles.) In the MyPushButton event handler, we would set up a QStyleOption (actually, a QStyleOptionButton) and call QStyle::drawControl() as follows:

```
void MyPushButton::paintEvent(QPaintEvent * /* event */)
{
    QPainter painter(this);

    QStyleOptionButton option;
    option.initFrom(this);
    if (isFlat())
        option.features |= QStyleOptionButton::Flat;
    option.text = text();

    style()->drawControl(QStyle::CE_PushButton, &option, &painter, this);
}
```

The QStyleOption::initFrom function initializes the fundamental member variables that represent a widget, as rect, state (enabled, focused, etc.), and palette. Member variables specific to QStyleOptionButton must be initialized in this manner. In the MyPushButton example, we initialize features and text and iconSize take their default values.

The QWidget::style function returns the appropriate style for drawing the widget. The style is normally set for the entire application using QApplication::setStyle(), but it is also possible to override it for individual widgets using QWidget::setStyle().

The drawControl function is implemented by the various QStyle subclasses to draw QPushButton and other simple widgets. A typical implementation might look like this:

```
void QMotStyle::drawControl(ControlElement element,
                             const QStyleOption *option,
                             QPainter painter,
                             const QWidget widget) const
{
    switch (element) {
    case CE_CheckBox:
        ...
    case CE_RadioButton:
        ...
    case CE_PushButton:
        if (const QStyleOptionButton *buttonOption =
            qstyleoption_cast<const QStyleOptionButton *>(option))
            // draw push button
        break;
        ...
    }
}
```

The element indicates the style code of widget to draw. If the type is CE_PushButton, the QStyle subclass uses the QOption parameter. If the cast is successful, the push button is drawn. The drawback with this version is that QPushButton cannot be used to render. For this reason, the built-in QStyle subclasses use the QOption parameter whenever possible to obtain information about the widget. In the rest of this section, we will review the code for the Bronze style shown in Figure 19.17. The Bronze style features round buttons with gradient background, unconventional placement of spin buttons, extravagant checkmarks, and a "brushed" background. To implement this, it uses advanced 2D graphics such as antialiasing, semi-transparency, linear gradients, and composition modes.

# Figure 19.17. Widgets in the style

![](img/5a524abdf0b0d58fa99d30abb4463611_747_0.png)

Here is the BronzeStyle class definition:

Code View:

```
class BronzeStyle : public QStyle
{
    Q_OBJECT

public:
    BronzeStyle() {}

    void polish(QPalette &palette);
    void polish(QWidget widget);
    void unpolish(QWidget widget);
    int styleHint(StyleHint which, const QStyleOption option,
                  const QWidget widget = 0,
                  QStyleHintReturn returnData = 0) const;
    int pixelMetric(PixelMetric which, const QStyleOption option,
                    const QWidget widget = 0) const;
    void drawPrimitive(PrimitiveElement which,
                       const QStyleOption option, QPainter painter,
                       const QWidget widget = 0) const;
    void drawComplexControl(ComplexControl which, const QStyleOptionComplex option,
                            QPainter painter,
                            const QWidget widget = 0) const;
    QRect subControl(ComplexControl which, const QStyleOptionComplex option,
                    SubControl sub,
                    const QWidget widget = 0) const;

public slots:
    QIcon standardIconImplementation(StandardPixmap which,
                                     const QStyleOption option,
                                     const QWidget widget = 0) const;

private:
    void drawBronzeFrame(const QStyleOption option,
                          QPainter painter) const;
    void drawBronzeBevel(const QStyleOption option,
                          QPainter painter) const;
    void drawBronzeCheckBoxIndicator(const QStyleOption option,
                                     QPainter painter) const;
    void drawBronzeSpinBoxButton(SubControl which,
                                 const QStyleOptionComplex option,
                                 QPainter *painter) const;
};
```

When creating a custom style, we usually base it on an existing style so that we
