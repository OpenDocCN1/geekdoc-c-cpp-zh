```
return;

QMimeData mimeData = new QMimeData;
MimeData->setText(plainText);
MimeData->setHtml(toHtml(plainText));
MimeData->setData("text/csv", toCsv(plainText).toUtf8());

QDrag *drag = new QDrag(this);
drag->setMimeData(mimeData);
if (drag->exec(Qt::CopyAction | Qt::MoveAction) == Qt::MoveAction)
deleteSelection();
```

The performDrag function is called from mouseMouseEvent to start dragging a rectangular selection. We set the text/plain and text/html MIME types using setText() and setHtml(), and we set the text/csv type using setData(), which takes an arbitrary MIME type and a QByteArray. The code for selectionAsString() is more or less the same as the Spreadsheet::copy() from Chapter 4 (p. 87).

```
QString MyTableWidget::toCsv(const QString &plainText)
{
    QString result = plainText;
    result.replace("\\\", "\\\\\");
    result.replace("\\", "\\\"");
    result.replace("\\t", "\\t"");
    result.replace("\\n", "\\\\n\");
    result.prepend("\\"");
    result.append(""");
    return result;
}
```

```
QString MyTableWidget::toHtml(const QString &plainText)
{
    QString result = Qt::escape(plainText);
    result.replace("\\t", "<td>");
    result.replace("\\n", "\n<<tr><td>");
    result.prepend("<table\n<<tr><td>");
    result.append("</td></tr>\n</table>");
    return result;
}
```

The toCsv() and toHtml() functions convert a "tabs and newlines" string into a