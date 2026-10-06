```
#include "findddialog.h"
#include "gotocelldialog.h"
#include "mainwindow.h"
#include "sortdialog.h"
#include "spreadsheet.h"
```

We include the <QtGui> header file, which contains the definition of all the Qt classes used in our subclass. We also include some custom header files, notably findddialog.h, gotocelldialog.h, and sortdialog.h from Chapter 2.

```
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

    findDialog = 0;

    setWindowIcon(QIcon(":images/icon.png"));
    setCurrentFile("");
}
```

In the constructor, we begin by creating a Spreadsheet widget and setting it to the main window's central widget. The central widget occupies the middle of the main window (see Figure 3.2). The Spreadsheet class is a QWidget subclass with some spreadsheet capabilities, such as support for spreadsheet formulas. We will implement it in Chapter 4.

# Figure 3.2. QMainWindow's areas