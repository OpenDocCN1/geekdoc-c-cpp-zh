
```cpp
str.remove(2, 6);
str.insert(2, "sunny");
```

首先，我们从位置 2 开始删除六个字符，得到字符串 "a day"（带有空格），然后在位置 2 插入 "sunny"。

`replace()` 还有重载版本，可以将第一个参数的所有出现处替换为第二个参数。例如，这里将字符串中所有的 "&" 替换为 "&amp;"：

```cpp
str.replace(\&", "&amp;");
```

一个频繁的需求是去除字符串中的空白（如空格、制表符和换行符）。`QString` 有一个函数可以消除字符串两端的空白：

```cpp
QString str = " BOB \t THE \nDOG \n";
qDebug() << str.trimmed();
```

字符串 `str` 可以描绘为

| | B | O | B | \t | T | H | E | \n | D | O | G | \n |

`trimmed()` 返回的字符串为：

```
BOB|\t|THE|\nDOG
```

在处理用户输入时，我们通常除了去除两端的空白字符外，还希望将每一个一个或多个内部空白字符序列替换为单个空格。这就是 `simplified()` 函数的作用：

```
QString str = " BOB \t THE \nDOG \n"
debug() << str.simplified();
```

`simplified()` 返回的字符串为：

```
BOB|THE|DOG
```

可以使用 `QString::split()` 将字符串分割为子字符串列表 `QStringList`：

```cpp
QString str = "polluter pays principle"
QStringList words = str.split(" ");
```

在前面的示例中，我们将字符串 "polluter pays principle" 拆分为三个子字符串："polluter"、pays" 和 "principle"。`split()` 函数有一个可选参数，用于指定是否保留（默认值）或丢弃空子字符串。

可以使用 `join()` 将 `QStringList` 中的项合并成单个字符串。`join()` 的参数被插入在每对连接的字符串之间。例如，这里是如何创建一个由 `QStringList` 中包含的所有字符串按字母顺序排序并用换行符分隔的单个字符串：

```
words.sort();
str = words.join("\n");
```

在处理字符串时，我们经常需要判断字符串是否为空。这可以通过调用 `isEmpty()` 或检查 `length()` 是否为 0 来。

在大多数情况下，从 `const char *` 字符串到 `QString` 的转换是自动的：

```cpp
str += " (1870)";
```

我们可以直接将 `const char *` 添加到 `QString` 中。要显式将 `const char *` 转换为 `QString`，只需使用 `QString` 强制转换，或调用 `fromAscii()` 或 `fromLatin1()`。（有关处理其他编码中的字面量字符串的说明，请参见第 18 章。）

将 `QString` 转换为 `const char *` 请使用 `toAscii()` 或 `toLatin1()`。这些函数返回一个 `QByteArray`，可以使用 `QByteArray::data()` 或 `QByteArray::constData()` 将其转换为 `const char *`。例如：

```cpp
printf("User: %s\n", str.toAscii().data());
```

为了方便，Qt 提供了 `qPrintable()` 宏，它的功能与 `toAscii().constData()` 相同：

```cpp
printf("User: %s\n", qPrintable(str));
```

当我们在 `QByteArray` 上调用 `data()` 或 `constData()` 时，返回的字符串由 `QByteArray` 对象拥有。这意味着我们不需要担心内存泄漏；Qt 会为我们回收内存。另一方面，我们必须注意不要长时间使用该指针。如果 `QByteArray` 没有存储在变量中，它将在语句结束时自动删除。

`QByteArray` 拥有与 `QString` 非常相似的 API。`left()`、`right()`、`toLower()`、`toUpper()`、`trimmed()` 和 `simplified()` 等函数在 `QByteArray` 中存在，其语义与其对应的 `QString` 版本相同。`QByteArray` 用于存储原始二进制数据和 8 位编码字符串。通常，我们建议使用 `QString` 存储文本而不是 `QByteArray`，因为 `QString` 支持 Unicode。

为了方便，`QByteArray` 会自动确保“最后一个字节之后”的字节始终为 '0'，这便于将 `QByteArray` 解析给接受 `const char *` 的函数。`QByteArray` 还支持嵌入 '\0' 字符，允许我们使用它存储二进制数据。

在某些情况下，我们需要在同一个变量中存储不同类型的数据。方法是将是将编码为 `QByteArray` 或 `QString`。例如，一个字符串可以包含文本值或字符串形式的数值。这些方法提供了完全的灵活性，但放弃了 C++ 的优势、类型安全性和效率。`QVariant` 提供了一种更清晰的方法处理不同类型：`QVariant`。

`QVariant` 类处理许多 Qt 类型，包括 `QBrush`、`QColor`、`Cursor`、`DateTime`、`QFont`、`QKeySequence`、`QPalette`、`QPen`、`QPixmap`、`QPoint`、`QRect`、`QRegion`、`QSize` 和 `QString`，以及 double、int 等基本 C++ 数字类型。`QVariant` 还可以包含：`QMap<QString, QVariant>`、`QStringList` 和 `List<QVariant>`。

