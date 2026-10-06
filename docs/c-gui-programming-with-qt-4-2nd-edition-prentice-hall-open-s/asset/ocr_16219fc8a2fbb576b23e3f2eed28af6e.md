# Implementing the File Menu

In this section, we will implement the File Menu and private functions necessary to make the File menu options work and to manage the recently opened files list.

```
void MainWindow::newFile()
{
    if (okToContinue()) {
        spreadsheet->clear();
        setCurrentFile("");
    }
}
```

The newFile slot is called when the user clicks the File|New menu option or clicks the toolbar button. The okToContinue() private function pops up the "Do you want to save your changes?" dialog shown in Figure 3.9, if there are unused changes. It returns true if the user chooses Yes or No (saving the document on Yes), and it returns false if the user chooses Cancel. The Spreadsheet::clear() clears all the spreadsheet's cells and formulas. The setCurrentFile() private function updates the window title to indicate that an untitled document is being edited, in addition to setting the curFile private variable and updating the recently opened files list.

Figure 3.9. "Do you want to save your changes?"

![](bbox=[0.01, 0.526, 0.353, 0.646])

```
bool MainWindow::okToContinue()
{
    if (isWindowModified()) {
        int r = QMessageBox::warning(this, tr("Spreadsheet"),
            tr("The document has been modified.\nDo you want to save your changes?"),
            QMessageBox::Yes | QMessageBox::No | QMessageBox::Cancel);

        if (r == QMessageBox::Yes) {
            return save();n        } else if (r == QMessageBox::Cancel) {
            return false;
        }
    }
}
```