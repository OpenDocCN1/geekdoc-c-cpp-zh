
使用 Arduino IDE 来了解更多关于用压电扬声器播放音符的内容）。

+   - 改进库的设计，使其更容易支持不同的输出设备。例如，你可以将某种 OutputDevice 对象传递给 Telegraph 构造函数。然后从 OutputDevice 派生一个 LedDevice 和一个 SpeakerDevice。如下所示：

```
class OutputDevice {
    public:
        virtual void output_symbol(const int length);
};

class Led : public OutputDevice {
    public:
        void output_symbol(const int length) {
            // ...
        }
};

class Speaker : public OutputDevice {
    public:
        void output_symbol(const int length) {
            // ...
        }
};
```

然后你可以按如下方式使用这些类：

```
Led led;
Speaker speaker;
OutputDevice* led_device = &led;
OutputDevice* speaker_device = &speaker;

led_device->output_symbol(200);
speaker_device->output_symbol(200);
```

其余部分由你来完成。

+   - 尝试学习摩尔斯电码。让别人在串行终端中输入一些消息，然后尝试识别他或她发送的内容。这对于学习 Arduino 开发并非必需，但非常有趣！

![](img/dcfd13a1bf99c4d3f9996627012a6526_102_0.png)

图 5.1：本章所需的所有部件

## 5.1 你需要什么

- 1. 一个 Parallax PING))) 传感器
- 2. 一个来自 Analog Devices 的 TMP36 温度传感器
- 3. 一块面包板
- 4. 一些导线
- 5. 一块 Arduino 板，如 Uno、Duemilanove 或 Diecimila
- 6. 一根用于将 Arduino 连接到电脑的 USB 线缆
- 7. 安装了 Processing 编程语言¹

¹ http://processing.org

## 5.2 使用超声波传感器测量距离

在许多情况下，自动且连续地测量距离会非常有用。想象一个自主寻找路径的机器人，或者一个自动防盗报警器，每当有人离你的房子或《蒙娜丽莎》太近时，它就会响铃或报警。所有这些都可以用 Arduino 实现。但在你能够制作那个防盗报警器或机器人之前，你需要理解一些关键概念。

可用于测量距离的传感器类型多种多样，Arduino 与其中大多数都能很好地配合。有些传感器使用超声波，而另一些则使用红外光甚至激光。但原则上所有传感器的工作方式都相同：它们发出信号，等待回波返回，并测量整个过程所花费的时间。因为我们知道声音和光在空气中传播的速度，所以可以将测得的时间转换为距离。

在我们的第一个项目中，我们将构建一个装置，用于测量到最近物体的距离，并将其输出到串行端口。在这个项目中，我们使用 Parallax PING))) 超声波传感器，² 因为它易于使用，附带出色的文档，并且功能丰富。它可以检测 2 厘米到 3 米范围内的物体，而且我们直接在面包板上使用它，因此无需焊接。它也是通过可变宽度脉冲提供信息的传感器的绝佳示例（稍后几段将详细介绍）。借助 PING))) 传感器，我们可以轻松构建声呐或能自动找到穿过迷宫路径而不碰墙的机器人。

如前所述，超声波传感器通常不会返回到最近物体的距离。相反，它们返回声音传播到物体并返回传感器所需的时间。PING))) 也不例外（见下一页的图 5.2），其内部相当复杂。幸运的是，它们隐藏在三个简单的引脚后面：电源、接地和信号。

这使得传感器很容易连接到 Arduino。首先，将 Arduino 的接地引脚和 5V 电源引脚连接到 PING))) 的对应引脚。然后将 PING))) 的传感器引脚连接到 Arduino 的某个数字 IO 引脚（我们使用引脚 7，并没有特别的原因）。电路图见下一页的图 5.3，实物照片见第 108 页的图 5.5。

2. http://www.parallax.com/StoreSearchResults/tabid/768/txtSearch/28015/List/0/SortField/4/ProductID/92/Default.aspx

![](img/dcfd13a1bf99c4d3f9996627012a6526_104_0.png)

图 5.2：PING))) 传感器的基本工作原理

![](img/dcfd13a1bf99c4d3f9996627012a6526_104_1.png)

图 5.3：PING))) 基本电路

