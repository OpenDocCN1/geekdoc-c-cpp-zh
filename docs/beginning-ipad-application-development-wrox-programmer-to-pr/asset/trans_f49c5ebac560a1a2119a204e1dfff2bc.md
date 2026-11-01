
## DiT4Edit: 图像编辑的可扩展扩散 Transformer

Kunyang Han1,2 · Lv Tang2 · Qi Chu2 · Zongxin Yang2 · Junjing Guo2 · Bin Liu2 · Zhiyuan Zhao2 · Zhenchao Tang2 · Nenghai Yu2

1 浙江大学 2 中国科学技术大学

通讯作者: binliu@ustc.edu.cn; yunh@ustc.edu.cn

**摘要。** 扩散 Transformer (DiT) 在图像生成领域表现出色，但在图像编辑领域尚未充分探索。在本文中，我们提出了一个简单而强大的可扩展 DiT 框架，用于图像编辑。我们通过直接以文本条件作为输入来统一不同的编辑任务，并设计了一种新颖的互注意力机制来促进文本与图像令牌之间的交互。考虑到编辑任务对细节保持的高要求，我们提出的模型 (a) 有效处理高频细节的保留，(b) 全面解决多轮编辑中的累积误差问题，以及 (c) 在真实编辑场景中实现卓越的鲁棒性和可扩展性。大量实验证明，我们的方法在定性和定量评估中均达到了最先进水平。

**关键词: 扩散 transformers · 图像编辑 · 互注意力**

![](img/744c5ec15e15ca7891c98be71dc25d13_526_0.png)

**图 1:** DiT4Edit、Adobe Firefly、InstructPix2Pix、UltraEdit 和 MGEdit 在简单多轮编辑和真实局部编辑场景下的定性比较。

### 1 引言

近年来，随着扩散模型的出现，图像生成领域经历了深刻的范式转变[27, 40, 42]。尤其是扩散 Transformer (DiT) [35] 的引入，代表了一次关键的理论演进，将扩散模型中的传统 U-Net 骨干网络[41] 替换为基于 Transformer 的架构。这一变化之所以重要，不仅仅因为它是一种架构上的替代；它构成了向可扩展且灵活的统一框架的根本转变。通过利用 Transformer 架构，DiT 实现了显著的可扩展性，并受益于大规模预训练，使其成为广泛生成应用中通用且强大的骨干网络。

然而，DiT 在图像生成中的成功并未平滑地迁移到图像编辑领域。图像生成和图像编辑之间的一个根本区别在于条件机制。在图像编辑中，条件不仅包括简单的类别标签或文本描述，还包括输入图像，而输入图像通常包含需要与用户指令结合考虑的高频细节。这些额外的复杂性使得将 DiT 直接应用于图像编辑任务变得颇具挑战。尽管诸如基于 UNet 的图像编辑方法[3, 4, 13, 15, 16] 以及最近基于 DiT 的尝试[7, 44] 探索了这一方向，但现有方法通常在编辑保真度、多轮稳定性和真实场景的泛化能力方面存在不足。我们深入研究了这些挑战，确定了三个核心问题：

- 1. **高频保留。** 在编辑过程中保留图像的高频细节，对于保持高质量的编辑效果至关重要。然而，Autoencoder (AE) 在对输入图像进行下采样时通常存在高频信息丢失的问题。因此，在生成过程中需要额外的高频补偿机制。现有方法通常通过将输入图像直接馈送到当前采样步骤来缓解此问题[22]，但这种做法导致交互不足，并且限制了模型控制输入条件的能力。

- 2. **多轮累积误差。** 多轮编辑要求模型在前一轮编辑结果的基础上进行迭代改进，而现有方法往往在传播过程中引入误差和噪声。

## 问题 2 的答案

三个事件是

- `motionBegan:`
- `motionEnded:`
- `motionCancelled:`

## 第 14 章 练习解答

### 问题 1 的答案

三种方式是：SOAP 1.1/1.2、HTTP GET 和 HTTP POST。

### 问题 2 的答案

三个关键事件是：

- `connection:didReceiveResponse:`
- `connection:didReceiveData:`
- `connectionDidFinishLoading:`

### 问题 3 的答案

NSXmlParser 类在解析 XML 文档内容时触发以下事件：

- `parser:didStartElement:namespaceURI:qualifiedName:attributes:`
- `parser:foundCharacters:`
- `parser:didEndElement:namespaceURI:qualifiedName:`

## 第 15 章 练习解答

### 问题 1 的答案

类是 GKPeerPickerController。

### 问题 2 的答案

类是 GKSession。

### 问题 3 的答案

从 `GKVoiceChatService` 类调用 `startVoiceChatWithParticipantID:error:` 方法。

### 问题 4 的答案

在发起方，调用 `GKVoiceChatClient` 协议中定义的 `voiceChatService:sendData:toParticipantID:` 方法。

在接收方，调用 `GKVoiceChatClient` 协议中定义的 `receivedData:fromParticipantID:` 方法。

## 第 16 章 练习解答

### 问题 1 的答案

类是 `NSNetService`。

### 问题 2 的答案

