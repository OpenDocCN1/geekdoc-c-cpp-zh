

## 3. 创建主窗口

![](img/5a524abdf0b0d58fa99d30abb4463611_88_0.png)

- * 子类化 QMainWindow
- 创建菜单和工具栏
- 设置状态栏
- 实现文件菜单
- 使用对话框
- 存储设置
- 多文档支持
- 启动界面

本章将教你如何使用 Qt 创建主窗口。到本章结束时，你将能够构建应用程序的整个用户界面，包括菜单、工具栏、状态栏以及应用程序所需的任意对话框。

应用程序的主窗口为应用程序用户界面的构建提供了框架。图 3.1 所示的电子表格（Spreadsheet）应用程序的主窗口将构成本章的基础。该电子表格应用程序使用了我们在第 2 章中创建的“查找”、“跳转单元格”和“排序”对话框。

# 图 3.1. 电子表格应用程序

[查看全图]

![](img/5a524abdf0b0d58fa99d30abb4463611_89_0.png)

GUI 应用程序背后是一系列提供底层功能的代码——例如，读取和写入文件的代码或处理用户界面中显示的数据的代码。在第 4 章中，我们将学习如何实现此类功能，再次以电子表格应用程序作为示例。

### 子类化 QMainWindow

应用程序的主窗口是通过子类化 QMainWindow 创建的。我们在第 2 章看到的许多创建对话框的技巧也适用于创建主窗口，因为 QDialog 和 QMainWindow 都派自 QWidget。

可以使用 Qt Designer 创建主窗口，在本章中，我们将通过代码完成所有操作，以演示其实现方法。如果你更倾向于可视化的方法，请参阅 Qt 在线手册中的“在 Qt Designer 中创建主窗口”章节。

应用程序主窗口源代码分布在 `mainwindow.h` 和 `mainwindow.cpp` 中。让我们从头文件开始：

```cpp
#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow>

class QAction;
class QLabel;
class FindDialog;
class Spreadsheet;
```

```cpp
class MainWindow : public QMainWindow
{
  Q_OBJECT

public:
    MainWindow();

protected:
    void closeEvent(QCloseEvent *event);
```

我们将 `MainWindow` 类定义为 `QMainWindow` 的子类。它包含了 `Q_OBJECT` 宏，因为它提供了自己的信号和槽。

`closeEvent()` 函数是 `QWidget` 中的一个虚拟函数，当用户关闭窗口时会自动调用。我们在 `MainWindow` 中重新实现了它，以便向用户询问标准问题“你要保存更改吗？”并将用户偏好保存到磁盘。

```cpp
private slots:
    void newFile();
    void open();
    bool save();
    bool saveAs();
    void find();
    void gotoCell();
    void sort();
    void about();
```

一些菜单选项（如“文件|新建”和“帮助|关于”）在 `MainWindow` 中实现为私有槽。大多数槽的返回值为 `void`，但 `save()` 和 `saveAs()` 返回 `bool`。当在响应信号时执行时，返回值会被忽略；当我们像函数一样调用一个槽时，返回值对我们是可用的，就像调用任何普通的 C++ 函数一样。

```cpp
void openRecentFile();
    void updateStatusBars();
    void spreadsheetModified();
```

```cpp
private:
    void createActions();
    void createMenus();
    void createContextMenu();
    void createToolBars();
```

```cpp
void createStatusBar();
void readSettings();
void writeSettings();
bool okToContinue(const QString &fileName);
bool loadFile(const QString &fileName);
bool saveFile(const QString &fileName);
void setCurrentFile(const QString &fileName);
void updateRecentFileActions();
QString strippedName(const QString &fullFileName);
```

主窗口还需要一些槽和几个私有函数来支持用户界面。

```cpp
Spreadsheet *spreadsheet;
FindDialog findDialog;
QLabel locationLabel;
QLabel formulaLabel;
QString recentFiles;
QString curFile;

enum { MaxRecentFiles = 5 };
QAction recentFileActions[MaxRecentFiles];
QAction separatorAction;

QMenu fileMenu;
QMenu editMenu;
...
ToolBar fileToolbar;
QToolBar editToolbar;
QAction newAction;
QAction openAction;
...
QAction aboutQtAction;
```

除了私有槽和私有函数外，`MainWindow` 还有许多私有变量。我们将在使用它们时解释所有内容。

现在我们来看实现代码：

```cpp
#include <QtGui>
```

```cpp
#include "findddialog.h"
#include "gotocelldialog.h"
#include "mainwindow.h"
#include "sortdialog.h"
#include "spreadsheet.h"
```

我们包含了 `<QtGui>` 头文件，它包含了子类中使用的所有 Qt 类的定义。我们还包含了一些自定义头文件，特别是第 2 章中的 `findddialog.h`、`gotocelldialog.h` 和 `sortdialog.h`。

```cpp
MainWindow::MainWindow()
{
    spreadsheet = new Spreadsheet;
    setCentralWidget(spreadsheet);

    createActions();
    createMenus();
    createContextMenu();
    createToolBars();
    createStatusBar();

    readSettings();
    writeSettings();

    findDialog = new FindDialog(this);
}
```

