

![](img/dcfd13a1bf99c4d3f9996627012a6526_115_0.png)

## 图 5.7：TMP36 和 PING))) 传感器协同工作

现在我们有两个独立的电路：一个用于测量距离，一个用于测量温度。参见图 5.7 以及第 120 页的图 5.8，将它们组合成一个单一电路。使用以下程序使电路运行起来：

```
Download ultrasonic/PreciseSensor/PreciseSensor.pde
Line 1  const unsigned int TEMP_SENSOR_PIN = 0;
- const float SUPPLY_VOLTAGE = 5.0;
- const unsigned int PING_SENSOR_IO_PIN = 7;
- const float SENSOR_GAP = 0.2;
5 const unsigned int BAUD_RATE = 9600;
- 
- float current_temperature = 0.0;
```

```
unsigned long last_measurement = millis();

void setup() {
  Serial.begin(BAUD_RATE);
}

void loop() {
  unsigned long current_millis = millis();
  if (abs(current_millis - last_measurement) >= 1000) {
    current_temperature = get_temperature();
    last_measurement = current_millis;
  }
  Serial.print(scaled_value(current_temperature));
  Serial.print(",");
  const unsigned long duration = measure_distance();
  Serial.println(scaled_value(microseconds_to_cm(duration)));
}

long scaled_value(const float value) {
  float round_offset = value < 0 ? -0.5 : 0.5;
  return (long)(value * 100 + round_offset);
}

const float get_temperature() {
  const int sensor_voltage = analogRead(TEMP_SENSOR_PIN);
  const float voltage = sensor_voltage * SUPPLY_VOLTAGE / 1024;
  return (voltage * 1000 - 500) / 10;
}

const float microseconds_per_cm() {
  return 1 / ((331.5 + (0.6 * current_temperature)) / 10000);
}

const float sensor_offset() {
  return SENSOR_GAP * microseconds_per_cm() * 2;
}

const float microseconds_to_cm(const unsigned long microseconds) {
  const float net_distance = max(0, microseconds - sensor_offset());
  return net_distance / microseconds_per_cm() / 2;
}

const unsigned long measure_distance() {
  pinMode(PING_SENSOR_IO_PIN, OUTPUT);
  digitalWrite(PING_SENSOR_IO_PIN, LOW);
  delayMicroseconds(2);

  digitalWrite(PING_SENSOR_IO_PIN, HIGH);
  delayMicroseconds(5);
  digitalWrite(PING_SENSOR_IO_PIN, LOW);

```

```
pinMode(PING_SENSOR_IO_PIN, INPUT);
return pulseIn(PING_SENSOR_IO_PIN, HIGH);
}
```

代码几乎是用于使 PING))) 和 TMP36 传感器工作的程序的完美合并。只做了少量改动：

- 常量 MICROSECONDS_PER_CM 已被 microseconds_per_cm() 函数取代，该函数根据当前温度动态确定声波传播 1 厘米所需的微秒数。
- 由于当前温度通常不会经常或快速变化，我们不再永久测量它，而是每秒测量一次。我们使用第 8 行的 millis() 来确定自 Arduino 启动以来经过了多少毫秒。从第 15 行到第 19 行，我们检查自上次测量以来是否已过去一秒。如果是，我们再次测量当前温度。
- 我们不再通过串口以浮点数的形式传输传感器数据，而是改用缩放后的整数值。这由 scaled_value() 函数完成，该函数将浮点值四舍五入到两位小数，并通过乘以 100 转换为 long 值。在接收端，你需要再次除以 100。

如果你将程序上传到 Arduino 并在传感器前挥动手，会看到类似以下的输出：

```
1940,2818
2914,3032
3045,34156
3005,2843
3045,2476
3085,2414
```

输出是以逗号分隔的值列表，其中第一个值表示当前温度，单位为摄氏度，第二个值是到最近物体的距离，单位为厘米。两个值都必须除以 100 才能得到实际的传感器数据。

