
setFormula() private function sets the formula for a given cell. If the cell already has a Cell object, otherwise we create a new Cell object and use QWidgetItem::setItem() to insert into the table. At the end, we call the cell's setFormula() function, which will cause the cell to be reprinted if it's off-screen. We don't need to worry about deleting the Cell later on; QWidgetItem takes ownership of the cell and will delete it automatically at the right time.

```
QString Spreadsheet::currentLocation() const {
  return QChar('A' + currentColumn())
  + QString::number(currentRow() + 1);
}
```

The currentLocation() returns the current cell's location in the usual spreadsheet format of column letter followed by row number. MainWindow::updateStatusBar() uses it to show the location in the status bar.

```
QString Spreadsheet::currentFormula() const {
  return formula(currentRow(), currentColumn());
}
```

```
void Spreadsheet::somethingChanged() {
  if (autoRecalc)
    recalculate();
  emit modified();
}
```

The somethingChanged() private slot recalculates the whole spreadsheet if "auto-recalculate" is enabled. It also emits the modified() signal.

# Loading and Saving

We will now implement the loading and saving of Spreadsheet files using a custom binary format. We will do this using QFile and QDataStream, which together provide platform-independent binary I/O.

We will start with writing a Spreadsheet file:

Code View:

```cpp
bool Spreadsheet::writeFile(const QString &fileName)
{
    QFile file(fileName);
    if (!file.open(QIODevice::WriteOnly)) {
        QMessageBox::warning(this, tr("Spreadsheet"),
            tr("Cannot write file %1:%n2.") .arg(fileName).arg(file.errorString()));
        return false;
    }
    QDataStream out(&file);
    out.setVersion(QDataStream::Qt_4_3);

    out << quint32(MagicNumber);

    QApplication::overrideCursor(Qt::WaitCursor);
    for (int row = 0; row < RowCount; ++row) {
        for (int column = 0; column < ColumnCount; ++column) {
            QString str = formula(row, column);
            if (!str.isEmpty())
                out << quint16(column) << str;
        }
    }
    QApplication::restoreCursor();
    return true;
}
```

The writeFile() function is called from MainWindow::saveFile() to write the file to disk. It returns true on success, false on error.

We create a QFile object with the given name and call open() to open the file for writing. We also create a QDataStream object that operates on the QFile and use it to write out the data.

Just before we write the data, we change the application's cursor to the standard (usually an hourglass) and restore the normal cursor once all the data is written. At the end of the function, the file is automatically closed by QFile destructor.

QDataStream supports basic C++ types as well as many of Qt's. The syntax is modeled after the Standard C++ <iostream> classes. For example,

```
out << x << y << z;
```

writes the variables x, y, and z to a stream, and

```
in >> x >> y >> z;
```

reads from a stream. Because the C++ primitive integer types may have different sizes on different platforms, it is safest to cast these values to one of quint8, quint16, quint32, quint64, or qint8 up to qint64, which are guaranteed to be the size they identify as (in bits).

The Spreadsheet application's file format is fairly simple. A Spreadsheet file starts with a 32-bit number that identifies the file format (MagicNumber, defined as 0x7F5CC83 in spreadsheet.h, an arbitrary number). Then comes a series of blocks, each containing a single cell's row, column, and formula. To save space, we don't output empty cells. The format is shown in Figure 4.3.

# Figure 4.3. The Spreadsheet file format

![](img/5a524abdf0b0d58fa99d30abb4463611_148_0.png)

The precise binary representation of data types is determined by QDataStream. For example, quint16 is stored as two bytes in big-endian order, and QString as the string's length followed by Unicode characters.

The binary representation of Qt types has evolved quite a lot since 1.0. It is likely to continue evolving in future Qt releases to keep pace with the evolution of existing types and allow for new types. By default, QDataStream uses the most recent version of the binary format (version 9), but it can be set to read older versions. To avoid compatibility problems if the application is recompiled using a newer Qt release, we explicitly tell QDataStream to use the version of Qt we are compiling.

