

```c
options.c_cc[VMIN]  = 0;
options.c_cc[VTIME] = 20;

if (tcsetattr(fd, TCSANOW, &toptions) < 0) {
    perror("init_serialport: Couldn't set term attributes");
    return -1;
}

return fd;
}
```

如果你熟悉 Unix 文件处理，那么这里的一切对你来说都很好理解。如果不熟悉，也没关系，你仍然可以通过这段代码来访问连接到计算机串口的 Arduino。下面介绍如何使用这段代码与我们的模拟读取器草图（analog reader sketch）通信（注意，以下代码运行在你的 PC 上，而不是 Arduino 上）：

```c
#include <stdio.h>
#include <unistd.h>
#include "arduino-serial.h"

#define MAX_LINE 256

int main(int argc, char* argv[]) {
    if (argc == 1) {
        printf("You have to pass the name of a serial port.\n");
        return -1;
    }

    int baudrate = B9600;
    int arduino = serialport_init(argv[1], baudrate);
    if (arduino == -1) {
        printf("Could not open serial port %s.\n", argv[1]);
        return -1;
    }
    sleep(2);

    char line[MAX_LINE];
    while (1) {
        int rc = serialport_write(arduino, "a0\n");
        if (rc == -1) {
            printf("Could not write to serial port.\n");
        } else {
            serialport_read_until(arduino, line, '\n');
            printf("%s", line);
        }
    }
    return 0;
}
```

首先，我们导入所需的所有库，并为将要读取的 Arduino 数据行定义一个最大长度常量。然后，我们定义一个 `main()` 函数。

在确保命令行中传入了串口名称后，我们在第 14 行初始化一个串口。然后休眠两秒，让 Arduino 有时间做好准备。之后，我们开始一个循环，在第 23 行不断向 Arduino 发送字符串 “a0”。我们检查 `serialport_write()` 的结果，如果写入成功，就在第 27 行读取 Arduino 返回的结果。下面来编译这个小程序：

```bash
maik> gcc arduino-serial.c analog_reader.c -o analog_reader
```

确定你的 Arduino 连接到了哪个串口（我的 Arduino 连接在 `/dev/tty.usbmodemfa141`），然后像这样运行程序：

```bash
maik> ./analog_reader /dev/tty.usbmodemfa141
a0: 495
a0: 376
a0: 368
^C
```

一切如期工作，用 C 语言访问串口并没有那么难。要把这段代码嵌入到 C++ 程序中，你应该将其包装在一个名为 `SerialPort` 的类或类似的类中。

## Java

