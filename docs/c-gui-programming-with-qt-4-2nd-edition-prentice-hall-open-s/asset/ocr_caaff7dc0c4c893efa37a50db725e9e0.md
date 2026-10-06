![](bbox=[0.012, 0.007, 0.595, 0.381])

Behind GUI applications lies a body of code that provides the underlying functionality—for example, code to read and write files or to process the data presented in the user interface. [Chapter 4](#), we will see how to implement such functionality, again using the Spreadsheet application as our example.

# Subclassing QMainWindow

An application's main window is created by subclassing [QMainWindow](#). Many of the techniques we saw in [Chapter 2](#) for creating dialogs are also relevant for creating main windows, since both [QDialog](#) and [QMainWindow](#) are derived from [QWidget](#).

Main windows can be created using Qt Designer, and in this chapter we will do everything in code to demonstrate how it's done. If you prefer the more visual approach, see the "Creating Main Windows in Qt Designer" chapter in Qt Designer's online manual.

The source code for the application's main window is spread across [mainwindow.h](#) and [mainwindow.cpp](#). Let's start with the header file:

```
#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow>

class QAction;
class QLabel;
class FindDialog;
class Spreadsheet;
```