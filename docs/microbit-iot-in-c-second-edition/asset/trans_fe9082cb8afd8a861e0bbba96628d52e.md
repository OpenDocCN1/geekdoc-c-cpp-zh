
注意，现在我们指定了目标，即轮询尝试之间的毫秒级间隔，以及超时时间（即函数放弃之前的重试次数）。请注意，如果发生失败且重试循环超时，函数返回 0；否则返回剩余的重试次数。

使用此实用函数可以这样写 ATWiFi：

```c
int ATWiFi() {
    uBit.serial.send("AT\n", SYNC_SPINWAIT);
    return waitForWiFi("OK",150,10);
}
```

这种写法更短且更容易理解。

假设你已经成功让 AT 命令工作，现在是时候处理其他 AT 命令了。第一个实用的命令是查找固件的版本号。这与 AT 函数基本相同，但命令是 `ATGMR`，并且我们会收到数据——因此等待时间更长：

```c
int getVersionWiFi() {
    uBit.serial.send("ATGMR\n", SYNC_SPINWAIT);
    return waitForWiFi("OK",200,10);
}
```

它将返回使用的设备信息：

AT+GMR
AT version:0.60.0.0(Jan 29 2016 15:10:17)
SDK version:1.5.2(7eee54f)
Ai-Thinker Technology Co. Ltd.
May 5 2016 17:30:30
OK

手册上说它应该返回 AT、SDK 和编译时间，所以通过这个第三方设备我们获得了一些额外信息。

另一个实用的函数是启动重置。设备经常会卡死，重置是你唯一尝试的方法。这是软件重置；另一个选项是使用 GPIO 线连接到复位引脚 6。通过控制这条线，你可以强制设备重置。软重置命令是 `AT+RST`，理论上你只会得到 OK，但实践中，设备会发送几百字节的配置数据：

```c
int resetWiFi() {
    uBit.serial.send("AT+RST\r\n", SYNC_SPINWAIT);
    return waitForWiFi("OK", 1000,10);
}
```

最后一个实用函数是将串口连接参数设置为 115200 波特率、8 位、1 个停止位、无校验、无流控：

```c
int setWiFi() {
  uBit.serial.send("AT+UART CUR=115200,8,1,0\r\n", SYNC_SPINWAIT);
  return waitForWiFi("OK", 200, 10);
}
```

如果你将波特率更改为当前设置之外的其他值，无疑会丢失与设备的通信，直到你重新配置 micro:bit 的串口连接。

# 配置 WiFi

我们首先需要配置的是工作模式。ESP8622 可以作为访问点（AP）运行，即它可以允许其他设备连接到它。但在大多数情况下，你希望它以客户端模式工作，连接到现有的 WiFi。

# 模式

设置工作模式的函数是：

```c
int modeWiFi(int mode) {
  ManagedString cmd="AT+CWMODE CUR="+String(mode)+"\r\n";
  uBit.serial.send(cmd, SYNC_SPINWAIT);
  return waitForWiFi("OK", 200, 10);
}
```

现在注意，我们是在单独的步骤中构建发送给设备的命令。如果你尝试在函数调用中动态进行此操作，串口数据的传输速率会变化，设备可能会超时。在实践中，先构建所有要发送给设备的命令，然后再发送它们。

在这种情况下，命令是：

```
AT+CWMODE_n
```

其中 n 1 代表客户端，2 代表访问点，3 代表两者都是。如果你想让更改永久生效，请将 `CUR` 改为 `DEF`，设置将存储在 Flash 中。旧设备不支持 `CWMODE_CUR`。只需将其更改为 `CWMODE` 即可（已弃用）。

设置 WiFi 时可以调用：
modeWiFi(1);

并看到返回的 OK。

# 扫描

扫描函数是每个人都想尝试的，但在实践中它并不好用。你为什么需要 WiFi 网络列表？这个函数确实有一些用途，但并没有你想象的那么多。在大多数情况下，你只想连接到已知的 WiFi 网络，这就是我们在下一节中做的。

