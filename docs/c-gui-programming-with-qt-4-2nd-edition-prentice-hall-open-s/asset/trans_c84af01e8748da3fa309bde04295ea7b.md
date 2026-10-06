

```
connectToHost(host, port)
login()

cd(directory_1)
list()
...
cd(directory_N)
list()
  emit listInfo(file_1_1)
  emit listInfo(file_1_2)
  ...
  emit listInfo(file_N_1)
  emit listInfo(file_N_2)
  ...
emit done()

get(file_1_1)
emit done()

get(file_1_2)
emit done()
...
get(file_N_1)
emit done()

get(file_N_2)
emit done()
...
```

另一种解决方案是每个文件使用一个 QFtp 对象。这允许我们通过单独的 FTP 连接并行下载文件。

```cpp
int main(int argc, char *argv[])
{
  QCoreApplication app(argc, argv);
  QStringList args = QCoreApplication::arguments();
  if (args.count() != 2) {
    std::cerr << "Usage: spider url" << std::endl
    << "Example:" << std::endl
    << "spider ftp://ftp.trolltech.com/freebies/"
    << "leafnode" << std::endl;
    return 1;
}

Spider spider;
if (!spider.isDirectory(QUrl(args[1])))
    return 1;

QObject::connect(&spider, SIGNAL(done()), &app, SLOT(quit));

return app.exec();
}
```

`main()` 函数完成了程序。如果用户没有在命令行上指定 URL，我们将给出一个错误消息并终止程序。

在两个 FTP 示例中，使用 `get()` 获取的数据都被写入了 `QFile`。事实并非如此。如果我们想在内存中保留数据，可以使用 `QBuffer`，它是封装 `QByteArray` 的 `QIODevice` 子类。例如：

```cpp
QBuffer *buffer = new QBuffer;
buffer->open(QIODevice::WriteOnly);
ftp.get(urlInfo.name(), buffer);
```

我们也可以省略 `get()` 的 I/O 设备参数或传递一个空指针。`QFtp` 类每当有新数据可用时都会发出 `readyRead()` 信号，可以使用 `read()` 或 `readAll()` 读取数据。

## 编写 HTTP 客户端

`Http` 类在 Qt 中实现了 HTTP 协议的客户端部分。它提供了各种函数来执行最常见的 HTTP 操作，包括 `get()` 和 `post()`，并提供了发送任意 HTTP 请求的方法。如果你读过之前关于 `QHttp` 的章节，你会发现 `QHttp` 和 `Http` 之间有很多相似之处。

`Http` 类是异步工作的。当我们调用如 `get()` 或 `post()` 函数时，函数会立即返回，数据传输将在稍后控制回到 Qt 事件循环时发生。这确保了在处理 HTTP 请求时，应用程序的用户界面仍然保持响应。

我们将回顾一个名为 `httpget` 的控制台应用程序示例，它展示了如何使用 HTTP 协议下载文件。它与上一节中的 `ftpget` 示例在功能和实现上非常相似，因此我们不会显示头文件。

```cpp
HttpGet::HttpGet(QObject *parent)
{
    QObject(parent)
    connect(&http, SIGNAL(done(bool)), this, SLOT(httpDone(bool)));
}
```

在构造函数中，我们将 `QHttp` 对象的 `done(bool)` 信号连接到私有的 `httpDone(bool)` 槽。

代码视图：

```cpp
bool HttpGet::getFile(const QUrl &url)
{
    if (!url.isValid()) {
        std::cerr << "Error: Invalid URL" << std::endl;
        return false;
    }

    if (url.scheme() != "http") {
        std::cerr << "Error: URL must start with 'http:'" << std::endl;
        return false;
    }

    if (url.path().isEmpty()) {
        std::cerr << "Error: URL has no path" << std::endl;
        return false;
    }

    QString localFileName = QFileInfo(url.path()).fileName();

    if (localFileName.isEmpty())
        localFileName = "httpget.out";

    file.setFileName(localFileName);
    if (!file.open(QIODevice::WriteOnly)) {
        std::cerr << "Error: Cannot write file "
        << qPrintable(file.fileName()) << ": "
        << qPrintable(file.errorString()) << std::endl;
        return false;
    }

    http.setHost(url.host(), url.port(80));
    http.get(url.path(), &file);
    http.close();
    return true;
}
```

