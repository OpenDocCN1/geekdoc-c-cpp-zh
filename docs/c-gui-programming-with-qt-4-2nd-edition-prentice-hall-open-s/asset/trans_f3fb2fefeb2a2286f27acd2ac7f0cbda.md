

```cpp
return currencyMap.count();
}
int CurrencyModel::columnCount(const QModelIndex &parent *) const {
    return currencyMap.count();
}
```

对于这个表格，行数和列数是货币映射中货币的数量。`parent` 参数对于表格模型来说没有意义；这是因为 `rowCount()` 和 `columnIndex()` 继承自更通用的基类 `QAbstractWidgetItem`，该基类支持层次结构。

```cpp
QVariant CurrencyModel::data(const QModelIndex &index, int role) const {
    if (!index.isValid())
        return QVariant();

    if (role == Qt::TextAlignmentRole) {
        return int(Qt::AlignRight | Qt::AlignVCenter);
    } else if (role == Qt::DisplayRole) {
        QString currency = currencyAt(index.row());
        QString columnCurrency = currencyAt(index.column());

        if (currencyMap.value(currency) == 0.0)
            return "####";

        double amount = currencyMap.value(columnCurrency)
            / currencyMap.value(currency);

        return QString("%1").arg(amount, 0, 'f', 4);
    }
    return QVariant();
}
```

`data()` 函数返回项的任何角色值。该项通过 `QModelIndex` 指定。对于表格模型，`QModelIndex` 有意义的组件是它的行号和列号，可以通过 `row()` 和 `column()` 获取。

如果角色是 `Qt::TextAlignmentRole`，我们返回一个适用于数字的对齐方式。如果显示角色是 `Qt::DisplayRole`，我们查找每种货币的值并计算汇率。

委托。相反，我们将值作为字符串返回，并按照我们想要进行格式化。

```cpp
QVariant CurrencyModel::headerData(int section, Qt::Orientation /* orientation */, int role) const
{
    if (role != Qt::DisplayRole)
        return QVariant();
    return currencyAt(section);
}
```

`headerData()` 函数由视图调用，用于填充其水平表头和垂直表头。`section` 参数是行号或列号（取决于方向）。由于行和列具有相同的货币代码，我们不关心方向，简单地返回给定区域号的货币。

```cpp
void CurrencyModel::setCurrencyMap(const QMap<QString, double>& map)
{
    currencyMap = map;
    reset();
}
```

调用者可以使用 `setCurrencyMap()` 更改货币映射。`QAbstractItem::reset()` 调用会告诉任何使用该模型的视图它们的所有数据都已失效；这将强制它们为可见的项请求新数据。

```cpp
QString CurrencyModel::currencyAt(int offset) const
{
    return (currencyMap.begin() + offset).key();
}
```

`currencyAt()` 函数返回货币映射中给定偏移量处的键（货币代码）。我们使用 STL 风格的迭代器来查找项并在其上调用 `key()`。

正如我们所看到的，创建只读模型并不困难，而且取决于底层数据的性质，良好的模型在内存和速度上都有潜在的节省空间。下一个示例，图 10.12 中的 Cities 应用程序也是基于表格的，但这次所有数据都是由……输入的

# 图 10.12. Cities 应用程序

![](img/5a524abdf0b0d58fa99d30abb4463611_405_0.png)

该应用程序用于存储任意两个城市之间距离的值。与上一个示例一样，我们可以简单地为每个城市对使用一个 `QWidgetItem` 项。然而，自定义模型可能会更高效，因为从任何城市 A 到任何不同城市 B 的距离无论从 A 到 B 还是从 B 到 A 都是，因此项沿主对角线镜像。

为了查看自定义模型与简单表格的比较，假设我们有三个城市 A、B 和 C。如果我们为每种组合存储一个值，我们需要存储九个值。设计良好的模型只需要三个项 (A, B)、(A, C) 和 (B, C)。

以下是我们如何设置和使用模型：

```cpp
QStringList cities;
cities << "Arvika" << "Boden" << "Eskilatuna" << "Falun"
<< "Filipstad" << "Halmstad" << "Helsingburg" << "Karlstad"
<< "Kiruna" << "Kramfors" << "Motala" << "Sandviken"
<< "Skara" << "Stockholm" << "Sundsvall" << "Trelleborg";
```

```cpp
CityModel cityModel;
cityModel.setCities(cities);

QTableView tableView;
tableView.setModel(&cityModel);
tableView.setAlternatingRowColors(true);
```

我们重新实现了与上一个示例相同的函数。此外，我们还必须重新实现 `setData()` 和 `flags()` 以使模型完备。以下是类定义：
```cpp
class CityModel : public QAbstractTableModel
{
  Q_OBJECT
public:
  CityModel(QObject *parent = 0);

  void setCities(const QStringList &cityNames);
  int rowCount(const QModelIndex &parent) const;
  int columnCount(const QModelIndex &parent) const;
  QVariant data(const QModelIndex &index, int role) const;
  bool setData(const QModelIndex &index, const QVariant &value, int role);
  QVariant headerData(int section, Qt::Orientation orientation, int role) const;
  Qt::ItemFlags flags(const QModelIndex &index) const;
private:
  int offsetOf(int row, int column) const;

  QStringList cities;
  QVector<int> distances;
};
```

```cpp
CityModel::CityModel(QObject *parent)
  : QAbstractTableModel(parent)
{}
```

构造函数除了将 `parent` 参数传递给基类外没有做其他事情。

```cpp
int CityModel::rowCount(const QModelIndex &/* parent */) const
{
  return cities.count();
}
int CityModel::columnCount(const QModelIndex &parent*) const
{
    return cities.count();
}
```

由于我们是正方形格，列数等于行数。

```cpp
QVariant CityModel::data(const QModelIndex &index, int role) const {
    if (!index.isValid()) {
        return QVariant();
    }

    if (role == Qt::TextAlignmentRole) {
        return int(Qt::AlignRight | Qt::AlignVCenter);
    } else if (role == Qt::DisplayRole) {
        if (index.row() == index.column()) {
            return 0;
        }
        int offset = offsetOf(index.row(), index.column());
        return distances[offset];
    }
    return QVariant();
}
```

`data()` 函数与我们在 `CurrencyModel` 中所做的相似。如果行和列相同，则返回 0；否则，在 `distances` 向量中查找行和列的项并返回它。

```cpp
QVariant CityModel::headerData(int section, Qt::Orientation /* orientation */, int role) const {
    if (role == Qt::DisplayRole) {
        return cities[section];
    }
    return QVariant();
}
```

`headerData()` 函数很简单，因为我们有一个方形表格，每一行都有相同的列。我们简单地返回给定偏移量处的城市名称。

```cpp
bool CityModel::setData(const QModelIndex &index, const QVariant &value, int role) {
    if (index.isValid() && index.row() != index.column() && role == Qt::EditRole) {
        int offset = offsetOf(index.row(), index.column());
        distances[offset] = value.toInt();

        QModelIndex transposedIndex = createIndex(index.column(), index.row());

        emit dataChanged(index, index);
        emit dataChanged(transposedIndex, transposedIndex);
        return true;
    }
    return false;
}
```

