
items can be selected.

## Single Selection
Only one item can be selected at a time.

## Multi Selection
Multiple items can be selected simultaneously.

## Extended Selection
Users can select a range of items by holding the Shift key.

```cpp
Copy code
tableView->setSelectionMode(QAbstractItemView::ExtendedSelection);
```

## Editing Items
By default, views are set to allow editing of items. To enable or disable editing, you can set the appropriate flags in your model.

```cpp
Copy code
Qt::ItemFlags CustomModel::flags(const QModelIndex &index) const {
    if (!index.isValid())
        return Qt::NoItemFlags;
    return Qt::ItemIsEditable | Qt::ItemIsEnabled |
Qt::ItemIsSelectable;
}
```

## Example Application: Implementing a Simple Table
To illustrate the Model-View architecture in action, let’s implement a simple application that displays a table of items.

## Creating the Model
Start by creating a custom model that holds a list of items.

```cpp
Copy code
class ItemModel : public QAbstractTableModel {
    Q_OBJECT
public:
    ItemModel(QObject *parent = nullptr) :
QAbstractTableModel(parent) {
        items = {"Item 1", "Item 2", "Item 3"};
    }

    int rowCount(const QModelIndex &parent =
QModelIndex()) const override {
        return items.size();
    }

    int columnCount(const QModelIndex &parent =
QModelIndex()) const override {
        return 1; // Single column for the item name
    }

    QVariant data(const QModelIndex &index, int role =
Qt::DisplayRole) const override {
        if (role == Qt::DisplayRole) {
            return items.at(index.row());
        }
        return QVariant();
    }
private:
    QStringList items;
};
```

## Setting Up the View
Use QTableView to display the items in the model.

```cpp
int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    ItemModel *model = new ItemModel();
    QTableView *tableView = new QTableView();
    tableView->setModel(model);
    tableView->show();
    return app.exec();
}
```

## Summary
This chapter provided a detailed overview of the Model-View architecture in Qt, highlighting the roles of models and views, the core classes involved, and how to create custom models. Understanding these concepts is essential for developing applications that effectively manage and present data. By leveraging the power of Qt's Model-View framework, developers can create responsive and user-friendly applications that handle data efficiently.

## Chapter 13: Event Handling and User Interaction in Qt
In Qt, user interaction and event handling are crucial for creating responsive and intuitive applications. This chapter delves into the event handling system in Qt, including how to respond to user inputs, manage events, and create an interactive user experience. We'll explore the concepts of signals and slots, event filters, and how to handle different types of events in a Qt application.

## Understanding Events in Qt
An event in Qt is a notification that something has occurred, such as a user action (like a mouse click or key press) or a system-triggered occurrence (like a timer timeout). Qt provides a comprehensive event handling mechanism that allows developers to respond to various events in their applications.

### Event Loop
The event loop is the core of Qt's event handling system. It continuously checks for events and dispatches them to the appropriate objects for handling. Every Qt application has an event loop that processes events sequentially.
To start the event loop, the QApplication::exec() method is called. This method blocks the program flow until the application exits.

```cpp
Copy code
int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    // Initialize application
    return app.exec(); // Start the event loop
}
```

## Event Types
Qt defines various event types, including:

**Mouse Events**: Triggered by mouse actions (e.g., QEvent::MouseButtonPress, QEvent::MouseMove).

**Keyboard Events**: Triggered by keyboard actions (e.g., QEvent::KeyPress, QEvent::KeyRelease).

**Timer Events**: Triggered when a timer times out (e.g., QEvent::Timer).

**Focus Events**: Triggered when a widget gains or loses focus (e.g., QEvent::FocusIn, QEvent::FocusOut).

## Handling Events in Qt
To handle events in Qt, you typically need to override specific event handler methods in your widget class. Each event type has a corresponding handler method that you can implement.

## Mouse Events
Mouse events can be handled by overriding the mousePressEvent(), mouseMoveEvent(), and mouseReleaseEvent() methods.

```cpp
Copy code
void MyWidget::mousePressEvent(QMouseEvent *event) {
    if (event->button() == Qt::LeftButton) {
        // Handle left mouse button press
    }
}

void MyWidget::mouseMoveEvent(QMouseEvent *event) {
    // Handle mouse movement
}
```

```cpp
void MyWidget::mouseReleaseEvent(QMouseEvent *event) {
    // Handle mouse button release
}
```

## Keyboard Events
Keyboard events are handled by overriding keyPressEvent() and keyReleaseEvent() methods.

```cpp
Copy code
void MyWidget::keyPressEvent(QKeyEvent *event) {
    if (event->key() == Qt::Key_Escape) {
        // Handle Escape key press
    }
}
```

```cpp
void MyWidget::keyReleaseEvent(QKeyEvent *event) {
    // Handle key release
}
```

## Timer Events
To handle timer events, you must start a timer and override the timerEvent() method.

```cpp
Copy code
void MyWidget::startTimer() {
    startTimer(1000); // Start a timer that triggers every second
}
```

```cpp
void MyWidget::timerEvent(QTimerEvent *event) {
    // Handle timer event
}
```

## Focus Events
Focus events can be handled by overriding focusInEvent() and focusOutEvent() methods.

```cpp
Copy code
void MyWidget::focusInEvent(QFocusEvent *event) {
    // Handle gaining focus
}

void MyWidget::focusOutEvent(QFocusEvent *event) {
    // Handle losing focus
}
```

## Signals and Slots: Qt's Communication Mechanism
One of the most powerful features of Qt is its signals and slots mechanism, which provides a way to communicate between objects. This mechanism allows you to connect signals (events) from one object to slots (functions) in another object.

## Signals
A signal is emitted when a particular event occurs. For example, a button can emit a clicked() signal when it is pressed.

```cpp
Copy code
QPushButton *button = new QPushButton("Click Me");
connect(button, &QPushButton::clicked, this, &MyClass::onButtonClicked);
```

## Slots
A slot is a function that is called in response to a particular signal. You can define your own slots or use existing ones.

```cpp
Copy code
void MyClass::onButtonClicked() {
    // Handle button click
}
```

## Connecting Signals and Slots
You can connect signals to slots using the connect() function. This establishes a relationship between the signal and the slot, enabling the slot to be called when the signal is emitted.

```cpp
Copy code
connect(senderObject, SIGNAL(signalName()),
receiverObject, SLOT(slotName()));
```

In modern Qt (Qt5 and later), you can use the new syntax:

```cpp
Copy code
connect(senderObject, &SenderClass::signalName,
receiverObject, &ReceiverClass::slotName);
```

## Emitting Signals
To emit a signal, simply call it like a regular function. For example, to emit a custom signal:

```cpp
Copy code
emit customSignal();
```

## Event Filters: Intercepting Events
Event filters allow you to intercept events before they reach the target object. This can be useful for implementing custom behavior or handling specific events without modifying the target object.

## Installing an Event Filter
You can install an event filter on an object using the `installEventFilter()` method.

```cpp
MyWidget *widget = new MyWidget();
widget->installEventFilter(this); // 'this' is the object that will handle the events
```

## Handling Events in the Filter
To handle events in the filter, you need to override the `eventFilter()` method.

```cpp
bool MyClass::eventFilter(QObject *obj, QEvent *event) {
    if (event->type() == QEvent::KeyPress) {
        QKeyEvent *keyEvent = static_cast<QKeyEvent *>(event);
        if (keyEvent->key() == Qt::Key_Space) {
            // Handle space key press
            return true; // Event handled
        }
    }
    return QObject::eventFilter(obj, event); // Pass the event to the base class
}
```
