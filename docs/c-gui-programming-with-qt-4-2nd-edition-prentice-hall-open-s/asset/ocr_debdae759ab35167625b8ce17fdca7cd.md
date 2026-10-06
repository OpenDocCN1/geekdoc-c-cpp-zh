In the constructor, we initialize the private variables.

```
QStringList TableMimeData::formats() const
{
    return myFormats;
}
```

The formats() function returns a list of MIME types provided by the MIME data object. The precise order of the formats is usually irrelevant, but it's good practice to put the "best" formats first. Applications that support many formats will sometimes use the first one that matches.

```
QVariant TableMimeData::retrieveData(const QString &format, QVariant::Type preferredType)
{
    if (format == "text/plain") {
        return rangeAsPlainText();
    } else if (format == "text/csv") {
        return toCsv(rangeAsPlainText());
    } else if (format == "text/html") {
        return toHtml(rangeAsPlainText());
    } else {
        return QMimeData::retrieveData(format, preferredType);
    }
}
```

The retrieveData() function returns the data for a given MIME type as a QVariant. The value of the format parameter is normally one of the strings returned by formats(), we cannot assume that, since all applications check the MIME type against formats(). The getter functions text(), html(), urls(), imageData(), colorData(), and data() provided by QMimeData are implemented in retrieveData.

The preferredType parameter gives us a hint about which type we put in the QVariant. Here, we ignore it and trust QMimeData to convert the return value into the desired, if necessary.

```
void MyTableWidget::dropEvent(QDropEvent event)
{
    const TableMimeData tableData = qobject_cast<const TableMimeData>(event->mimeData());
```