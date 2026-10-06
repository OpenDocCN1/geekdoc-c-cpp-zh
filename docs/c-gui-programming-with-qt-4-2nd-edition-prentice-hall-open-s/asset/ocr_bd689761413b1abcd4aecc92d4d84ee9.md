implement TableWidget inherited function EditSelectItem, since that is provided by QAbstractItem::selectAll().

```
void Spreadsheet::findNext(const QString &str, Qt::CaseSensitivity cs) {
    int row = currentRow();
    int column = currentColumn() + 1;

    while (row < RowCount) {
        while (column < ColumnCount) {
            if (text(row, column).contains(str, cs)) {
                clearSelection();
                setCurrentCell(row, column);
                activateWindow();
                return;
            }
            ++column;
        }
        column = 0;
        ++row;
    }
    QApplication::beep();
}
```

The findNext() slot iterates through the cells starting from the cell to the right of the cursor and moving right until the last column is reached, then continues from the first column in the row below, and so on until the text is found or until the very last cell is reached. For example, if the current cell is C24, we search D24, E24, ..., Z24, then A25, B25, C25, ..., Z25, and clear the current selection, move the cursor to the cell that matched, and make the window that contains the Spreadsheet active.

If we find a match, we move the cursor to the cell that matched. If no match is found, we make the application beep to indicate that the search finished unsuccessfully.

```
void Spreadsheet::findPrevious(const QString &str, Qt::CaseSensitivity cs) {
    int row = currentRow();
    int column = currentColumn() - 1;

    while (row >= 0) {
        while (column >= 0) {
            if (text(row, column).contains(str, cs)) {
                clearSelection();
```