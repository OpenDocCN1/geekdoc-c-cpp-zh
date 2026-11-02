

## 启动你的 Xcode

要测试你的 iPhone 应用程序在你的设备上，你需要从 iPhone 开发者计划门户获取 iPhone 开发证书。以下章节将引导你完成从获取证书到将应用程序部署到设备上的必要步骤。

首先，获取唯一标识你的 iPhone/iPod Touch 的 40 字符标识符。为此，将你的设备连接到 Mac 并启动 Xcode。选择 Window > Organizer 启动 Organizer 应用程序。图 E-1 显示了 Organizer 应用程序显示我的 iPhone 标识符的情况。复制你获取的标识符并保存在某处。稍后你将需要此标识符。

![](img/aab2d775c46f70cd606f2e58e2521324_513_0.png)

图 E-1

## 生成证书签名请求

要向 Apple 请求开发证书，你需要生成证书签名请求。你可以使用位于 Applications/Utilities/ 文件夹中的钥匙串访问应用程序来完成此操作（见图 E-2）。

![](img/aab2d775c46f70cd606f2e58e2521324_514_0.png)

**图 E-2**

在钥匙串访问应用程序中，选择 Keychain Access > Certificate Assistant，然后选择 Request a Certificate From a Certificate Authority（见图 E-3）。

![](img/aab2d775c46f70cd606f2e58e2521324_514_1.png)

**图 E-3**

在证书助手窗口中（见图 E-4），输入你的电子邮件地址，选择“保存到磁盘”单选按钮，并选中“让我指定密钥对信息”复选框。单击“继续”。

![](img/aab2d775c46f70cd606f2e58e2521324_515_0.png)

图 E-4

选择 2048 位的密钥大小，并选择 RSA 算法（见图 E-5）。单击“继续”。

![](img/aab2d775c46f70cd606f2e58e2521324_515_1.png)

图 E-5

系统要求你将请求保存到文件。使用建议的默认名称，并单击“保存”（见图 E-6）。

![](img/aab2d775c46f70cd606f2e58e2521324_516_0.png)

图 E-6

## 登录 iPhone 开发者计划门户

生成证书签名请求后，你需要登录 Apple 的 iPhone Dev Center（见图 E-7）。单击页面右侧的 iPhone Developer Program Portal 链接。请记住，你需要支付 99 美元才能访问此页面。

> **警告** 请务必尽早注册，因为审批过程需要一段时间——从几小时到几天。

![](img/aab2d775c46f70cd606f2e58e2521324_516_1.png)

图 E-7

在 iPhone Developer Program Portal 页面上，单击 Launch Assistant 按钮（见图 E-8），它将引导你完成配置 iPhone 和生成开发证书的过程。

![](img/aab2d775c46f70cd606f2e58e2521324_517_0.png)

图 E-8

你应该会看到欢迎页面。单击“继续”。

首先，系统要求你创建一个 App ID（见图 E-9）。App ID 是一系列字符，用于唯一标识你 iPhone 上的一个（或多个）应用程序。输入一个友好名称来描述此 App ID（将由 Apple 生成）。单击“继续”。

![](img/aab2d775c46f70cd606f2e58e2521324_518_0.png)

下一个屏幕允许你提供你的 iPhone/iPod Touch 的描述。你需要提供之前获取的设备 ID（见图 E-10）。单击“继续”。

![](img/aab2d775c46f70cd606f2e58e2521324_518_1.png)

## 18. 如图, 在正方形 ABCD 中, AB=4, E 是 BC 的中点, 点 P 在射线 AD 上, 将 △ABP 沿 AP 所在直线翻折, 得到 △AB'P, 连接 DB'、EB', 当 △DB'E 是直角三角形时, 求线段 PA 的长.

![](img/aab2d775c46f70cd606f2e58e2521324_519_0.png)

备用图

解: ∵ 正方形 ABCD 中, AB=4, E 是 BC 的中点

∴ BE=CE=2, BC=CD=AD=AB=4, ∠ABC=∠BCD=∠CDA=∠DAB=90°

设 PA=x, 则 PD=|4-x|

① 当 ∠B'DE=90° 时, 如图1

![](img/aab2d775c46f70cd606f2e58e2521324_520_0.png)

图 E-12

将生成一个预置描述文件（见图 E-13）。完成后单击“继续”。

![](img/aab2d775c46f70cd606f2e58e2521324_520_1.png)

图 E-13

你可以通过单击“立即下载”按钮将生成的预置描述文件下载到你的 Mac（见图 E-14）。接下来，单击“继续”。

![](img/aab2d775c46f70cd606f2e58e2521324_521_0.png)

图 E-14

将下载的预置描述文件（默认保存在 Mac 的 Downloads 文件夹中）拖放到 Xcode（位于 Dock 中）。这样会将预置描述文件安装到你连接的 iPhone 或 iPod Touch 上。单击“继续”（见图 E-15）。

