
行程规划器（Trip Planner）提供了一个出发地字段、一个目的地字段、一个日期字段以及一个出发或到达的大致时间字段。当用户点击搜索按钮时，应用程序会向服务器发送请求，服务器将在 `QTableWidget` 中显示符合用户标准的行程计划列表。该列表显示在行程规划器中。窗口的最底部由一个 `QLabel` 占据，显示最后一次操作的状态和一个 `QProgressBar`。

行程规划器的用户界面是使用 Qt Designer 在一个名为 `triplanner.ui` 的文件中创建的。在这里，我们将关注实现应用程序功能的 `QDialog` 子类的源代码：

```cpp
#include "ui_triplanner.h"

class QQPushButton;

class TripPlanner : public QDialog, private Ui::TripPlanner
{
    Q_OBJECT
public:
    TripPlanner(QWidget parent = 0);

private slots:
    void connectToServer();
    void sendRequest();
    void updateTableWidget();
    void stopSearch();
    void connectionClosedByServer();
    void error();

private:
    void closeConnection();

    QPushButton searchButton;
    QPushButton *stopButton;
    QTcpSocket tcpSocket;
    quint16 nextBlockSize;
};
```

`TripPlanner` 类除了继承自 `QDialog` 外，还继承自 `Ui::TripPlanner`（由 `uic` 从 `triplanner.ui` 生成）。`tcpSocket` 成员变量封装了 TCP 连接。`nextBlockSize` 变量用于解析从服务器接收到的块。

```cpp
TripPlanner::TripPlanner(QWidget *parent)
: QDialog(parent)
{
    setupUi(this);

    searchButton = buttonBox->addButton(tr("&搜索"), QDialogButton::ActionRole);
    stopButton = buttonBox->addButton(tr("&停止"), QDialogButton::ActionRole);
    stopButton->setEnabled(false);
    buttonBox->button(QDialogButton::Close)->setText(tr("&退出"));

    QDateTime dateTime = QDateTime::currentDateTime();
    dateEdit->setDate(dateTime.date());
    timeEdit->setTime(QTime(dateTime.time().hour(), 0));

    progressBar->hide();
    progressBar->setSizePolicy(QSizePolicy::Preferred, QSizePolicy::Ignored);

    tableWidget->verticalHeader()->hide();
    tableWidget->setEditTriggers(QAbstractItemView::NoEditTriggers);

    connect(searchButton, SIGNAL(clicked()), this, SLOT(connectServer()));
    connect(stopButton, SIGNAL(clicked()), this, SLOT(stopSearch()));
    connect(buttonBox, SIGNAL(rejected()), this, SLOT(reject()));

    connect(&tcpSocket, SIGNAL(connected()), this, SLOT(sendRequest()));
    connect(&tcpSocket, SIGNAL(disconnected()), this, SLOT(connectionClosedByServer()));
    connect(&tcpSocket, SIGNAL(readyRead()), this, SLOT(updateTableWidget()));
    connect(&tcpSocket, SIGNAL(error(QAbstractSocket::SocketError)), this, SLOT(error()));
}
```

在构造函数中，我们根据当前日期和时间初始化了日期和时间编辑器。我们还隐藏了进度条，因为我们只想在连接激活时才显示它。在 Qt Designer 中，进度条的最小和最大属性都被设置为 0。这告诉 `QProgressBar` 表现像一个忙碌指示器，而不是标准的基于百分比进度条。

同样在构造函数中，我们将 `QTcpSocket::connected()`、`disconnected()`、`readyRead()` 和 `error(QAbstractSocket::SocketError)` 连接到私有槽。

```cpp
void TripPlanner::connectToServer() {
    tcpSocket.connectToHost("tripserver.zugbahn.de", 6178);

    tableWidget->setRowCount(0);
    searchButton->setEnabled(false);
    stopButton->setEnabled(true);
    statusLabel->setText("正在连接服务器...");
    progressBar->show();

    nextBlockSize = 0;
}
```

`connectToServer()` 槽在用户点击搜索时执行，以启动服务器。`tcpSocket` 就会在 `connected()` 信号触发时，表示连接已建立。`sendRequest()` 槽的任务是生成一个到服务器的请求，包含用户输入的信息。请求是一个二进制块，格式如下：

| | |
|---|---|
| quint16 | 块大小（不包含此字段） |
| quint8 | 请求类型（始终 'S'） |
| QString | 出发地 |
| QString | 目的地 |
| QDate | 旅行日期 |
| QTime | 大致旅行时间 |
| quint8 | 是出发 ('D') 还是到达 ('A') |

我们首先将数据写入一个名为 `block` 的 `QByteArray` 中。我们无法直接将数据写入 `tcpSocket`，因为我们还不知道块的大小，必须在将所有数据放入块之后先发送块的大小。我们最初在块中写入 0 作为块大小，通过在块设备上调用 `seek(0)` 回到开头。大小是通过对块计数减去 `sizeof(quint16)` 计算的。然后我们将块写入 `tcpSocket`。

```cpp
void TripPlanner::sendRequest() {
    QByteArray block;
    QDataStream out(&block, QIODevice::WriteOnly);
    out.setVersion(QDataStream::Qt_4_3);
    out << uint16(0) << uint8('S') << comboBox->currentText()
    << comboBox->currentText() << dateEdit->date()
    << timeEdit->time();

    if (departureRadioButton->isChecked()) {
        out << uint8('D');
    } else {
        out << uint8('A');
    }
    out.device()->seek(0);
    out << uint16(block.size() - sizeof(quint16));
    tcpSocket.write(block);
}
```

```cpp
statusLabel->setText(tr("正在发送请求..."));
```

`sendRequest()` 在 `tcpSocket` 发出 `connected()` 信号时异步执行。如果连接过程中发生 `error(QAbstractSocket::SocketError)`，则连接失败。接下来，我们更新用户界面，特别是进度条。最后，我们将 `nextBlockSize` 变量设为 0。这意味着从服务器接收的块长度。

```cpp
void TripPlanner::updateTableWidget() {
    QDataStream in(&tcpSocket);
    in.setVersion(QDataStream::Qt_4_3);

    while (true) {
        int row = tableWidget->rowCount();

        if (nextBlockSize == 0) {
            if (tcpSocket.availableBytes() < sizeof(quint16))
                break;
            in >> nextBlockSize;
        }

        if (nextBlockSize == 0xFFFF) {
            closeConnection();
            statusLabel->setText(tr("找到 %1 条行程").arg(row));
            break;
        }

        if (tcpSocket.availableBytes() < nextBlockSize)
            break;

        QDate date;
        QTime departureTime;
        quint16 duration;
        quint8 changes;
        QString trainType;

        in >> date >> departureTime >> duration >> changes >> trainType;
        tableWidget->insertRow(row);

        QStringList fields;
        fields << date.toString(Qt::ISODate)
               << departureTime.toString(tr("hh:mm"))
               << tr("%1 hr %2 min").arg(duration / 60).arg(duration % 60)
               << trainType;

        for (int i = 0; i < fields.count(); ++i) {
            tableWidget->setItem(row, i, new QWidgetItem(fields[i]));
        }

        nextBlockSize = 0;
    }
}
```
