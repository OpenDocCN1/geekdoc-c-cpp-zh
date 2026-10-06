
我们读取的 QDataStream 版本与写入时使用的版本相同。这必须如此。通过硬编码版本号，我们保证了应用程序始终能够读取和写入数据（假设它是使用 Qt 4.3 或更高版本编译的）。

QDataStream 存储数据的方式使我们能够无缝地读回数据。QByteArray 表示为 32 位的字节计数，随后紧跟字节本身。QDataStream 也可以用于读取和写入字节，并带有任何字节计数器、`readRawBytes()` 和 `writeRawBytes()`。

从 QDataStream 读取数据时的错误处理相当简单。返回的 `status()` 值可以是 `QDataStream::Ok`、`QDataStream::ReadPastEnd` 或 `QDataStream::ReadCorruptData`。一旦发生错误，`>>` 运算符将读取零值或空值。这意味着我们通常可以简单地读取整个文件而不必担心潜在错误，并在最后检查 `status()` 值以查看具体情况。

QDataStream 处理多种 C++ 和 Qt 数据类型；完整列表请见 http://doc.troll.com/4.3/datastreamformat.html。我们也可以通过重载 `<<` 和 `>>` 运算符为自定义类型添加支持。这里是一个可以与 QDataStream 一的自定义数据类型的定义：

```cpp
class Painting
public:
    Painting() : myYear = 0; {}
    Painting(const QString &title, const QString &artist, int year) {
        myTitle = title;
        myArtist = artist;
        myYear = year;
    }

    void setTitle(const QString &title) { myTitle = title; }
    QString title() const { return myTitle; }
    ...
private:
    QString myTitle;
    QString myArtist;
    int myYear;
};

QDataStream &operator<<(QDataStream &out, const Painting &painting);
QDataStream &operator>>(QDataStream &in, Painting &painting);
```

```cpp
QDataStream &operator<<(QDataStream &out, const Painting &painting) {
    out << painting.title() << painting.artist()
    << quint32(painting.year());
    return out;
}
```

要输出一个 `Painting` 对象，我们只需输出两个 `QString` 和一个 `quint32`。在函数末尾，我们返回流。这是一个常见的 C++ 惯用法，允许我们在输出流上使用 `<<` 运算符链。例如：

```cpp
out << painting1 << painting2 << painting3;
```

`operator>>()` 的实现与 `operator<<()` 的实现相似：

```cpp
QDataStream &operator>>(QDataStream &in, Painting &painting) {
    QString title;
    QString artist;
    quint32 year;

    in >> title >> artist >> year;
    painting = Painting(title, artist, year);
    return in;
}
```

为自定义数据类型提供流运算符有几个好处。其中之一是允许我们流处理使用自定义类型的容器。例如：

```cpp
QList<Painting> paintings = ...;
out << paintings;
```

```cpp
QList<Painting> paintings;
in >> paintings;
```

提供流的另一个好处是，如果 `Painting` 没有支持自定义类型的 `<<` 和 `>>`，编译器会报错。我们还可以使用 `QVariant` 存储类型的值，这使得它们更具可用性——例如通过 `QSettings`。只要按照第 11 节（第 292 页）所述提前使用 `qRegisterTypeStreamOperators<T>()` 注册该类型，即可生效。

当我们使用 QStream 时，Qt 会负责读取和写入每个条目，包括包含任意数量项目的容器。这减轻了我们对写入内容结构以及对读取内容进行任何类型解析的需要。我们唯一的义务是确保按照写入相同的顺序读取所有条目，让 Qt 处理所有细节。

QDataStream 对于我们自定义的格式和标准二进制格式非常有用。我们可以使用在对象上的流（如 `quint16` 和 `float`）或使用 `readRawBytes()` 和 `writeRawBytes()` 来读取和写入标准二进制格式。如果 QDataStream 纯粹用于读取和写入基本 C++ 数据类型，我们甚至不需要调用 `setVersion()`。

