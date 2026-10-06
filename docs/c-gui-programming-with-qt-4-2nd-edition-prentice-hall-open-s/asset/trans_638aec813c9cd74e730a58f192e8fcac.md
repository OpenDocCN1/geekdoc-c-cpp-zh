
我们只需将字符追加到 `currentText` 变量。

```cpp
bool SaxHandler::endElement(const QString & /* namespaceURI,
                               const QString & localName */,
                               const QString &qName)
{
    if (qName == "entry") {
        currentItem = currentItem->parent();
    } else if (qName == "page") {
        if (currentItem) {
            QString allPages = currentItem->text(1);
            if (!allPages.isEmpty())
                allPages += ",";
            allPages += currentText;
            currentItem->setText(1, allPages);
        }
    }
    return true;
}
```

当读取器遇到结束标签时会调用 `endElement()` 函数。与 `startElement()`一样，第三个参数是标签名称。

如果标签是 `</entry>`，我们将私有变量 `currentItem`指向当前 `QTreeWidgetItem` 的父节点。（由于历史原因，顶层项返回 0 作为其父节点，而不是根节点。）这确保了 `currentItem` 变量恢复到读取相应的 `<entry>` 标签之前所在的值。

如果标签是 `</page>`，我们将指定的页码或页范围添加到当前项第 1 列文本的逗号分隔列表中。

```cpp
bool SaxHandler::fatalError(const XmlParseException &exception)
{
    std::cerr << "Parse error at line " << exception.lineNumber()
               << "," << "column " << exception.columnNumber() << ": "
               << qPrintable(exception.message()) << std::endl;
    return false;
}
```

读取器无法解析 XML 文件时，会调用 `fatalError()` 函数。如果发生这种情况，我们只需向控制台打印一条消息，给出行号、列号和解析器的错误文本。

`SaxHandler` 的实现此完成。使用它的 `main()` 函数与我们在上一节中审查的 `DomParser` 的函数几乎完全相同，区别在于我们使用了 `SaxHandler` 而不是 `DomParser`。

# 写入 XML

大多数读取 XML 文件的应用程序也需要写入此类文件。从 Qt 应用程序生成 XML 文件有三种方法：

- 我们可以使用 `QXmlStreamWriter`。
- 我们可以构建 DOM 树并对其调用 `save()`。
- 我们可以手动生成 XML。

这些方法之间的选择主要取决于我们是否使用 `QXmlStreamReader`、`DOM` 或 `SAX` 读取 XML 文档，尽管如果数据存储在 DOM 树中，直接保存该树通常是有意义的。

使用 `QXmlStreamWriter` 类写入 XML 特别简单，因为该类为我们处理特殊字符的转义。如果我们想使用 `QXmlStreamWriter` 输出来自 `QWidget` 的索引数据，可以使用两个函数来实现。第一个函数接收一个文件名和一个 `QWidget *` 指针，并遍历树中的所有顶层项：

代码视图：

```cpp
bool writeXml(const QString &fileName, QWidget *treeWidget) {
    QFile file(fileName);
    if (!file.open(QFile::WriteOnly | QFile::Text)) {
        std::cerr << "Error: Cannot write file "
                  << qprintable(fileName) << ":"
                  << qprintable(file.errorString()) << std::endl;
        return false;
    }

    QXmlStreamWriter xmlWriter(&file);
    xmlWriter.setAutoFormatting(true);
    xmlWriter.writeStartElement("bookindex");
    for (int i = 0; i < treeWidget->topLevelItemCount(); ++i)
        writeEntry(&xmlWriter, treeWidget->topLevelItem(i));
    xmlWriter.writeEndDocument();
    file.close();
    if (file.error()) {
        std::cerr << "Error: Cannot write file "
                  << qprintable(fileName) << ":"
                  << qprintable(file.errorString()) << std::endl;
        return false;
    }
    return true;
}
```

如果开启自动格式化，XML 将以更符合人类习惯的风格输出，使用缩进来显示数据的递归结构。`writeStartDocument()` 函数写入 XML 头部行：

```xml
<?xml version="1.0" encoding="UTF-8"?>
```

`writeStartElement()` 函数根据给定的标签文本生成一个新的起始标签。`writeEndDocument()` 函数关闭任何已打开的起始标签。对于顶层项，我们使用 `writeIndexEntry()`，并其传递 `QXmlStreamWriter` 和要输出的项。以下是 `writeIndexEntry()` 的代码：

