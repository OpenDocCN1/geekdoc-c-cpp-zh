
加入后，您可以发布新消息并回复其他用户发布的消息。您可以在 Web 上随时阅读消息。如果您希望将特定论坛的新消息通过电子邮件发送给您，请在论坛列表中点击论坛名称旁边的“订阅此论坛”图标。

有关如何使用 Wrox P2P 的更多信息，请务必阅读 P2P 常见问题解答，以了解论坛软件的工作原理以及 P2P 和 Wrox 书籍的许多常见问题。要阅读常见问题解答，请点击任何 P2P 页面上的 FAQ 链接。

## 第一部分：入门

- 第 1 章：开始 iPhone 编程
- 第 2 章：编写您的第一个 Hello World！应用程序
- 第 3 章：Outlets、Actions 和 View Controllers
- 第 4 章：探索视图
- 第 5 章：键盘输入
- 第 6 章：屏幕旋转

## 1 开始 iPhone 编程

### 本章您将学到什么

- 如何获取 iPhone SDK
- iPhone SDK 包含的组件
- 开发工具的功能 — Xcode、Interface Builder、iPhone Simulator
- iPhone Simulator 的功能
- iPhone OS 的架构
- iPhone SDK 的框架
- iPhone 的限制和特性

欢迎来到 iPhone 编程的世界！您现在手持本书的事实表明，您对开发 iPhone 应用程序的想法着迷，并希望加入那些数以万计的开发者的行列，他们的应用程序已经部署在 App Store 中。

正如古老的中国谚语所说，“要完成你的使命，先磨利你的工具。”成功的编程首先要求你很好地了解你的工具。事实上，对于 iPhone 编程来说，这一点再正确不过了——在你甚至开始之前，你需要了解相当多的工具。因此，本章的目标是向你展示你需要了解的各种相关工具和信息，以便加入 iPhone 开发的行列。

不用多说，是时候开始工作了。

### 获取 iPhone SDK

要为 iPhone 或 iPod Touch 开发，您首先需要在 http://developer.apple.com/iphone/program/start/register/ 注册为注册的 iPhone 开发者。注册是免费的，并为您提供访问 iPhone SDK 以及开始所需的有用资源的权限。

注册后，您可以下载 iPhone SDK（见图 1-1）。

![](img/aab2d775c46f70cd606f2e58e2521324_33_0.png)

图 1-1

在安装 iPhone SDK 之前，请确保满足以下系统要求：

- 仅支持 Intel Mac，因此如果您使用的是其他处理器类型（如较旧的 G4 或 G5 Mac），您就无缘了。
- 您已使用最新的 Mac OS X 版本更新了系统。

强烈建议使用 iPhone/iPod Touch 设备，但并非严格必要。要测试您的应用程序，您可以使用包含的 iPhone Simulator。但是，如果您想测试相机、加速度计等某些硬件功能，您将需要使用真实设备。

下载 SDK 后，继续安装（见图 1-2）。您将被要求接受一些许可协议，然后选择要安装 SDK 的目标文件夹。

![](img/aab2d775c46f70cd606f2e58e2521324_34_0.png)

图 1-2

如果您在安装阶段选择了默认设置，安装后您应该能够在 /Developer/Applications 文件夹中找到各种已安装的工具（见图 1-3）。

![](img/aab2d775c46f70cd606f2e58e2521324_34_1.png)

图 1-3

### iPhone SDK 的组件

iPhone SDK 包含一套开发工具，可帮助您为 iPhone 和 iPod Touch 开发应用程序。它包括：

- **Xcode** — 集成开发环境（IDE），允许您管理、编辑和调试项目。
- **Dashcode** — 集成开发环境（IDE），允许您开发基于 Web 的 iPhone 应用程序和 Dashboard 小部件。Dashcode 超出了本书的范围。
- iPhone Simulator — 提供软件模拟器在您的 Mac 上模拟 iPhone。
- Interface Builder — 提供可视化编辑器，用于设计 iPhone 应用程序的用户界面。
- Instruments — 分析工具，可帮助您实时优化应用程序。

下面的各节更详细地讨论每个工具。

### Xcode

如前所述，所有 iPhone SDK 中的工具都安装在 `/Developer/Applications` 文件夹中（使用默认设置时）。其中一个工具是 Xcode。

