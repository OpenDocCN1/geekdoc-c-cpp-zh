
- 1. 选择 **工具 > NuGet 包管理器 > 管理解决方案的 NuGet 包…**
- 2. 在 **浏览** 选项卡中，搜索“**gsl-msvc-**”，然后选择 **gsl-msvc-x64**。
- 3. 在 NuGet 包管理器右侧，单击项目名称旁边的复选框，然后单击 **安装** 将该库添加到项目。

## 在 macOS 上安装 gnuplot

使用 Homebrew 包管理器安装 gnuplot，如下所示：

```
brew install gnuplot
```

## 在 Windows 上安装 gnuplot

从以下地址下载并运行 gnuplot Windows 安装程序（gp541-win64-mingw.exe）：

```
https://sourceforge.net/projects/gnuplot/files/gnuplot/5.4.1/
```

单击 **下一步**，直到进入 **选择附加任务** 步骤，然后：

- 在 **选择 gnuplot 的默认终端** 下，选择 **windows** 单选按钮。
- 滚动到设置底部，勾选 **将应用程序目录添加到 PATH 环境变量** 复选框。

单击 **下一步**，然后单击 **安装**。安装完成后，重新启动计算机。

## 在 macOS 上编译并运行程序

在 macOS 上，通过以下步骤编译 anscombe_macos.c：

- 1. 打开“终端”窗口。
- 2. 使用 **cd** 命令切换到本章示例文件夹中的 AnscombesQuartet 子文件夹。
- 3. 使用以下命令编译程序：
- 4. 运行程序：

```
clang -std=c18 anscombe_macos.c -lgsl -o anscombe_macos
```

```
./anscombe_macos
```

在 macOS 上，该程序将在 anscombe_macos.c 所在的同一文件夹中创建四个 PNG 图像文件。您可以打开这些图像文件以查看这四个图。

## 在 Windows 上编译并运行程序

在添加了 GNU Scientific 库的 Visual Studio 解决方案中：

- 将本章示例文件夹的 AnscombesQuartet 子文件夹中的 anscombe_windows.c 文件添加到项目中。
- 修改第 72 行，以指定 anscombe.csv 在您系统上的位置。
- 生成并运行项目。

运行该程序时，它将在项目文件夹中创建四个 PNG 图像文件。使用 **文件资源管理器** 导航到该文件夹，然后打开这些图像文件以查看这四个图。

能够通过 Web 服务检索数据。同样，一个缺乏执行特定计算所需处理能力的应用程序，可以使用 Web 服务来利用另一个系统更强大的资源。

## 表述性状态转移（REST）

如今大多数 Web 服务使用一种称为表述性状态转移（REST）的架构风格，通常称为 RESTful Web 服务。在 RESTful Web 服务中，您可以调用的每个函数都由唯一的 URL 标识。URL（统一资源定位符）唯一标识 Internet 上资源的位置，例如网站和 Web 服务。当 Web 服务器收到对 RESTful Web 服务的请求时，它会立即知道要在该服务器上调用哪个函数。可以从程序中调用 RESTful Web 服务（如此处将要做的），也可以通过输入适当的 URL 直接从 Web 浏览器的地址栏调用。

## OpenWeatherMap

OpenWeatherMap 为其许多天气 Web 服务提供免费套餐。在使用这些服务之前，您必须在 https://openweathermap.org/ 注册一个免费账户。他们会向您发送一封电子邮件以验证您的账户。验证后，他们会回复一封包含您免费 API 密钥的电子邮件。登录该网站后，您也可以在账户的 API Keys 选项卡下找到该密钥。

您可以在以下地址查看各种 OpenWeatherMap API 及其文档：

https://openweathermap.org/api

有些是免费的，有些仅对订阅者可用。使用免费 API 密钥，您可以访问：

- 指定位置的 **当前天气数据**，我们在本案例研究中使用该数据。
- **One Call API**，它返回指定位置的当前和未来天气数据的组合，以及
- 指定位置的 **5 天 / 3 小时预报**。

## JavaScript 对象表示法（JSON）

许多基于云的服务（如 OpenWeatherMap）通过 JSON 对象与您的应用程序通信。JSON（JavaScript 对象表示法）是一种基于文本、人类和计算机均可读的数据交换格式，用于将数据表示为名称/值对的集合。JSON 已成为在 Internet 上应用程序之间传输数据的首选数据格式。对于调用基于云的 Web 服务而言尤其如此。

每个 JSON 对象包含用花括号括起来、以逗号分隔的*属性名*和*值*列表。例如，以下键值对可能表示一条客户记录：

```json
{"account": 100, "name": "Jones", "balance": 24.98}
```

JSON 还支持数组，即方括号中以逗号分隔的值。例如，以下是一个可接受的 JSON 数字数组：

```
[100, 200, 300]
```

JSON 对象和数组中的值可以是：

- 双引号中的字符串（如 "Jones"），
- 数字（如 100 或 24.98），
- JSON 布尔值（表示为 true 或 false），
- null（表示无值，如 C 中的 NULL），
- 数组（如 [100, 200, 300]），以及
- 其他 JSON 对象。

