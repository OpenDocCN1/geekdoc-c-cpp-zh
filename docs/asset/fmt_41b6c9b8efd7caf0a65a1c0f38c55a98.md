
Qt 的许多非 GUI 类（包括 `QImage`、`QString` 和容器类）使用隐式共享（implicit sharing）作为优化。虽然这种优化通常会使类变得不可重入，但在 Qt 中这不是问题，因为 Qt 使用原子语言指令来实现线程安全的引用计数，使得隐式共享类变为重入。

`QtSql` 模块也可以用于多线程应用程序，但它有自己的限制，这些限制随数据库而异。详细信息请参阅 `http://doc.qt-project.com/4.3/sql-driver.html`。多线程注意事项的完整列表请参阅 `http://doc.qt-project.com/4.3/threads.html`。

## 15. 网络

- 编写 FTP 客户端
- 编写 HTTP 客户端
- 编写 TCP 服务器应用程序
- 发送和接收 UDP 报文

Qt 提供了 `QFtp` 和 `QHttp` 类用于处理 FTP 和 HTTP 协议。这些类对于下载和上传文件、向 Web 服务器发送请求以及获取结果非常容易。Qt 还提供了更底层的 `TcpSocket` 和 `QUdpSocket` 类。TCP 是一种可靠的面向连接协议，以节点间传输的数据流运行；而 UDP 是一种基于节点间发送的离散数据包的不可靠无连接协议。两者都可以用于创建网络客户端和服务器应用程序。对于服务器，我们还需要 `TcpServer` 类来处理传入的连接。可以使用 `QSSocket` 建立 SSL/TLS 连接。

### 编写 FTP 客户端

`QFtp` 类实现了 Qt 中 FTP 协议的客户端部分。它提供了各种函数来执行常见的 FTP 操作，并允许我们执行 FTP 命令。`QFtp` 类是异步工作的。当我们调用类似 `get()` 或 `put()` 的函数时，它会立即返回，控制权交回 Qt 的事件循环。这确保了在执行 FTP 命令时用户界面仍然保持响应。

我们将从一个示例开始，展示如何使用 `get()` 获取单个文件。该示例是一个控制台应用程序，用于下载命令行指定的远程文件。让我们从 `main()` 函数开始：

```cpp
int main(int argc, char *argv[])
{
    QCoreApplication app(argc, argv);
    QStringList args = QCoreApplication::arguments();
    if (args.count() != 2) {
      std::cerr << "Usage:" << std::endl;
      std::cerr << "Example:" << std::endl;
      std::cerr << "ftpget <url>" << std::endl;
      return 1;
    }
    FtpGet getter;
    if (!getter.getFile(QUrl(args[1]))) {
      return 1;
    }
    QObject::connect(&getter, SIGNAL(done()), &app, SLOT(quit()));
    return app.exec();
}
```

我们创建一个 `QCoreApplication` 以避免链接 Qt 库。`QCoreApplication::arguments()` 返回命令行参数的 `QStringList`，第一个参数。`main()` 函数的核心是构造 `FtpGet` 对象并调用 `getFile()`。如果调用成功，让事件循环运行直到下载完成。工作由 `FtpGet` 子类完成，其定义如下：

```cpp
class FtpGet : public QObject
{
  Q_OBJECT
public:
  FtpGet(QObject *parent = 0);
  bool getFile(const QUrl &url);
signals:
  void done();
private slots:
  void ftpDone(bool error);
private:
  Ftp ftp;
  QFile file;
};
```

类有一个公共函数 `getFile()`，通过 URL 获取文件。`QUrl` 类提供了高级接口来提取 URL 的不同部分，如文件名、路径、协议和端口。

`FtpGet` 有一个私有槽 `ftpDone()` 在文件传输完成后被调用，并在下载完成后发射 `done()` 信号。该类还有两个私有变量：`Ftp` 类型的 `ftp`（封装了与 FTP 服务器的连接）以及用于写入下载文件的 `file` 变量。

```cpp
FtpGet::FtpGet(QObject *parent)
: QObject(parent)
{
 connect(&ftp, SIGNAL(done(bool)), this, SLOT(ftpDone(bool)));
}
```

在构造函数中，我们将 `QFtp::done(bool)` 信号连接到我们的私有槽 `ftpDone()` `QFtp` 在处理完所有请求后发射 `done(bool)`。`bool` 参数表示是否发生了错误。

