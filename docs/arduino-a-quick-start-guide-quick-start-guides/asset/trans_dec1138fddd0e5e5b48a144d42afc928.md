
位移位运算符 `<<` 和 `>>` 允许你在处理位之前将它们移动到某个位置。第一个将位向左移动，第二个将位向右移动：

```
int x = 42; // In binary this is 101010
int y = x << 1; // y == 84 == B1010100
int z = x >> 2; // z == 10 == B1010
```

移位操作可能看起来很直观，但在移动有符号值时你必须小心。³ 虽然它们看起来相似，位运算符与布尔运算符并不相同。布尔运算符如 `&&` 和 `||` 不在位级上操作，它们实现的是布尔代数规则。⁴

![](img/dcfd13a1bf99c4d3f9996627012a6526_251_0.png)

图 C.1：位级串行通信

一种协议，并且在图 C.1 中，你可以看到典型的串行通信是什么样子。位的不同状态由不同的电压电平表示。通常，0 位由 0 伏表示，而 5 伏代表 1 位（有些协议分别使用 -12V 和 12V）。

以下参数控制串行通信：

-   一个*起始位*表示数据字的开始，用于同步发送器和接收器。它始终为 0。
-   一个*停止位*告诉我们最后一个数据位何时被发送，并分隔两个连续的数据字。根据特定的协议约定，可能有多个停止位，但这种情况很少发生。
-   信息以二进制*数据位*的形式传输；也就是说，例如，如果你想传输字母 M，你必须先将其转换为数字。有几种字符集编码可用，但在使用 Arduino 时，ASCII 编码最合适。在 ASCII 中，大写 M 被编码为十进制数 77，即二进制中的 01001101。这就是最终被传输的位序列。
-   *校验位*指示数据中 1 的个数是奇数还是偶数。这是一种简单的错误检查算法，现在很少使用，它源于网络连接不如今天可靠的时代。

```
char pin_name[MAX_PIN_NAME + 1];

if (Serial.available()) {
    int i = 0;
    while (Serial.available() && i < MAX_PIN_NAME) {
        const char c = Serial.read();
        if (c != -1 && c != '\n')
            pin_name[i++] = c;
        delay(SERIAL_DELAY);
    }
    pin_name[i] = 0;
    if (strlen(pin_name) > 1 &&
        (pin_name[0] == 'a' || pin_name[0] == 'A'))
    {
        const int pin = atoi(&pin_name[1]);
        if (pin < NUM_PINS) {
            Serial.print(pin_name);
            Serial.print(": ");
            Serial.println(analogRead(pin));
        } else {
            Serial.print("Unknown pin: ");
            Serial.println(pin);
        }
    } else {
        Serial.print("Unknown pin name: ");
        Serial.println(pin_name);
    }
}
```

该程序等待一个模拟引脚（a0, a1, ... a5）的名称，并返回其当前值。因此，我们所有的客户端都必须向 Arduino 发送数据（引脚的名称），并且必须接收结果（在下一页的图 C.2 中，你可以看到它与 IDE 的串口监视器配合工作的效果）。

所有客户端看起来都很相似：它们期望将要连接的串口名称作为命令行参数。它们会不断向 Arduino 发送字符串“a0”，以获取模拟引脚 0 的当前值，然后将结果打印到控制台。它们都使用恒定的 9600 波特率，并且在打开串口后都会等待两秒，因为许多 Arduino 在打开串行连接时会重新启动。要更全面地了解串行通信，请参阅第 251 页的 C.1 节“深入了解串行通信”。

对于某些客户端，你需要安装额外的库。在某些情况下，你必须以机器上的管理员用户身份执行此操作。在接下来的章节中，我不会明确提及这一点。此外，你应该确保

![](img/dcfd13a1bf99c4d3f9996627012a6526_254_0.png)

# 图 C.2：我们的测试草图返回模拟引脚的当前值。

在运行以下部分中的任一示例时，没有打开任何串口监视器窗口。

## C/C++

