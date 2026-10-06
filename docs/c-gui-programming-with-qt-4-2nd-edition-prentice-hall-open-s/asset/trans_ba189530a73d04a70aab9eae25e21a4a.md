
如果 Qt 不支持为自定义类型提供 `<< >>`，由于我们可以使用 `QVariant` 来存储这些类型的值，那么在编译器错误中提供流操作符将使它们变得实用得多——例如通过 `QSettings`。前提是我们需要预先使用 `qRegisterTypeStreamOperators<T>()` 注册该类型，正如第 11 节（第 292 页）所示。

当我们使用 `QStream` 时，Qt 会处理每个条目的读写，包括包含任意数量项的容器。这让我们免去了构建结构化写入内容以及对读取内容进行任何类型解析的负担。我们唯一的责任是确保读取所有条目的顺序与写入的顺序完全一致，将所有细节交给 Qt 处理。

`QDataStream` 对于我们自定义的二进制格式和标准二进制格式非常有用。我们可以使用流操作符对对象（如 `quint16` 和 `float`）或使用 `readRawBytes()` 和 `writeRawBytes()` 来读取和写入标准二进制格式。如果 `QDataStream` 仅用于读取和写入基础 C++ 数据类型，我们甚至不需要调用 `setVersion()`。

到为止，我们一直硬编码流版本为 `QDataStream::Qt_4_3` 来加载和保存数据。这种方法简单且安全，但有一个小缺陷：我们无法利用新或更新的格式。例如，如果 Qt 的后续版本为某个类添加了新属性，而我们硬编码版本号为 `Qt_4_3`，那么该属性将无法被保存或加载。有两种解决方案。第一种是在文件中嵌入 `QDataStream` 版本号：

```
QDataStream out(&file);
out << quint32(MagicNumber) << quint16(out.version());
```

（`MagicNumber` 是一个唯一标识文件类型的常量。）这种方法确保了我们始终使用最新版本的 `QDataStream` 来读取数据，无论发生什么情况。当我们要读取文件时，我们读取流：

```
quint32 magic;
quint16 streamVersion;
QDataStream in(&file);
in >> magic >> streamVersion;
```

```
if (magic != MagicNumber) {
    std::cerr << "File is not recognized by this application"
        << std::endl;
} else if (streamVersion > in.version()) {
```

```
std::cerr << "File is from a more recent version of the "application" << std::endl;
}
```

```
in.setVersion(streamVersion);
```

只要流版本小于或等于应用程序使用的版本，我们就可以读取数据；否则，我们会报告错误。

如果文件格式包含自己的版本号，我们可以用它来推断流版本，而不是显式存储。例如，假设文件格式适用于我们应用程序的 1.3 版本。我们可能如下方式将其写入数据中：

```
QDataStream out(&file);
out.setVersion(QDataStream::Qt_4_3);
out << quint32(MagicNumber) << quint16(0x0103);
```

当我们读回它时，根据应用程序的版本号来决定使用哪个 `QDataStream` 版本：

```
QDataStream in(&file);
in >> magic >> appVersion;
```

```
if (magic != MagicNumber) {
  std::cerr << "File is not recognized by this application"
  << std::endl;
  return false;
} else if (appVersion > 0x0103) {
  std::cerr << "File is from a more recent version of the "application" << std::endl;
  return false;
}
```

```
if (appVersion < 0x0103) {
  in.setVersion(QDataStream::Qt_3_0);
} else {
  in.setVersion(QDataStream::Qt_4_3);
}
```

在这个示例中，我们指定了任何使用 1.3 之前的版本保存的文件。

在其他场景下，直接访问 `QIODevice` 比使用 `QDataStream` 更合适。`QIODevice` 提供了一个 `peek()` 函数，可以在不移动设备位置的情况下返回下一个字节，以及一个 `unChar()` 函数，它可以“撤销”一个字节的读取。这对于随机访问设备（如文件）和顺序设备（如网络套字）都有效。对于支持随机访问的设备，还有一个设置设备位置的 `seek()` 函数。二进制文件提供了存储数据最灵活且紧的方法，而 `QDataStream` 让访问二进制数据变得简单。除了本节的示例外，我们已经在第 4 节见过 `QDataStream` 的用法，并在第 21 节再次看到，在那里用它来读写光标文件。

# 2. 输入/输出

- 读取和写入二进制数据
- 读取和写入文本
- 遍历目录
- 嵌入资源
- 进程通信

从文件或其他设备读取或写入的需求几乎几乎每个应用程序共有的。Qt 通过 `QDevice` 为 I/O 提供了卓越的支持，这是一个封装了能够读写字节块的“设备”的强大抽象。Qt 包含了 `QDevice` 子类：

| 类 | 说明 |
| --- | --- |
| QFile | 访问本地系统和嵌入资源中的文件 |
| QTemporaryFile | 在本地系统中创建并访问临时文件 |
| QBuffer | 从 QByteArray 读取数据或向其写入数据 |
| QProcess | 运行外部进程并处理进程间通信 |
| QTcpSocket | 使用 TCP 在网络上传输数据流 |
| QUdpSocket | 在网络上发送或接收数据报 |
| QssSocket | 使用 SSL/TLS 在网络上传输加密数据 |

`QProcess`、`QTcpSocket`、`QUdpSocket` 和 `QssSocket` 是顺序设备，这意味着数据只能从第一个字节开始，线性进展到最后一个字节访问一次。`QFile`、`QTemporaryFile` 和 `QBuffer` 是随机访问设备，因此可以从任何位置读取多次字节；它们提供了 `QDevice::seek()` 函数来重定位文件指针。除了设备类外，Qt 还提供了两个更高级的流类，我们可以用它们读写 I/O 设备：用于二进制的 `QDataStream` 和用于文本的 `QTextStream`。这些类处理了如字节序等问题，使得在不同平台或不同国家运行的 Qt 能够读写彼此的文件。这使得 Qt 的 I/O 类比对应的标准 C++ 类更方便，后者将这些问题留给了应用程序程序员。`QFile` 使得访问单个文件变得简单，无论它们是在文件系统中的，还是作为资源嵌入在应用程序的可执行文件中。对于需要识别处理哪些组文件的应用程序，Qt 提供了 `QDir`。