到目前为止，我们使用硬编码为 `QDataStream::Qt_43` 的流版本来加载和保存数据。这种方法简单安全，但它有一个缺陷：我们无法利用新格式或更新的格式。例如，如果后来的 Qt 版本添加了新属性，它将无法被保存或加载。有两种解决方案。第一种方法是将 QDataStream 版本嵌入到文件中：

```cpp
QDataStream out(&file);
out << quint32(MagicNumber) << quint16(out.version());
```

(`MagicNumber` 是一个唯一标识文件的常量。）这种方法确保了我们始终使用最新版本读取数据，无论发生什么。当我们来读取文件时，我们读取流：

```cpp
quint32 magic;
quint16 streamVersion;
QDataStream in(&file);
in >> magic >> streamVersion;
```

```cpp
if (magic != MagicNumber) {
    std::cerr << "File is not recognized by this application" << std::endl;
} else if (streamVersion > in.version()) {
    std::cerr << "File is from a more recent version of the application" << std::endl;
    return false;
}
```

```cpp
if (streamVersion < in.version()) {
    in.setVersion(QDataStream::Qt_3_0);
} else {
    in.setVersion(QDataStream::Qt_4_3);
}
```

在这个示例中，我们指定对于任何使用应用程序 1.3 之前的版本保存的文件，我们使用它来推断流版本，而不是显式存储。例如，假设文件格式适用于我们应用程序的 1.3 版本。我们可以如下将其写入数据：

```cpp
QDataStream out(&file);
out.setVersion(QDataStream::Qt_4_3);
out << quint32(MagicNumber) << quint16(0x0103);
```

当我们读回它时，根据应用程序的版本号确定使用哪种 QDataStream 版本：

```cpp
QDataStream in(&file);
in >> magic >> appVersion;
```

```cpp
if (magic != MagicNumber) {
  std::cerr << "File is not recognized by this application" << std::endl;
  return false;
} else if (appVersion > 0x0103) {
  std::cerr << "File is from a more recent version of the application" << std::endl;
  return false;
}
```

在这个示例中，我们指定对于任何使用应用程序 1.3 之前的版本保存的文件，我们使用它来推断流版本，而不是显式存储。

# 读取和写入文本

二进制文件通常比文本格式更紧凑，后者不是人类可读或可编辑的。在这些问题的情况下，可以使用文本格式。Qt 提供了 `QStream` 类用于读取和写入纯文本文件以及其他文本格式的文件，如 HTML、XML 和源代码。我们在第 16 节专门处理 XML 文件。

QStream 负责在 Unicode 和系统本地编码或其他任何编码之间进行转换，并透明地处理不同操作系统使用的行结束（Windows 上的 "\n"，Unix 和 Mac OS 上的 "\n"）。QStream 使用 16 位的 `QString` 类型作为其基本数据单元。除了字符和字符串外，QStream 还支持 C++ 基本数值类型以及字符串。例如，以下代码向 `sf-book.txt` 文件写入 "Thomas M. Disch: 334\n"：

```cpp
QFile file("sf-book.txt");
if (!file.open(IODevice::WriteOnly)) {
    std::cerr << "Cannot open file for writing: "
    << qPrintable(file.errorString()) << std::endl;
    return;
}
```

```cpp
QTextStream out(&file);
out << "Thomas M. Disch: " << 334 << endl;
```

写入文本非常简单，但读取文本可能具有挑战，因为文本数据（与使用 QDataStream 写入的二进制数据不同）本质上是模糊的。让我们考虑以下示例：

```cpp
out << "Denmark" << "Norway";
```

如果 `out` 是一个 `QTextStream`，实际的数据是字符串 "DenmarkNorway"。我们无法期望以下代码能够正确读取数据：

```cpp
in >> str1 >> str2;
```

事实上，发生的情况是 `str1` 获取了整个单词 "DenmarkNorway"，而 `str2` 什么都没有得到。这个问题在使用 QDataStream 时不会发生，因为它在字符数据之前存储了每个字符串的长度。