Java 平台标准化了诸多方面，并定义了如何在 Java Communications API 中访问串口。[²](http://java.sun.com/products/javacomm/) 但该 API 只是一个规范，仍然需要实现。RXTX 项目就是一个很好的实现。[³](http://rxtx.qbang.org/)

下载最新的发行版，并按照针对你平台的安装说明进行安装。确保 `RXTXcomm.jar` 位于你的类路径中。然后在你喜欢的 IDE 或文本编辑器中输入以下代码：

下载 `SerialProgramming/java/AnalogReaderTest.java`

```java
import java.io.InputStream;
import java.io.OutputStream;
import gnu.io.CommPortIdentifier;
import gnu.io.SerialPort;

class AnalogReader {
    private InputStream _input;
    private OutputStream _output;

    public AnalogReader(
        final String portName,
        final int baudRate) throws Exception
    {
        final int timeout = 1000;
        final String appName = "analog reader client";
        CommPortIdentifier portId =
            CommPortIdentifier.getPortIdentifier(portName);
        SerialPort port = (SerialPort)portId.open(
            appName,
            timeout
        );
        _input = port.getInputStream();
        _output = port.getOutputStream();
        port.setSerialPortParams(
            baudRate,
            SerialPort.DATABITS_8,
            SerialPort.STOPBITS_1,
            SerialPort.PARITY_NONE
        );
    }

    public void run() throws Exception {
        byte[] buffer = new byte[255];
        Thread.sleep(2000);
        while (true) {
            _output.write("a0\n".getBytes());
            Thread.sleep(100);
            if (_input.available() > 0) {
                _input.read(buffer);
                System.out.print(new String(buffer));
            }
        }
    }
}

public class AnalogReaderTest {
    public static void main(String[] args) throws Exception {
        if (args.length != 1) {
            System.out.println(
                "You have to pass the name of a serial port."
            );
            System.exit(1);
        }
        AnalogReader analogReader = new AnalogReader(args[0], 9600);
        analogReader.run();
    }
}
```

该文件定义了两个类：AnalogReader 和 AnalogReaderTest。AnalogReader 实际上封装了对 Arduino 的访问。它在 `_input` 中存储一个 InputStream 对象以接收数据，并在 `_output` 中存储一个 OutputStream 对象以向 Arduino 发送数据。

构造函数初始化串口连接，并将其输入流和输出流赋给我们的成员变量。要获得串口连接，我们必须先获取一个 `CommPortIdentifier` 对象。从该对象中，我们可以创建一个 `SerialPort` 对象。这个对象让我们能够访问底层流，也允许我们设置端口参数，如波特率。

我们在 `run()` 方法中实现了 Arduino 草图的协议。在那里我们等待两秒，然后开始一个循环。在循环中，我们使用 `OutputStream` 的 `write()` 方法将字符串 “a0” 发送到串口。发送字符串之前，我们调用 `getBytes()` 将其转换为字节数组。为了给 Arduino 一些时间来生成结果，我们再等待 100 毫秒。之后，我们检查是否有可用结果，并通过调用 `InputStream` 的 `read()` 方法来读取它。

AnalogReaderTest 只是一个小型驱动程序类，它实现了 `main()` 方法，创建一个 AnalogReader 对象，并调用它的 `run()` 方法。下面介绍如何编译和使用该程序：

```bash
maik> javac AnalogReaderTest.java
maik> java AnalogReaderTest /dev/tty.usbmodemfa141
Experimental:  JNI_OnLoad called.
Stable Library
================================
Native lib Version = RXTX-2.1-7
Java lib Version  = RXTX-2.1-7
a0: 496
a0: 433
a0: 328
a0: 328
^C
```

在输出一些来自所用库的调试信息之后，AnalogReaderTest 完全按预期工作：它持续打印模拟引脚 0 的值。如果使用正确的库，在 Java 中访问串口就是小菜一碟。

## Ruby

即使是像 Ruby 这样的动态语言，也能让你即时访问计算机的串口，以及连接到串口的 Arduino。但在此之前，你需要安装 serialport gem：

```bash
maik> gem install serialport
```

使用它，你只需 30 行代码就能连接到 Arduino。

下载 `SerialProgramming/ruby/analog_reader.rb`

```ruby
require 'rubygems'
require 'serialport'

if ARGV.size != 1
  puts "You have to pass the name of a serial port."
  exit 1
end

port_name = ARGV[0]
baud_rate = 9600
data_bits = 8
stop_bits = 1
parity    = SerialPort::NONE

arduino = SerialPort.new(
  port_name,
  baud_rate,
  data_bits,
  stop_bits,
  parity
)

sleep 2
while true
  arduino.write "a0"
  line = arduino.gets.chomp
  puts line
end
```

我们在第 15 行创建了一个新的 `SerialPort` 对象，并向它传递所有常用参数。在休眠两秒后，我们启动一个循环，并在 `SerialPort` 对象上调用 `write()`。为了从 Arduino 取回结果，我们调用 `gets()`，然后将结果打印到控制台。下面你可以看到程序的实际运行效果：

```bash
maik> ruby analog_reader.rb /dev/tty.usbserial-A60061a3
a0: 496
a0: 456
a0: 382
^Canalog_reader.rb:21:in `gets': Interrupt
  from analog_reader.rb:21
```

使用 Ruby 访问 Arduino 是一个不错的选择，因为你可以完全专注于自己的应用程序。在其他编程语言中需要处理的那些繁琐的现实世界细节，在这里都被很好地隐藏了起来。

## Python

Python 是另一种动态编程语言，你可以用它快速创建 Arduino 客户端。要进行串口编程，请先下载并安装 pyserial 库。Windows 有一个专门的安装程序，但通常按如下方式安装就足够了：

```bash
maik> python setup.py install
```

```python
import sys
import time
import serial

if len(sys.argv) != 2:
    print "You have to pass the name of a serial port."
    sys.exit(1)

serial_port = sys.argv[1]
arduino = serial.Serial(
    serial_port,
    9600,
    serial.EIGHTBITS,
    serial.PARITY_NONE,
    serial.STOPBITS_ONE
)

time.sleep(2)

while 1:
    arduino.write('a0')
    line = arduino.readline().rstrip()
    print line
```

我们确保命令行中带有串口名称。然后在第 10 行创建一个新的 `Serial` 对象，并向它传递我们希望用于串口通信的所有参数。

休眠两秒后，我们启动一个无限循环。在循环中，我们调用 `write()` 将字符串 `"a0"` 发送到串口。我们使用 `readline()` 方法读取 Arduino 返回的结果，并将结果输出到控制台。下面是一个典型会话的示例：

```bash
maik> python analog_reader.py /dev/tty.usbserial-A60061a3
a0: 497
a0: 458
a0: 383
^C
```

