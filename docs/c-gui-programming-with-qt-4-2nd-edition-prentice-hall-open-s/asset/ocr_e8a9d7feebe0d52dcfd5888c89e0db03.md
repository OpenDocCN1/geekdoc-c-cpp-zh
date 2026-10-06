indicator requires very little space, and when the window is resized, the cell indicator goes to the right. This is achieved by specifying a stretch factor of 1 in the formula label QStatusBar::addWidget() call. The cell indicator has the default stretch factor of 0, meaning that it prefers not to be stretched.

When QStatusBar updates layout indicators, it tries to respect each widget's size as given by Widget::sizeHint() and stretches each stretchable widget to fill the available space. A widget's size is itself dependent on the widget's contents and varies as we change them. To avoid resizing of the contents we set its minimum size to be wide enough to contain the largest possible text ("W999"), with a little extra space. We also set its alignment to Qt::AlignCenter to horizontally center the text.

Near the end of the function, we connect two signals to MainWindow's slots: updateStatusBar() and spreadsheetModified().

```
void MainWindow::updateStatusBar()
{
    locationLabel->setText(spreadsheet->currentLocation());
    formulaLabel->setText(spreadsheet->currentFormula());
}
```

The updateStatusBar() slot updates the cell location and the cell formula indicators. It is called whenever the user moves the cell cursor to a new cell. The slot is also used as an ordinary function at the end of the createStatusBar() initialize the indicators. This is necessary because Spreadsheet doesn't emit the currentCellChanged() signal at startup.

```
void MainWindow::spreadsheetModified()
{
    setWindowModified(true);
    updateStatusBar();
}
```

The spreadsheetModified() slot sets the windowModified property to true, updating the title bar. The function also updates the location and formula indicators so that they reflect the current state of affairs.