扫描命令很简单——只需发送 `AT+CWLAP`，设备就会向你发送一个完整的 WiFi 网络列表。问题是扫描耗时很长且经常挂起。这是我们确实需要指定较长时间超时的情况之一：

```c
int scanWiFi() {
  uBit.serial("AT+CWLAP\r\n", SYNC_SPINWAIT);
  return waitForWiFi("OK", 200, 20);
}
```

有时循环带有完整的列表完成，有时则不会。这取决于可用的 WiFi 网络以及它们如何响应请求。

# 连接 WiFi

我们最后也是最实用的函数是将设备连接到已知的 WiFi 网络。你只需要提供 SSID 和密码。该命令还有版本允许你更精确地指定连接，但这种通用形式是最用的。

连接到网络需要一段时间，并且有大量数据。如果你使用的是旧设备，可能需要将 `CUR` 改为 `DEF`。它存储在 Flash 中。软重置命令是 `AT+RST`，理论上你只会得到 OK，但实践中，设备会发送几百字节的配置数据：

手册上说它应该返回 AT、SDK 和编译时间，所以通过这个第三方设备我们获得了一些额外信息。

另一个实用的函数是启动重置。设备经常会卡死，重置是你唯一尝试的方法。这是软件重置；另一个选项是使用 GPIO 线连接到复位引脚 6。通过控制这条线，你可以强制设备重置。

它将返回使用的设备信息：

AT+GMR
AT version:0.60.0.0(Jan 29 2016 15:10:17)
SDK version:1.5.2(7eee54f)
Ai-Thinker Technology Co. Ltd.
May 5 2016 17:30:30
OK

最后一个实用函数是将串口连接参数设置为 115200 波特率、8 位、1 个停止位、无校验、无流控：

```c
int setWiFi() {
  uBit.serial.send("AT+UART CUR=115200,8,1,0\r\n", SYNC_SPINWAIT);
  return waitForWiFi("OK", 200, 10);
}
```

如果你将波特率更改为当前设置之外的其他值，无疑会丢失与设备的通信，直到你重新配置 micro:bit 的串口连接。

现在注意，我们是在单独的步骤中构建发送给设备的命令。如果你尝试在函数调用中动态进行此操作，串口数据的传输速率会变化，设备可能会超时。在实践中，先构建所有要发送给设备的命令，然后发送它们。

一旦连接并收到“WIFI GOT IP”消息，你可以询问：

```c
int resetWiFi() {
    uBit.serial.send("AT+RST\r\n", SYNC_SPINWAIT);
    return waitForWiFi("OK", 1000,10);
}
```

几秒后你应该看到：

```
AT+CWAP="myPassword"
WIFI CONNECTED
WIFI GOT IP
```

设置 WiFi 时可以调用：
modeWiFi(1);

并看到返回的 OK。

如果请求网页，很有可能会：

```c
int getVersionWiFi() {
    uBit.serial.send("ATGMR\n", SYNC_SPINWAIT);
    return waitForWiFi("OK",200,10);
}
```

获取 IP 地址使用：

```
AT+CIPS?
```

在这种情况下，命令是：

```
AT+CWMODE_n
```

其中 n 1 代表客户端，2 代表访问点，3 代表两者都是。如果你想让更改永久生效，请将 `CUR` 改为 `DEF`，设置将存储在 Flash 中。旧设备不支持 `CWMODE_CUR`。只需将其更改为 `CWMODE` 即可（已弃用）。

注意 HTTP 请求总是以一个空行结束。要发送此内容，使用 `CIPEND` 命令，它指定了将随其后的字符数量：

[content] 
注意 HTTP 请求总是以一个空行结束。
要发送此内容，使用 `CIPEND` 命令，它指定了将随其后的字符数量：

```c
cmd = "AT+CIPSEND=" + ManagedString(http.length()) + "\r\n"
uBit.serial.send(cmd, SYNC_SPINWAIT);
```
