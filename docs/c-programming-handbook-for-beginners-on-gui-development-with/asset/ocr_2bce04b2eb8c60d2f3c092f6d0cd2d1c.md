```
// Custom behavior before button press
QPushButton::mousePressEvent(event); // Call base class implementation
}
};
```

# Managing Multiple Event Sources

In more complex applications, you might have multiple widgets and event sources that need to be managed. Qt provides ways to handle events across different components seamlessly.

# Using Event Dispatchers:

For applications with multiple event sources, you can implement a centralized event dispatcher that manages events and routes them to the appropriate handlers.

```
cpp
Copy code
class EventDispatcher : public QObject {
    Q_OBJECT
public:
    void addEventSource(QObject *source) {
        // Add source and connect its signals
        connect(source, SIGNAL(someSignal()), this, SLOT(handleEvent()));
    }

public slots:
    void handleEvent() {
        // Handle events from any source
    }
};
```