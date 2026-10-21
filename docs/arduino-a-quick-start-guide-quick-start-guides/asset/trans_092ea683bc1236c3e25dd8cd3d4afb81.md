

![](img/dcfd13a1bf99c4d3f9996627012a6526_192_0.png)

![](img/dcfd13a1bf99c4d3f9996627012a6526_192_1.png)

图8.7：被动红外传感器的顶部和底部

几乎每一个物体都会发出红外线，而PIR传感器（图8.7中的那个）测量的正是这部分光线。如果你已经能够接收传感器视野中物体发出的红外辐射，那么检测运动就相对容易了。例如，如果传感器接收到墙壁发出的红外光，而突然有一个人或动物在墙壁前移动，红外光信号就会发生变化。

现成的传感器隐藏了这些细节，因此你可以使用一个数字引脚来检查是否有人在传感器视野中移动。Parallax PIR传感器¹⁶就是这类设备的一个很好的例子，我们将以它为基础来制作防盗报警器。

PIR传感器有三个引脚：电源、接地和信号。将电源连接到Arduino的5V供电，接地连接到Arduino的GND引脚之一，信号连接到数字引脚2（参见下一页的图8.8电路图）。传感器还有一个跳线，可以用来改变其行为。对于我们的项目，它必须处于H位置；也就是说，跳线必须覆盖H旁边的引脚（Lady Ada有一篇关于PIR传感器的优秀教程）。¹⁷

然后在Arduino IDE中输入以下代码：

16. http://www.parallax.com/Store/Sensors/ObjectDetection/tabid/176/ProductID/83/List/0/Default.aspx
17. http://www.ladyada.net/learn/sensors/pir.html

![](img/dcfd13a1bf99c4d3f9996627012a6526_193_0.png)

## 图8.8：一个极简PIR传感器电路

```
Download Ethernet/MotionDetector/MotionDetector.pde
Line 1
const unsigned int PIR_INPUT_PIN = 2;
const unsigned int BAUD_RATE = 9600;

class PassiveInfraredSensor {
  int _input_pin;

public:

  PassiveInfraredSensor(const int input_pin) {
    _input_pin = input_pin;
    pinMode(_input_pin, INPUT);
  }

  const bool motion_detected() const {
    return digitalRead(_input_pin) == HIGH;
  }
};

PassiveInfraredSensor pir(PIR_INPUT_PIN);

void setup() {
  Serial.begin(BAUD_RATE);
}

void loop() {
  if (pir.motion_detected()) {
    Serial.println("Motion detected");
  } else {
    Serial.println("No motion detected");
  }
  delay(200);
}
```

```
No motion detected
No motion detected
No motion detected
No motion detected
No motion detected
No motion detected
No motion detected
No motion detected
No motion detected
No motion detected
Motion detected
Motion detected
Motion detected
Motion detected
Motion detected
Motion detected
Motion detected
Motion detected
Motion detected
Motion detected
```

## 图8.9：PIR传感器的典型输出

使用常量PIR_INPUT_PIN，你可以定义连接PIR传感器的数字引脚。在第4行，我们开始定义一个名为PassiveInfraredSensor的类，它封装了与PIR传感器相关的所有内容。

我们定义了一个名为_input_pin的成员变量，用于存储连接传感器的数字引脚编号。然后我们定义一个构造函数，它接受引脚编号作为参数，并将其赋值给我们的成员变量。

我们需要定义的唯一方法是motion_detected()。如果当前检测到运动，它返回true，否则返回false。因此，它只需检查传感器数字引脚的当前状态是HIGH还是LOW。

编译这个草图，上传到你的Arduino上，当你开始在传感器前挥手时，你应该会看到类似于图8.9的输出。

现在我们已经构建了防盗报警器的两个主要组件，剩下要做的事就是把它们结合在一起。我们将在下一节进行这项工作。

![](img/dcfd13a1bf99c4d3f9996627012a6526_195_0.png)

图8.10：一个发送电子邮件的防盗报警器

## 8.9 将一切整合在一起

有了我们的PassiveInfraredSensor和SmtpService类，构建一个发送电子邮件的防盗报警器就是小菜一碟。将PIR传感器连接到以太网扩展板，如图8.10所示，并将以下代码上传到你的Arduino：

