```
private:
bool readFile(const QString &fileName);
TextEdit *textEdit;
};
```

The MainWindow class reimplements dragEnterEvent() and dropEvent() from QWidget. Since the purpose of the example is to show drag and drop, much of the functionality we would expect to be in a main window class has been omitted.

```
MainWindow::MainWindow()
{
    textEdit = new QTextEdit();
    setCentralWidget(textEdit);

    textEdit->setAcceptDrops(false);
    setAcceptDrops(true);

    setWindowTitle(tr("Text Editor"));
}
```

In the constructor, we create a QTextEdit and set it as the central widget. By default, QTextEdit accepts textual drags from other applications, and if the user drops a file onto it, it will insert the file name into the text. Since drop events are propagated from child to parent, by disabling dropping on the QTextEdit and enabling it on the main window, we get the drop events for the whole window in MainWindow.

```
void MainWindow::dragEnterEvent(QDragEvent *event)
{
    if (event->mimeData()->hasFormat("text/uri-list"))
        event->acceptProposedAction();
}
```

The dragEnterEvent() is called whenever the user drags an object onto a widget. If we call acceptProposedAction() on the event, we indicate that the user can drop the drag object on this widget. By default, the widget wouldn't accept the drag. Qt automatically changes the cursor to indicate to the user whether the widget is a legitimate drop site.

Here we want the user to be allowed to drag files, but nothing else. To do so, we check the MIME type of the drag. The MIME type text/uri-list is used to store a list of uniform resource identifiers (URIs), which can be file names, URLs (such as