QDataStream is very versatile. It can be used on a QFile, QBuffer, QProcess, TCPSocket and UDPSocket. Qt also offers QTextStream that can be used instead of QDataStream for reading and writing. Chapter 12 explains these classes in depth, and also describes various approaches to handling DataStream versions.

Code View:

```cpp
bool Spreadsheet::readFile(const QString&fileName)
{
    QFile file(fileName);
    if (!file.open(QIODevice::ReadOnly)) {
        QMessageBox::warning(this, tr("Spreadsheet"),
            tr("Cannot read file %1:%n2.") .arg(fileName).arg(file.errorString()));
        return false;
    }

    QDataStream in(&file);
    in.setVersion(QDataStream::Qt_4_3);

    uint32 magic;
    in >> magic;
    if (magic != MagicNumber) {
        QMessageBox::warning(this, tr("Spreadsheet"),
            tr("The file is not a Spreadsheet file.
        return false;
    }

    clear();

    uint16 row;
    uint16 column;
    QString str;

    QApplication::setOverrideCursor(Qt::WaitCursor);
    while (!in.atEnd()) {
        in >> row >> column >> str;
        setFormula(row, column, str);
    }
    QApplication::restoreCursor();
    return true;
}
```

readFile() function is very similar to writeFile(). We use QFile to read the file, using the QIODevice::ReadOnly flag rather than QIODevice::WriteOnly. Then we set the QDataStream version to 9. The format for reading must always be the same as writing.

If the file has the correct magic number at the beginning, we call clear() to blank out all cells in the spreadsheet, and we read the cell data. Since the file only contains the data for non-empty cells, and it is unlikely that every cell in the spreadsheet will be set, we must ensure all cells are cleared before reading.

# Implementing the Edit Menu

We are now ready to implement the slots that correspond to the application's Edit menu. The menu is shown in Figure 4.4.

# Figure 4.4. The Spreadsheet application's Edit menu

![](img/5a524abdf0b0d58fa99d30abb4463611_151_0.png)

```cpp
void Spreadsheet::cut()
{
    copy();
    clear();
}
```

The cut() slot corresponds to Edit|Cut. The implementation is simple since Cut is the same as Copy followed by Delete.

```cpp
void Spreadsheet::copy()
{
    QTableWidgetSelectionRange range = selectedRange();
    QString str;

    for (int i = 0; i < range.rowCount(); ++i) {
        if (i > 0)
            str += "\n";
        for (int j = 0; j < range.columnCount(); ++j) {
            if (j > 0)
                str += "\t";
            str += formula(range.topRow() + i, range.leftColumn() + j);
        }
    }
    QApplication::clipboard()->setText(str);
}
```

The copy() slot corresponds to Edit|Copy. It iterates over the current selection which is simply the current cell if there is no explicit selection. Each selected cell's formula is added to a QString, with rows separated by newline characters and columns separated by tab characters. This is illustrated in Figure 4.5.

# Figure 4.5. Copying a selection onto the clipboard

| | C | D | E |
|---|---|---|---|
| 2 | Red | Green | Blue |
| 3 | Cyan | Magenta | Yellow |

"Red\tGreen\tBlue\nCyan\tMagenta\tYellow"

The system clipboard is available in Qt through the QApplication::clipboard() static function. By calling QClipboard::setText(), we make the text available on the clipboard, by this application and to other applications that support plain text. Our format with tab and newline characters as separators is understood by a variety of applications, including Microsoft Excel.

The TableWidget::selectedRanges() function returns a list of selection ranges. We know there can be more than one because we set the selection mode to QAbstractItemView::ContiguousSelection in the constructor. For our convenience, we define a selectedRange() function that returns the selection range:

```cpp
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

```cpp
void Spreadsheet::paste() {
  QTableWidgetSelectionRange range = selectedRange();
  QString str = QApplication::clipboard()->text();
```