要启动 Xcode，请双击 Xcode 图标（参见图 1-3）。或者，走捷径使用 Spotlight：只需在搜索框中输入 Xcode，Xcode 应该位于顶部命中位置。

启动 Xcode 后，您会看到欢迎屏幕，如图 1-4 所示。

![](img/aab2d775c46f70cd606f2e58e2521324_35_0.png)

图 1-4

使用 Xcode，您可以开发不同类型的 iPhone 和 Mac OS X 应用程序（见图 1-5）。

![](img/aab2d775c46f70cd606f2e58e2521324_36_0.png)

**图 1-5**

Xcode 中的 IDE 提供了许多工具和功能，使您的开发生活变得更加轻松。其中一个功能是代码补全（见图 1-6），它会显示一个弹出列表，显示可用的类和成员（例如方法、属性等）。

![](img/aab2d775c46f70cd606f2e58e2521324_37_0.png)

图 1-6

> **注意** 有关 Xcode 中一些最常用的功能的更全面描述，请参阅附录 B。

### iPhone Simulator

iPhone Simulator（见图 1-7）是 iPhone SDK 中包含的一个非常有用的工具，您可以在不使用实际 iPhone/iPod Touch 的情况下使用它来测试您的应用程序。iPhone Simulator 位于 /Developer/iPhone OS/Platforms/iPhoneSimulator.platform/Developer/Applications/ 文件夹中。大多数情况下，您不需要直接启动 iPhone Simulator — 在 Xcode 中运行（或调试）您的应用程序会自动启动 iPhone Simulator。Xcode 会自动将应用程序安装到 iPhone Simulator 上。

### iPhone Simulator 不是仿真器

iPhone Simulator 是一个模拟器，而不是仿真器。那么区别是什么呢？嗯，模拟器试图模仿真实设备的行为。就 iPhone Simulator 而言，它模拟实际 iPhone 设备的真实行为。然而，模拟器本身使用安装在 Mac 上的各种库（如 QuickTime）来执行其渲染，以便效果看起来与实际 iPhone 相同。此外，在模拟器上测试的应用程序被编译为 x86 代码，即模拟器理解的字节码。

相比之下，仿真器仿真真实设备的工作方式。在仿真器上测试的应用程序被编译为真实设备实际使用的字节码。仿真器通过将字节码翻译成可在运行仿真器的主机计算机上执行的形式来执行应用程序。

理解模拟和仿真之间细微差别的良好方法是：想象你试图说服一个孩子玩刀是危险的。为了模拟这一点，你假装用刀割伤自己并痛苦地呻吟。为了仿真这一点，你拿起一把刀并真正割伤自己。

![](img/aab2d775c46f70cd606f2e58e2521324_38_0.png)

图 1-7

iPhone Simulator 可以模拟不同版本的 iPhone OS（见图 1-8）。如果您需要支持平台的旧版本以及在特定 OS 版本上测试和调试应用程序报告的错误，此功能非常有用。

![](img/aab2d775c46f70cd606f2e58e2521324_38_1.png)

图 1-8

### iPhone Simulator 的功能

iPhone Simulator 模拟了真实 iPhone 或 iPod touch 设备的各种功能。您可以在 iPhone Simulator 上测试的功能包括：

- 屏幕旋转 — 左、上、右
- 手势支持：
    - Tap
    - Touch and Hold
    - Double Tap
    - Swipe
    - Flick
    - Drag
    - Pinch
- 低内存警告模拟

然而，iPhone Simulator 作为真实设备的软件模拟器，确实存在其局限性。iPhone Simulator 上不可用的功能包括：

- 获取位置数据 — 它仅返回固定的坐标，例如北纬 37.3317，经度 122.0307 西
- 进行电话呼叫
- 访问加速度计
- 发送和接收短信
- 从 App Store 安装应用程序
- 相机
- 麦克风
- OpenGL ES 的多个功能

值得注意的是，iPhone Simulator 的速度与您的 Mac 的性能更紧密地相关，而与实际设备的性能无关。因此，重要的是您在真实设备上测试您的应用程序，而不是完全依赖 iPhone Simulator 进行测试。

尽管 iPhone Simulator 有局限性，但它确实是一个有用的工具，可以让您测试应用程序。话虽如此，在将应用程序部署到 App Store 之前，在真实的 iPhone 或 iPod touch 设备上测试应用程序是必不可少的。