```cpp
void writeIndexEntry(QXmlStreamWriter xmlWriter,
```

该函数创建一个与接收到的参数 `QTreeWidgetItem` 对应的 `<entry>` 元素。`writeAttribute()` 为已写入的标签添加属性；例如，它可能会将 `<entry>` 变为 `<entry term="sidebars">`。如果有页码，它们将按逗号分割，对于每个页码，都会写入单独的 `<page>...</page>` 标签，中间是页文本。这是通过调用 `writeTextElement()` 并传递标签名和要放在起始与结束标签之间的文本来实现的。所有情况下，`QXmlStreamWriter` 都会处理 XML 特殊字符的转义，因此我们无需担心这个问题。

如果该项有子节点，我们对每个子节点递归地调用 `writeIndexEntry()`。最后，我们调用 `writeEndElement()` 输出 `</entry>`。

使用 `QXmlStreamWriter` 写入 XML 是简单且安全的方法，但如果我们已经在 DOM 中有了树，可以仅通过调用 `QDomDocument` 对象的 `save()` 方法让树输出相关的 XML。默认情况下，`save()` 使用 UTF-8 作为生成文件的编码。我们可以通过在 DOM 树之前添加类似 `<?xml?>` 的声明来使用其他编码：

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
```

以下代码片段显示了如何这样做：

```cpp
const int Indent = 4;

QDomDocument doc;
...
TextStream out(&file);
DomNode xmlNode = doc.createProcessingInstruction("xml", "version='1.0' encoding=\"ISO-8859-1\"");
doc.insertBefore(xmlNode, doc.firstChild());
doc.save(out, Indent);
```

手动生成 XML 文件并不比使用 DOM 困难多少。我们可以使用 `QTextStream` 并像处理任何其他文本文件一样写入字符串。困难的部分是转义文本和属性值中的特殊字符。`Qt::escape()` 函数会转义字符 `<`、`>` 和 `&`。这里是使用它的代码：

```cpp
QTextStream out(&file);
out.setCodec("UTF-8");
out << "<doc\n"
 << "  <quote>" << Qt::escape(quoteText) << "</quote>\n"
 << "  <translation>" << Qt::escape(translationText)
 << "</translation>\n"
 << "</doc>\n";
```

在像这样生成 XML 文件时，除了必须写入 `<?xml?>` 声明并设置正确的编码外，我们必须忘记转义写入的文本，如果必须转义值中的单引号或双引号。使用 `QXmlStreamWriter` 要容易得多，因为它为我们处理了所有这些。

# 17. 提供在线帮助

![](img/5a524abdf0b0d58fa99d30abb4463611_650_0.png)

- 工具提示（Tooltips）、状态提示（Status Tips）和“这是什么？”
- 使用浏览器提供在线帮助
- 使用 QTextBrowser 作为简单的帮助引擎
- 使用 Qt Assistant 提供强大的在线帮助

大多数应用程序为用户提供在线帮助。有些帮助是简短的，例如工具提示、状态提示和“这是什么？”。当然，Qt 支持所有这些。其他帮助可能详细得多，涉及大量页面。对于这类帮助，你可以使用 `QTextBrowser` 作为简单的在线帮助浏览器，或者从你的应用程序中调用 Qt Assistant 或 HTML 浏览器。

# 工具提示、状态提示和“这是什么？”帮助

工具提示是鼠标悬停在控件上一段时间后出现的小段文本。工具提示以黑字黄底的形式呈现。它们的主要用途为工具栏按钮提供文本描述。

我们可以在代码中使用 `QWidget::setToolTip()` 为任意控件添加工具提示。例如：

```cpp
findButton->setToolTip(tr("Find next"));
```

要为添加到菜单或工具栏的 QAction 设置工具提示，只需调用 `setToolTip()`。例如：

```cpp
newAction = new QAction(tr("&New"), this);
newAction->setToolTip(tr("New document"));
```

如果没有显式设置工具提示，QAction 将自动使用动作文本。
状态提示也是简短的描述文本，通常比工具提示长。当鼠标悬停在工具栏按钮或菜单选项上，状态提示出现在状态栏中。调用 `setStatusTip()` 为动作或控件添加状态提示：

```cpp
newAction->setStatusTip(tr("Create a new document"));
```