我们的这个小项目现在有两个传感器。其中一个连接到数字引脚，而另一个使用模拟引脚。在下一节中，你将学习如何将传感器数据传回 PC 并利用它创建基于现实世界当前状态的应用程序。

## 如何编码传感器数据

编码传感器数据是 Arduino 项目中经常需要解决的问题，因为我们收集的所有漂亮数据通常都需要由在普通计算机上运行的应用程序来解释。

在定义数据格式时，你需要考虑多个因素。例如，格式不应浪费 Arduino 宝贵的内存。在我们的例子中，我们本可以使用 XML 来编码传感器数据，例如：

```
<sensor-data>
  <temperature>30.05</temperature>
  <distance>51.19</distance>
</sensor-data>
```

显然这不是一个好的选择，因为现在我们浪费了多倍于实际数据的内存来创建文件格式的结构。此外，接收应用程序必须使用 XML 解析器来解释数据。

但你也不应走向另一个极端。也就是说，只有在绝对必要时或接收应用程序本来就期望二进制数据时，才应使用二进制格式。

总的来说，像字符分隔值（CSV）这样最简单的数据格式通常是最好的选择。

## 5.5 使用 Processing 将数据传回你的计算机

本章中的所有程序都使用串口将传感器数据传回你的计算机。但到目前为止，我们只是在 IDE 的串口监视器中观看数据流过，并未在自己的应用程序中使用它。

在本节中，我们将构建一个图形化可视化传感器数据的应用程序。该程序将实现一种倒置的声纳：它在屏幕上绘制一个小点显示到最近物体的距离，同时该点本身会沿圆周移动（参见第 130 页的图片）。

为了实现该应用程序，我们将使用 Processing 编程语言，在图 5.9 中，第 121 页，你可以看到我们将如何组织项目。Processing 代码在我们的计算机上运行，而所有

![](img/dcfd13a1bf99c4d3f9996627012a6526_119_0.png)

图 5.8：最终电路的照片

## 使用声纳传感器拯救气候

来自西北大学和密歇根大学的研究人员创建了一个声纳系统，它仅使用计算机的麦克风和扬声器来检测计算机当前是否正在使用中。* 如果未使用，计算机会自动关闭屏幕，从而保护环境。

与其使用麦克风和扬声器，你也可以使用 PING))) 传感器。凭借本章中学到的知识，你可以轻松自行构建这样的系统。试试看！

* http://blog.makezine.com/archive/2009/10/using_sonar_to_save_power.html

![](img/dcfd13a1bf99c4d3f9996627012a6526_120_0.png)

图 5.9：我们倒置声纳项目的系统架构

PING))) 传感器代码仍在 Arduino 上运行。Processing 代码与 Arduino 之间的通信通过串口进行。

Processing 是 Java 编程语言的扩展，其重点在于计算艺术。使用 Processing 创建多媒体应用程序非常容易：产生声音和动画 2D 或 3D 图像的应用程序。它对用户交互的支持也很出色，并且文档完善（例如，参见 Processing: Creative Coding and Computational Art [Gre07]）。

![](img/dcfd13a1bf99c4d3f9996627012a6526_121_0.png)

图 5.10：Processing IDE 是 Arduino IDE 的基础。

它最初是为没有太多编程经验的设计学生而构建的，但他们仍然希望使用计算机和电子设备来创建交互式艺术作品。这就是为什么 Processing 易于学习且非常适合初学者。但许多人也将其用于严肃和高级任务，尤其是以视觉吸引力的方式呈现数据。

你可以免费下载 Processing，⁵ 它为所有流行的操作系统提供一键安装程序。启动它或查看图 5.10。看起来很熟悉，不是吗？这并非巧合，因为 Arduino IDE 是从 Processing IDE 派生出来的。取而代之的是 writ-

5. http://processing.org/download/

