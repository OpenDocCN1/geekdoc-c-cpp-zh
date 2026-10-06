```
if (index.isValid() && index.row() != index.column())
    && role == Qt::EditRole) {
    int offset = offsetOf(index.row(), index.column());
    distances[offset] = value.toInt();

    QModelIndex transposedIndex = createIndex(index.column(),
        index.row());

    emit dataChanged(index, index);
    emit dataChanged(transposedIndex, transposedIndex);
    return true;
}
return false;
}
```

The setData function is called when the user edits an item. Providing the model is valid, the two cities are different, and the data element to modify is the Qt::EditRole, the function stores the user value entered in the distances vector.

The createIndex() function is used to generate a model index. We need it to get the model index of the item on the other side of the main diagonal that corresponds with the item set, since both items must show the same data. The createIndex() function takes the row before the column; we invert the parameters to get the model index of the diagonally opposite item to the one specified by index.

We emit the dataChanged() signal with the model index of the item that was changed. This signal takes two model indices because it is possible for a change to affect a rectangular region of more than one row and column, so the indexes passed are the index of the top-left and bottom-right items of those that have changed. We also emit the dataChanged() signal for the transposed index to ensure that the view will refresh the item. Finally, we return true or false to indicate whether the edit succeeded.

```
Qt::ItemFlags CityModel::flags(const QModelIndex &index) const
{
    Qt::ItemFlags flags = QAbstract::flags(index);
    if (index.row() != index.column()) {
        flags |= Qt::ItemIsEditable;
    }
    return flags;
}
```