Once we have the column labels, we iterate through the coordinate data that was passed in. For every (x, y) we add a new row using the private function `addRow()`.

By default, `QTableWidget` allows editing. The user can edit any cell in the table by navigating to it and then pressing F2 or simply by typing. All changes the user has made in the view will be automatically reflected in the `QTableWidgetItems`. To prevent editing, we can call `setEditTriggers(QAbstractItemView::NoEditTriggers)`.

```
void CoordinateSetter::addRow()
{
    int row = tableWidget->rowCount();
    tableWidget->insertRow(row);

    QTableWidgetItem item0 = new QTableWidgetItem();
    item0->setTextAlignment(Qt::AlignRight | Qt::AlignVCenter);
    tableWidget->setItem(row, 0, item0);

    QTableWidgetItem item1 = new QTableWidgetItem();
    item1->setTextAlignment(Qt::AlignRight | Qt::AlignVCenter);
    tableWidget->setItem(row, 1, item1);

    tableWidget->setCurrentItem(item0);
}
```

The `addRow()` slot is invoked when the user clicks the Add Row button; in the constructor. We append a new row using `QTableWidget::insertRow()`. Then we create two `QTableWidgetItems` and add them to the table using `QTableWidget::setItem()`, which takes a row and a column in addition to the item. Finally, we set the current item so that the user can start editing the new row's first item.

```
void CoordinateSetter::done(int result)
{
    if (result == QDialog::Accepted) {
        coordinates->clear();
        for (int row = 0; row < tableWidget->rowCount(); row++) {
            double x = tableWidget->item(row, 0)->text().toDouble();
            double y = tableWidget->item(row, 1)->text().toDouble();
            coordinates->append(QPointF(x, y));
        }
    }
    QDialog::done(result);
```