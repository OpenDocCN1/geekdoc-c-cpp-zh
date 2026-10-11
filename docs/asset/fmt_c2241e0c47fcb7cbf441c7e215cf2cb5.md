
现在让我们来实现服务器。服务器由两个类组成：`TripServer` 和 `ClientSocket`。`TripServer` 类派自 `TcpServer`，该类允许我们接受 TCP 连接。`ClientSocket` 重新实现了 `TcpSocket` 并处理单个连接。在任何时候，内存中都有许多 `ClientSocket` 对象，因为有许多正在服务的客户端。

```cpp
class TripServer : public TcpServer
{
    Q_OBJECT
public:
    TripServer(QObject *parent = 0);
private:
    void incomingConnection(int socketId);
};
```

`TripServer` 类实现了 `TcpServer` 的 `incomingConnection()` 函数。每当客户端尝试连接到它正在监听的服务器时，该函数就会被调用。

```cpp
TripServer::TripServer(QObject *parent)
    : TcpServer(parent)
{}
```

`TripServer` 构造函数非常简单。

```cpp
void TripServer::incomingConnection(int socketId)
{
    ClientSocket *socket = new ClientSocket(this);
    socket->setSocketDescriptor(socketId);
}
```

在 `incomingConnection()` 中，我们创建了一个 `ClientSocket` 对象作为 `TripServer` 的子对象，并将其套接字描述符设置为我们提供的提供的数字。当连接终止时，`ClientSocket` 对象将自动删除。

```cpp
class ClientSocket : public TcpSocket
{
    Q_OBJECT
public:
    ClientSocket(QObject *parent = 0);
private slots:
    void readClient();
private:
    void generateRandomTrip(const QString &from, const QString &to, const QDate &date, const QTime &time);
    uint16 nextBlockSize;
}
```

`ClientSocket` 类派自 `TcpSocket` 并封装了单个客户端的状态。

```cpp
ClientSocket::ClientSocket(QObject *parent)
    : TcpSocket(parent)
{
    connect(this, SIGNAL(readyRead()), this, SLOT(readClient()));
    connect(this, SIGNAL(disconnected()), this, SLOT(deleteLater()));
    nextBlockSize = 0;
}
```

在构造函数中，我们建立了必要的信号与槽连接，并将 `nextBlockSize` 变量设置为 0，表示我们尚不知道由客户端发送的块的大小。

`disconnected()` 信号连接到 `deleteLater()`，这是一个继承自 `QObject` 的函数，当控制权返回 Qt 事件循环时会删除该对象。这确保了当套接字连接关闭时，`ClientSocket` 对象会被删除。

代码视图：

```cpp
void ClientSocket::readClient()
{
QDataStream in(this);
    in.setVersion(Qt_4_3);
    if (nextBlockSize == 0) {
        if (bytesAvailable() < sizeof(quint16)) {
            return;
        }
        in >> nextBlockSize;
    }
    if (bytesAvailable() < nextBlockSize) {
        return;
    }
    quint16 requestType;
    QString from;
    QString to;
    QDate date;
    QTime time;
    quint8 flag;
    if (requestType == 'S') {
        in >> from >> to >> date >> time >> flag;
    }
    // ... 处理行程的逻辑 ...
    // std::rand(from.length()) * 3600 + to.length() * 60 + time.hour();
    int numTrips = std::rand() % 8;
    for (int i = 0; i < numTrips; ++i) {
        // ... 处理 ...
    }
}
```

```cpp
void ClientSocket::generateRandomTrip(const QString &from, const QString &to, const QDate &date, const QTime &time)
{
    QByteArray block;
    QDataStream out(&block, QIODevice::WriteOnly);
    out.setVersion(Qt_4_3);
    quint8 duration = std::rand() % 200;
    out << quint16(block.size()) << date << time;
    write(block);
}
```

`generateRandomTrip()` 函数展示了如何在 TCP 连接上发送数据。这与我们在客户端中所做的非常相似。

