
```
private slots:
    void addContact() {
        Contact newContact = { "John Doe", "123-456-7890"
};
        model->addContact(newContact);
    }

private:
    ContactModel *model;
    QListView *listView;
};
```

## Running the Application:

In the main function, set up the application and show the main window.

cpp

Copy code

```
int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    MainWindow mainWindow;
    mainWindow.show();
    return app.exec();
}
```

## Conclusion

Data management in Qt through the Model/View architecture provides developers with powerful tools for handling and displaying data. By utilizing built-in models and views, as well as creating custom models and delegates, you can efficiently manage data in your applications. Understanding how to implement these components will allow you to build responsive and
interactive applications that provide a seamless user experience. In the next chapter, we will explore advanced GUI components and layouts in Qt, enhancing the visual appeal and functionality of our applications.

## Chapter 10: Advanced GUI Components and Layouts in Qt

Creating a user-friendly and visually appealing application requires a solid understanding of advanced GUI components and layouts. Qt provides a rich set of widgets and layout managers that enable developers to create complex user interfaces. In this chapter, we will explore various advanced components, their properties, and how to effectively utilize layouts to enhance the user experience.

## Advanced GUI Components

Qt offers a wide range of advanced GUI components that allow for sophisticated user interaction. Here are some key components to consider:

### QTabWidget:

The QTabWidget allows you to create a tabbed interface, which is useful for organizing multiple views within a single window. Each tab can contain different widgets or layouts, making it easy for users to navigate between different sections of your application.

```
cpp
Copy code
QTabWidget *tabWidget = new QTabWidget(this);
QWidget *firstTab = new QWidget();
QWidget *secondTab = new QWidget();
tabWidget->addTab(firstTab, "First Tab");
tabWidget->addTab(secondTab, "Second Tab");
```

### QStackedWidget:

The QStackedWidget provides a stack of widgets where only one widget is visible at a time. This component is
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

### QSplitter:

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

### QGroupBox:

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

```
QVBoxLayout *groupLayout = new QVBoxLayout();
groupLayout->addWidget(new QCheckBox("Option 1"));
groupLayout->addWidget(new QCheckBox("Option 2"));
groupBox->setLayout(groupLayout);
```

### QProgressBar:

The QProgressBar is used to indicate the progress of an operation. It can be set to show either a determinate or indeterminate state, depending on whether you know the total progress.

cpp

Copy code

```
QProgressBar *progressBar = new QProgressBar(this);
progressBar->setRange(0, 100);
progressBar->setValue(50); // Set current progress
```

### QLineEdit and QTextEdit:

These are essential components for text input. QLineEdit is designed for single-line text input, while QTextEdit supports multi-line text and rich text formatting. Both can be customized with validation rules, input masks, and other properties.

cpp

Copy code

```
QLineEdit *lineEdit = new QLineEdit(this);
lineEdit->setPlaceholderText("Enter text...");
QTextEdit *textEdit = new QTextEdit(this);
```

### QComboBox:

The QComboBox provides a drop-down list of options. This
component is useful for selecting from a predefined set of choices without taking up much screen space.

cpp
Copy code

```
QComboBox *comboBox = new QComboBox(this);
comboBox->addItem("Option 1");
comboBox->addItem("Option 2");
```

### QTreeWidget and QTableWidget:

The QTreeWidget is used to display hierarchical data, while QTableWidget is designed for tabular data. Both components offer built-in editing capabilities, making them easy to use for data entry applications.

cpp
Copy code

```
QTreeWidget *treeWidget = new QTreeWidget(this);
treeWidget->setHeaderLabel("Items");
QTreeWidgetItem *item = new QTreeWidgetItem(treeWidget);
item->setText(0, "Parent Item");
```

## Layout Management in Qt

Proper layout management is crucial for creating responsive and well-structured user interfaces. Qt provides several layout classes to arrange widgets within a container.

### QVBoxLayout and QHBoxLayout:

These layouts arrange widgets vertically and horizontally, respectively. They are straightforward to use and automatically adjust widget sizes based on their content.

cpp

Copy code

```
QVBoxLayout *vLayout = new QVBoxLayout();
vLayout->addWidget(new QPushButton("Button 1"));
vLayout->addWidget(new QPushButton("Button 2"));
```

### QGridLayout:

The QGridLayout arranges widgets in a grid format, allowing for more complex layouts. You can specify the row and column for each widget, enabling you to create forms and tables easily.

cpp

Copy code

```
QGridLayout *gridLayout = new QGridLayout();
gridLayout->addWidget(new QLabel("Name:"), 0, 0);
gridLayout->addWidget(new QLineEdit(), 0, 1);
gridLayout->addWidget(new QLabel("Email:"), 1, 0);
gridLayout->addWidget(new QLineEdit(), 1, 1);
```

### QFormLayout:

The QFormLayout is specialized for creating forms with labels and fields. This layout automatically aligns labels and input fields, enhancing readability.

cpp

Copy code

```
QFormLayout *formLayout = new QFormLayout();
formLayout->addRow("Username:", new QLineEdit());
formLayout->addRow("Password:", new QLineEdit());
```

### Nested Layouts:

You can nest layouts to create more complex arrangements.
For example, you can place a vertical layout inside a horizontal layout, allowing for a variety of arrangements.

```
```cpp
QHBoxLayout *hLayout = new QHBoxLayout();
QVBoxLayout *vLayout = new QVBoxLayout();
vLayout->addWidget(new QPushButton("Button 1"));
vLayout->addWidget(new QPushButton("Button 2"));
hLayout->addLayout(vLayout);
hLayout->addWidget(new QLabel("Label"));
```
```

### Spacer Items:

Spacer items are useful for creating flexible spaces within layouts. They allow you to control the positioning of widgets dynamically, providing a cleaner appearance.

```
```cpp
QSpacerItem *spacer = new QSpacerItem(20, 40, QSizePolicy::Minimum, QSizePolicy::Expanding);
vLayout->addItem(spacer);
```
```

## Example Application: A Simple To-Do List

To demonstrate the use of advanced GUI components and layouts, let’s create a simple to-do list application that allows users to add, remove, and display tasks.

### Setting Up the Main Window:

Begin by creating a main window with a QVBoxLayout to hold the components.

```
```cpp
class TodoWindow : public QMainWindow {
```
```

```
Q_OBJECT
public:
    TodoWindow(QWidget *parent = nullptr) :
QMainWindow(parent) {
        QWidget *centralWidget = new QWidget(this);
        setCentralWidget(centralWidget);

        QVBoxLayout *layout = new
QVBoxLayout(centralWidget);

        taskInput = new QLineEdit(this);
        addButton = new QPushButton("Add Task", this);
        taskList = new QListWidget(this);

        layout->addWidget(taskInput);
        layout->addWidget(addButton);
        layout->addWidget(taskList);

        connect(addButton, &QPushButton::clicked, this,
&TodoWindow::addTask);
    }

private slots:
    void addTask() {
        QString task = taskInput->text();
        if (!task.isEmpty()) {
            taskList->addItem(task);
            taskInput->clear();
        }
    }

private:
    QLineEdit *taskInput;
    QPushButton *addButton;
    QListWidget *taskList;
};
```