项视图（item view）扩展了数据库模块，广泛允许我们读取和写入项数据、数据库数据以及任何传递的兼容 `QVariant` 类型的用户偏好。我们已经在第 3 章看到过这个示例，其中我们将一个 `QRect`、一个 `QString` 和几个变体传递给 `QSettings::setValue()`，并在以后检索了它们。

可以通过 `QVariant` 通过嵌套不同类型的容器创建任意复杂的数据结构：

```cpp
QMap<QString, QVariant> pearMap;
pearMap["Standard"] = 1.95;
pearMap["Organic"] = 2.25;

QMap<QString, QVariant> fruitMap;
fruitMap["Orange"] = 2.10;
fruitMap["Pineapple"] = 3.85;
fruitMap["Pear"] = pearMap;
```

在这里，我们创建了一个具有字符串键（产品名）和浮点数（价格）或 map 值。顶层 map 包含三个键："Orange"、"Pear" 和 "Pineapple"。与 "Pear" 键关联的值是一个包含两个键（"Standard" 和 "Organic"）的 map。在迭代持有变体值的 map 时，我们需要使用 `type()` 来检查变体持有的类型，以便我们恰当地返回。

创建这样的数据结构可能非常有吸引力，因为我们可以按照喜欢的方式组织数据。但 `QVariant` 的便利性是以效率和可读性为代价的。原则上，只要尽可能定义一个合适的 C++ 类来存储我们的数据是值得的。

`QVariant` 被 Qt 的元对象系统使用，因此是 Qt Core 的。尽管如此，当我们链接到 Qt Gui 模块时，`QVariant` 可以存储 GUI 相关的类型，如 `QColor`、`QFont`、`QIcon`、`QImage` 和 `QPixmap`：

```cpp
QIcon icon("open.png");
QVariant variant = icon;
```

要从 `QVariant` 获取 GUI 相关类型的值，我们可以如下使用 `QVariant::value<T>()` 模板成员函数：

```cpp
QIcon icon = variant.value<QIcon>();
```

`value<T>()` 函数也适用于非 GUI 数据类型与 QVariant 之间的转换，但在实践中，我们通常对非 GUI 类型使用 to... 转换函数（例如 `toString()`）。

`QVariant` 还可以用于存储自定义数据类型，假设它们提供了默认构造函数和拷贝构造函数。为了这项工作，我们必须首先使用 `Q_DECLARE_METATYPE()` 宏注册该类型，通常在头文件中的类定义下方：

```cpp
Q_DECLARE_METATYPE(BusinessCard)
```

这允许我们编写如下代码：

```cpp
BusinessCard businessCard;
QVariant variant = QVariant::fromValue(businessCard);
if (variant.canConvert<BusinessCard>()) {
    BusinessCard card = variant.value<BusinessCard>();
    ...
}
```

由于编译器的限制，这些模板成员函数不支持 MSVC 6。如果你需要使用该编译器，请改用全局函数 `qVariantFromValue()`、`qVariantValue<T>()` 和 `qVariantCanConvert<T>()`。

如果自定义数据类型具有用于读写 `QDataStream` 的 << 和 >> 运算符，我们可以使用 `qRegisterMetaTypeStreamOperators<T>()` 注册它们。这使得可以使用 `QSettings` 等工具存储自定义数据类型的偏好。例如：

```cpp
qRegisterMetaTypeStreamOperators<BusinessCard>("BusinessCard");
```

Variant 侧重于 Qt 容器以及 `QString`、`QByteArray`。除了这些类，Qt 还提供了其他容器。其中一个是 `QPair<T1, T2>`，它简单地存储两个值，类似于 `std::pair<T1, T2>`。另一个是 `QByteArray`，我们将在第 21 节节使用它。最后是 `QVarLengthArray<T, Prealloc>`，它是 `QVector<T>` 的底层替代方案。因为它在栈上预分配内存且不是隐式共享，它的开销比 `QVector<T>` 小，更适用于密集循环。

Qt 算法（包括此处未涵盖的 qCopyBackward() 和 qEqual()）在 Qt 文档中描述：http://doc.trolltech.com/4.3/qtalgorithms.html。关于 Qt 容器的更多细节，包括有关其时间复杂度和增长策略的信息，请参见 http://doc.trolltech.com/4.3/containers.html。

## 2. 输入/输出

![](img/5a524abdf0b0d58fa99d30abb4463611_464_0.png)

- 读写二进制数据
- 读写文本
- 遍历目录
- 嵌入资源
- 进程间通信

从文件或其他设备读取或写入数据是几乎每个应用程序共同的需求。Qt 通过 `QIODevice` 提供了优秀的 I/O 支持，这是一个强大的抽象，它封装了能够读写字节块的“设备”。Qt 包含了以下 `QIODevice` 子类：

