```
const QString &qName,
const QXmlAttributes &attributes
```

```
if (qName == "entry") {
    currentItem = new QTreeWidgetItem(currentItem ?
    currentItem : treeWidget->invisibleRootItem());
    currentItem->setText(0, attributes.value("term"));
} else if (qName == "page") {
    currentText.clear();
}
return true;
```

The startElement() function is called when the reader encounters a new opening tag. The third parameter is the tag's name (or more precisely, its "qualified name"). The fourth parameter is the list of attributes. In this example, we ignore the first and second parameters. They are useful for XML files that use XML's namespace mechanism, a subject that is discussed in the reference documentation.

If the tag is <entry>, we create a new QTreeWidgetItem. If the tag is nested within another <entry> tag, the new tag defines a sub-entry in the index, and the new QTreeWidgetItem is created as a child of the QTreeWidgetItem that represents the encompassing entry. Otherwise, we create the QTreeWidgetItem as a top-level item, using the tree's invisible root item as the parent. We call setText() to set the text in column 0 to the value of the <entry> tag's term attribute.

If the tag is <page>, we set the currentText variable to be an empty entry. The variable serves as an accumulator for the text located between the <page> and </page> tags.

At the end, we return true to SAX to continue parsing the file. If we wanted to return unknown tags as errors, we would return false in those cases. We would then reimplement errorString() from QXmlDefaultHandler to return an appropriate error message.

```
bool SaxHandler::characters(const QString &str) {
    currentText += str;
    return true;
}
```

The characters() function is called to report character data in the XML document.