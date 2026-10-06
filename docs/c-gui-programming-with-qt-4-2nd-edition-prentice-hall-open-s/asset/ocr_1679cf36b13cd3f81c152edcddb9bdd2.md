```
const QStyleOptionViewItem &option,
const QModelIndex &index) const;
const QModelIndex &index) const
void setDataData(Widget editor, const QModelIndex &index) const
void setModelData(Widget editor, QAbstractItemModel *model,
const QModelIndex &index) const;
```

```
private slots:
void commitAndCloseEditor();
```

```
private:
int durationColumn;
};
```

We use QItemDelegate as our base class so that we benefit from the default delegate implementation. We could also have used QAbstractDelegate if we had wanted to start from scratch.[[*] To provide a delegate that can edit data, we must implement createEditor(), setData(), and setModelData(). We also implement paint() to change the rendering of the duration column.

> [*] Qt 4.4 is expected to introduce a QStyledItemDelegate and use it as the default. Unlike QItemDelegate, QStyledItemDelegate would rely on the current style to draw its items.

```
TrackDelegate::TrackDelegate(int durationColumn, QObject *parent)
: QItemDelegate(parent)
{
this->durationColumn = durationColumn;
}
```

The durationColumn parameter to the constructor tells the delegate which column holds the duration track.

```
void TrackDelegate::paint(QPainter *painter,
const QStyleOptionViewItem &option,
const QModelIndex &index) const
const QModelIndex &index) const
if (index.column() == durationColumn) {
int secs = index.model()->data(index, Qt::DisplayRole).toInt()
QString text = QString("%1:%2")
.arg(secs / 60, 2, 10, QChar('0'))
.arg(secs % 60, 2, 10, QChar('0'));
QStyleOptionViewItem myOption = option;
myOption.alignment = Qt::AlignRight | Qt::AlignVCenter;
```