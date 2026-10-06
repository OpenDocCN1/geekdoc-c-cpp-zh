
Qt examples/network/threadedfortuneserver directory illustrates how to do this.

## Sending and Receiving UDP Datagrams

The QUdpSocket class can be used to send and receive UDP datagrams. UDP is an unreliable, datagram-oriented protocol. Some application-level protocols use UDP because it is more lightweight than TCP. With UDP, data is sent as packets (datagrams) from one to another. There is no concept of connection, and if a UDP packet doesn't get delivered successfully, no error is reported to the sender.

We will see how to use UDP from a Qt application through the Weather Balloon and Weather Station application. The Weather Balloon application mimics a weather balloon that sends a UDP datagram (presumably using a wireless connection) containing the current atmospheric conditions every two seconds. The Weather Station application (shown in Figure 15.3), receives these datagrams and displays them on-screen. We will start by reviewing the code for the Weather Balloon.

# Figure 15.3. The Weather Station application

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

The WeatherBalloon class is derived from QPushButton. It uses its QUdpSocket private variable: communicating with the Weather Station.

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

In the constructor, we start a QTimer to invoke sendDatagram() every 2 seconds.

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

In sendDatagram(), we generate and send a datagram containing the current date, time, temperature, humidity, and altitude:

| DateTime | Date and time of measurement |
| :--- | :--- |
| double | Temperature (in °C) |
| double | Humidity (in %) |
| double | Altitude (in meters) |

The datagram is sent using QUdpSocket::writeDatagram(). The second and third arguments to writeDatagram() are the IP address and the port number of the peer (Weather Station). For this example, we assume that the Weather Station is running on the same machine as the Weather Balloon, so we use an IP address of 127.0.0.1 (QHostAddress::LocalHost), a special address that designates the local host.

QUcpSocket::connectTo(), QUdpSocket::writeDatagram() does not accept name as only host addresses. If we wanted to resolve a name to an IP address host, we have two choices. If we are prepared to block the lookup takes place, we can use the static QHostInfo::fromName() function. Otherwise, we can use QHostInfo::lookupHost() function, which returns immediately and calls the slot it is passed with a QHostInfo object containing the corresponding addresses when the lookup is complete.

```cpp
int main(int argc, char *argv[])
{
    QApplication app(argc, argv);
    WeatherBalloon balloon;
    balloon.show();
    return app.exec();
}
```

The main() function simply creates a WeatherBalloon object, which serves both as a UDP peer and as a QPushButton on-screen. By clicking the QPushButton, the user can quit the application.

Now let's review the source code for the Weather Station client.

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

The WeatherStation class is derived from QDialog. It listens to a particular UDP port, parses any incoming datagrams (from the Weather Balloon), and displays in five read-only QLineEdits. The only private variable of interest is udpSocket of type QUdpSocket, which we will use to receive datagrams.

## WeatherStation::WeatherStation(QWidget *parent)
: QDialog(parent)

```cpp
{
    udpSocket.bind(5824);

    connect(&udpSocket, SIGNAL(readyRead()),
           this, SLOT(processPendingDatagrams()));
           ....
}
```

In the constructor, we start by binding the QUdpSocket to the port that the weather balloon is transmitting to. Since we have not specified a host address, the socket will accept datagrams sent to any IP address that belongs to the machine the Weather Station is running on. Then, we connect the socket's readyRead() signal to the private processPendingDatagrams() which extracts and displays the data.

## void WeatherStation::processPendingDatagrams()

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

processPendingDatagrams() slot is called when a datagram has arrived. The pendingDatagramSize() function returns the size of the datagram. The readData() call copies the contents of the XML into the buffer and advances to the next datagram.

QXmlStreamReader is the fastest and easiest to use and offers an API that is consistent with the rest of Qt. It is ideal for writing one-pass parsers. DOM's main benefit is that lets us navigate a tree representation of the XML document in any order, allowing us to implement multi-pass parsing algorithms.

```cpp
int main(int argc, char *argv[])
{
    QApplication app(argc, argv);
    WeatherStation station;
    station.show();
    return app.exec();
}
```

Finally, in main(), we create and show the WeatherStation.

We have now finished our sender and receiver. The Weather Balloon sending and the Weather Station receiving them.