```cpp
int main(int argc, char *argv[])
{
QApplication app(argc, argv);
    TripServer server;
    if (!server.listen(QHostAddress::Any, 6178)) {
        std::cerr << "无法绑定到端口" << std::endl;
        return 1;
    }
    QPushButton quitButton(QObject::tr("退出"));
    QObject::connect(&quitButton, SIGNAL(clicked()),
        &app, SLOT(quit()));
    quitButton.show();
    return app.exec();
}
```

在 `main()` 中，我们创建了一个 `TripServer` 对象和一个允许用户停止服务器的 `QPushButton`。我们通过调用 `TcpSocket::listen()` 来启动服务器，该函数接受我们要接受连接的 IP 地址和端口号。特殊地址 0.0.0.0 `QHostAddress::Any` 表示本地主机上的任何接口。

使用 `QPushButton` 表示服务器在开发过程中是方便的。然而，部署的服务器需要在没有 GUI 的情况下运行，例如 Windows 服务或 Unix 守护进程。Trolltech 为此目的提供了一个商业插件，称为 `QtService`。

`Qt examples/network/threadedfortuneserver` 目录演示了如何实现这一点。

## 发送和接收 UDP 数据报

`QUdpSocket` 类用于发送和接收 UDP 数据报。UDP 是一种不可靠的、面向数据报协议。某些应用层协议使用 UDP 是因为它比 TCP 更轻量。在 UDP 中，数据以包（数据报）的形式从一个端发送到另一个端。没有连接的概念，如果 UDP 数据包没有成功送，不会向发送者报告错误。

我们将通过 `WeatherBalloon`（气象球）和 `WeatherStation`（气象站）应用程序查看如何在 Qt 应用程序中使用 UDP。`WeatherBalloon` 应用程序模拟气象球，它每两秒发送一次包含当前大气状况的 UDP 数据报（假设使用无线连接）。`WeatherStation` 应用程序（如图 15.3 所示）接收这些数据报并将它们显示在屏幕上。我们将从回顾 `WeatherBalloon` 的代码开始。

### 图 15.3 气象站应用程序

![](img/5a524abdf0b0d58fa99d30abb4463611_607_0.png)

```cpp
class WeatherBalloon : public QPushButton
{
    Q_OBJECT
public:
    WeatherBalloon(QWidget *parent = 0);
    double temperature() const;
    double humidity() const;
    double altitude() const;
private slots:
    void sendDatagram();
private:
    QUdpSocket udpSocket;
    QTimer timer;
};
```

`WeatherBalloon` 类派自 `QPushButton`。它使用其私有变量 `udpSocket`：与 `WeatherStation` 通通信。

```cpp
WeatherBalloon::WeatherBalloon(QWidget *parent)
: QPushButton(tr("Quit"), parent)
{
    connect(this, SIGNAL(clicked()), this, SLOT(close));
    connect(this, SIGNAL(timeout()), this, SLOT(sendDatagram()));
    timer.start(2 * 1000);
    setWindowTitle(tr("Weather Balloon"));
}
```

在构造函数中，我们启动了一个 `QTimer` 来每 2 秒调用一次 `sendDatagram()`。

```cpp
void WeatherBalloon::sendDatagram()
{
    QByteArray datagram;
    QDataStream out(&datagram, QIODevice::WriteOnly);
    out.setVersion(QDataStream::Qt_4_3);
    out << QDateTime::currentDateTime() << temperature() << humidity() << altitude();
    udpSocket.writeDatagram(datagram, QHostAddress::LocalHost, 5824);
}
```

在 `sendDatagram()` 中，我们生成并发送一个包含当前日期、时间、温度、湿度和高度的数据报：

| DateTime | 测量日期和时间 |
| :--- | :--- |
| double | 温度（单位 °C） |
| double | 湿度（单位 %） |
| double | 高度（单位 米） |