为了让电路工作起来，我们需要一些与 PING))) 传感器通信的代码：

```
```cpp
const unsigned int PING_SENSOR_IO_PIN = 7;
const unsigned int BAUD_RATE = 9600;

void setup() {
  Serial.begin(BAUD_RATE);
}

void loop() {
  pinMode(PING_SENSOR_IO_PIN, OUTPUT);
  digitalWrite(PING_SENSOR_IO_PIN, LOW);
  delayMicroseconds(2);

  digitalWrite(PING_SENSOR_IO_PIN, HIGH);
  delayMicroseconds(5);
  digitalWrite(PING_SENSOR_IO_PIN, LOW);

  pinMode(PING_SENSOR_IO_PIN, INPUT);
  const unsigned long duration = pulseIn(PING_SENSOR_IO_PIN, HIGH);
  if (duration == 0) {
    Serial.println("Warning: We did not get a pulse from sensor.");
  } else {
    Serial.print("Distance to nearest object: ");
    Serial.print(microseconds_to_cm(duration));
    Serial.println(" cm");
  }

  delay(100);
}

unsigned long microseconds_to_cm(const unsigned long microseconds) {
  return microseconds / 29 / 2;
}
```
```

首先，我们为 PING))) 传感器所连接的 IO 引脚定义一个常量。如果你想将传感器连接到其他数字 IO 引脚，就必须改变程序的第一行。在 setup() 方法中，我们将串行端口的波特率设置为 9600，因为我们希望在串行监视器上看到一些传感器数据。

真正的操作发生在 loop() 中，我们在这里实际实现 PING))) 协议。根据数据手册，³ 我们可以使用脉冲控制传感器，而它也会以可变宽度的脉冲返回结果。

> 3. http://www.parallax.com/dl/docs/prod/acc/28015-PING-v1.5.pdf

![](img/dcfd13a1bf99c4d3f9996627012a6526_106_0.png)

图 5.4：PING))) 脉冲图

在第 9 到 11 行，我们将传感器的信号引脚设为 LOW 并持续 2 微秒，以使其进入适当的状态。这将确保下一步所需的干净 HIGH 脉冲（在电子领域，你应始终为电源中的抖动做好准备）。

最后，是时候让传感器开始工作了。在第 13 到 15 行，我们将传感器的信号引脚设为 HIGH 并持续 5 微秒，以开始一次新的测量。之后，我们再次将引脚设为 LOW，因为传感器将在同一引脚上以可变长度的 HIGH 脉冲作为响应。

对于数字引脚，可用来传输信息的方式只有几种。你可以将引脚设为 HIGH 或 LOW，并且可以控制它保持特定状态的时间。对于许多用途来说，这完全足够，在我们的场景中也是如此。当 PING))) 传感器发出其 40 kHz 的啁啾声时，它会将信号引脚设为 HIGH，并在收到回波时将其设回 LOW。也就是说，信号引脚保持 HIGH 状态的时间恰好是声音传播到物体并返回传感器所需的时间。粗略地说，我们是在使用数字引脚测量模拟信号。在图 5.4 中，你可以看到连接 PING))) 传感器的数字引脚上的典型活动图。

我们可以手动测量引脚保持 HIGH 状态的持续时间，但 pulseIn() 方法已经替我们完成了所有这些繁琐工作。因此，在我们将信号引脚重新设置为输入模式后，在第 18 行使用它。pulseIn() 接受三个参数：

- *pin*：要从中读取脉冲的引脚编号。
- *type*：应读取的脉冲类型。可以是 HIGH 或 LOW。

![](img/dcfd13a1bf99c4d3f9996627012a6526_107_0.png)

# 图 5.5：PING))) 基本电路照片

- *timeout*：以微秒为单位的超时时间。如果在超时时间内无法检测到脉冲，pulseIn() 将返回 0。此参数是可选的，默认值为一秒。

请注意，在整个过程中，只使用一个引脚与 PING))) 通信。迟早你会意识到，IO 引脚在 Arduino 上是稀缺资源，因此 PING))) 只使用一个数字引脚确实是一个很好的特性。当你可以选择不同部件来完成同一任务时，尽量使用尽可能少的引脚。
