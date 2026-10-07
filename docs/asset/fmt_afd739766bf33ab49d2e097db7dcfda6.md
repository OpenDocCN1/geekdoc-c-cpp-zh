
现在你应该有一个像这样的项目布局。

![](img/9ad62c521b3df94dc74d517230e21e72_247_0.png)

如果你构建了项目，你将在测试运行器中看到这个。

![](img/9ad62c521b3df94dc74d517230e21e72_247_0)

接下来，让我们逐一查看这些测试。

## Trello 板

要运行 Trello 测试，你需要一个 `https://trello.com` 账户。

在 Trello 上创建一个看板，并在其中创建一个列表。然后，你需要获取你的 Trello API 的 Token 和 Key。

关于 Trello 的 Token 和 Key 可以在 `https://trello.com/developer/api` 获取详细信息：

![](img/9ad62c521b3df94dc74d517230e21e72_247_0)

接下来，让我们查看这些测试。

## 删除看板

为了在 Trello 上删除看板，你可以在 `https://trello.com` 上操作。

![](img/9ad62c521b3df94dc74d517230e21e72_247_0)

接下来，让我们查看这些测试。

## 创建列表

为了在 Trello 上创建列表，你可以在 `https://trello.com` 上操作。

![](img/9ad62c521b3df94dc74d517230e21e72_247_0)

接下来，让我们查看这些测试。

## 创建看板

为了在 Trello 上创建看板，你可以在 `https://trello.com` 上操作。

![](img/9ad62c521b3df94dc74d517230e21e72_247_0)

接下来，让我们查看这些测试。

- JDBC 请求
- Java 对象请求
- LDAP 请求
- SOAP/XML-RPC 请求
- Webservice (SOAP) 请求

因此接下来我们需要添加 HTTP 请求采样器（HTTP request samplers），毕竟我们我们需要加载一些网页。在线程组（Thread Group）下添加一个 HTTP Request。

![](img/9ad62c521b3df94dc74d517230e21e72_252_0.png)

添加后，完成的请求看起来像这样

现在按照下面的步骤重复此过程

## HTTP Request

Name: Kevs Bikes
Comments:

Basic（基础） Advanced（高级）
Web Server（Web 服务器）
Protocol [http]: https
Server Name or IP: kevsbox.com
HTTP Request
GET Path: /bikes.html

我们将添加一个计时器（timer）来帮助测试。当用户点击我们的网站或应用时，他们自然会有暂停和延迟。这些是需要考虑的。常量计时器（Constant timers）是 JMeter 中最常用的。它们简单地决定了请求之间等待多少毫秒。

![](img/9ad62c521b3df94dc74d517230e21e72_253_0.png)

然后将其设置为等待 200 毫秒。

## Constant Timer

Name: Kevsbox Timer
Comments:
thread Delay (in milliseconds): 200

最后，我们需要一种在运行测试后查看结果的方法。这是通过监听器（listeners）实现的，它是一种显示结果的记录机制，包括日志和调试信息。
结果树（View Results Tree）是最常用的监听器，我们将在本示例中使用它。

![](img/9ad62c521b3df94dc74d517230e21e72_254_0.png)

另一个选项是添加聚合报告（summary report）。

![](img/9ad62c521b3df94dc74d517230e21e72_254_1.png)

这是聚合报告的典型输出

![](img/9ad62c521b3df94dc74d517230e21e72_254_2.png)

write results to file / Read from filename

**Label（标签）：** 在下方区域，你将能够看到运行期间或测试运行后记录的所有 http 请求。

**Samples（样本）：** 样本表示为给定线程运行的 http 请求数，或者接收网页所需的平均时间。

例如，我们有一个 http 请求，并用 5 个用户运行它，样本数将是 5x1。因此，如果单个用户运行了两次，那么 5 个用户的样本数将是 5x2=10。

**Average（平均值）：** 平均值是该特定 http 请求的平均响应时间。该响应时间以毫秒为单位。这是所有响应的算术平均值（所有时间总和 / 计数）。

**Min（最小值）：** Min 表示 http 请求花费的最小响应时间。

**Max（最大值）：** Max 表示 http 请求花费的最大响应时间。

**Std. Deviation（标准差）：** 这显示了发现了多少偏离接收时间平均值的异常情况。该值越小，假设时间模式越一致。

**Error %（错误率）：** 这表示运行期间样本中的错误百分比。此错误可以是 404（文件未找到），可能是异常或测试运行期间的任何错误都会显示在 Error % 中。在上面的图中，错误率为零，因为所有请求都成功运行了。

