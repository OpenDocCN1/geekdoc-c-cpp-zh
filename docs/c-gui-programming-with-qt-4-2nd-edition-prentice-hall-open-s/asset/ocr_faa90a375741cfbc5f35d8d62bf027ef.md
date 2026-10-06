```
connect(this, SIGNAL(itemChanged(QTableWidgetItem)),
    this, SLOT(somethingChanged()));

clear();
```

Normally, when the user enters some text on an empty cell, the QWidget automatically create a QTableWidgetItem to hold the text. In our spreadsheet, we Cell items to be created instead. This is achieved by the setItemPrototype() call in the constructor. Internally, QWidget clones the item as a prototype every time a new item is required.

Also in the constructor, we set the selection mode to QAbstractItemView::ContiguousSelection to allow a single rectangular selection. We connect the table's itemChanged() signal to the private somethingChanged() slot; ensures that when the user edits a cell, somethingChanged() slot is called. Finally, we call clear() to resize the table and to set the column headings.

```
void Spreadsheet::clear())
{
    setRowCount(0);
    setColumnCount(0);
    setRowCount(RowCount);
    setColumnCount(ColumnCount);

    for (int i = 0; i < ColumnCount; ++i) {
        QTableWidgetItem *item = new QTableWidgetItem;
        item->setText(QString(QChar('A') + i));
        setHorizontalHeader(i, item);
    }

    setCurrentCell(0, 0);
}
```

The clear() function is called from the Spreadsheet constructor to initialize the spreadsheet. It is also called from MainWindow::newFile().

We have used QWidget::clear() to clear all the items and selections, but would have left the headers at their current size. Instead, we resize the table down to 0 x 0. This clears the entire spreadsheet, including the headers. We then resize the table to ColumnCount x RowCount (26 x 999) and