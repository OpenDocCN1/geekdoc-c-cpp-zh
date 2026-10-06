```
(tableData) {
  const QTableWidget otherTable = tableData->tableWidget();
  QTableSelectionRange otherRange = tableData->range();

  event->acceptedActionPerformed();
} else if (event->mimeData()->hasFormat("text/csv")) {
  QByteArray csvData = event->mimeData()->data("text/csv");
  QString csvText = QString::fromUtf8(csvData);

  event->acceptedActionPerformed();
} else if (event->mimeData()->hasFormat("text/plain")) {
  QString plainText = event->mimeData()->text();
  ...
  event->acceptedActionPerformed();
}
  QTableWidget::mouseEvent(event);
}
```

The dropEvent() function is similar to the one we had earlier in this section, but here we optimize it by first checking whether we safely cast the QMimeData object to a TableMimeData. If the works, the drag was originated by a MyTableWidget in the same application, and we can directly access the table data instead of going through QMimeData's API. If the cast fails, we extract the data the standard way.

In this example, we have encoded the CSV text using the UTF-8 encoding. If we want to be certain of using the right encoding, we could use the charset parameter of the text/plain MIME type to specify an explicit encoding. Here are a few examples:
text/plain;charset=US-ASCII
text/plain;charset=ISO-8859-1
text/plain;charset=Shift_JIS
text/plain;charset=UTF-8