尽管你用 C++ 为 Arduino 编程，但你不需要用 C++ 或 C 编写与 Arduino 通信的客户端。不过，如果以 Tod E. Kurt 出色的 arduino_serial.c¹ 为基础，你仍然可以做到，而且很容易。

原始程序实现了一个完整的命令行工具，提供了许多有用的选项。就我们的目的而言，这没有必要，所以我将其中的四个主要函数提取到了一个 C 头文件中：

下载 SerialProgramming/c/arduino-serial.h

```
#ifndef __ARDUINO_SERIAL__
#define __ARDUINO_SERIAL__

#include <fcntl.h>
#include <sys/ioctl.h>
#include <termios.h>
```

> 1. http://todbot.com/blog/2006/12/06/arduino-serial-c-code-to-talk-to-arduino/

```
#include <stdint.h>
#include <string.h>

int serialport_init(const char* serialport, int baud);
int serialport_writebyte(int fd, uint8_t b);
int serialport_write(int fd, const char* str);
int serialport_read_until(int fd, char* buf, char until);

#endif
```

它们的含义如下：

-   serialport_init() 打开一个串口连接。它期望被打开的串口名称和要使用的波特率。如果一切正常，它返回一个文件描述符，否则返回 -1。
-   使用 serialport_writebyte()，你可以向连接到计算机串口的 Arduino 发送单个字节。只需将 serialport_init() 返回的文件描述符和要写入的字节传递给它。如果发生错误，它返回 -1。否则返回 0。
-   serialport_write() 向串口写入整个字符串。它期望一个文件描述符和要写入的字符串。如果发生错误，它返回 -1。否则返回 0。
-   使用 serialport_read_until() 从串口读取数据。向它传递一个文件描述符和一个用于填充所读取数据的缓冲区。该方法还期望一个分隔符字符。serial_port_read_until() 读取数据，直到找到该字符，并且它总是返回 0。

为了完整起见，我们来看看这四个函数的实现：

下载：SerialProgramming/c/arduino-serial.c

```
#include "arduino-serial.h"

int serialport_writebyte(int fd, uint8_t b) {
    int n = write(fd, &b, 1);
    return (n != 1) ? -1 : 0;
}

int serialport_write(int fd, const char* str) {
    int len = strlen(str);
    int n = write(fd, str, len);
    return (n != len) ? -1 : 0;
}

int serialport_read_until(int fd, char* buf, char until) {
```

```
char b[1];
int i = 0;
do {
    int n = read(fd, b, 1);
    if (n == -1)
        return -1;
    if (n == 0) {
        usleep(10 * 1000);
        continue;
    }
    buf[i++] = b[0];
} while (b[0] != until);

buf[i] = 0;
return 0;
}

int serialport_init(const char* serialport, int baud) {
    int fd = open(serialport, O_RDWR | O_NOCTTY | O_NDELAY);
    if (fd == -1) {
        perror("init_serialport: Unable to open port");
        return -1;
    }

    struct termios toptions;
    if (tcgetattr(fd, &toptions) < 0) {
        perror("init_serialport: Couldn't get term attributes");
        return -1;
    }

    speed_t brate = baud;
    switch(baud) {
        case 4800:  brate = B4800;  break;
        case 9600:  brate = B9600;  break;
        case 19200: brate = B19200; break;
        case 38400: brate = B38400; break;
        case 57600: brate = B57600; break;
        case 115200: brate = B115200; break;
    }
    cfsetispeed(&toptions, brate);

    toptions.c_cflag &= ~PARENB;
    toptions.c_cflag &= ~CSTOPB;
    toptions.c_cflag &= ~CSIZE;
    toptions.c_cflag |= CS8;
    toptions.c_cflag &= ~CRTSCTS;
    toptions.c_cflag |= CREAD | CLOCAL;
    toptions.c_iflag &= ~(IXON | IXOFF | IXANY);
    toptions.c_lflag &= ~(ICANON | ECHO | ECHOE | ISIG);
    toptions.c_oflag &= ~OPOST;
```

