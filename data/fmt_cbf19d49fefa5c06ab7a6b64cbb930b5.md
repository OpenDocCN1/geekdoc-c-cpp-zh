
`QStringList` `pendingDirs`;

};

起始目录被指定为 `QUrl`，并使用 `getDirectory()` 函数设置。

```cpp
Spider::Spider(QObject *parent)
  : QObject(parent)
{
  connect(&ftp, SIGNAL(done(bool)), this, SLOT(ftpDone(bool)));
  connect(&ftp, SIGNAL(listInfo(const QUrlInfo&)),
         this, SLOT(ftpListInfo(const QUrlInfo&)));
}
```

在构造函数中，我们建立了两个信号槽连接。当我们为获取的每个文件请求目录列表 `getDirectory()` 时，`QFtp` 会发出 `listInfo(const QUrlInfo&)` 信号。该信号被连接到一个名为 `ftpListInfo()` 的槽，该槽会下载与给定 URL 关联的文件。

```cpp
bool Spider::isValid(const QUrl &url)
{
  if (!url.isValid()) {
    std::cerr << "Error: Invalid URL" << std::endl;
    return false;
  }
  if (url.scheme() != "ftp") {
    std::cerr << "Error: URL must start with 'ftp:'" << std::endl;
    return false;
  }
  ftp.connectToHost(url.host(), url.port(21));
  ftp.login();
  QString path = url.path();
  if (path.isEmpty())
```

当调用 `getDirectory()` 函数时，它首先开始一些健全性检查，如果一切正常，它将尝试建立 FTP 连接。它跟踪必须处理的路径，并调用 `processNextDirectory()` 开始下载根目录。

`processNextDirectory()` 函数从 `pendingDirs` 中取出第一个远程目录，并在本地文件系统中创建一个对应的目录。它告诉 `QFtp` 对象切换到目录并列出其文件。对于 `list()` 处理的每个文件，它都会发出 `listInfo()` 信号，导致下载与该 URL 关联的文件。

当命令队列为空时，会发出 `done(bool)` 信号。

当发生错误时，`QFtp` 会自动清空命令队列。这意味着如果连接或登录失败，队列中后续命令将永远不会执行。如果在错误发生后使用同一个 `QFtp` 对象调度了新命令，这些命令将被排队并执行。

这里的 `listInfo` 槽提供了关于远程文件的详细信息。参数 `urlInfo`

在 `Spider` 类中，`ftpDone` 槽实现如下：

```cpp
void Spider::ftpDone(bool error) {
    if (error) {
        std::cerr << "Error: " << qPrintable(ftp.errorString())
                   << std::endl;
    } else {
        std::cout << "Download complete!" << std::endl;
    }
}
```

当 `done()` 信号发出时，表示下载已完成。

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

另一种解决方案是每个文件使用一个 `QFtp` 对象。这允许我们通过单独的 FTP 连接并行下载文件。

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

`getFile()` 函数执行了与之前在网站上显示的 `FtpGetter::getFile()` 相同的错误检查，并使用相同的方法为文件指定本地名称。从网站检索内容时，不需要登录，因此我们只需设置主机和端口，如果 URL 中未指定，则使用默认 HTTP 端口 80，并将数据下载到文件中，因为 `Http::get()` 的第二个参数指定了输出 I/O 设备。

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
```

