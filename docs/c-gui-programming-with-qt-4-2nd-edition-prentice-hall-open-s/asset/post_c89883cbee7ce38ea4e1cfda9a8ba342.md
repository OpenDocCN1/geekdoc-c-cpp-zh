
```cpp
mdiArea->closeAllSubWindows();
if (!mdiArea->subWindowList().isEmpty()) {
    event->ignore();
} else {
    event->accept();
}
```

The `closeEvent()` function is implemented to close all subwindows, causing each subwindow to receive a close event. If one of the subwindows "ignores" its event (because the user canceled the "unsaved changes" message box), we ignore the close event for the MainWindow; otherwise, we accept it, resulting in Qt closing the entire application. If we didn't implement `closeEvent()` in MainWindow, the user would not have the opportunity to save unsaved changes.

We have finished our review of MainWindow, so we can move on to the Editor implementation. The Editor class represents one subwindow. It is derived from QTextEdit, which provides the text editing functionality. In a real-world application, if a code editing component is required, we might also consider using Scintilla, available for Qt as QSintilla/ http://www.riverbankcomputing.co.uk/qintilla/

Just as any widget can be used as a stand-alone window, any Qt widget can be put inside a QMdiSubWindow and used as a subwindow in an MDI area.

Code View:

```cpp
class Editor : public QTextEdit {
    Q_OBJECT

public:
    Editor(QWidget parent = 0);

    void newFile();
    bool save();
    bool saveAs();
    QSize sizeHint(const QStyleOption **) const override;
    QAction windowMenuAction() const { return action; }

    static Editor openFile(QWidget parent = 0);
    static Editor openFile(const QString &fileName,
```protected:
    void closeEvent(QCloseEvent event);

private slots:
    void documentWasModified();