使用 `QUdpSocket::writeDatagram()` 发送数据报。`writeDatagram()` 的第二个和第三个参数是对方（`WeatherStation`）的 IP 地址和端口号。对于此示例，我们假设 `WeatherStation` 运行与 `WeatherBalloon` 相同的机器上，因此我们使用 IP 地址 127.0.0.1 (`QHostAddress::LocalHost`)，这是一个指定本地主机的特殊地址。

`QUdpSocket::connectTo()` 和 `QUdpSocket::writeDatagram()` 不接受名称，只接受主机地址。如果我们想将名称解析为 IP 地址主机，我们有两个选择。如果我们准备好让查找发生阻塞，可以使用静态函数 `QHostInfo::fromName()`。否则，我们可以使用 `QHostInfo::lookupHost()` 函数，它会立即返回，并在完成后调用传递给它的槽，并传入一个包含相应地址的 `QHostInfo` 对象。

```cpp
int main(int argc, char *argv[])
{
    QApplication app(argc, argv);
    WeatherBalloon balloon;
    balloon.show();
    return app.exec();
}
```

`main()` 函数简单地创建一个 `WeatherBalloon` 对象，它既作为 UDP 对端，也作为屏幕上的 `QPushButton`。通过点击 `QPushButton`，用户可以退出应用程序。

现在让我们回顾一下 `WeatherStation` 客户端的源代码。

```cpp
class WeatherStation : public QDialog
{
    Q_OBJECT
public:
    WeatherStation(QWidget parent = 0);
private slots:
    void processPendingDatagrams();
private:
    QUdpSocket udpSocket;
    QLabel dateLabel;
    QLabel timeLabel;
    ...
    QLineEdit altitudeLineEdit;
};
```

`WeatherStation` 类派自 `QDialog`。它监听特定的 UDP 端口，解析任何传入的数据报（来自 `WeatherBalloon`），并显示在五个只读的 `QLineEdit` 中。唯一感兴趣的私有变量是类型为 `QUdpSocket` 的 `udpSocket`，我们将用它接收数据报。

### WeatherStation::WeatherStation(QWidget *parent)

```cpp
: QDialog(parent)
{
    udpSocket.bind(5824);
    connect(&udpSocket, SIGNAL(readyRead()),
           this, SLOT(processPendingDatagrams()));
           ....
}
```

在构造函数中，我们首先将 `QUdpSocket` 绑定到气象球传输的端口。由于我们没有指定主机地址，套接字将接受发送到运行 `WeatherStation` 机器任意 IP 地址的数据报。然后，我们将套接字的 `readyRead()` 信号连接到私有的 `processPendingDatagrams()`，它负责提取并显示数据。

### void WeatherStation::processPendingDatagrams()

```cpp
{
    QByteArray datagram;
    do {
        datagram.resize(udpSocket.pendingDatagramSize());
        udpSocket.readData(datagram.data(), datagram.size());
    } while (udpSocket.hasPendingDatagrams());
    QTime dateTime;
    double temperature;
    double humidity;
    double altitude;
    QDataStream in(&datagram, QIODevice::ReadOnly);
    in.setVersion(QDataStream::Qt_4_3);
    in >> dateTime >> temperature >> humidity >> altitude;
    dateLineEdit->setText(dateTime.date().toString());
    timeLineEdit->setText(dateTime.time().toString());
    temperatureLineEdit->setText(tr("%1 °C")).arg(temperature));
    humidityLineEdit->setText(tr("%1%%")).arg(humidity));
    altitudeLineEdit->setText(tr("%1 m")).arg(altitude));
}
```

当数据报到达时，会调用 `processPendingDatagrams()` 槽。`pendingDatagramSize()` 函数返回数据报的大小。`readData()` 调用将 XML 内容复制到缓冲区并移动到下一个数据报。

`QXmlStreamReader` 是最快且易于使用的，并提供了与 Qt 其他部分一致的 API。它是编写单次解析器的理想选择。DOM 的主要优势是允许我们以任何顺序遍历 XML 文档的树表示，从而我们能够实现多次解析算法。

```cpp
int main(int argc, char *argv[])
{
    QApplication app(argc, argv);
