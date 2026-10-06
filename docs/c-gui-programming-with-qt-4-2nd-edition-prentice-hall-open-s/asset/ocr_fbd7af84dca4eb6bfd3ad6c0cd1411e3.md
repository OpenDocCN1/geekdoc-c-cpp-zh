# Implementing Application Functionality

![](bbox=[0.012, 0.046, 0.191, 0.133])

+   * The Central Widget
* Subclassing QTableWidget
* Loading and Saving
* Implementing the Edit Menu
* Implementing the Other Menus
* Subclassing QTableWidgetItem

In the previous two chapters, we explained how to create the Spreadsheet application's user interface. In this chapter, we will complete the program by coding its underlying functionality. Among other things, we will see how to load and save files, how to store data in memory, how to implement clipboard operations, and how to add support for spreadsheet formulas to QTableWidget.

# The Central Widget

The central area of QMainWindow can be occupied by any kind of widget. Here's an overview of the possibilities:

# 1. Use a standard Qt widget.

A standard widget as QTableWidget or QTextEdit can be used as the central widget. In this case, the application's functionality, such as loading and saving files, must be implemented elsewhere (e.g., in QMainWindow subclass).

# 2. Use a custom widget.

Specialized applications often need to show data in a custom widget. For example, an icon editor program would have an IconEditor widget as its central widget. Chapter 5 explains how to write custom widgets in Qt.

# 3. Use a plain QWidget with a layout manager.

Sometimes the application's central area is occupied by many widgets. This can be done by using a QWidget as the parent of all the other widgets, and using layout managers to size and position the child widgets.