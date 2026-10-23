useful for creating wizard-style interfaces or any scenario
where you want to switch between different views without
cluttering the user interface.

```
```cpp
QStackedWidget *stackedWidget = new QStackedWidget(this);
stackedWidget->addWidget(new QWidget()); // Add first page
stackedWidget->addWidget(new QWidget()); // Add second page
```
```

# QSplitter:

The QSplitter allows users to resize widgets within a layout
dynamically. This is useful when you want to provide a more
flexible interface. You can add multiple widgets to a splitter,
and users can adjust their sizes by dragging the separator.

```
```cpp
QSplitter *splitter = new QSplitter(this);
splitter->addWidget(new QTextEdit());
splitter->addWidget(new QListView());
```
```

# QGroupBox:

The QGroupBox is used to group related widgets together,
enhancing the organization of your UI. You can add a title to
the group box, making it clear what the contained widgets
represents.

```
```cpp
QGroupBox *groupBox = new QGroupBox("Group Title",
this);
```
```