**Throughput（吞吐量）：** 吞吐量是测试期间单位时间内（秒、分钟、小时）设置到服务器的请求数。越大越好。

**KB/Sec：** 每秒千字节的吞吐量。

**Avg. Bytes（平均字节）：** 样本响应的平均大小（字节）。

还有一个响应时间图（Response Time Graph）

![](img/9ad62c521b3df94dc74d517230e21e72_255_0.png)

如果你添加了所有这些内容，你拥有这样一个项目。

现在我们准备好运行此测试了。点击 Save（保存），你的测试将保存为 `.jmx` 文件。

现在是运行测试的时间了，点击 View Tree（查看树）。

![](img/9ad62c521b3df94dc74d517230e21e72_256_0.png)

现在开始测试并观察结果

![](img/9ad62c521b3df94dc74d517230e21e72_256_1.png)

完成后，结果 Tree 看起来像这样

## The View Results Table（结果表）

| Sample #（样本号） | Start Time（开始时间） | Thread Name（线程名称） | Label（标签） | Sample Time(ms)（样本时间） |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 15:07:05.921 | Kevsbox Thread... | Kevbox Home Page | 443 |
| 2 | 15:07:06.585 | Kevsbox Thread... | Kevbox Bikes | 45 |
| 3 | 15:07:07.989 | Kevsbox Thread... | Kevbox Home Page | 202 |
| 4 | 15:07:08.256 | Kevsbox Thread... | Kevbox Bikes | 18 |
| 5 | 15:07:09.839 | Kevsbox Thread... | Kevbox Home Page | 175 |
| 6 | 15:07:10.237 | Kevsbox Thread... | Kevbox Bikes | 32 |
| 7 | 15:07:11.871 | Kevsbox Thread... | Kevbox Home Page | 168 |
| 8 | 15:07:12.241 | Kevsbox Thread... | Kevbox Bikes | 31 |
| 9 | 15:07:13.849 | Kevsbox Thread... | Kevbox Home Page | 192 |

| Status（状态） | Sent Bytes（发送字节） | Latency（延迟） | Connect Time(ms)（连接时间） |
| :--- | :--- | :--- | :--- |
| OK | 13844 | 83 | 47 |
| OK | 20492 | 123 | 45 |
| OK | 13844 | 58 | 27 |
| OK | 20492 | 123 | 38 |
| OK | 13844 | 55 | 23 |
| OK | 20492 | 31 | 20 |
| OK | 13844 | 52 | 22 |
| OK | 20492 | 30 | 0 |
| OK | 13844 | 54 | 24 |
| OK | 20492 | 29 | 0 |

这就是一个简单的运行，但 JMeter 还可以做很多。对于这个高级方案，我们将深入探讨这个有趣的领域。

![](img/9ad62c521b3df94dc74d517230e21e72_257_0.png)

下一个测试套件提供了更多场景。首先我们有一个 Thread Group（线程组）

![](img/9ad62c521b3df94dc74d517230e21e72_258_0.png)

这里有 10 秒的 ramp-up（启动时间）和 10 个用户，循环 10 次，所以这里有 100 次执行。

接下来是一个 HTTP Request Defaults 元素，这里保存了基础 URL。

![](img/9ad62c521b3df94dc74d517230e21e72_258_1.png)

接下来是一个 loop controller（循环控制器），设置为循环 3 次。现在我们有 100 次 3 循环，所以这里有 300 次执行。

![](img/9ad62c521b3df94dc74d517230e21e72_259_0.png)

下一个元素必须作为子元素放在 loop controller 下方。

![](img/9ad62c521b3df94dc74d517230e21e72_259_1.png)

这些都是 http 请求，像这里所示添加 3 个。你会注意到 protocol 和 Server Name/IP 是从 HTTP Request Defaults 元素获取的，唯一的是 Path。

![](img/9ad62c521b3df94dc74d517230e21e72_259_2.png)

现在每个 300 个当前请求中都有 3 个 http 请求，总请求数为 900 个测试请求。现在添加你的报告，你就有了这样的布局。

![](img/9ad62c521b3df94dc74d517230e21e72_260_0.png)

像之前一样保存并运行。
全部完成，现在让我们看看结果。样本数应该是 900，所有循环已完成。

## The View Results Table（结果表）

