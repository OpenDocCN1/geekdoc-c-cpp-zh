```
bool autoRecalculate() const { return autoRecalc; }
QString currentLocation() const;
QString currentFormula() const;
QTableWidgetSelectionRange selectedRange() const;
void clear();
bool readFile(const QString &fileName);
bool writeFile(const QString &fileName);
void sort(const SpreadsheetCompare &compare);
```

The autoRecalculate() function is implemented inline since it returns whether or not auto-recalculate is in force.

In Chapter 3, we relied on some public functions in Spreadsheet when we implemented MainWindow. For example, we called clear() from MainWindow::newFile() to reset the spreadsheet. We also use functions inherited from QTableWidget, notably setCurrentCell() and setShowGrid().

+   public slots:
void cut();
void copy();
void paste();
void del();
void selectCurrentRow();
void selectCurrentColumn();
void recalculate();
void setAutoRecalculate(bool recalc);
void findNext(const QString &str, Qt::CaseSensitivity cs);
void findPrevious(const QString &str, Qt::CaseSensitivity cs);

+   signals:
void modified();

Spreadsheet provides many slots that implement actions from the Edit, Tools, and Options menus, and it provides one signal, modified(), to announce any change that has occurred.

+   private slots:
void somethingChanged();

We define one private slot used internally by the Spreadsheet class.