```
Download Ethernet/BurglarAlarm/burglar_alarm.h

Line 1 #ifndef __BURGLAR_ALARM_H__
#define __BURGLAR_ALARM_H__

#include "pir_sensor.h"
#include "smtp_service.h"

class BurglarAlarm {
  PassiveInfraredSensor _pir_sensor;
  SmtpService           _smtp_service;

  void send_alarm() {
    Email email(
      "arduino@example.com",
      "info@example.net",
      "Intruder Alert!",
      "Someone's moving in your living room!"
    );
    _smtp_service.send_email(email);
  }
}
```

```
public:

BurglarAlarm(
    const PassiveInfraredSensor& pir_sensor,
    const SmtpService&           smtp_service) :
        _pir_sensor(pir_sensor),
        _smtp_service(smtp_service)
{
}

void check() {
    Serial.println("Checking");
    if (_pir_sensor.motion_detected()) {
        Serial.println("Intruder detected!");
        send_alarm();
    }
};

#endif
```

这定义了一个名为BurglarAlarm的类，它聚合了我们迄今为止编写的所有代码。它封装了一个SmtpService实例和一个PassiveInfraredSensor对象。其最复杂的方法是send_alarm()，它发送一封预定义的电子邮件。

BurglarAlarm类的其余部分非常简单。从第23行开始，我们定义了初始化所有私有成员的构造函数。check()方法检查PIR传感器是否检测到移动。如果检测到，我们就发送一封电子邮件。

让我们使用BurglarAlarm类：

Download Ethernet/BurglarAlarm/BurglarAlarm.pde

```
#include <SPI.h>
#include <Ethernet.h>
#include "burglar_alarm.h"

const unsigned int PIR_INPUT_PIN = 2;
const unsigned int SMTP_PORT = 25;
const unsigned int BAUD_RATE = 9600;

byte mac[]      = { 0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED };
byte my_ip[]    = { 192, 168, 2, 120 };

// Insert IP of your SMTP server below!
byte smtp_server[] = { 0, 0, 0, 0 };

PassiveInfraredSensor pir_sensor(PIR_INPUT_PIN);
SmtpService           smtp_service(smtp_server, SMTP_PORT);
```

![](img/dcfd13a1bf99c4d3f9996627012a6526_197_0.png)

## 图8.11：防盗报警器的输出

```
BurglarAlarm    burglar_alarm(pir_sensor, smtp_service);
```

```
void setup() {
  Ethernet.begin(mac, my_ip);
  Serial.begin(BAUD_RATE);
  delay(20 * 1000);
}
```

```
void loop() {
  burglar_alarm.check();
  delay(3000);
}
```

首先我们定义所需的所有库，并为PIR传感器引脚和MAC地址定义常量。然后我们定义SmtpService和PassiveInfraredSensor对象，并使用它们来定义一个BurglarAlarm实例。

在setup()方法中，我们定义串口和以太网扩展板。我还添加了二十秒的延迟，这让你有足够的时间在报警器开始工作前离开房间。

loop()函数也很简单。它将所有工作委托给BurglarAlarm的check()方法。在上一页的图8.11中，你可以看到当防盗报警器检测到入侵者时会发生什么。

你有没有注意到在嵌入式设备上进行面向对象编程也可以如此简单？我们显然将电子邮件和PIR传感器的复杂性都隐藏在了两个小类中。为了构建防盗报警器，我们只需编写一些胶水代码。

关于隐私说一句：不要滥用本章的项目在他人不知情的情况下观察他人。这不仅不道德，在许多国家甚至是违法的！

在本章中，你学习了将Arduino连接到互联网的不同方法。其中一些需要额外的PC，另一些则需要以太网扩展板，但它们都为一整类全新的嵌入式计算应用打开了大门。

网络是那些可能对外界产生直接影响的技术之一。在下一章中，你将学习另一种具有类似效果的技术；你将学习如何远程控制设备。

## 8.10 如果不工作怎么办？

网络是复杂而繁琐的东西，尝试本章示例时可能有很多地方出错。最常见的问题如下：

- 你在Processing应用程序中选择了错误的串口。默认情况下，应用程序使用它能找到的第一个串口。可能你的Arduino连接到了另一个端口。在这种情况下，你必须相应地修改语句`arduinoPort = new Serial(this, Serial.list()[0], BAUD_RATE);`中的索引0。
- 你忘记将以太网电缆插入以太网扩展板。
- 你的网络路由器有MAC白名单，只允许某些MAC地址访问网络。确保你在草图中使用的MAC地址被列入白名单。请查看路由器的文档。
- 你在网络上重复使用了相同的MAC地址。