`getFile()` 函数执行了与之前在网站上显示的 `FtpGetter::getFile()` 相同的错误检查，并使用相同的方法为文件指定本地名称。从网站检索内容时，不需要登录，因此我们只需设置主机和端口（如果 URL 中未指定，则使用默认 HTTP 端口 80），并将数据下载到文件中，因为 `Http::get()` 的第二个参数指定了输出 I/O 设备。

HTTP 请求在 Qt 事件循环中排队并异步执行。请求的完成通过 `Http` 的 `done(bool)` 信号指示，我们在构造函数中将其连接到 `httpDone(bool)`。

```cpp
void HttpGet::httpDone(bool error)
{
    if (error) {
        // ... 错误处理
    } else {
        // ... 成功处理
    }
}
```

`main()` 函数完成了程序。如果用户没有在命令行上指定 URL，我们将给出一个错误消息并终止程序。

```cpp
int main(int argc, char *argv[])
{
  QCoreApplication app(argc, argv);
  QStringList args = QCoreApplication::arguments();
  if (args.count() != 2) {
    std::cerr << "Usage: spider url" << std::endl
    << "Example:" << std::endl
    << "spider ftp://ftp.trolltech.com/freebies/"
    << "leafnode" << std::endl;
    return 1;
}

Spider spider;
if (!spider.isDirectory(QUrl(args[1])))
    return 1;

QObject::connect(&spider, SIGNAL(done()), &app, SLOT(quit));

return app.exec();
}
```

在两个 FTP 示例中，使用 `get()` 获取的数据都被写入了 `QFile`。事实并非如此。如果我们想在内存中保留数据，可以使用 `QBuffer`，它是封装 `QByteArray` 的 `QIODevice` 子类。例如：

```cpp
QBuffer *buffer = new QBuffer;
buffer->open(QIODevice::WriteOnly);
ftp.get(urlInfo.name(), buffer);
```

我们也可以省略 `get()` 的 I/O 设备参数或传递一个空指针。`QFtp` 类每当有新数据可用时都会发出 `readyRead()` 信号，可以使用 `read()` 或 `readAll()` 读取数据。

## 编写 HTTP 客户端

`Http` 类在 Qt 中实现了 HTTP 协议的客户端部分。它提供了各种函数来执行最常见的 HTTP 操作，包括 `get()` 和 `post()`，并提供了发送任意 HTTP 请求的方法。如果你读过之前关于 `QHttp` 的章节，你会发现 `QHttp` 和 `Http` 之间有很多相似之处。

`Http` 类是异步工作的。当我们调用如 `get()` 或 `post()` 函数时，函数会立即返回，数据传输将在稍后控制回到 Qt 事件循环时发生。这确保了在处理 HTTP 请求时，应用程序的用户界面仍然保持响应。

我们将回顾一个名为 `httpget` 的控制台应用程序示例，它展示了如何使用 HTTP 协议下载文件。它与上一节中的 `ftpget` 示例在功能和实现上非常相似，因此我们不会显示头文件。

```cpp
HttpGet::HttpGet(QObject *parent)
{
    QObject(parent)
    connect(&http, SIGNAL(done(bool)), this, SLOT(httpDone(bool)));
}
```

在构造函数中，我们将 `QHttp` 对象的 `done(bool)` 信号连接到私有的 `httpDone(bool)` 槽。

代码视图：

