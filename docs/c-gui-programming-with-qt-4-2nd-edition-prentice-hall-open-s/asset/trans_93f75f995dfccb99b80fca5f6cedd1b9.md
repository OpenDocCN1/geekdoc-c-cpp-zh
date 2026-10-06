

| | <!DOCTYPE, text(notationDeclarations(), entityDeclarations()) |
| EntityReference | &trade; name(), text() |
| ProcessingInstruction | <?alert?> processingInstructionTarget(), processingInstructionData() |
| Invalid | &<! error(), errorString() |

请考虑以下 XML 内容：

```
<doc>
  <quote>Einmal ist keinmal</quote>
</doc>
```

如果我们解析此文档，每次 `readNext()` 调用将产生一个新的令牌（token），并可以使用获取函数获取额外信息：

```
StartDocument
StartElement (name == "doc")
StartElement (name == "quote")
Characters (text() == "Einmal ist keinmal")
EndElement (name == "quote")
EndElement (name == "doc")
EndDocument
```

在每次调用 `readNext()` 之后，我们可以使用 `isStartElement()`、`isCharacters()` 和类似的函数来测试当前令牌的类型，或者简单地使用 `state()`。

我们将回顾一个示例，展示如何使用 `QXmlStreamReader` 解析一个临时的 XML 文件并将其内容渲染在 `QTreeWidget` 中。我们将解析的格式是书籍索引的一部分，包含条目和子条目。图 16.2 显示的书籍索引文件：

```xml
<?xml version="1.0"?>
<bookindex>
  <entry term="sidebearings">
    <page>10</page>
    <page>34-35</page>
    <page>307-308</page>
  </entry>
  <entry term="subtraction">
    <entry term="of pictures"
```

# 图 16.2. XML 流读取器应用程序

![](img/5a524abdf0b0d58fa99d30abb4463611_626_0.png)

我们将首先查看应用程序 `main()` 函数的一个片段，以查看 XML 读取器在上下文中是如何被使用的，然后我们将查看读取器的实现。

```cpp
int main(int argc, char *argv[])
{
    Application app(argc, argv);
    QStringList args = QApplication::arguments();
    ..
    QTreeWidget treeWidget;
    ....
    XmlStreamReader reader(&treeWidget);
    for (int i = 1; i < args.count(); ++i)
        reader.readFile(args[i]);
    return app.exec();
}
```

图 16.2 所示的应用程序首先创建一个 `QTreeWidget`。它随后创建一个 `XmlStreamReader`，将树部件传递给它，并要求它解析命令行指定的每个文件。

```cpp
class XmlStreamReader{
public:
    XmlStreamReader(QTreeWidget *tree);

    bool readFile(const QString &fileName);

private:
    void readBookIndexElement();
    void readEntryElement(QTreeWidgetItem *parent);
    void readPageElement(QTreeWidgetItem *parent);
    void skipUnknownElement();

    QTreeWidget *treeWidget;
    XmlStreamReader reader;
};
```

`XmlStreamReader` 类提供了两个公共函数：构造函数和 `parseFile()`。该类使用 `XmlStreamReader` 实例来解析 XML 文件，并填充 `QTree` 以反映读取的 XML 数据。解析是通过递归下降完成的：

- `readBookIndexElement()` 解析一个包含零或多个 `<entry>` 元素的 `<bookindex>...</bookindex>` 元素。
- `readEntryElement()` 解析一个 `<entry>...</entry>` 元素，它包含零或多个 `<page>` 元素和嵌套任意深度的 `<entry>` 元素。
- `readPageElement()` 解析一个 `<page>...</page>` 元素。
- `skipUnknownElement()` 跳过未识别的元素。

我们现在查看 `XmlStreamReader` 类的实现，从构造函数开始。

```cpp
XmlStreamReader::XmlStreamReader(QTreeWidget *tree)
{
    treeWidget = tree;
}
```

构造函数仅用于建立读取器使用的 `QTreeWidget`。所有的操作都发生在 `readFile()` 函数中（从 `main()` 调用），我们将分三个部分来看它。

```cpp
bool XmlStreamReader::readFile(const QString &fileName)
{
    QFile file(fileName);
    if (!file.open(QFile::ReadOnly | QFile::Text)) {
        std::cerr << "Error: Cannot read file " << qPrintable(fileName)
                  << qPrintable(file.errorString())
                  << std::endl;
        return false;
    }
    reader.setDevice(&file);
```

`readFile()` 函数通过尝试打开文件开始。如果失败，它输出错误消息并返回 `false`。如果文件成功打开，它将被设置为 `QXmlStreamReader` 的输入设备。

