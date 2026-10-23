```
QPushButton *button1 = new QPushButton("Button 1", this);
QPushButton *button2 = new QPushButton("Button 2", this);
buttonLayout->addWidget(button1);
buttonLayout->addWidget(button2);
mainLayout->addLayout(buttonLayout);
setLayout(mainLayout);
```

# Spacing and Margins:

Layouts in Qt can be customized using spacing and margins.
You can set the spacing between widgets and the margins around the layout. For example:

cpp
Copy code

```
layout->setSpacing(10); // Set spacing between widgets
layout->setContentsMargins(5, 5, 5, 5); // Set margins (left, top, right, bottom)
```

# Custom Widget Creation

In many cases, the provided widgets may not meet all requirements, and you may need to create custom widgets. Custom widgets allow you to encapsulate complex functionality and create reusable components.

# Subclassing QWidget:

To create a custom widget, subclass QWidget (or another existing widget) and implement your specific logic. Here’s a basic example of a custom widget that displays a colored rectangle:

cpp
Copy code

```
class ColorWidget : public QWidget {
public:
```