```cpp
bool HttpGet::getFile(const QUrl &url)
{
    if (!url.isValid()) {
        std::cerr << "Error: Invalid URL" << std::endl;
        return false;
    }

    if (url.scheme() != "http") {
        std::cerr << "Error: URL must start with 'http:'" << std::endl;
        return false;
    }

    if (url.path().isEmpty()) {
        std::cerr << "Error: URL has no path" << std::endl;
        return false;
    }

    QString localFileName = QFileInfo(url.path()).fileName();

    if (localFileName.isEmpty())
        localFileName = "httpget.out";

    file.setFileName(localFileName);
    if (!file.open(QIODevice::WriteOnly)) {
        std::cerr << "Error: Cannot write file "
        << qPrintable(file.fileName()) << ": "
        << qPrintable(file.errorString()) << std::endl;
        return false;
    }

    http.setHost(url.host(), url.port(80));
    http.get(url.path(), &file);
    http.close();
    return true;
}
```

`getFile()` 函数执行了与之前在网站上显示的 `FtpGetter::getFile()` 相同的错误检查，并使用相同的方法为文件指定本地名称。从网站检索内容时，不需要登录，因此我们只需设置主机和端口（如果 URL 中未指定，则使用默认 HTTP 端口 80），并将数据下载到文件中，因为 `Http::get()` 的第二个参数指定了输出 I/O 设备。

HTTP 请求在 Qt 事件循环中排队并异步执行。请求的完成通过 `Http` 的 `done(bool)` 信号指示，我们在构造函数中将其连接到 `httpDone(bool)`。

```cpp
void HttpGet::httpDone(bool error)
{
    if (error) {
        // ... 错误处理
    } else {
        // ... 成功处理
    }
}
```

`main()` 函数完成了程序。如果用户没有在命令行上指定 URL，我们将给出一个错误消息并终止程序。

```cpp
int main(int argc, char *argv[])
{
  QCoreApplication app(argc, argv);
  QStringList args = QCoreApplication::arguments();
  if (args.count() != 2) {
    std::cerr << "Usage: spider url" << std::endl
    << "Example:" << std::endl
    << "spider ftp://ftp.trolltech.com/freebies/"
    << "leafnode" << std::endl;
    return 1;
}

Spider spider;
if (!spider.isDirectory(QUrl(args[1])))
    return 1;

QObject::connect(&spider, SIGNAL(done()), &app, SLOT(quit));

return app.exec();
}
```

在两个 FTP 示例中，使用 `get()` 获取的数据都被写入了 `QFile`。事实并非如此。如果我们想在内存中保留数据，可以使用 `QBuffer`，它是封装 `QByteArray` 的 `QIODevice` 子类。例如：

```cpp
QBuffer *buffer = new QBuffer;
buffer->open(QIODevice::WriteOnly);
ftp.get(urlInfo.name(), buffer);
```

## 编写 TCP 客户端-服务器应用程序

`TcpSocket` `TcpServer` 类用于实现 TCP 客户端和服务器。TCP 是一种传输协议，构成了大多数应用层协议（包括 FTP 和 HTTP）的基础，也可以用于自定义协议。

TCP 是面向流的协议。对于应用程序而言，数据看起来像是一个长流，类似于一个大型平面文件。构建在 TCP 之上的高级协议通常是面向行或面向块的：

- 面向行的协议以文本行传输数据，每行都以换行符结束。
- 面向块的协议以二进制数据块传输数据。每个块由一个大小字段和相应长度的数据组成。

`TcpSocket` 间接派自 `QIODevice`（通过 `QAbstractSocket`），因此可以使用 `QDataStream` 或 `QTextStream` 进行读写。从网络读取数据与从文件读取数据相比，一个显著区别在于在使用 `>>` 运算符之前，我们必须确保已经从对端接收了足够的数据。这样做可能会导致未定义行为。

在本节中，我们将回顾使用自定义面向块协议的客户端和服务器代码。图 15.1 所示的客户端称为 `Trip Planner`，允许用户规划下一次旅行之旅。服务器称为 `Trip Server`，它为客户端提供旅行信息。我们将从编写 `Trip Planner` 客户端开始。

