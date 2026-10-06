is simply the current cell if there is no explicit selection. Each selected cell's formula is added to a QString, with rows separated by newline characters and columns separated by tab characters. This is illustrated in Figure 4.5.

# Figure 4.5. Copying a selection onto the clipboard

| | C | D | E |
|---|---|---|---|n| 2 | Red | Green | Blue |
| 3 | Cyan | Magenta | Yellow |

"Red\tGreen\tBlue\nCyan\tMagenta\tYellow"

The system clipboard is available in Qt through the QApplication::clipboard() static function. By calling QClipboard::setText(), we make the text available on the clipboard, by this application and to other applications that support plain text. Our format with tab and newline characters as separators is understood by a variety of applications, including Microsoft Excel.

The TableWidget::selectedRanges() function returns a list of selection ranges. We know there can be more than one because we set the selection mode to QAbstractItemView::ContiguousSelection in the constructor. For our convenience, we define a selectedRange() function that returns the selection range:

```
QTableWidgetSelectionRange Spreadsheet::selectedRange() const {
  QList<QTableWidgetSelectionRange> ranges = selectedRanges();
  if (ranges.isEmpty()) {
    return QTableWidgetSelectionRange();
  }
  return ranges.first();
}
```

If there is a selection at all, we simply return the first (and only) one. There should always be a selection since the ContiguousSelection mode treats the current cell as being selected. To protect against the possibility of a bug in our program that makes no cell current, we handle this case.

Code View:

```
void Spreadsheet::paste() {
  QTableWidgetSelectionRange range = selectedRange();
  QString str = QApplication::clipboard()->text();
```