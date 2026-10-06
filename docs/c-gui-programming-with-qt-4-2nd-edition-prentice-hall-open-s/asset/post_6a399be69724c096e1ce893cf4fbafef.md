
```cpp
public:
 int operator()(int x) const { return x * x; }
}
```

The Square class provides one function, operator(int), that returns the square of its parameter. By naming the function operator()(int) rather than say, compute(int), we gain the capability of using an object of type Square as though it was a function:

```cpp
Square square;
int y = square(5);
// y equals 25
```

Now let's see an example involving SpreadsheetCompare:

```cpp
QStringList row1, row2;
SpreadsheetCompare compare;

if (compare(row1, row2)) {
  // row1 is less than row2
}
```

The compare object can be used just as though it had been a plain compare(). Additionally, its implementation can access all the sort keys and sort orders, which are stored as member variables.

An alternative to this scheme would have been to store the sort keys and sort orders in global variables and use a plain compare() function. However, communicating through global variables is elegant and can lead to subtle bugs. Functors are a more powerful idiom for interfacing with template functions such as qStableSort().

Here is the implementation of the function that is used to compare two spreadsheet rows:

```cpp
bool SpreadsheetCompare::operator()(const QStringList &row1,
const QStringList &row2) const {
  for (int i = 0; i < KeyCount; ++i) {
    int column = keys[i];
    if (column != -1)
if (row1[column] != row2[column]) {
    if (ascending[i]) {
        return row1[column] < row2[column];
    } else {
        return row1[column] > row2[column];
    }
}
return false;
```

The operator returns true if the first row is less than the second row; otherwise, it returns false. The qStableSort() function uses the result of this function to perform the sort.

The SpreadsheetCompare object's keys and ascending arrays are populated in the MainWindow::sort() function (shown in Chapter 2). Each key holds a column index, or -1 ("None").

We compare the corresponding cell entries in the two rows for each key in order. As soon as we find a difference, we return an appropriate true or false value. If all the comparisons turn out to be equal, we return false. The qStableSort() function uses the order before the sort to resolve tie situations; if row1 preceded row2 originally and neither compares as "less than" the other, row1 will still precede row2 in the result. This is what distinguishes qStableSort() from its unstable cousin qSort().

We have now completed the Spreadsheet class. In the next section, we will review the Cell class. This class is used to hold cell formulas and provides a reimplementation of QTableWidgetItem::data() function that Spreadsheet cells calls directly, through QTableWidgetItem::text() function, to display the result of calculating a cell's formula.

## Subclassing QTableWidgetItem

The Cell class is derived from QTableWidgetItem. The class is designed to work well with Spreadsheet, but it has no specific dependencies on that class and could in theory be used in any TableWidget. Here's the header file:

```cpp
#ifndef CELL_H
#define CELL_H

#include <QTableWidgetItem>

class Cell : public QTableWidgetItem {
public:
    Cell();

    QTableWidgetItem *clone() const;
    void setData(int role, const QVariant &value);
    QVariant data(int role) const;
    void setFormula(const QString &formula);
    QString formula() const;
    void setDirty();

private:
    QVariant value() const;
    QVariant evalExpression(const QString &str, int &pos) const;
    QVariant evalTerm(const QString &str, int &pos) const;
    QVariant evalFactor(const QString &str, int &pos) const;

    mutable QVariant cachedValue;
    mutable bool cacheDirty;
};

#endif
```

The Cell class extends QTableWidgetItem by adding two private variables:

- cachedValue caches the cell's value as a QVariant.
- cacheDirty is true if the cached value isn't up-to-date.

We use QVariant because some cells have a double value, while others have a QString value. cachedValue and cacheDirty variables are declared mutable. This allows us to modify these variables in const functions. Alternatively, we could recalculate the value each time text(), but that would be inefficient.

Notice that there is no Q_OBJECT macro in the class definition. Cell is C++, with no signals or slots. In fact, item classes are not derived from QObject to keep their overhead to a bare minimum. If signals and slots are needed, they can be implemented in the widget that contains the items or, exceptionally, using multiple inheritance with QObject. Here's the start of cell.cpp:

```cpp
#include <QtGui>
#include "cell.h"

Cell::Cell()
{
    setDirty();
}
```

In the constructor, we only need to set cache as dirty. There is no need to pass a parent; when the cell is inserted into a QWidgetItem with setItem(), the QWidgetItem will automatically take ownership of it. Most commonly used roles are EditRole and DisplayRole. The edit role is used for data that is to be edited, and the display role is for data be displayed. Often the data for both is the same, but in Cell the role corresponds to the cell's formula and the display role corresponds to the cell's value (the result of evaluating the formula).

```cpp
QTableWidgetItem *Cell::clone() const
{
    return new Cell(*this);
}
```

The clone() function is called by QTreeWidgetItem when it needs to create a new cell—for example, when the user starts typing into an empty cell that has not used before. Member-wise copying is sufficient for Cell, so we are Cell instances at the clone() function.

```cpp
void Cell::setFormula(const QString &formula)
{
    setData(Qt::EditRole, formula);
}
```

The formula() function sets the cell's formula. It is simply a convenience function for calling setData() with the edit role. It is called from Spreadsheet::setFormula().

```cpp
QString Cell::formula() const
{
    return data(Qt::EditRole).toString();
}
```

The formula() function is called from Spreadsheet::formula(). Like setFormula(), it is a convenience function retrieving the item's EditRole data.

```cpp
void Cell::setData(int role, const QVariant &value)
{
    QTableWidgetItem::setData(role, value);
    if (role == Qt::EditRole)
        setDirty();
}
```

If we have a new formula, we set cacheDirty to true to ensure that the cell is recalculated the next time text() is called.

There is no text() function defined in Cell, although we call text() on Cell instances in Spreadsheet::text(). The text() function is a convenience function provided by QTableWidgetItem; it is the equivalent of calling data(Qt::DisplayRole).toString().

```cpp
void Cell::setDirty()
{
    cacheIsDirty = true;
}
```

setDirty() function is called to force a recalculation of the cell's value. It simply sets cacheDirty to true, meaning that cachedValue is no longer up-to-date. The recalculation is not performed until it is necessary.

```cpp
QVariant Cell::data(int role) const {
if (role == Qt::DisplayRole) {
    if (value().isValid()) {
        return value().toString();
    } else {
        return "####";
    }
} else if (role == Qt::TextAlignmentRole) {
    if (value.type() == QVariant::String) {
        return int(Qt::AlignLeft | Qt::AlignCenter);
    } else {
        return int(Qt::AlignRight | Qt::AlignCenter);
    }
} else {
    return QTableWidgetItem::data(role);
}
}
```

The data() function is implemented from QTableWidgetItem. It returns the text that should be shown in the spreadsheet if called with Qt::DisplayRole, and the formula if called with Qt::EditRole. In the DisplayRole case, it relies on value() to compute the cell's value. If the value is invalid (because the formula is wrong), we return "####".

The Cell::value() function used in data() returns a QVariant. A QVariant can store values of different types, such as double and QString, and provides functions to convert them to other types. For example, calling toString() on a variant that holds a double produces a string representation of the double. A QVariant constructed using the default constructor is an "invalid" variant.

Code View:

```cpp
const QVariant Invalid;
QVariant Cell::value() const {
if (cacheIsDirty) {
    cacheDirty = false;
}

QString formulaStr = formula();
}
```