![](img/aab2d775c46f70cd606f2e58e2521324_522_0.png)

**图 E-15**

你可以通过转到 Organizer 应用程序并查看 Provisioning 部分来验证预置描述文件是否已正确安装在你的设备上（见图 E-16）。

![](img/aab2d775c46f70cd606f2e58e2521324_522_1.png)

**图 E-16**

回到 iPhone Developer Program Portal，你现在可以下载开发证书并将其安装到你的 iPhone 或 iPod Touch 上。单击“立即下载”按钮（见图 E-17）将开发证书下载到你的 Mac。单击“继续”。

![](img/aab2d775c46f70cd606f2e58e2521324_523_0.png)

图 E-17

在 Mac 的 Downloads 文件夹中，双击刚下载的 developer_identity.cer 文件，将其安装到 Mac 的钥匙串中。当出现提示时（见图 E-18），单击 OK。

回到 iPhone Developer Program Portal，现在它会向你展示如何验证证书已正确安装到钥匙串访问应用程序中（见图 E-19）。单击“继续”。

![](img/aab2d775c46f70cd606f2e58e2521324_523_1.png)

图 E-18

![](img/aab2d775c46f70cd606f2e58e2521324_524_0.png)

图 E-19

在钥匙串访问应用程序中，选择登录钥匙串，并查找名为 iPhone Developer: your name 的证书（见图 E-20）。如果你能看到它，则说明你的证书已正确安装。

![](img/aab2d775c46f70cd606f2e58e2521324_524_1.png)

图 E-20

你现在几乎已经准备好将 iPhone 应用程序部署到你的 iPhone 或 iPod Touch 上。单击“继续”（见图 E-21）。

![](img/aab2d775c46f70cd606f2e58e2521324_525_0.png)

单击“完成”关闭对话框。

在 Xcode 中，找到 Active SDK 项。如果此项尚未在工具栏上，请选择 View → Customize Toolbar 并将其添加到工具栏。然后，在 Active SDK 下，选择当前连接到 Mac 的设备的 OS 版本号。就我而言，我的 iPhone 运行的是较旧的 iPhone OS 2.0，因此我选择了 `iPhone Device (2.0)`（见图 E-22）。

![](img/aab2d775c46f70cd606f2e58e2521324_525_1.png)

按 Command-R 运行应用程序。系统会提示你允许访问保存在钥匙串中的证书。单击 Allow（或 Always Allow）以继续签名（见图 E-23）。

![](img/aab2d775c46f70cd606f2e58e2521324_526_0.png)

图 E-23

你的应用程序现在将部署到设备上。你可以在 Organizer 应用程序的 Summary 选项卡中查看其进度（见图 E-24）。

![](img/aab2d775c46f70cd606f2e58e2521324_526_1.png)

图 E-24

应用程序部署到设备上后，它将自动启动。你可以通过单击 Organizer 应用程序的 Screenshot 选项卡来捕获设备的屏幕截图（见图 E-25）。

![](img/aab2d775c46f70cd606f2e58e2521324_527_0.png)

图 E-25

## 小结

在本附录中，你已经了解了将应用程序部署到你的 iPhone 或 iPod Touch 所需的各种步骤。虽然步骤数量看起来可能令人生畏，但实际上这是一个相当直接的过程。iPhone Developer 计划允许你为测试目的配置最多 100 台设备。设备配置完成后，你可以使用开发证书将应用程序部署到该设备上。

## 索引

## 索引

~（波浪号）, 302
加速度计, 377–382
访问数据, 379–382
轴, 378–379
accelerometer:didAccelerate: 事件, 382
访问权限 (Objective-C), 458
访问器, 63
操作表, 80–82
操作
编码, 62–64
创建, 52–58, 445–448
定义, 64–65
实现, 65–67
链接到视图, 173–175
输出口, 连接, 65
视图控制器, 链接, 58–61
设备被摇动时, 389
Add Child 按钮, 270
Add Sibling 按钮, 269
AddCountry 视图, 221
仿射变换, 343
CGAffineTransform 数据结构, 344
警告视图, 77–80
alloc 关键字 (Objective-C), 467
allTouches 方法, 319
动画, 336

弹跳球, 337–342
曲线, 179
NSTimer 类, 336
旋转, 343, 345–347
缩放, 343, 347
图像序列, 347–349
切换视图, 178–180
定时器, 触发间隔秒数, 342
变换视图, 343–347
过渡, 107–108, 178–180
平移, 343, 344–345
视图, 89
视觉变化, 342–343
animationDuration 属性, 349
应用程序文件夹, 301–302
应用程序偏好设置, 263. 另请参见 偏好设置
创建, 264–268
修改, 269–273
applicationDidFinishLaunching: 方法, 200
applicationFrame, 135
应用程序
后台, 19–20, 21
调试
断点, 432–434
文档, 435–436
错误, 429–430
NSLog, 434–435
运行时异常, 432
警告, 430–432