代码视图：

```cpp
bool FtpGet::getFile(const QUrl &url)
{
  if (!url.isValid()) {
    std::cerr << "Error: Invalid URL" << std::endl;
    return false;
  }
  if (url.scheme() != "ftp") {
    std::cerr << "Error: URL must start with 'ftp:'" << std::endl;
    return false;
  }
  if (url.path().isEmpty()) {
    std::cerr << "Error: URL has no path" << std::endl;
    return false;
  }
  QString localFileName = QFileInfo(url.path()).fileName();
  if (localFileName.isEmpty()) {
    localFileName = "ftpget.out";
  }
  file.setFileName(localFileName);
}
```

```cpp
if (!file.open(IODevice::WriteOnly)) {
    std::cerr << "Error: Cannot write file "
              << qPrintable(file.fileName()) << ": "
              << qPrintable(file.errorString()) << std::endl;
    return false;
}
ftp.connectToHost(url.host(), url.port(21));
ftp.login();
ftp.get(url.path(), &file);
ftp.close();
return true;
}
```

`getFile()` 函数首先检查传入的 URL。如果遇到问题，函数将向 `cerr` 打印错误信息并返回 `false` 以表示下载失败。

我们没有强制用户自己指定本地文件名，而是尝试使用 URL 本身来创建一个合理的名称，并以 `ftpgetout` 作为备选方案。如果无法打开文件，我们将打印错误信息并返回 `false`。

接下来，我们使用对象 `QFtp` 执行了一系列连续的四个 FTP 命令。`url.port(21)` 调用返回 URL 中指定的端口号，如果 URL 本身未指定，则返回 21。由于 `login()` 函数没有提供用户名或密码，因此将尝试匿名登录。`get()` 的第二个参数指定输出 I/O 设备。

FTP 命令被队列并在 Qt 的事件循环中执行。所有命令的完成挂钩在 `QFtp` 的 `done(bool)` 信号上，我们在构造函数中将其将其连接到了 `ftpDone(bool)`。

```cpp
void Ftp::ftpDone(bool error)
{
    if (error) {
        std::cerr << "Error: " << qPrintable(ftp.errorString())
                  << std::endl;
    } else {
        std::cerr << "File downloaded as "
                  << qPrintable(file.fileName()) << std::endl;
    }
    file.close();
    emit done();
}
```

一旦 FTP 命令执行完毕，我们就关闭文件并发射我们的 `done()` 信号。在这里关闭文件而不是在 `getFile()` 函数末尾的 `ftp.close()` 之后关闭，看起来可能很奇怪，但请记住，FTP 命令是异步执行的，在 `getFile()` 函数返回后可能仍在进行中。只有当 `QFtp` 对象的 `done()` 信号发射时，我们才知道下载已完成并安全地关闭文件。

`QFtp` 提供了多个 FTP 命令，包括 `connectToHost()`、`login()`、`close()`、`list()`、`cd()`、`get()`、`put()`、`remove()`、`mkdir()`、`rmdir()` 和 `rename()`。所有这些函数都会调度 FTP 命令并返回一个标识命令的 ID 数字。还可以控制传输模式（默认为被动模式）和传输类型（默认为二进制）。

可以使用 `rawCommand()` 执行任意 FTP 命令。例如，这里是执行 `SITE CHMOD` 命令的方法：

```cpp
ftp.rawCommand("SITE CHMOD 755 fortune");
```

`QFtp` 在开始执行命令时发射 `commandStarted(int)` 信号，在命令完成时发射 `commandFinished(int, bool)` 信号。`int` 参数是标识命令的 ID 数字。如果我们对单个命令的命运感兴趣，我们可以在调度命令时存储这些 ID。跟踪 ID 允许我们向用户提供详细的反馈。例如：

```cpp
bool FtpGet::getFile(const QUrl &url)
..
  connectId = ftp.connectToHost(url.host(), url.port(21));
  loginId = ftp.login();
  getId = ftp.get(url.path(), &file);
  closeId = ftp.close();
  return true;
```

```cpp
void FtpGet::ftpCommandStarted(int id)
{
  if (id == connectId) {
    std::cerr << "Connecting..." << std::endl;
  } else if (id == loginId) {
    std::cerr << "Logging..." << std::endl;
    ...
  }
}
```

