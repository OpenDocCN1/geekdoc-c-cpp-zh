Here's an extract from the ColorNamesDialog constructor:

```
ColorNamesDialog::ColorNamesDialog(QWidget *parent)
 : QDialog(parent)
{
    sourceModel = new QStringListModel(this);
    sourceModel->setStringList(QColor::colorNames());

    proxyModel = new QSortFilterProxyModel(this);
    proxyModel->setSourceModel(sourceModel);
    proxyModel->setFilterKeyColumn(0);

    listView = new QListView();
    listView->setModel(proxyModel);

    syntaxComboBox = new QComboBox();
    syntaxComboBox->addItem(tr("Regular expression"), QExp::RegExp);
    syntaxComboBox->addItem(tr("Wildcard"), QExp::Wildcard);
    syntaxComboBox->addItem(tr("Fixed string"), QExp::FixedString);
}
```

The QStringListModel is created and populated the usual way. This is followed by the construction of the QSortFilterProxyModel. We pass the underlying model using setSourceModel() and tell the proxy to filter based on column 0 of the original model. The QComboBox::addItem() function accepts an optional "data" argument of type QVariant; we use this to store the QExp::PatternSyntax that corresponds to each item's text.

```
void ColorNamesDialog::reapplyFilter()
{
```