

## CHAPTER 1
什么是 Cocoa？

其中一个最大的区别是，在 iOS 中，Cocoa 应用程序用户界面中出现的对象看起来和行为方式与在 Mac OS 上运行的 Cocoa 应用程序中的对应对象不同。常见的例子有文本视图、表格视图和按钮。此外，两个平台上 Cocoa 应用程序的事件处理和绘图模型也存在显著差异。以下各节解释了这些及其他差异的原因。

你可以通过三种方式向应用程序的用户界面添加 UIKit 对象：

- 使用 Interface Builder 开发应用程序将窗口、视图和其他对象从对象库中拖拽出来。
- 以编程方式创建、定位和配置框架对象。
- 通过子类化 UIView 或继承自 UIView 的类来实现自定义用户界面对象。

# UIKit 类概述

与 AppKit 一样，UIKit 框架的类最终都继承自 NSObject。图 1-9 以继承关系展示了 UIKit 框架的类。

## CHAPTER 1
## 什么是 Cocoa？

### 图 1-9 UIKit 类层次结构

![](img/0c5ea7638a6e08e6bdc6bc222975f6ee_45_0.png)

## CHAPTER 1
## 是 Cocoa？

与 AppKit 一样，基础响应者位于最大的 UIKit 类的根部。Responder 还定义了事件处理方法和响应者链的接口和默认行为（如果有），响应者链是一个可能处理事件的对象链。当用户用手指滚动表格视图或在虚拟键盘上触摸按键时，UIKit 生成一个事件，该事件沿响应者链向上传递，直到某个对象处理它。响应者对象——应用程序（UIApplication）、窗口（UIWindow）和视图（UIView）——都直接或间接继承自 Responder。

与 UIKit 不同，Cocoa 确实使用了 cells。在 UIKit 中——所有继承自 UIControl 的对象——都不需要 cells 来执行其主要角色：向目标发送动作消息。UIKit 定义了一组用于控件的事件类型；例如，一个按钮（UIButton）向目标发送动作消息，UIControl 方法将动作与一个或多个控件事件关联。当其中一个事件发生时，控件会处理它。

UIKit 框架大量使用了委托，这是 UIKit 的另一种设计模式。然而，UIKit 对委托的实现是不同的。UIKit 不是使用非正式协议，而是使用带可能代理方法标记的正式协议。

> 注：有关 UIKit 和 AppKit 中目标-动作机制的完整描述，请参阅“Target-Action Mechanism”（第 182 页）。要了解有关委托和协议的更多信息，包括正式和非正式协议，请参阅“Delegates and Data Sources”（第 176 页）和“Protocols”（第 59 页）。

# 应用程序协调

在 iOS 上运行的每个应用程序都由一个单例应用程序对象管理，该对象的工作几乎与全局 UIApplication 对象的相同。UIApplication 对象控制事件循环，跟踪应用程序的窗口和视图，并将传入事件分发给适当的响应者对象。

UIApplication 还接收系统级和应用程序级事件的通知。其中许多事件会传递给其委托，允许其在应用程序启动和终止时注入应用程序特定的行为，以响应低内存警告和时间变化，并处理其他任务。

# 事件和绘图模型的差异

在 Mac OS X 中，鼠标和键盘生成大多数用户事件。AppKit 使用 NSEvent 对象来封装这些事件。在 iOS 中，是用户在屏幕上的手指移动生成事件。UIKit 也有一个类 UIEvent 来表示这些事件。手指触摸或更多触摸可以形成一个离散事件——例如手势。UIEvent 对象包含一个或多个表示触摸的对象（UITouch）。在平台上将事件分发和派发给可以处理它们的对象的模型几乎相同。然而，要处理一个事件，一个对象必须考虑到该事件指定的触摸序列。

UIKit 具有手势识别器，可自动检测触摸。手势识别器识别一系列触摸，当它识别出手势时，向目标发送动作消息。UIKit 为滑动、旋转和拖拽等手势提供了现成的手势识别器。你也可以创建自定义手势识别器来检测应用程序特定的手势。

AppKit 和 UIKit 的绘图模型相似。动画已集成到 UIKit 绘图实现中。UIKit 以编程方式直接提供的软件绘图功能与 AppKit 相比更有限。框架提供了贝塞尔路径、PDF 生成以及未附加的线条和矩形绘图类和函数（通过 Graphics.h 中的函数）。你使用 UIColor 对象在当前图形上下文中设置颜色，并使用 UIImage 对象表示和封装它们。对于更复杂的绘图，应用程序必须使用 Core Graphics 或 OpenGL ES。

# 通用用户界面类

