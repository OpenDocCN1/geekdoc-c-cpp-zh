# Running the Application:

In the main function, initialize the application and display the main window.

cpp
Copy code

```
int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    TodoWindow window;
    window.setWindowTitle("To-Do List");
    window.resize(300, 400);
    window.show();
    return app.exec();
}
```

# Customizing Widgets

Beyond using default properties, customizing widget appearance can enhance user experience. Qt allows you to change the look and feel of widgets using stylesheets.

# Applying Stylesheets:

Stylesheets in Qt provide a powerful way to customize the appearance of widgets similar to CSS. You can change colors, borders, padding, and more.

cpp
Copy code

```
QPushButton *button = new QPushButton("Click Me", this);
button->setStyleSheet("background-color: blue; color: white; font-size: 16px;");
```

# Using QPalette:

The QPalette class enables you to customize widget colors at a more fundamental level. You can set colors for different