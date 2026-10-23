transitions and interactive feedback.

```
```cpp
QPropertyAnimation *animation = new
QPropertyAnimation(slider, "value");
animation->setDuration(1000);
animation->setStartValue(0);
animation->setEndValue(100);
animation->start();
```
```

# Example Application: Drawing Shapes

To illustrate the concepts discussed in this chapter, we will create a simple application that allows users to draw shapes on a canvas using mouse events.

# Setting Up the Application:

Create a custom widget that captures mouse events and draws shapes based on user input.

```
```cpp
class DrawingWidget : public QWidget {
    Q_OBJECT

public:
    DrawingWidget(QWidget *parent = nullptr) :
    QWidget(parent) {}

protected:
    void paintEvent(QPaintEvent *event) override {
        QPainter painter(this);
        for (const QRect &rect : shapes) {
            painter.drawRect(rect);
        }
    }
}
```
```