图 11.8 包含来自 OpenWeatherMap 的 Current Weather Data Web 服务的示例 JSON 响应，我们为提高可读性对其进行了格式化。即使您可能从未见过 JSON 编码的数据，也应该会发现它组织良好、可读且相当容易理解。

```json
{
  "coord": {
    "lon": -71.06,
    "lat": 42.36
  },
  "weather": [
    {
      "id": 803,
      "main": "Clouds",
      "description": "broken clouds",
      "icon": "04n"
    }
  ],
  "base": "stations",
  "main": {
    "temp": 0.03,
    "feels_like": -4.96,
    "temp_min": -1.11,
    "temp_max": 1.11,
    "pressure": 1014,
    "humidity": 93
  },
  "visibility": 10000,
  "wind": {
    "speed": 4.1,
    "deg": 360
  },
  "clouds": {
    "all": 75
  },
  "dt": 1609815037,
  "sys": {
    "type": 1,
    "id": 3486,
    "country": "US",
    "sunrise": 1609762409,
    "sunset": 1609795488
  },
  "timezone": -18000,
  "id": 4930956,
  "name": "Boston",
  "cod": 200
}
```

图 11.8 | 美国马萨诸塞州波士顿的 OpenWeatherMap 示例响应。（第 1 部分，共 2 部分。）

图 11.8 | 美国马萨诸塞州波士顿的 OpenWeatherMap 示例响应。（第 2 部分，共 2 部分。）

## 开源 libcurl 库

为了获得图 11.8 中的 JSON 响应，我们的应用程序使用开源 libcurl 库中的函数：

https://curl.se/libcurl/

该库支持许多用于在应用程序之间传输数据的 Internet 和 Web 协议，并可用于调用 Web 服务并接收其响应。您可以在以下地址找到 libcurl 的 C 函数文档：

https://curl.se/libcurl/c/

在我们完整编码的示例 weather.c 中（位于本章示例文件夹的 weather 文件夹中），我们详细注释了调用 Web 服务并将其响应保存到文件所需的 libcurl 函数。

要在 macOS 或 Linux 上安装 libcurl：

- 对于 macOS，您可以使用 Homebrew 包管理器¹²按如下方式安装 libcurl 库：
  - `brew install libcurl4`
- 对于 Ubuntu Linux，请执行以下命令
  - `sudo apt install libcurl4-openssl-dev`

在 Visual Studio 中，您可以将 libcurl 添加到每个希望使用它的项目中。在 Visual Studio 中打开项目后，执行以下步骤：

- 1. 选择“工具”>“NuGet 包管理器”>“管理解决方案的 NuGet 包...”。
- 2. 在“浏览”选项卡中，搜索“curl”，然后选择“curl by curl contributors”。
- 3. 在 NuGet 包管理器右侧，单击项目名称旁边的复选框，然后单击“安装”将该库添加到项目。

## 开源 cJSON 库

我们应用程序的 libcurl 部分将 OpenWeatherMap 的 JSON 响应写入文件。为了显示天气报告，我们的应用将文件内容读入字符串，然后使用开源 cJSON 库从 JSON 中提取各项。您可以从以下地址下载 cJSON：

```
https://github.com/DaveGamble/cJSON
```

此库没有安装过程。您只需将库的 cJSON.h 和 cJSON.c 文件包含在项目中。

cJSON 的函数使您能够访问 JSON 响应中的各项，以便我们可以显示如下天气报告：

```
Boston Weather
Temperature: 0.0 C
Feels like: -5.0 C
Pressure: 1014 hPa
Humidity: 93%
Conditions: broken clouds
```

在 weather.c 中，我们详细注释了提取上述数据所需的 cJSON 函数，这些数据针对您运行应用程序时指定的城市（下文讨论）。

## 在 macOS 和 Linux 上编译并运行程序

在 macOS 和 Linux 上，通过以下步骤编译 weather 应用：

- 1. 打开“终端”窗口。
- 2. 使用 cd 命令切换到本章示例文件夹中的 weather 子文件夹。
- 3. 使用以下命令之一编译程序——在 macOS 上使用 clang，在 Linux 上使用 gcc：

```
clang -std=c18 -Wall weather.c cJSON.c -lcurl -o weather
gcc -std=c18 -Wall weather.c cJSON.c -lcurl -o weather
```

此应用程序接收两个命令行参数。尽管我们到 15.3 节才讨论命令行参数的细节，但这个完整编码的模拟程序提供了接收命令行参数所需的语句。第一个参数是您希望获取当前天气的城市，例如 `Boston,MA,USA`。如果城市名称包含空格，请将位置用引号括起来：`"Los Angeles,CA,USA"`。第二个命令行参数是您的 OpenWeatherMap API 密钥。以下命令将获取美国马萨诸塞州波士顿的当前天气数据：`./weather Boston,MA,USA API_KEY`。请务必将 API_KEY 替换为您注册免费账户时收到的 OpenWeatherMap API 密钥。编译程序并运行多次。接下来，研究此应用程序的代码（包括大量注释）。

12. 如果找不到 brew 命令，请访问 https://brew.sh/ 获取安装说明。
