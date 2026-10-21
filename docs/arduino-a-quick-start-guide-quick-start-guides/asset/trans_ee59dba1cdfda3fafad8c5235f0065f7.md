

![](img/dcfd13a1bf99c4d3f9996627012a6526_180_0.png)

# 图 8.6：Arduino 的两个以太网盾

硬件只是将 Arduino 变为网络设备的一个方面。我们还需要一些用于网络通信的软件。Arduino IDE 附带了一个方便的 Ethernet 库，其中包含一些与网络相关的类。我们现在将使用它来访问互联网上的一个 DAYTIME 服务。

一个 DAYTIME 服务⁹ 会以 ASCII 字符串的形式返回当前日期和时间。DAYTIME 服务器监听 TCP 或 UDP 端口 13。你可以在互联网上找到许多 DAYTIME 服务；其中一个运行在 time.nist.gov 上。在使用 Arduino 以编程方式使用该服务之前，先看看使用 telnet 命令它是如何工作的：

```
maik> telnet time.nist.gov 13
Trying 192.43.244.18...
Connected to time.nist.gov.
Escape character is '^[A'].
55480 10-10-11 13:25:35 28 0 0 138.5 UTC(NIST) *
Connection closed by foreign host.
```

> 9. http://en.wikipedia.org/wiki/DAYTIME

首先，我们包含 Ethernet 库并为 DAYTIME 服务端口定义一个常量（我们还必须包含 SPI 库，因为 Ethernet 库依赖于它）。然后我们定义三个字节数组：

- mac 包含我们将要为以太网盾使用的 MAC 地址。MAC 地址是一个 48 位的数字，用于唯一标识网络设备。¹¹ 通常，制造商会设置此标识符，但对于以太网盾，我们必须自己设置它；我们使用一个任意数字。

重要提示：MAC 地址必须在你的网络上是唯一的。如果连接多个 Arduino，请确保它们都有不同的 MAC 地址！

- 每当你将 PC 连接到互联网时，它通常会通过动态主机配置协议（DHCP）¹² 获取一个新的 IP 地址。对于大多数 Arduino 应用来说，DHCP 实现相对昂贵，因此你通常会手动分配 IP 地址。在大多数情况下，这将是 192.168.x.y 范围内的本地地址；我们将此地址存储在 my_ip 数组中。

- 要将 time.nist.gov 等域名转换为 IP 地址，你需要访问域名系统（DNS）。Arduino 的标准库不支持 DNS，因此我们必须自己查找 IP 地址。我们将其分配给 time_server。telnet 命令已经为我们将 DAYTIME 服务域名转换为 IP 地址了。或者，你可以使用以下其中一个命令来确定域名的 IP 地址：

```
maik> host time.nist.gov
time.nist.gov has address 192.43.244.18
maik> dig +short time.nist.gov
192.43.244.18
maik> resolveip time.nist.gov
IP address of time.nist.gov is 192.43.244.18
maik> ping -c 1 time.nist.gov
PING time.nist.gov (192.43.244.18): 56 data bytes
64 bytes from 192.43.244.18: icmp_seq=0 ttl=48 time=173.598 ms

--- time.nist.gov ping statistics ---
1 packets transmitted, 1 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 173.598/173.598/173.598/0.000 ms
```

11. http://en.wikipedia.org/wiki/Mac_address
12. http://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol

![](img/dcfd13a1bf99c4d3f9996627012a6526_182_0.png)

在第 11 行，我们创建一个新的 Client 对象。此类是 Ethernet 库的一部分，允许我们创建连接到特定 IP 地址和端口的网络客户端。

现在我们必须初始化以太网盾本身；我们在 setup() 函数的第 14 行执行此操作。我们必须调用 Ethernet.begin()，并传入我们的 MAC 和 IP 地址。然后我们初始化串口，以便我们可以输出一些调试消息。此时，我们已初始化所需的所有组件，因此我们可以最终连接到 DAYTIME 服务器并读取其输出。

请注意，你也可以将网络网关的 IP 地址和子网掩码传递给 Ethernet.begin()。如果 Arduino 不是直接连接到互联网而是通过路由器或电缆调制解调器连接，则需要这样做。在这种情况下，你可以按如下方式传递网关地址：

```
// ...
byte mac[] = { 0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED };
byte my_ip[] = { 192, 168, 2, 120 };
byte time_server[] = { 192, 43, 244, 18 }; // time.nist.gov
// 在下方插入你的电缆或 DSL 路由器的 IP 地址：
byte gateway[] = { 192, 168, 13, 254 };

Client client(time_server, DAYTIME_PORT);

void setup() {
  Ethernet.begin(mac, my_ip, gateway);
  Serial.begin(BAUD_RATE);
}
// ...
```

