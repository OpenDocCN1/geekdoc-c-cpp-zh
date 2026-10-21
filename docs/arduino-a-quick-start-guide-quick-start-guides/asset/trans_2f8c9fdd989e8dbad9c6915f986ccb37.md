

## 第 8 章：使用 Arduino 进行联网

使用独立的 Arduino，你可以创建无数有趣且实用的项目。但一旦你将 Arduino 变成网络设备，你就打开了一个充满可能性的全新世界。

现在你可以访问互联网上的所有信息，因此只需从天气服务读取数据，就能将 Arduino 变成一个酷炫的极客风格气象站。你还可以将 Arduino 变成一个 Web 服务器，为网络中的其他设备或计算机提供传感器数据。

在本章中，我们将构建一个能发送电子邮件的防盗报警器。它能够检测你客厅中的移动，当在你外出期间检测到移动时，Arduino 会向你发送电子邮件。由于这是一个较为高级的项目，我们将首先完成一些较小的项目，以学习所需的所有技术和技能。

我们将从一块没有任何网络功能的“裸”Arduino 开始。只要连接到 PC，你仍然可以让它接入互联网。

对于第二个项目，我们将通过以太网扩展板大幅改善这种状况。现在你的 Arduino 变成了一个功能完备的网络设备，可以直接访问 IP 服务，例如 DAYTIME 服务。这将使你的 Arduino 变成一个非常精确的时钟。

一旦我们能够访问 IP 服务，我们将学习如何直接从带有以太网扩展板的 Arduino 发送电子邮件。对于我们的防盗报警器，接下来只需要知道如何检测移动。为此，我们将使用一个被动红外传感器（PIR），因此在本章中，你不仅将学习各种网络技术，还将学习如何使用 PIR 传感器。

最后，我们将结合所学的一切，构建这个能发送电子邮件的防盗报警器。一旦它运行起来，你会感到安全得多。

### 8.1 你需要什么

![](img/dcfd13a1bf99c4d3f9996627012a6526_170_0.png)

图 8.1：本章所需的全部部件

- 一块用于 Arduino 的以太网扩展板
- 一个 TMP36 温度传感器
- 一个 PIR 红外运动传感器
- 一块面包板
- 一些导线
- 一块 Arduino 板，如 Uno、Duemilanove 或 Diecimila
- 一条用于将 Arduino 连接到计算机的 USB 线缆

### 8.2 使用 PC 将传感器数据传输到互联网

![](img/dcfd13a1bf99c4d3f9996627012a6526_171_0.png)

图 8.2：使用 PC 将 Arduino 连接到互联网。

还记得大约十五年前，你将 PC 连接到互联网的情景吗？一切始于一个 38,400 波特率的调制解调器、Netscape Navigator 3，以及你在邮件中收到的 AOL 软盘或光盘。如今，你可能通过有线电视、卫星或 DSL 使用宽带接入，而且可能通过 WiFi 在你家的每个角落都能上网。因此，我们将从使用你现有的连接将 Arduino 连接到互联网开始。

在图 8.2 中，你可以看到将 Arduino 连接到互联网的典型设置。一个程序在你的 PC 上运行，并通过串口与 Arduino 通信。当应用程序需要访问互联网时，由 PC 上的程序来处理。使用这种架构，你可以将有趣的传感器数据发推文¹。

¹ http://twitter.com

我们将构建一个系统，当你的工作室或办公室温度超过某个阈值（即 32 摄氏度（90 华氏度））时，它会自动发布一条推文。请重新构建第 113 页上的 5.4 节“使用温度传感器提高精度”中的温度传感器示例（尝试不看第 114 页上的图 5.6 来完成），并将以下代码上传到你的 Arduino：

Download Ethernet/TwitterTemperature/TwitterTemperature.pde

```
#define CELSIUS

const unsigned int TEMP_SENSOR_PIN = 0;
const unsigned int BAUD_RATE = 9600;
const float SUPPLY_VOLTAGE = 5.0;

void setup() {
  Serial.begin(BAUD_RATE);
}

void loop() {
  const int sensor_voltage = analogRead(TEMP_SENSOR_PIN);
  const float voltage = sensor_voltage * SUPPLY_VOLTAGE / 1024;
  const float celsius = (voltage * 1000 - 500) / 10;
#ifdef CELSIUS
  Serial.print(celsius);
  Serial.println(" C");
#else
  Serial.print(9.0 / 5.0 * celsius + 32.0);
  Serial.println(" F");
#endif
  delay(5000);
}
```

这与我们之前使用的代码几乎相同。请记住，如果你使用的是 3.3V 而非 5V 供电的 Arduino，则必须将第 5 行中的 SUPPLY_VOLTAGE 设置为 3.3。

我们现在同时支持摄氏度和华氏度值，你可以通过预处理器常量来控制应使用哪个单位。如果在第一行设置常量 CELSIUS，应用程序将输出摄氏度温度。如果删除第一行或将其改为注释行，则将使用华氏度。

为了改变应用程序的行为，我们使用 #ifdef 预处理器指令。它检查某个预处理器常量是否已设置，然后有条件地编译代码。在我们的例子中，仅当未设置常量 CELSIUS 时，它才会编译第 19 行中的摄氏度转华氏度公式。

上传代码后，它将每五秒钟向串口输出一次当前温度。输出如下所示：

```
27.15 C
26.66 C
27.15 C
```

现在我们需要一个在你的 PC 上运行的程序，它读取该输出，并在温度高于 32 摄氏度（90 华氏度）时发布一条推文。我们可以使用任何能够读取串口并支持 Twitter 的编程语言，但由于我们在所有其他示例中一直使用 Processing，因此我们也将在这个项目中使用它。

### 用于发布传感器数据的 Web 服务

随着廉价开源硬件和传感器的出现，用于发布传感器数据的 Web 服务在过去几年中变得流行起来。这类服务允许你发布、读取和分析传感器数据。来自世界各地的人们发布来自其气象站、环境传感器等的数据，并在互联网上免费提供。

最流行的服务是 Pachube* 和 Sensorpedia†。原则上，它们的运作方式相同：你注册一个账户，并获得一个 API 密钥。然后，你可以使用该密钥向服务进行身份验证并上传传感器数据。

* http://pachube.com
† http://sensorpedia.com/

### 8.3 向 Twitter 注册应用程序

在开始编码之前，我们必须先在 Twitter 网站上注册我们的应用程序，以获得一个 OAuth 访问令牌。² OAuth 是一种允许应用程序使用其他应用程序资源的身份验证方案。在我们的例子中，我们将授予我们自己的应用程序更新 Twitter 动态的权利，而无需使用我们的 Twitter 用户名和密码。

² http://en.wikipedia.org/wiki/Oauth

很长一段时间里，Twitter 支持 HTTP 基本身份验证。³ 自动化服务只需要用户名和密码即可请求或更新 Twitter 动态。但自 2010 年 8 月起，Twitter 已取消对基本身份验证的支持，现在改用 OAuth。

³ http://en.wikipedia.org/wiki/Basic_authentication

要获得 OAuth 访问令牌，请在 Twitter 网站的开发者部分注册你的新应用程序。⁴ 登录后，点击“注册应用”链接，并填写你在下一页图 8.3 中看到的表单。确保将应用程序类型设置为 Client，并将默认访问类型设置为 Read & Write。你可以将应用程序名称设置为任意字符串，每当你使用该应用程序发布推文时，它都会出现在你的 Twitter 频道上。例如，如果你将其设置为 RescueMeFromWork，你的推文将通过 RescueMeFromWork 发布。

⁴ http://dev.twitter.com