```cpp
reader.readNext();
while (!reader.atEnd()) {
    if (reader.isStartElement()) {
        if (reader.name() == "bookindex") {
            readBookIndexElement();
        } else {
            reader.raiseError(QObject::tr("Not a bookindex file"));
        }
    } else {
        reader.readNext();
    }
}
```

`QXmlStreamReader` 的 `readNext()` 从输入流读取下一个令牌。如果成功读取了令牌且尚未到达 XML 文件的末，函数将进入 `while` 循环。由于索引文件的结构，我们知道循环内部有三种可能性：读取了一个 `<book>`起始标签，读取了另一个起始标签（以防文件异常），或者读取了其他令牌。

在每次 `readNext()` 调用之后，我们可以使用 `isStartElement()`、`isCharacters()` 和类似的函数来测试当前令牌的类型，或者简单地使用 `state()`。

我们将回顾一个示例，展示如何使用 `QXmlStreamReader` 解析一个临时的 XML 文件并在 `QTreeWidget` 中渲染其内容。我们将解析的格式是书籍索引的一部分，包含条目和子条目。图 16.2 显示的书籍索引文件：

```cpp
reader.readNext();
while (!reader.atEnd()) {
    if (reader.isStartElement()) {
        if (reader.name() == "bookindex") {
            readBookIndexElement();
        } else {
            reader.raiseError(QObject::tr("Not a bookindex file"));
        }
    } else {
        reader.readNext();
    }
}
```

`QXmlStreamReader` 的 `readNext()` 从输入流读取下一个令牌。如果成功读取了令牌且尚未到达 XML 文件的末，函数将进入 `while` 循环。由于索引文件的结构，我们知道循环内部有三种可能性：读取了一个 `<book>` 起始标签，读取了另一个起始标签（以防文件异常），或者读取了其他令牌。

`QXmlStreamReader` 的 `readNext()` 从输入流读取下一个令牌。如果成功读取了令牌且尚未到达 XML 文件的末，函数将进入 `while` 循环。由于索引文件的结构，我们知道循环内部有三种可能性：读取了一个 `<book>` 起始标签，读取了另一个起始标签（以防文件异常），或者读取了其他令牌。

```cpp
file.close();
if (reader.hasError()) {
    std::cerr << "Error: Failed to parse " << qPrintable(fileName)
              << ":" << qPrintable(reader.errorString())
              << std::endl;
    return false;
} else if (file.error() != QFile::NoError) {
    std::cerr << "Error: Cannot read file " << qPrintable(fileName)
              << ":" << qPrintable(file.errorString())
              << std::endl;
    return false;
}
return true;
```

一旦处理完成，文件将被关闭。如果存在解析错误或文件错误，函数输出错误消息并返回 `false`；否则它返回 `true` 以报告成功解析。

```cpp
void XmlStreamReader::readBookIndexElement()
{
    reader.readNext();
    while (!reader.atEnd()) {
        if (reader.isEndElement()) {
            reader.readNext();
            break;
        }
        if (reader.isStartElement()) {
            if (reader.name() == "entry") {
                readEntryElement(treeWidget->rootItem());
            } else {
                skipUnknownElement();
            }
        } else {
            reader.readNext();
        }
    }
}
```

`readBookIndexElement()` 负责读取文件的主要部分。它通过跳过当前令牌（此时为 `<bookindex>` 起始标签）开始遍历输入。

如果读取了标签，它只能是 `</bookindex>` 标签，否则 `QXmlStreamReader` 将报告错误（意外元素）。在此，我们跳过该标签并跳出循环。否则，我们得到了顶层索引 `<entry>` 起始标签。这是为了处理条目数据；如果不是，我们调用 `skipUnknownElement()`。使用 `skipUnknownElement()` 而不是调用 `raiseError()` 意味着我们在将来扩展书籍索引格式以包含新标签时，该读取器将继续工作，因为它将简单忽略它不识别的标签。

`readEntryElement()` 接受一个 `TreeWidgetItem *` 参数来标识父项。我们将 `QTree::rootItem()` 传递父项以使新项成为根项。在 `readEntryElement()` 中，我们将递归调用 `readEntryElement()` 并传入不同的父项。

代码视图：

```cpp
void XmlStreamReader::readEntryElement(QTreeWidgetItem *parent)
{
    QTreeWidgetItem *item = new QTreeWidgetItem(parent);
    item->setText(0, reader.attributes().value("term").toString());

    reader.readNext();
    while (!reader.atEnd()) {
        if (reader.isEndElement()) {
            reader.readNext();
            break;
        }
        if (reader.isStartElement()) {
            if (reader.name() == "entry") {
                readEntryElement(item);
            } else if (reader.name() == "page") {
                readPageElement(item);
            } else {
                skipUnknownElement();
            }
        } else {
            reader.readNext();
        }
    }
}
```

