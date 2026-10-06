
QDialog::DontConfirmOverwrite This behavior can be changed by passing QFileDialog::overwrite as an additional argument to getSaveFileName().

```
void MainWindow::closeEvent(QCloseEvent *event)
{
    if (okToContinue()) {
        writeSettings();
        event->accept();
    } else {
        event->ignore();
    }
}
```

When the user clicks File->Exit or clicks the close button in the window's title bar, QWidget::close() slot is called. This sends a "close" event to the widget. By reimplementing QWidget::closeEvent(), we can intercept attempts to close the main window and decide whether we want the window to actually close or not.

If there are unsaved changes and the user chooses Cancel, we "ignore" the event and leave the window unaffected by it. In the normal case, we accept the event, resulting in Qt hiding the window. We also call the function writeSettings() to save the application's current settings.

When the last window is closed, the application terminates. If needed, we can disable this behavior by setting QApplication::quitLastWindowClosed property to false, in which case the application keeps running until we call QApplication::quit().

```
void MainWindow::setCurrentFile(const QString &fileName)
{
    curFile = fileName;
    setWindowModified(false);
    QString shownName = tr("Untitled");
    if (!curFile.isEmpty()) {
        shownName = strippedName(curFile);
        recentFiles.removeAll(curFile);
        recentFiles.prepend(curFile);
        updateRecentFileActions();
    }

    setWindowTitle(tr("%1[*] - %2%").arg(tr("Spreadsheet")));
}
```

QString MainWindow::strippedName(const QString &fullFileName)

```
return QFileInfo(fullFileName).fileName();
}
```

setsetCurrentFile(), we set the curFile private variable that stores the name of the file being edited. Before we show the file name in the title bar, we remove the path with strippedName() to make it more user-friendly.

Every QWidget has a windowModified property that should be set to true if the document's window has unsaved changes, and to false otherwise. On Mac OS X, unsaved changes are indicated by a dot in the close button of the window's title bar; on other platforms, they are indicated by an asterisk following the name. Qt takes care of this behavior automatically, as long as we keep the windowModified property up-to-date and place the marker "[*]" in the window title where we want the asterisk to appear when it is required.

The text passed to the setWindowTitle() function was tr("%1[*] - %2").arg(shownName).arg(tr("Spreadsheet"));

The QString::arg() function replaces the lowest-numbered "%n" parameter with its argument and returning the string with its argument and returning the resulting string. In this case, arg() is used with two "%n" parameters. The first call to arg() replaces "%1"; the second call replaces "%2". If the file name is "budget.sp" - Spreadsheet, the resulting string would be "budget.sp[*] - Spreadsheet". It would have been easier to write

```
setWindowTitle(shownName + tr("[*] - Spreadsheet"));
```

but using arg() provides more flexibility for human translators.

If there is a name, we update recentFiles, the application's recently opened files list. We call removeAll() to remove any occurrences of the file name in the list, to avoid duplicates; then we call prepend() to add the file name as the first item. After updating the list, we call the private function updateRecentFileActions() to update the entries in the File menu.

```
void MainWindow::updateRecentFileActions() {
    QMutableStringListIterator i(recentFiles);
    while (i.hasNext()) {
if (!QFile::exists(i.next()))
  i.remove();

for (int j = 0; j < MaxRecentFiles; j++) {
  if (j < recentFiles.count()) {
    QString text = tr("&1 %2")
    .arg(j + 1)
    .arg(strippedName(recentFiles[j]));
    recentFileActions[j]->setText(text);
    recentFileActions[j]->setData(recentFiles[j]);
    recentFileActions[j]->setVisible(true);
  } else {
    recentFileActions[j]->setVisible(false);
  }
}
separatorAction->setVisible(!recentFiles.isEmpty());
}
```

We begin by removing any files that no longer exist using a Java-style iterator. Some files might have been used in a previous session, but have since been deleted. The recentFiles variable is of type QStringList (list of QString). Chapter 11 explains container classes as QStringList in detail, showing how they relate to the C++ Standard Template Library (STL), and the use of Qt's Java-style iterator classes. We then go through the list of files again, this time using array-style indexing. For each file, we create a string consisting of an ampersand, a digit (j + 1), a space, and the file name (without its path). We set the corresponding action to use this text. For example, if the first file was C:\My Documents\tab04.sp, the first action's text would be "&1 tab04.sp". Figure 3.11 shows the correspondence between the recentFileActions array and the resulting menu.

# Figure 3.11. The File menu with recently opened files

[View full size image]

Every action can have an associated "data" item of type QVariant. The QVariant type can hold values of C++ and Qt; we cover it in Chapter 11. Here, we store the full name in the action's data so we can easily retrieve it later. We also set the action to be visible.

If there are more actions than files, we hide the extra actions. Finally, if there is at least one file, we set the separator to be visible.

```
void MainWindow::openRecentFile() {
  if (okToContinue()) {
    QAction action = qobject_cast<QAction>(sender());
    if (action) {
      loadFile(action->data().toString());
    }
  }
}
```

When the user chooses a recent file, the openRecentFile() slot is called. The okToContinue() function is used in case there are unsaved changes, provided the user did not cancel. We use qobject_cast<T>() to cast a QObject pointer to a QAction. The object_cast<T>() performs a dynamic cast based on the meta-information generated by moc. It returns a pointer of the requested QObject subclass, or 0 if the object cannot be cast. Incidentally, since we know the sender is a QAction, the program would work fine if we used static_cast<T>() or a traditional C-style cast instead. Refer to "Type Conversions" section of Appendix D for an overview of the different C++ casts.

# Using Dialogs

In this section, we will explain how to use dialogs in Qt—how to create and initialize them, run them, and respond to choices made by the user. We will make use of the Find, Go to Cell, and Sort dialogs that we created in Chapter 2. We will also create Simple.

We will begin with the Find dialog shown in Figure 3.12. Since we want the user to be able to switch between the main Spreadsheet window and the Find dialog at will, the Find dialog must be modeless. A modeless window is one that runs independently of any other windows in the application.

# Figure 3.12. The Spreadsheet application's Find dialog

When modeless dialogs are created, they normally have their signals connected to slots that respond to the user's interactions.

```
void MainWindow::find()
{
    if (!findDialog) {
        findDialog = new FindDialog(this);
        connect(findDialog, SIGNAL(findNext(const QString &, Qt::CaseSensitivity)),
            spreadsheet, SLOT(findNext(const QString &, Qt::CaseSensitivity)));
        connect(findDialog, SIGNAL(findPrevious(const QString &, Qt::CaseSensitivity)),
            spreadsheet, SLOT(findPrevious(const QString &, Qt::CaseSensitivity))));
    }

    findDialog->show();
    findDialog->raise();
    findDialog->activateWindow();
}
```

The Find dialog is a window that enables the user to search for text in the spreadsheet. The find()Kinder is called when the user clicks Edit to pop up the Find dialog. At that point, several scenarios are possible:
