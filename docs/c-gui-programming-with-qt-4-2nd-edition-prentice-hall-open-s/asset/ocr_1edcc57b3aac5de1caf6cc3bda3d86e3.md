```
CurrencyModel(QObject *parent = 0);
```

```
void setCurrencyMap(const QMap<QString, double> &map);
int rowCount(const QModelIndex &parent) const;
int columnCount(const QModelIndex &parent) const;
QVariant data(const QModelIndex &index, int role) const;
QVariant headerData(int section, Qt::Orientation orientation, int role) const;
```

```
private:
    QString currencyAt(int offset) const;

    QMap<QString, double> currencyMap;
```

We have chosen to subclass QAbstractTableModel for our model since most closely matches our data source. Qt provides several model base classes, including QAbstractListModel, QAbstractTableModel, and QAbstractItemList; Figure 10.11. The QAbstractItem class is used to support a wide variety of models, including those that are on recursive data structures, while QAbstractListModel and QAbstractTableModel classes are provided for convenience using one-dimensional or two-dimensional data sets.

# Figure 10.11. Inheritance tree for the abstract model classes

![](bbox=[0.01, 0.542, 0.333, 0.626])

For a read-only table model, we must reimplement three functions: rowCount(), columnCount(), and data(). In this case we have also reimplemented headerData(), and we provide a function to initialize the data (setCurrencyMap()).

```
CurrencyModel::CurrencyModel(QObject *parent)
    : QAbstractTableModel(parent)
{}
```

We do not need to do anything in the constructor, except pass the parent parameter to the base class.

```
int CurrencyModel::rowCount(const QModelIndex & parent ) const {
```