我们草图的 loop() 函数以一个短暂的延迟开始，以便所有组件能够正确初始化。这是因为以太网盾是一个能够与 Arduino 并行工作的自主设备。在第 22 行，我们尝试连接到 DAYTIME 服务。如果无法建立连接，我们会打印错误消息。否则，我们等待半秒钟以给服务一些准备时间，然后我们逐字符读取并打印其输出。

请注意，客户端的接口与 Serial 类的接口类似。借助 available()，我们可以检查是否还有字节可用，而 read() 返回下一个字节。最后，我们调用 stop() 以断开与服务的连接，然后重新开始。

编译并将程序上传到 Arduino。然后打开串行监视器，你应该会看到类似这样的内容：

```
Connecting...connected.

55480 10-10-11 13:32:23 28 0 0 579.9 UTC(NIST) *
Disconnecting.
Connecting...connected.

55480 10-10-11 13:32:26 28 0 0 34.5 UTC(NIST) *
Disconnecting.
```

我们完成了！我们的 Arduino 直接连接到互联网，而且它甚至做了一些有用的事情：我们把它变成了一个非常精确的时钟。

总的来说，如果使用以太网盾，Arduino 的网络连接与 PC 的网络连接并没有太大区别。在下一节中，你将学习如何使用 Arduino 发送电子邮件。

# 使用 Arduino 进行网络的更多乐趣

可穿戴设备和电子纺织品越来越受欢迎，它们仍然是给同事和朋友留下深刻印象的好方法。各种类型的互动 T 恤在每个品种齐全的极客商店中都有售。其中一些显示当前的 WiFi 强度，而另一些则带有全功能的均衡器，可以分析环境噪音。

使用 Arduino Lilypad、* 一个蓝牙 dongle 和一部 Android 手机，你可以制作一件显示收件箱中未读邮件数量的 T 恤。†

你不仅可以在 T 恤上显示未读邮件的数量，还可以使用桌上的指针设备显示你的当前情绪——至少只要你在用 Arduino 监控的 IRC 频道中宣布它。‡

虽然不是用 Arduino 构建的，Luminet 项目§ 非常令人印象深刻。它是一个由互联智能 LED 像素组成的网络，Luminet 团队用它制作了一件非常酷的互动夹克。

- *. http://arduino.cc/en/Main/ArduinoBoardLilyPad
- †. http://blog.makezine.com/archive/2010/03/email-counting_t-shirt.html
- ‡. http://blog.makezine.com/archive/2010/01/arduino_powered_mood_meter.html
- §. http://luminet.cc

# 有用的网络库

Arduino IDE 附带的 Ethernet 库相当有限也不太方便。例如，它不支持 DNS 或 DHCP。因此，对于高级项目，你应该看看 Arduino Ethernet 库。

如果你想将 Arduino 变成网络服务器，你应该看看 Webduino 库。它有一些很棒的功能，而且相当成熟。

但要警告：所有这些库都会消耗大量的内存，因此留给应用程序代码的内存就不多了。此外，它们相当脆弱，因为它们通常依赖于官方 Ethernet 库的内部结构，而这些内部结构会不时发生变化。因此，它们可能无法与最新的 Arduino IDE 一起使用。

# 8.6 从命令行发送电子邮件

现在我们知道如何访问网络服务，我们将继续构建一个更高级的项目：自动防盗报警器。如果有人在我们的客厅里移动，我们希望收到一封电子邮件，因此我们必须学习如何从 Arduino 发送电子邮件。

尽管电子邮件是一项重要的服务，但只有少数人知道它在幕后是如何实际工作的。要从 Arduino 发送电子邮件，我们可以选择简单的方法并使用 PC 作为电子邮件中继，就像我们在第 8.4 节《使用 Processing 发送推文消息》中在第 175 页所做的那样来发送推文消息。作为真正的黑客，我们将遵循更复杂的方法并实现简单邮件传输协议（SMTP）的一个子集。

SMTP 是一个典型的互联网协议。它仅使用文本，并且主要是基于行的；也就是说，你逐行交换信息。一封典型的电子邮件只包含几个属性：发件人、收件人、主题和正文。要传输一封电子邮件，你必须向 SMTP 服务器发送请求。该请求必须遵守 SMTP 规范。

