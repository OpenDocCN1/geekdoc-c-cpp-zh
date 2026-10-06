```
QDomParser::readFile(const QString &fileName)
{
  QFile file(fileName);
  if (!file.open(QFile::ReadOnly | QFile::Text)) {
    std::cerr << ":" " << "Error: Cannot read file " << qprintable(fileName)
              << ":" " << qprintable(file.errorString()) << std::endl;
    return false;
  }

  QString errorStr;
  int errorLine;
  int errorColumn;

  QDomDocument doc(&file, false, &errorStr, &errorLine,
                    &errorColumn);
  if (!doc.setContent()) {
    std::cerr << "Error: Parse error at line " << errorLine << ", "
              << "column " << errorColumn << ": "
              << qprintable(errorStr) << std::endl;
    return false;
  }

  QDomElement root = doc.documentElement();
  if (root.tagName() != "bookindex") {
    std::cerr << "Error: Not a bookindex file" << std::endl;
    return false;
  }

  parseBookindexElement(root);
  return true;
}
```

In readFile(), we begin trying to open the file whose name was passed in. If an error occurs, we output an error message and return false to signify failure. Otherwise, we set up some variables to hold parse error information, should they be needed, and then create a QDomDocument. When we call setContent() on the DOM document, the XML document provided by the QIODevice is read and parsed. The setContent() function automatically opens the device if it isn't already open. The false argument to setContent disables namespace processing; refer to the QtXml reference documentation for an introduction to XML namespaces and how to handle them in Qt.