| Sample #（样本号） | Start Time（开始时间） | Thread Name（线程名称） | Label（标签） | Sample Time(ms)（样本时间） | Status（状态） |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 865 | 15:07:05.118 | Kevsbox Thread... | Kevbox Home Page | 443 | OK |
| 866 | 15:07:06.117 | Kevsbox Thread... | Kevbox Bikes | 45 | OK |
| 867 | 15:07:06.201 | Kevsbox Thread... | Kevbox Bikes | 29 | OK |
| 868 | 15:07:06.237 | Kevsbox Thread... | Kevbox Home Page | 27 | OK |
| 869 | 15:07:07.254 | Kevsbox Thread... | Kevbox Home Page | 43 | OK |
| 870 | 15:07:07.310 | Kevsbox Thread... | Kevbox Bikes | 36 | OK |
| 871 | 15:07:07.341 | Kevsbox Thread... | Kevbox Home Page | 31 | OK |
| 872 | 15:07:07.396 | Kevsbox Thread... | Kevbox Bikes | 30 | OK |
| 873 | 15:07:07.427 | Kevsbox Thread... | History of curry | 29 | OK |
| 874 | 15:07:07.458 | Kevsbox Thread... | Kevbox recipes | 30 | OK |
| 875 | 15:07:07.483 | Kevsbox Thread... | homepage | 34 | OK |
| 876 | 15:07:07.515 | Kevsbox Thread... | History of curry | 27 | OK |
| 877 | 15:07:07.551 | Kevsbox Thread... | Kevbox recipes | 28 | OK |
| 878 | 15:07:07.578 | Kevsbox Thread... | homepage | 29 | OK |
| 879 | 15:07:08.605 | Kevsbox Thread... | History of curry | 31 | OK |
| 881 | 15:07:08.634 | Kevsbox Thread... | history of curry | | |

树状输出也是很好的。

![](img/9ad62c521b3df94dc74d517230e21e72_261_0.png)

现在我们已经入门门了，让我们进一步观察。
接下来我们需要一个 Debug Sampler。

## 调试采样器 (Debug Sampler)

名称：
Spice Debugger
注释：
JMeter 属性: False
JMeter 变量: True
系统属性: False

点击此处移除所有之前的报告数据并保存您的项目。下次重新运行项目并等待完成。现在在“查看结果树”（View Results Tree）中查看结果，我们应该看到一些调试器的输出。

![](img/9ad62c521b3df94dc74d517230e21e72_262_0.png)

现在点击其中一个并查看输出，你将在那里看到 JMeter 变量。

| 响应体 | 响应标头 |
|---|---|
| JMeterVariables:<br>.JMeterThreadlast_sample_ok=true<br>.JMeterThread@org.apache.jmeter.threads.SamplePackage@7f3yd2d1<br>START HMS=149492<br>START MS=161909982735<br>START UTC=2021102010422<br>TEST MS=19181278399 | |___Spice Group_idx=6<br>|___Spice Loop Controller_idx=0<br>|jmeter.U.T..Spice Group 1-5<br>|jmv_SAME_USER=true |

现在让我们来看看系统属性。

## 调试采样器 (Debug Sampler)

| 名称: | Spice Debugger |
|---|---|
| 注释: | |
| JMeter 属性: | False |
| JMeter 变量: | False |
| 系统属性: | True |

进行这些更改、保存、重置并重新运行。

## Spice 调试器 (Spice Debugger)

- 首页
- 首页
- 咖喱历史
- 首页
- 咖喱历史
- 咖喱历史
- 辣椒食谱
- 辣椒食谱
- 首页
- 首页
- 咖喱历史
- 咖喱历史
- 咖喱历史
- 辣椒食谱
- Spice 调试器
- 辣椒食谱
- 辣椒食谱
- 首页
- 首页
- 咖喱历史
- 咖喱历史
- 辣椒食谱
- Spice 调试器
- 辣椒食谱
- Spice 调试器
- 首页
- 自动滚动？

| 响应体 | 响应标头 |

```
SystemProperties

darkafka.allowNativeCode=false

darkafka.serialization=file

encoding=Cp1252

separator=-1

java.class.path=-Apache:JMeter:core-;U::Meterlib|accessors-smart-1.2,jar;U::Meterlib|http-checker-2.10.0,jar;U::Meterlib|commons-codec-1.14,jar;commons-j3-3.1,jar;U::Meterlib|commons-lang-3.6,jar;U::Meterlib|line4j-1.8,jar;U::Meterlib|darkafka-2.1,jar;U::Meterlib|darkafka-macos-2.1.1,jar;U::Meterlib|darkafka-utils-2.1.1,jar;U::Meterlib|darkafka-windows-2-1.1,jar
```
