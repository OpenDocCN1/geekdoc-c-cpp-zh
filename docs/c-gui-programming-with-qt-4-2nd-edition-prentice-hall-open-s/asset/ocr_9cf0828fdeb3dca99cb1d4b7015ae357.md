This is the new main() function:

```
int main(int argc, char *argv[])
{
    QApplication app(argc, argv);
    MainWindow *mainWin = new MainWindow;
    mainWin->show();
    return app.exec();
}
```

With multiple windows, it now makes sense to create MainWindow with new, because then we can use delete on a main window when we have finished with it to save memory.

This is the new MainWindow::newFile() slot:

```
void MainWindow::newFile()
{
    MainWindow *mainWin = new MainWindow;
    mainWin->show();
}
```

We simply create a new MainWindow instance. It may seem odd that we don't keep any pointer to the new window, that isn't a problem since Qt keeps track of all the windows for us.

These are the actions for Close and Exit:

```
void MainWindow::createActions()
{
    ...
    closeAction = new QAction(tr("Close"), this);
    closeAction->setShortcut(QSequence::Close);
    closeAction->setToolTip(tr("Close this window"));
```