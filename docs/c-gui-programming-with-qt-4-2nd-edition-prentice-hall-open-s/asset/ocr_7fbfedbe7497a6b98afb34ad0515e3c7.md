![](bbox=[0.007, 0.007, 0.436, 0.246])

We begin with a simple dialog that lets the user pick a flowchart symbol from a list. Each item consists of an icon, a text, and a unique ID.

Let's start with an extract from the dialog's header file:

```
class FlowChartSymbolPicker : public QDialog
{
    Q_OBJECT

public:
    FlowChartSymbolPicker(const QMap<int, QString> &symbolMap,
        QWidget *parent = 0);

    int selectedId() const { return id; }
    void done(int result);
    ...
};
```

When we construct the dialog, we pass it a QMap<int, QString>, and after it has executed we can retrieve the chosen ID (or -1 if the user didn't select any item) by calling selectedId().

```
FlowChartSymbolPicker::FlowChartSymbolPicker(
    const QMap<int, QString> &symbolMap, QWidget *parent)
    : QDialog(parent)
{
    id = -1;

    listWidget = new QListWidget;
    listWidget->setIconSize(QSize(60, 60));

    QMapIterator<int, QString> i(symbolMap);
```