另一种提供反馈的方法是连接到 `QFtp` 的 `stateChanged()`，每当连接进入新状态（`QFtp::Connecting`、`QFtp::Connected`、`QFtp::LoggedIn` 等）时，该信号就会被发射。

在应用程序中，我们只关心整个命令序列的命运，而不是特定的命令。在这种情况下，我们可以简单地连接到 `done(bool)` 信号，每当命令队列为空时，该信号就会被发射。

当发生错误时，`QFtp` 会清空命令队列。这意味着如果连接或登录失败，队列中后续的命令将永远不会执行。如果在错误发生后使用同一个 `QFtp` 对象调度了新命令，这些命令将被放入队列并执行。

在应用程序的 `.pro` 文件中，我们需要以下行来链接 `QtNetwork` 库：

```pro
QT += network
```

我们现在将查看一个更高级的示例。爬虫命令行程序下载 FTP 目录中的所有文件，递归地下载该目录的所有子目录。网络逻辑位于 `Spider` 类中：

```cpp
class Spider : public QObject
{
    Q_OBJECT
public:
    Spider(QObject *parent = 0);
    bool getDirectory(const QUrl &url);
signals:
    void done();
private slots:
    void ftpDone(bool error);
    void ftpListInfo(const QUrlInfo &urlInfo);
private:
    void processNextDirectory();
    QFtp ftp;
    QList<QFile *> openedFiles;
    QString currentDir;
    QString currentLocalDir;
    QString pendingDirs;
};
```

`getDirectory()` 函数通过使用 URL 建立 FTP 连接。`processNextDirectory()` 函数从 `pendingDirs` 列表中取出第一个目录并在系统中创建相应的目录。它告诉 `QFtp` 对象切换目录并列出其文件。对于 `list()` 处理的每一个文件，它发射 `list()` 信号导致 `ftpListInfo()` 槽被调用。

如果没有更多需要处理的目录，该函数发射 `done()` 信号表示下载已完成。

```cpp
void Spider::ftpListInfo(const QUrlInfo &urlInfo)
{
  if (urlInfo.isFile()) {
    if (urlInfo.isReadable()) {
      QFile *file = new QFile(currentLocalDir + urlInfo.name());
      if (!file->open(IODevice::WriteOnly)) {
        std::cerr << "Warning: Cannot write file "
                  << QDir::toNativeSeparators(file->fileName())
                  << ":" << qPrintable(file->errorString())
                  << std::endl;
        return;
      }
      ftp.get(urlInfo.name(), file);
      openedFiles.append(file);
    }
  } else if (urlInfo.isDir() && !urlInfo.isSymLink()) {
    pendingDirs.append(currentDir + "/" + urlInfo.name());
  }
}
```

`ftpInfo()` 槽的 `urlInfo` 参数提供了远程文件的详细信息。如果文件是普通文件（不是目录）且可读，我们调用 `get()` 下载它。用于下载的 `QFile` 对象使用 `new` 分配并存储在 `openedFiles` 列表中。

如果 `QUrlInfo` 持有非符号链接的远程目录详情，我们将该目录添加到 `pendingDirs`。我们跳过符号链接，因为它们很容易导致无限递归。

```cpp
void Spider::ftpDone(bool error) {
    if (error) {
        std::cerr << "Error: " << qPrintable(ftp.errorString())
        << std::endl;
    } else {
        std::cout << "Downloaded " << qPrintable(currentDir) << " to "
        << QDir::toNativeSeparators(QDir(currentLocalDir).canonicalPath());
    }
    qDeleteAll(openedFiles);
    openedFiles.clear();
    processNextDirectory();
}
```

`ftpDone()` 槽在所有 FTP 命令执行完毕或如果一个
发生了错误。我们会删除 `QFile` 对象以防止内存泄漏并关闭每个文件。最后，如果还有任何目录，整个过程将针对列表中的下一个目录重新开始；否则，下载停止并发出 `done()`。

如果没有错误，FTP 命令和信号的序列如下：

```
connectToHost(host, port)
login()
```

```
cd(directory_1)
list()
  emit listInfo(file_1_1)
  get(file_1_1)
  emit listInfo(file_1_2)
  get(file_1_2)
  ..
```

```
emit done()
...
```

```
cd(directory_N)
list()
  emit listInfo(file_N_1)
  get(file_N_1)
  emit listInfo(file_N_2)
  get(file_N_2)
  ..
```

```
emit done()
```