private:
    bool okToContinue(const QString &fileName);
    bool saveFile(const QString &fileName);
    void setCurrentFile(const QString &fileName);
    bool readFile(const QString &fileName);
    bool writeFile(const QString &fileName);
    QString strippedName(const QString &fullFileName);

    QString curFile;
    bool isUntitled;
    QAction action;
};
```

Four of the private functions that were in the Spreadsheet application's MainWindow class (p. 59) are also present in the Editor class: `okToContinue()`, `saveFile()`, `setCurrentFile()`, and `strippedName()`.

Editor::Editor(QWidget parent)
    : QTextEdit(parent)
{

```cpp
action = new QAction(this);
action->setCheckable(true);
connect(action
```

First, we create a QAction representing the editor in the application's Window menu and connect that action to the `show()` and `setFocus()` slots.

Since we allow users to create any number of editor windows, we must make some provision for naming them so that they can be distinguished before they have been saved for the first time. One common way of handling this is to allocate names that include a number (e.g., document1.txt). We use the `Untitled` variable to distinguish between names supplied by the user and names we have created programmatically.

We connect the text document's `contentsChanged` signal to the private `documentWasModified()` slot. This simple slot calls `setWindowModified(true)`.

Finally, we set the `Qt::WA_DeleteOnChange` attribute to prevent memory leaks when the user closes an Editor window.

```cpp
void Editor::newFile()
{
    static int documentNumber = 1;

    curFile = tr("document%1.txt").arg(documentNumber);
    setWindowTitle(curFile + "[*]");
    isUntitled = true;
    ++documentNumber;
}
```

The `newFile()` function generates a name like document1.txt for the new document. The code belongs in `newFile()`, rather than the constructor, we don't want to consume numbers when we call `open()` to open an existing document in a newly created Editor. Since `documentNumber` is declared static it is shared across all Editor instances.

The `"*"` marker in the window title is a place marker where we want the asterisk to appear when the file has unsaved changes on platforms other than Mac OS. On Mac OS X, unsaved documents have a dot in their window's close button. We covered this marker in Chapter 3 (p. 61).

In addition to creating files, users often want to open existing files, picked from either a file dialog or a list as recently opened files list. Two static functions are provided to support these: `open()` for choosing a file name from the file system, and `openFile()` to create an Editor and to read into it the contents of a specified file.

```cpp
Editor Editor::open(QWidget parent)
{
    QString fileName = 
        QFileDialog::getFileName(parent, tr("Open ".*"));
    if (fileName.isEmpty())
        return 0;

    return openFile(fileName, parent);
}
```

The static `open()` function pops up a file dialog through which the user can choose a file. If a file is chosen, `openFile()` is called to create an Editor and to read the file's contents.

```cpp
Editor Editor::openFile(const QString &fileName, QWidget parent)
{
    Editor *editor = new Editor(parent);

    if (editor->readFile(fileName)) {
        editor->setCurrentFile(fileName);
        return editor;
    } else {
        delete editor;
        return 0;
    }
}
```

This static function begins by creating a new Editor widget, and then attempts to read the specified file. If the read is successful, the editor is returned; otherwise, we delete the editor.

```cpp
bool Editor::save()
{
    if (isUntitled)
        return false;
    } else {
        return true;
    }
}
```

The `closeEvent()` function is implemented to close all subwindows, causing each subwindow to receive a close event. If one of the subwindows "ignores" its event (because the user canceled the "unsaved changes" message box), we ignore the close event for the MainWindow; otherwise, we accept it, resulting in Qt closing the entire application.

```cpp
void Editor::closeEvent(QCloseEvent *event)
{
    if (isUntitled || saveFile()) {
        QTextEdit::closeEvent(event);
    } else {
        event->ignore();
    }
}
```

The `newFile()` function generates a name like document1.txt for the new document. The code belongs in `newFile()`, rather than the constructor, we don't want to consume numbers when we call `open()` to open an existing document in a newly created Editor. Since `documentNumber` is declared static it is shared across all Editor instances.

The `"*"` marker in the window title is a place marker where we want the asterisk to appear when the file has unsaved changes on platforms other than Mac OS. On Mac OS X, unsaved documents have a dot in their window's close button. We covered this marker in Chapter 3 (p. 61).

```cpp
void Editor::setCurrentFile(const QString &fileName)
{
    curFile = fileName;
    isUntitled = false;
    setWindowTitle(fileName);
}
```

The `documentWasModified()` slot calls `setWindowModified(true)`.

```cpp
void Editor::documentWasModified()
{
    setWindowModified(true);
}
```

The `Editor` class represents one subwindow. It is derived from QTextEdit, which provides the text editing functionality. In a real-world application, if a code editing component is required, we might also consider using Scintilla, available for Qt as QSintilla/ http://www.riverbankcomputing.co.uk/qintilla/

Just as any widget can be used as a stand-alone window, any Qt widget can be put inside a QMdiSubWindow and used as a subwindow in an MDI area.

## 7. Event Processing

![](img/5a524abdf0b0d58fa9930abb446311_266_0)

- Reimplementing Event Handlers
- Installing Event Filters
- Staying Responsive during Intensive Processing

Events are generated by the window system or Qt itself in response to various occurrences. When the user presses or releases a key or mouse button, a key or mouse event is generated; when a window is shown for the first time, a paint event is generated to tell the newly visible window that it needs to draw. Most events are generated in response to user actions, but some, such as timer events, are generated independently.

When we program with Qt, we seldom need to think about events, because Qt widgets emit signals when something occurs. Events become useful when we write our custom widgets or when we want to modify the behavior of existing Qt widgets.

Events should not be confused with signals. As a rule, signals are useful when using a widget, whereas events are useful when implementing a widget. For example, when we are using `QPushButton`, we are more interested in its `clicked()` signal than in the low-level mouse or key events that caused the signal to be emitted. But if we are implementing a class as `QPushButton`, we need to write code to handle mouse and key events and emit the `clicked()` signal when necessary.

### Reimplementing Event Handlers

In Qt, an event is an instance of a `QEvent` subclass. Qt handles more than a hundred types of events, each identified by an enum value. For example, `Event::type()` returns `QEvent::MouseButtonPress` for mouse press events.

Many events require more information than can be stored in a plain `QEvent` object; for example, mouse press events need to store which mouse button triggered the event as well as where the mouse pointer was positioned when the event occurred. This additional information is stored in dedicated `QLineEdit` subclasses, such as `QMouseEvent`.

Events are notified to objects through `event()`, inherited from `QObject`. The `event()` implementation in `QWidget` forwards the most common
