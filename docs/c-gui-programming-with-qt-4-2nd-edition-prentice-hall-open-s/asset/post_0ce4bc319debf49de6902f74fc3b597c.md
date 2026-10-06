
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

Another solution would be to use one QFtp object per file. This would enable us to download the files in the parallel, through separate FTP connections.

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

The main() function completes the program. If the user does not specify a URL on the command line, we give an error message and terminate the program-gram.

In both FTP examples, the data retrieved using get() was written to a QFile. This need not be the case. If we wanted the data in memory, we could use a QBuffer, the QIODevice subclass that wraps a QByteArray. For example:

```cpp
QBuffer *buffer = new QBuffer;
buffer->open(QIODevice::WriteOnly);
ftp.get(urlInfo.name(), buffer);
```

We could also omit the I/O device argument to get() or pass a null pointer. The QFtp class emits a readyRead() signal every time new data is available, the data can be read using read() or readAll().

## Writing HTTP Clients

The Http class implements the client side of the HTTP protocol in Qt. It provides various functions to perform the most common HTTP operations, including get() and post(), and provides a means of sending arbitrary HTTP requests. If you read the previous section about QHttp, you will find that there are many similarities between QHttp and Http.

The Http class works asynchronously. When we call a function as get() or post(), the function returns immediately, and the data transfer occurs later, when control returns to Qt's event loop. This ensures that the application's user interface remains responsive while HTTP requests are being processed.

We will review a console application example called httpget that shows how to download a file using the HTTP protocol. It is very similar to the ftpget example from the previous section, in both function and implementation, so we will not show the header file.

```cpp
HttpGet::HttpGet(QObject *parent)
{
    QObject(parent)
    connect(&http, SIGNAL(done(bool)), this, SLOT(httpDone(bool)));
}
```

In the constructor, we connect the QHttp object's done(bool) signal to the private httpDone(bool) slot.

Code View:

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

The getFile() function performs the same kind of error checks as the FtpGetter::getFile() shown earlier on web sites, and uses the same approach to giving the file a local name. When retrieving from web sites, no login is necessary, so we simply set the host and port (using the default HTTP port 80 if none is specified in the URL) and download the data into the file, since the second argument to Http::get() specifies the output I/O device.

The HTTP requests are queued and executed asynchronously in Qt's event loop. The completion of the requests is indicated by Http's done(bool) signal, which we connected to httpDone(bool) in the constructor.

```cpp
void HttpGet::httpDone(bool error)
{
    if (error) {
        // ... error handling
    } else {
        // ... success handling
    }
}
```

The main() function completes the program. If the user does not specify a URL on the command line, we give an error message and terminate the program.

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

In both FTP examples, the data retrieved using get() was written to a QFile. This need not be the case. If we wanted the data in memory, we could use a QBuffer, the QIODevice subclass that wraps a QByteArray. For example:

```cpp
QBuffer *buffer = new QBuffer;
buffer->open(QIODevice::WriteOnly);
ftp.get(urlInfo.name(), buffer);
```

We could also omit the I/O device argument to get() or pass a null pointer. The QFtp class emits a readyRead() signal every time new data is available, the data can be read using read() or readAll().

## Writing HTTP Clients

The Http class implements the client side of the HTTP protocol in Qt. It provides various functions to perform the most common HTTP operations, including get() and post(), and provides a means of sending arbitrary HTTP requests. If you read the previous section about QHttp, you will find that there are many similarities between QHttp and Http.

The Http class works asynchronously. When we call a function as get() or post(), the function returns immediately, and the data transfer occurs later, when control returns to Qt's event loop. This ensures that the application's user interface remains responsive while HTTP requests are being processed.

We will review a console application example called httpget that shows how to download a file using the HTTP protocol. It is very similar to the ftpget example from the previous section, in both function and implementation, so we will not show the header file.

```cpp
HttpGet::HttpGet(QObject *parent)
{
    QObject(parent)
    connect(&http, SIGNAL(done(bool)), this, SLOT(httpDone(bool)));
}
```

In the constructor, we connect the QHttp object's done(bool) signal to the private httpDone(bool) slot.

Code View:

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

The getFile() function performs the same kind of error checks as the FtpGetter::getFile() shown earlier on web sites, and uses the same approach to giving the file a local name. When retrieving from web sites, no login is necessary, so we simply set the host and port (using the default HTTP port 80 if none is specified in the URL) and download the data into the file, since the second argument to Http::get() specifies the output I/O device.

The HTTP requests are queued and executed asynchronously in Qt's event loop. The completion of the requests is indicated by Http's done(bool) signal, which we connected to httpDone(bool) in the constructor.

```cpp
void HttpGet::httpDone(bool error)
{
    if (error) {
        // ... error handling
    } else {
        // ... success handling
    }
}
```

The main() function completes the program. If the user does not specify a URL on the command line, we give an error message and terminate the program.

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

## Writing TCP Client-Server Applications

The TcpSocket TcpServer classes are used to implement TCP clients and servers. TCP is a transport protocol that forms the basis of most application-level protocols, including FTP and HTTP, and that can also be used for custom protocols.

TCP is a stream-oriented protocol. For applications, the data appears to be a long stream, rather like a large flat file. The high-level protocols built on top of TCP are typically line-oriented or block-oriented:

- Line-oriented protocols transfer data as lines of text, each terminated by a newline.
- Block-oriented protocols transfer data as binary data blocks. Each block consists of a size field followed by that much data.

TcpSocket is indirectly derived from QIODevice (through QAbstractSocket), so it can be read from and written using a QDataStream or a QTextStream. One notable difference when reading data from a network compared with reading from a file is that we must make sure we have received enough data from the peer before we use the >> operator. Failing to do so may result in undefined behavior.

In this section, we will review the code of a client and a server that use a custom block-oriented protocol. The client, shown in Figure 15.1, is called Trip Planner and allows users to plan their next trip train. The server is called Trip Server and provides the trip information to the client. We will start by writing the Trip Planner client.
