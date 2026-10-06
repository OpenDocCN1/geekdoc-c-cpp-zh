```
TrackEditor::TrackEditor(QList<Track> tracks, QWidget parent)
    : QDialog(parent)
{
    this->tracks = tracks;

    tableWidget = new QTableWidget(tracks->count(), 2);
    tableWidget->setItemDelegate(new TrackDelegate(1));
    tableWidget->setHorizontalHeaderLabels(
        QStringList() << tr("Track") << tr("Duration"));

    for (int row = 0; row < tracks->count(); ++row) {
        Track track = tracks->at(row);

        QTableWidgetItem item0 = new QTableWidgetItem(track.title);
        tableWidget->setItem(row, 0, item0);

        QTableWidgetItem item1
            = new QTableWidgetItem(QString::number(track.duration));
        item1->setTextAlignment(Qt::AlignRight);
        tableWidget->setItem(row, 1, item1);
    }
    ...
}
```

The constructor creates a table widget, and instead of simply using the default delegate, we set our custom TrackDelegate, passing it the column that holds time data. We begin by setting the column headings, and then iterate through the data, populating the rows with the name and duration of each track.

The rest of the constructor and the rest of the TrackEditor class holds no surprises, so we will now look at the TrackDelegate that handles the rendering and editing of track data.

```
class TrackDelegate : public QItemDelegate
{
    Q_OBJECT

public:
    TrackDelegate(int durationColumn, QObject parent = 0);

    void paint(QPainter painter, const QStyleOptionViewItem &option,
               const QModelIndex &index) const;
    QWidget* createEditor(QWidget parent,
```