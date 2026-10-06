
# Using Qt's Classes in Secondary Threads

A function is said to be thread-safe when it can be safely called from different threads simultaneously. If two thread-safe functions are called concurrently from different threads on the same shared data, the result is always defined. An extension, a class is said to be thread-safe when all of its functions can be called from different threads simultaneously without interfering with each other, even when operating on the same object.

Qt's thread-safe classes include QMutex, QMutexLocker, QReadWriteLock, QReadLocker, QWriterLock, QSemaphore, QThreadStorage<T>, and WaitCondition. In addition, parts of the QThread API and several other functions are thread-safe, notably QObject::connect(), QObject::disconnect(), and QCoreApplication::postEvent(), and QCoreApplication::removePostedEvents().

Most of Qt's non-GUI classes have a less stringent requirement: They are reentrant. A class is reentrant if different instances of the class can be used simultaneously in different threads. However, accessing the same reentrant object in multiple threads is not safe, and such accesses should be protected with a mutex. Reentrant classes are marked as such in the Qt reference documentation. Typically, any C++ class that doesn't reference global or otherwise shared data is reentrant.

QObject is reentrant, but there are three constraints to keep in mind:

- Child QObjects must be created in their parent's thread.

In particular, this means that the objects created in a secondary thread must never be created with the QThread object as parent, because that object was created in another thread (either the main thread or a different secondary thread).

- We must delete all QObjects created in a secondary thread before deleting the corresponding QThread object.

This can be done by creating the objects on the stack in QThread::run().

- QObjects must be deleted in the thread that created them.

If we need to delete a QObject that exists in a different thread, we must call the thread-safe QObject::deleteLater() function instead, which posts a "deferred" event.

Non-GUI QObject subclasses such as QTimer, QProcess, and the network classes are reentrant. We can use them in any thread, as long as the thread has an event loop. For secondary threads, the event loop is started by calling QThread::exec() or by convenience functions such as QProcess::waitFinished() or AbstractSocket::WaitForDisconnected().

Because of limitations inherited from the low-level libraries on which Qt GUI support is built, QWidget and its subclasses are not reentrant. One consequence of this is that we cannot directly call functions on a widget from a secondary thread. If we want to change the text of a QLabel from a secondary thread, we can emit a signal connected to QLabel::setText() or call QMetaObject::invokeMethod() from that thread. For example:

```cpp
void MyThread::run()
{
    ... QMetaObject::invokeMethod(label, SLOT(setText(const QString&)), Q_ARG(QString, "Hello"));
    ...
}
```

Many of Qt's non-GUI classes, including QImage, QString, and the container classes, use implicit sharing as an optimization. Although this optimization usually makes a class non-reentrant, in Qt this is not an issue because Qt uses atomic language instructions to implement thread-safe reference counting, making implicitly shared classes reentrant.

QtSql module can also be used in multithreaded applications, but it has its own restrictions, which vary from database to database. For details, see http://doc.qt-project.com/4.3/sql-driver.html. For a complete list of multithreading caveats, see http://doc.qt-project.com/4.3/threads.html.

## 15. Networking

- Writing FTP Clients
- Writing HTTP Clients
- Writing TCP-Server Applications
- Sending and Receiving UDP Datagrams

Qt provides the QFtp and QHttp classes for working with FTP and HTTP protocols. These are easy to use for downloading and uploading files, and for sending requests to web servers and retrieving the results. Qt also provides the lower-level TcpSocket and QUdpSocket classes. TCP is a reliable connection-oriented protocol that operates in terms of data streams transmitted between nodes, and UDP is an unreliable connectionless protocol based on discrete packets sent between nodes. Both can be used to create network client and server applications. For servers, we also need TcpServer class to handle incoming connections. SSL/TLS connections can be established using QSSocket instead of TcpSocket.

### Writing FTP Clients

The QFtp class implements the client side of the FTP protocol in Qt. It offers various functions to perform the most common FTP operations and lets us execute FTP commands. The QFtp class works asynchronously. When we call a function such as get() or put(), it returns immediately and control passes back to Qt's event loop. This ensures that the user interface remains responsive while FTP commands are executed.

We will start with an example that shows how to retrieve a single file using get(). The example is a console application that downloads the remote file specified on the command line. Let's begin with the main() function:

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

We create a QCoreApplication rather than its subclass to avoid linking in the Qt library. The QCoreApplication::arguments() function returns the command-line arguments as a QStringList, with the first item being the name it was invoked, and any Qt-specific arguments removed. The heart of the main() function is the construction of the FtpGet object and the getFile() call. If the call succeeds, we let the event loop run until the download finishes.

All the work is done by FtpGet subclass, which is defined as follows:

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

The class has a public function getFile(), that retrieves the file specified by a URL. The QUrl class provides a high-level interface for extracting the different parts of a URL, such as the file name, path, protocol, and port.

FtpGet has a private slot, ftpDone(), that is called when the file transfer is completed, and a done() signal that it emits when the file has been downloaded. The class also has two private variables: the ftp variable, of QFtp, which encapsulates the connection to an FTP server, and the file variable that is used for writing the downloaded file to disk.

```cpp
FtpGet::FtpGet(QObject *parent)
: QObject(parent)
{
 connect(&ftp, SIGNAL(done(bool)), this, SLOT(ftpDone(bool)));
}
```

In the constructor, we connect the QFtp::done(bool) signal to our ftpDone() private slot. QFtp emits done(bool) when it has finished processing all requests. The bool parameter indicates whether an error occurred or not.

Code View:

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
```
