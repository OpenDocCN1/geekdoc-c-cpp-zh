```
}
~MainWindow() {
    delete ui; // Clean up
}
private:
    Ui::MainWindow *ui;
};

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    MainWindow mainWindow;
    mainWindow.show();
    return app.exec();
}
```

In this example, the MainWindow class sets up the UI using the generated header file, allowing the application to render the designed interface when run.

# Best Practices for UI Design

When designing user interfaces, it's essential to follow best practices to ensure usability and accessibility.

**Consistency**: Maintain a consistent design across your application by using similar colors, fonts, and layouts. Consistency improves user experience and helps users navigate the application easily.

**User-Centric Design**: Consider the needs and expectations of your users when designing the interface. Use familiar widgets and interactions to make the application intuitive.

**Feedback Mechanisms**: Provide feedback for user actions, such as visual cues for button clicks or status messages