iOS 接口上的对象在视觉上与 Mac X 用户界面上的对象不同。由于设备的特性——具体来说是较小的尺寸以及使用手指而不是鼠标和键盘进行操作——iOS 中的用户对象通常更大（以便成为触摸的足够目标），同时又能高效利用屏幕空间。这些对象有时基于完全不同类型的视觉和触觉模拟。例如，考虑日期选择器对象，它由 UIKit 和 AppKit 框架都定义的类实例化。在 Mac OS X 中，日期选择器看起来像：

![](img/0c5ea7638a6e08e6bdc6bc222975f6ee_45_0.png)

| Day | Value |
| --- | --- |
| Mon | 1 |
| Tue | 2 |
| Wed | 3 |
| Thu | 4 |
| Fri | 5 |
| Sat | 6 |
| Sun | 7 |

| Day | Value |
| --- | --- |
| Mon | 29 |
| Tue | 30 |
| Wed | 31 |

| Day | Value |
| --- | --- |
| Today | 54 |

| Day | Value |
| --- | --- |
| Jan | 55 |

| Day | Value |
| --- | --- |
| Feb | 56 |

| Day | Value |
| --- | --- |
| Mar | 57 |

| Day | Value |
| --- | --- |
| Sun | 57 |

| Day | Value |
| --- | --- |
| Mon | 58 |
| Tue | 59 |
| Wed | 60 |
| Thu | 61 |
| Fri | 62 |
| Sat | 63 |
| Sun | 64 |

| Day | Value |
| --- | --- |
| Mon | 65 |
| Tue | 66 |
| Wed | 67 |
| Thu | 68 |
| Fri | 69 |
| Sat | 70 |
| Sun | 71 |

| Day | Value |
| --- | --- |
| Mon | 72 |
| Tue | 73 |
| Wed | 74 |
| Thu | 75 |
| Fri | 76 |
| Sat | 77 |
| Sun | 78 |

| Day | Value |
| --- | --- |
| Mon | 79 |
| Tue | 80 |
| Wed | 81 |
| Thu | 82 |
| Fri | 83 |
| Sat | 84 |
| Sun | 85 |

| Day | Value |
| --- | --- |
| Mon | 86 |
| Tue | 87 |
| Wed | 88 |
| Thu | 89 |
| Fri | 90 |
| Sat | 91 |
| Sun | 92 |

| Day | Value |
| --- | --- |
| Mon | 93 |
| Tue | 94 |
| Wed | 95 |
| Thu | 96 |
| Fri | 97 |
| Sat | 98 |
| Sun | 99 |

| Day | Value |
| --- | --- |
| Mon | 100 |
| Tue | 101 |
| Wed | 102 |
| Thu | 103 |
| Fri | 104 |
| Sat | 105 |
| Sun | 106 |

## CHAPTER 1
## 什么是 Cocoa？

# Cocoa 框架

## CHAPTER 1
## 什么是 Cocoa？

- **工具栏、导航栏、分栏视图和视图。** ViewController 是一个用于管理工具栏、导航栏、分栏视图和视图的类。UIKit 包含用于创建、观察和响应低内存警告的子类。应用程序使用工具栏和导航栏来管理视图；你使用工具栏（UIToolbar）在应用程序的不同模式或视图之间切换，以显示执行相对于当前视图的某些操作的一组功能。你使用导航栏（INavigationBar）来管理视图序列；例如，邮件应用程序使用导航栏从账户导航到文件夹再到单个消息。在 iPad 上，应用程序使用 UISplitViewController 来呈现主-细节界面。

# 文本

用户可以通过文本视图（UITextView）或文本字段（UITextField）在 iOS 应用程序中输入文本。这些类采用 UITextTraits 来指定在用户使用文本输入框时呈现的虚拟键盘的外观和行为。应用程序可以使用 NSStringDrawing 在视图中绘制文本，NSStringDrawing 是 NSString 类的一个分类。通过 UIFont 类可以指定所有对象中文本的字体特征，包括表格单元、导航栏和标签。

自行进行布局和字体管理的应用程序可以采用 UITextField 并使用相关类与 iOS 的文本系统通信。

# 比较 AppKit 和 UIKit 类

AppKit 和 UIKit 是为不同平台设计的 Cocoa 框架，一个用于 Mac OS X，另一个用于 iOS。由于这种亲和性，许多每个框架中的类具有相似的名称并不令人惊讶；在大多数情况下，前缀（“NS”“UI”）是唯一的名字区别。名称相似的类履行相似的角色，但存在差异。这些差异可能是范围、继承或设计方面的。一般来说，UIKit 类的方法比其 AppKit 对应类更少。

表 1-1 列出了每个框架中主要类的差异。

| Classes | Comparison |
| --- | --- |
| NSApplication | 这些类的首要角色在很大程度上非常相似。它们提供一个单例对象来设置应用程序的显示环境和视图循环，分发事件，并在发生应用程序特定事件（例如启动和终止）时通知委托。然而，NSApplication 类执行 iOS 应用程序不可用的功能（例如管理应用程序挂起、重新激活和隐藏）。 |

