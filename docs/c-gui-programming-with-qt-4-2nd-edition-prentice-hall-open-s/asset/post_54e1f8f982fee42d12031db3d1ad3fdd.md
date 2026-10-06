
```cpp
"Qt classes."));
```

The About box is obtained by calling QMessageBox::about(), a static convenience function. The function is similar to QMessageBox::warning(), except that it uses the parent window's icon instead of the standard "warning" icon. The resulting dialog is shown in Figure 3.15.

### Figure 3.15. About Spreadsheet

![](img/5a524abdf0b0d58fa99d30abb4463611_126_0.png)

So far, we have used several convenience static functions from both QMessageBox and QFileDialog. These functions create a dialog, initialize it, and call exec() on it. It is also possible, although less convenient, to create a QMessageBox or a QFileDialog widget like any other widget and explicitly call exec(), or even show(), on it.

##oring Settings

In the MainWindow constructor, we called readSettings() to load the application's stored settings. Similarly, in closeEvent(), we called writeSettings() to save the settings. These two functions are the last MainWindow member functions that need to be implemented.

```cpp
void MainWindow::writeSettings()
{
    QSettings settings("Software Inc.", "Spreadsheet");

    settings.setValue("geometry", saveGeometry());
    settings.setValue("recentFiles", recentFiles);
    settings.setValue("showGrid", showGridAction->isChecked());
    settings.setValue("autoRecalc", autoRecalcAction->isChecked());
}
```

The writeSettings() function saves the main window's geometry (position and size), the list of recently opened files, and the Show Grid and Auto-Recalulate options. By default, QSettings stores the application's settings in platform-specific locations. On Windows, it uses the system registry; on Unix, it stores the data in text files; on Mac OS X, it uses the Core Foundation Preferences API.

The constructor arguments specify the organization's name and the application's name. This information is used in a platform-specific way to find a location for the settings.
QSettings stores settings as key-value pairs. The key is similar to a file system path. Subkeys can be specified using a path-like syntax (e.g., finddialog/matchCase) or using beginGroup() and endGroup():

```cpp
settings.beginGroup("findDialog")
settings.setValue("matchCase", caseCheckBox->isChecked());
settings.setValue("searchBackward", backwardCheckBox->isChecked());
settings.endGroup();
```

The value can be an int, a bool, a double, a QString, a QString, or any other type supported by QVariant, including registered custom types.

```cpp
void MainWindow::readSettings()
{
    QSettings settings("Software Inc.", "Spreadsheet");

    restoreGeometry(settings.value("geometry").toByteArray());

```cpp
recentFiles = settings.value("recentFiles").toStringList();
updateRecentFilesActions();

bool showGrid = settings.value("showGrid", true).toBool();
showGridAction->setChecked(showGrid);

bool autoRecalc = settings.value("autoRecalc", true).toBool();
autoRecalcAction->setChecked(autoRecalc);
}
```

The readSettings() function loads the settings that were saved by writeSettings(). The second argument to the value() specifies a default value, in case there are no settings available. The default values are used the first time the application is run. Since no second argument is given for geometry or for the recent files list, the window will have an arbitrary but reasonable size and position, and the recent files list will be an empty list on the first run.

The arrangement we opted for in MainWindow, with all the QSettings-related code in readSettings() and writeSettings(), is one of many possible approaches. QSettings object can be created to query or modify some setting at any time during the execution of the application and from anywhere in the code.

We have now completed the Spreadsheet's MainWindow implementation. In the following sections, we will discuss how the Spreadsheet application can be modified to handle multiple documents and how to implement a splash screen. We will complete its functionality, including handling formulas and sorting, in the next chapter.

## Multiple Documents

We are now ready to code the Spreadsheet'application main() function:

```cpp
#include <QApplication>

#include "mainwindow.h"

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    MainWindow mainWin;
    mainWin.show();
    return app.exec();
}
```

This main() function is a little different from those we have written so far: We have created the MainWindow instance as a variable on the stack instead of using new. The MainWindow instance is then automatically destroyed when the function terminates.

With the main() function just shown, the Spreadsheet application provides a single main window and can handle only one document at a time. If we want to edit multiple documents at the same time, we could start multiple instances of the Spreadsheet application. But this isn't as convenient for users as having a single instance of the application providing multiple main windows, just as one instance of a web browser can provide multiple browser windows simultaneously.

We will modify the Spreadsheet application so that it can handle multiple documents. First, we need a slightly different File menu:

- FileNew creates a new main window with an empty document, instead of reusing the existing main window.
- FileClose closes the current main window.
- FileExit closes all windows.

In the original version of the File menu, there was no Close option that would have been the same as Exit. The new File menu is shown in Figure 3.16.

### Figure 3.16. The new File menu
