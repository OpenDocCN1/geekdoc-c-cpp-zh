# Implementing the Other Menus

We will now implement the slots for the Tools Options menus. These menus are shown in Figure 4.7.

# Figure 4.7. The Spreadsheet application's Tools and Options menus

![](bbox=[0.01, 0.139, 0.413, 0.218])

```
void Spreadsheet::recalculate()
{
    for (int row = 0; row < RowCount; ++row) {
        for (int column = 0; column < ColumnCount; ++column) {
            if (cell(row, column))
                cell(row, column)->setDirty();
        }
    }
    viewport()->update();
}
```

The recalculate() slot corresponds to Tools|Recalculate. It is also called automatically by Spreadsheet when necessary.

We iterate over all the cells and call setDirty() on every cell to mark one as requiring recalculation. The next time QTableWidget calls text() on a Cell to obtain the value to show in the spreadsheet, the value will be recalculated.

Then we call update() on the viewport to repaint the whole spreadsheet. The repaint code in QTableWidget calls text() on every visible cell to obtain the value. Because we called setDirty() on every cell, the calls to text() will use a freshly calculated value. The calculation may require non-visible cells to be recalculated, cascading the calculation until every cell that needs to be recalculated to display the correct text in the viewport has been freshly calculated performed by the Cell class.

```
void Spreadsheet::setAutoRecalculate(bool recalc)
{
    autoRecalc = recalc;
    if (autoRecalc)
        recalculate();
}
```