| 类 | 说明 |
| :--- | :--- |
| `QFile` | 访问本地文件系统和嵌入资源中的文件 |
| `QTemporaryFile` | 在本地文件系统中创建并访问临时文件 |
| `QBuffer` | 从 `QByteArray` 读取或向其写入数据 |
| `QProcess` | 运行外部进程并处理进程间通信 |
| `QTcpSocket` | 使用 TCP 在网络上传输数据流 |
| `QUdpSocket` | 在网络上发送或接收 UDP 数据报 |
| `QssSocket` | 使用 SSL/TLS 在网络上传输加密数据流 |

`QProcess`、`QTcpSocket`、`QUdpSocket` 和 `QssSocket` 是顺序设备，这意味着设备只能访问一次，从第一个字节开始逐个到最后一个字节。`QFile`、`QTemporaryFile` 和 `QBuffer` 是随机访问设备，因此可以从任何位置读取任意次数；它们提供了 `QIODevice::seek()` 函数来重置文件指针。

除了设备类之外，Qt 还提供了两个更高级的流类，我们可以使用它们来对任何 I/O 设备进行读写操作：用于二进制流的 `QDataStream` 和用于文本的 `QTextStream`。这些类处理了字节序和文本编码等问题，使得运行在不同平台或不同国家的 Qt 应用程序可以相互读写对方的文件。这使得 Qt 的 I/O 类比相应的标准 C++ 类更加方便，后者将这些问题留给了应用程序程序员处理。

`QFile` 使得访问单个文件变得简单，无论它们是在文件系统系统中，还是作为资源嵌入在应用程序的可执行文件中。对于需要标识要处理哪组文件的应用程序，Qt 提供了 `QDir` 和 `QFileInfo` 类，它们负责处理目录并提供内部文件的信息。

`QProcess` 允许我们启动外部程序并通过其标准输入、标准输出和错误通道（`cin`、`cout`、`cerr`）与其通信。我们可以设置外部应用程序将使用的环境变量和工作目录。默认情况下，与进程的通信是异步的（非阻塞），但也可以在某些操作上进行阻塞。

网络和读写 XML 是非常重要的主题，我们将在各自的专门章节中进行介绍（第 15 章和第 16 章）。

## 读写二进制数据

使用 Qt 加载和保存二进制数据简单的方法是实例化一个 `QFile`，打开文件并通过 `QDataStream` 对象进行访问。`QDataStream` 提供了一种与平台无关存储格式，支持 `int` 和 `double` 等 C++ 类型以及许多 Qt 数据类型，包括 `QByteArray`、`QFont`、`QImage`、`QPixmap`、`QString` 和 `QVariant`，以及 Qt 容器类如 `QList<T>` 和 `QMap<K, T>`。

以下是如何在 `QImage` (phil.png) 中存储一个整数、一个 `QImage` 和一个 `QMap<QString, QColor>`：

```
facts.dat:
Map<QString, QColor> map;
map.insert("red", Qt::red);
map.insert("green", Qt::green);
map.insert("blue", Qt::blue);

QFile file("facts.dat");
if (!file.open(IODevice::WriteOnly)) {
    std::cerr << "Cannot open file for writing: "
              << qPrintable(file.errorString()) << std::endl;
    return;
}
```

```
QDataStream out(&file);
```

```
out << uint32(0x12345678) << image << map;
```

（注：此处原文示例代码片段略有错乱，翻译时已根据逻辑对齐）

如果无法打开文件，我们将通知用户并返回。`qPrintable()` 返回一个 `const char *` 用于 `QString`。（另一种方法是使用 `toStd()`，它返回 `std::string`，`<iostream>` 有其重载。）

如果文件打开成功，我们创建一个 `QDataStream` 并设置其版本号。版本号是一个影响 Qt 类型表示方式的整数（基础 C++ 类型表示方式始终相同）。在 Qt 4.3 中，最全面的格式是版本 9。我们可以硬编码常量 9，也可以使用符号名 `QDataStream::Qt_4_3`。

为了确保数字 012345678 在所有平台上都被写入为 32 位无符号整数，我们可以将其强制转换为 `uint32`，这是一个保证为 32 字节的数据类型。为了确保互操作性，`QDataStream` 默认采用大端序；可以通过调用 `setByteOrder()` 进行更改。

不需要显式关闭文件，因为当 `QFile` 变量离开作用范围时会自动关闭。我们需要验证数据是否已写入，可以调用 `flush()` 并检查其返回值（true 表示成功）。

读取数据的代码与我们编写写入的代码镜像：

```
uint32 n;
QImage image;
QMap<QString, QColor> map;
```

```
QFile file("facts.dat");
if (!file.open(IODevice::ReadOnly)) {
  std::cerr << "Cannot open file for reading: "
            << qPrintable(file.errorString()) << std::endl;
  return;
}
```

```
QDataStream in(&file);
in.setVersion(QDataStream::Qt_4_3);
```

```
in >> n >> image >> map;
```