类是 `NSNetServiceBrowser`。

### 问题 3 的答案

方法名是 `netServiceBrowser:didFindService:moreComing:`。

### 问题 4 的答案

方法名是 `netServiceBrowser:didRemoveService:moreComing:`。

## 第 17 章 练习解答

### 问题 1 的答案

两个证书是开发证书和提供者应用程序的 SSL 证书。

### 问题 2 的答案

这是为了确保你拥有该证书的私钥和公钥对。

### 问题 3 的答案

方法是 `registerForRemoteNotificationTypes:`。

### 问题 4 的答案

设备令牌用于唯一标识推送通知的接收者，并且 APNs 服务器需要它。

### 问题 5 的答案

事件是 `application:didReceiveRemoteNotification:`。

## 第 18 章 练习解答

### 问题 1 的答案

属性是 `showsUserLocation`。

### 问题 2 的答案

协议是 `MKMapViewDelegate`。

### 问题 3 的答案

方法是 `startUpdatingLocation`。

### 问题 4 的答案

方法是 `startUpdatingHeading`。

### 问题 5 的答案

类是 `MKReverseGeocoder`。

![](img/744c5ec15e15ca7891c98be71dc25d13_530_0.png)

## 在 Xcode 中导航

Xcode 是 Apple 用于开发 Mac OS X、iPhone 和 iPad 应用程序的集成开发环境（IDE）。它是一套应用程序，包括一组编译器、文档和 Interface Builder（在附录 C 中讨论）。

使用 Xcode，你可以在智能文本编辑器的舒适环境中构建你的 iPad 应用程序，并结合许多不同的工具来帮助调试你的 iPad 应用程序。如果你是 Xcode 的新手，本附录可以作为快速入门的有用指南。附录 C 更详细地介绍了 Interface Builder。

### 启动 Xcode

启动 Xcode 的最简单方法是 在 Spotlight 的文本框中输入 **Xcode**。或者，你可以通过导航到 `/Developer/Applications/` 文件夹并双击 Xcode 图标来启动 Xcode。

> > **注意**  为了方便，你还可以将 Xcode 图标拖到 Dock 中，这样以后就可以直接从 Dock 启动它。

在撰写本文时，可用的 Xcode 版本是 3.2.2。

### 支持的项目类型

Xcode 支持构建 iPhone、iPad 和 Mac OS X 应用程序。当你在 Xcode 中创建新项目时（通过选择 File ➜ New Project），你会看到如图 B-1 所示的新建项目对话框。

如你所见，你有两个主要的项目类型可供创建（iPhone OS 和 Mac OS X）。在 iPhone OS 类别下，你有 Application 和 Library 项目。

![](img/744c5ec15e15ca7891c98be71dc25d13_531_0.png)

### 图 B-1

选择 Application 项目，你将看到可以创建的所有不同项目类型，如下所示：

- 基于导航的应用程序（仅 iPhone）
- OpenGL ES 应用程序（iPhone 和 iPad）
- 基于拆分视图的应用程序（仅 iPad）
- 标签栏应用程序（iPhone 和 iPad）
- 实用工具应用程序（仅 iPhone）
- 基于视图的应用程序（iPhone 和 iPad）
- 基于窗口的应用程序（iPhone 和 iPad）

对于基于导航的应用程序、基于拆分视图的应用程序、实用工具应用程序和基于窗口的项目类型，你可以选择使用 Core Data 进行存储。

> 注意 Core Data 是 Cocoa API 的一部分，最早在 iPhone SDK 3.0 中引入。它基本上是一个框架，用于在不担心存储和检索细节的情况下操作数据。Core Data 超出了本书的范围。

选择你想要创建的项目类型并单击 Choose 按钮。然后命名项目。

当项目创建后，Xcode 会显示构成你的项目的所有文件（见图 B-2）。

### 图 B-2

![](img/744c5ec15e15ca7891c98be71dc25d13_532_0.png)

Xcode 窗口分为五个部分：

- **工具栏：** 显示常用操作的按钮。
- **组和文件列表：** 显示项目中的文件。文件被分组到文件夹和类别中以便更好地管理。
- **状态栏：** 显示当前操作的状态信息。
- **详细信息视图：** 显示在“组和文件列表”部分中选定的文件夹和组中包含的文件。
- **编辑器：** 显示适当的编辑器，显示当前选定的文件。

要编辑代码文件，请单击文件名以打开适当的编辑器。例如，如果你单击 .h 或 .m 文件，则会显示可编辑源代码的代码编辑器（见图 B-3）。单击 .plist 文件，XML 属性列表编辑器将启动（见图 B-4）。

### 自定义工具栏

Xcode 窗口包含工具栏部分，你可以在其中放置常用项目以便快速访问。默认情况下，以下项目放置在工具栏中：

- **概览：** 使你能够选择目标设置，例如活动 SDK（iPhone OS 版本和设备与模拟器）以及活动配置（Debug 或 Release）。
- **操作：** 指定可对所选项目执行的操作。
- **断点：** 将 Build and Run 项目（见下一项）切换为 Build and Debug，以便你可以将调试器附加到应用程序。

