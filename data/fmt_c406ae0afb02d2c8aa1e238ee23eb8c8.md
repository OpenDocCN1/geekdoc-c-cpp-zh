
Foundation 为 Cocoa 编程引入了若干范式和策略，以确保在某些情况下项目对象之间具有一致的行为和预期：

- **对象的保留与释放。** Objective-C 运行时和 Foundation 为 Cocoa 程序提供了两种方式，以确保对象在需要时持久存在，并在不再需要时释放它们。Objective-C 2.0 引入的垃圾回收会自动跟踪并分解你不再需要的对象，从而释放内存。Foundation 仍然提供传统的内存管理方法。它确立了对象所有权策略，由其负责释放它们创建、复制或显式保留的对象。有关垃圾回收和显式内存管理的更多信息，请参阅[对象的保留与释放]。

运行 iOS 的应用程序不可用垃圾回收。

- **可变类。** Foundation 中的各种值类和容器类都有其不可变类的可变变体，可变类是不可变类的子类。如果你需要动态更改此类对象的值或成员，可以创建一个可变类的实例。由于它继承自不可变，你可以在接收不可变类型的方法传递可变实例。有关对象可变性的更多信息，请参阅“对象可变性”（第 90 页）。

- **类簇。** 类簇是一个私有子类的集合，抽象类作为接口。取决于上下文（特别是你用于创建对象的方法），将返回一个优化类的实例。例如，`NSString` 和 `NSMutableString` 作为针对不同存储类型的优化私有子类实例的代理。多年来，具体类的集合发生了多次变化而没有破坏应用程序。有关类簇的更多信息，请参阅“类簇”（第 95 页）。

- **通知。** 通知是 Cocoa 中的一种主要设计模式。它基于广播机制，允许对象（称为观察者）被另一个对象在用户或系统事件中所正在的操作或遭遇的情况。通知对象可能不知道观察者的存在或身份。通知有几种类型：同步、异步和分布式。Foundation 通知机制由 `NSNotificationCenter`、`NSNotificationQueue` 和 `NSDistributedNotificationCenter` 类实现。有关通知的更多信息，请参阅“通知”（第 190 页）。

## Foundation 类

Foundation 层次结构根于 `NSObject` 类，该类（结合 `NSObject` 和 `NSCopying` 协议）定义了基本的属性和行为。有关 `NSObject` 的进一步信息，请参见“根类”（第 66 页）。

Foundation 框架的其余部分由相关的类组以及一些单独类组成。表示字符串和字节数组等数据类型的类、存储其他对象的类、表示系统信息的类，以及类

# 第一章

## 什么是 Cocoa？

代表端口、线程和进程等系统实体。图 1-7 中的类层级结构图（为了打印目的，共分为三部分）描述了这些类构成的逻辑组以及它们的继承关系。蓝色阴影区域的类存在于 Mac OS 和 iOS 版本的 Foundation；灰色阴影区域的类仅存在于 Mac OS 版本。

### 图 1-7 Foundation 类层级结构

![](img/0c5ea7638a6e08e6bdc6bc222975f6ee_31_0.png)

## Objective-C Foundation 续接

| 操作系统服务 |
|--- |
| `NSError` |
| `NSHost` |
| `NSService` |
| `NSNetworkBrowser` |
| `NSPhotography` |
| `NSProcessInfo` |
| `NSLoop` |
| `NSSpellServer` |
| `NSTextCheckingResult` |
| `NSTimer` |
| `NSUserDefaults` |
| `NSBundle` |
| `NSFileHandle` |
| `NSFileManager` |
| `NSMetadata` |
| `NSMetadataQuery` |
| `NSMetadataQueryAttributeValueTuple` | `NSStream` |
| `NSMetadataQueryResultGroup` | OutputStream |
| `NSObject` |
| URL |
| `NSCHTTPURLResponse` |
| `NSHTTPCookie` |
| `NSHTTPCookieStorage` |
| `NSURL` | `NSURLAuthorizationChallenge` |
| `NSCache` |
| `NSConnection` |
| `NSCredential` |
| `NSDataStorage` |
| `NSURLDownload` |
| `NSURLProtectionSpace` |
| `NSProtocol` | `NSMutableURLRequest` |
| `NSRequest` |
| `NSResponse` | `NSHTTPURLResponse` |
| 进程间通信 |
|--- |
| `NSPipe` | `NSMachPort` |
| `NSPort` | `NSMessagePort` |
| `NSPortMessage` | `NSocketPort` |
| `NSPortNameServer` | `NSMachBootstrapNameServer` | `NSocketPortNameServer` |
| 锁/线程 |
|--- |
| `NSConditionLock` |
| `NSDistributedLock` |
| `NSLock` |
| `NSOperation` | `NSBlockOperation` |
| `NSOperationQueue` | `NSInvocationOperation` |
| `NSRecursiveLock` |
| `NSTask` |
| `NSThread` |

## Objective-C Foundation 续接

| 通知 | |
| --- | --- |
| `NSNotification` | `NSDributedNotificationCenter` |
| `NSNotificationCenter` | |
| `NSNotificationQueue` | |
| 归档与序列化 | |
| --- | --- |
| `NSCoder` | `NSArchiver` |
| `NSPropertyListSerialization` | `NSKeyArchiver` |
| | `NSKeyedUnarchiver` |
| | `NSPortCommand` |
| | `NSDataArchiver` |
| Objective-C 语言 | |
| --- | --- |
| `NSAssertionHandler` | |
| `NSAutoreleasePool` | |
| `NSClassDescription` | |
| `NSException` | |
| `NSGarbageCollector` | |
| `NSInvocation` | |
| `NSMethodSignature` | |
| `NSUndoManager` | |
| 脚本 | |
| --- | --- |
| `NSApplicationEventDescriptor` | `NSScriptClassDescription` |
| `NSApplicationEventManager` | `NSCCommand` |
| `NSScript` | `NSCountCommand` |
| | `NSCreateCommand` |
| `NSPitionalSpecifier` | `NSSelectCommand` |
| `NSCoercionHandler` | `NSMoveCommand` |
| `NSScriptCommand` | `NSSetCommand` |
| `NSScriptDescription` | `NSIndexSpecifier` |
| `NSScriptExecutionContext` | `NSNameSpecifier` |
| | `NSPropertySpecifier` |
| `NSObjectSpecifier` | `NSRandomSpecifier` |
| `NSRangeSpecifier` |
| | `NSValueSpecifier` |
| `NSiteRegistry` | `NSUniqueSpecifier` |
| `NSWhitelistTest` | `NSProxyTest` |
| | `NSLogicalTest` |
| | `NSSpecifiedTest` |
| 分布式对象 | |
| --- | --- |
| `NSConnection` | |
| `NSDistantObjectRequest` | |
| `NSDistantObject` | |
| `NSProtocolChecker` | |

这些图表逻辑上将 Foundation 框架的类分类（并指出了其他关联）。特别重要的是实例值为对象和集合的类。

### 值对象

值对象封装了原始类型的值，包括字符串、数字（整数和浮点数）、日期，甚至是结构。它们调解对这些值的访问，并以合适的方式对其进行操作。当你比较同一类的值对象时，比较的是它们封装的值，而不是它们的指针值。值对象是其他对象（包括自定义对象）的属性。

当然，你可以在程序中直接使用标量和其他原始类型——毕竟在 Objective-C 中，在许多情况下使用标量是合理的。但在其他情况下，将这些值封装在对象中是有益的或必要的。例如，因为值对象是对象，你在运行时可以检测它们的类，确定要发送的消息，并执行其他可以使用对象完成的任务。集合对象（如数组和字典）的元素必须是对象。Cocoa 框架的大多数方法都接收并返回字符串值，而日期要求这些值被封装在对象中。（特别是对于字符串，你应该始终使用 `NSString` 对象而不是 C 字符串）。

值对象的某些类有可变和不可变变——例如，`NSData` 和 `NSString` 类。不可变对象封装的值在创建后无法修改，而可变对象封装的值可以被修改。（对象的可变性（第 90 页）详细讨论了可变和不可变对象。）

以下是常用值对象的类：

- `NSData` 实例封装了字节。
- `NSNumber`（`NSString` 的子类）封装了整数、浮点数和双精度。
- Date 类提供了面向对象的字节存储，用于计算。
- CharacterSet 是一个字符的集合，用于显示。
- DateComponents 和 Locale 提供了基于时间的格式。
- UTF-8 是一个存储对象的无序集合，用于用户界面。

### 集合

这些图表逻辑上将 Foundation 框架的类分类（并指出了其他关联）。特别重要的是实例值为对象和集合的类。

集合是存储元素的有序对象。主要的集合类有不可变和可变变；为了这个目的，你需要 `NSMutableArray`。元素必须是对象，Foundation 定义了 iOS 和 Mac 通用的三个主要集合类：`NSArray`、`NSDictionary` 和 `NSSet`。关于保留、释放等相关术语，请参见“内存管理”（70 页）。

集合类提供了访问特定元素的方法。此外，还有特殊的枚举器对象（`NSEnumerator`），用于按顺序遍历集合。

主要的集合类根据它们使用的排序进行区分：

- 数组（`NSArray`）是使用零索引访问元素的有序集合。
- 字典（`NSDictionary`）是管理键值的集合；键是标识对象，由于这种键值方案，字典中的元素是无序的。在字典中，键必须唯一。
- 集合（`NSSet`）与数组类似，但它们提供元素的无序存储。换句话说，集合中元素的顺序并不重要。在 `NSSet` 中必须是唯一的；然而，`NSCountedSet`（`NSMutableSet` 的子类）实例可以包含同一个对象多次。

在 Mac OS 中，Foundation 框架包含了几个额外的类。`NSMapTable` 是一个类似于字典的可变类；但 `NSDictionary` 可以持有指针以及对象，并对其内容保持弱引用，NULL 值可以保持强引用或弱引用。`NSPinterArray` 是可以持有指针的数组。HashTable 是基于 `NSSet` 设计的，但它可以存储函数指针并提供不同的选项，特别是支持垃圾回收环境中的弱引用。

更多类和对象，请参见“集合编程主题”。

### Foundation 其他类别

Foundation 框架的其余类属于不同的类别，如图 1-7（第 32 页）所示。主要类别如下：

- 操作系统服务。许多 Foundation 类有助于访问操作系统的各种底层服务，同时让你不受操作系统特殊性的影响。例如，`NSProcessInfo` 可以查询应用程序运行的环境，`NSHost` 提供网络上主机系统的名称和地址。`NSUserDefaults` 提供了对系统全局（每主机）和每个用户默认值（偏好设置）数据库的程序接口。

## 什么是 Cocoa？

- **文件系统和 URL。** `NSFileManager` 为文件操作（如创建、删除和移动文件）提供了一致的接口；`NSFileHandle` 允许进行更低级的文件操作（例如在文件内查找）；`NSBundle` 在 bundle 中查找资源并动态加载其中某些资源（例如，nib 文件和代码）。你使用 `NSURL`... 来表示、访问和管理数据的 URL 源。

- **并发。** `NSThread` 用于创建多线程程序，并有各种锁类用于控制线程对访问的访问。你使用 `NSOperation` 和 `NSOperationQueue` 按照优先级和依赖关系来执行多个操作（并发或非并发）。通过 `NSTask`，你的程序可以派生一个进程来执行任务并监控其进度。

- **进程间通信。** 该类别中的大多数类代表了各种系统端口、套接字和服务器，这些对于实现低级 IPC 非常有用。`NSPipe` 代表一个 BSD 管道，它是进程之间单向的通信通道。

> 注意：这些类名在 iOS 版本中不存在。

- **网络。** `NSSystemService` 和 `NSServiceBrowser` 类支持零配置网络架构 Bonjour。Bonjour 是一个在 IP 网络上发布和浏览服务的强大系统。

- **通知。** 请参阅“基础范式与策略”（Foundation Paradigms and Policies）第 31 页中通知类的总结。

- **归档和序列化。** 该类别中的类使得对象分布和持久化成为可能。`NSCoder` 及其子类使用 `NSCoding` 协议，以与架构无关的方式表示数据对象，并使用类信息与数据一起存储。`NSKeyedarchiver` 和 `NSKeyedunarchiver` 提供了对对象和值进行编码以及对它们进行解码的方法，这种解码方式不依赖于编码方法的顺序。

- **Objective-C 类。** `NSException` 和 `NSAssertion` 提供了一种在代码中进行断言和处理异常的面对象方法。`NSInvocation` 是 Objective-C 消息的静态表示，你可以存储它并在后在另一个对象中调用消息；它被撤销管理器（UndoManager）和分布式对象系统使用。`NSMethodSignature` 记录类型信息，并用于方法转发。ClassDescription 是一个用于解码和查询类关系及属性的抽象类。

- **XML 处理。** 平台上的 Foundation 拥有 `XMLParser` 类，它是字符串解析器的面向对象实现，让你能够以事件驱动的方式处理 XML 数据。

- **谓词和表达式。** 谓词类——`NPredicate`、`NSCompoundPredicate` 和 `NSComparisonPredicate` 封装了用于获取或过滤对象的逻辑条件。`NSPrediction` 对象表示谓词中的表达式。

## 什么是 Cocoa？

适用于 iOS 的 Foundation 框架包含一个适用于 Mac OS X 的类子集。以下类类别仅存在于 Mac OS X 版本的 Foundation 中：

- *Spotlight 查询。* `NSMetadataItem`、`NSMetadataQuery` 以及相关的查询类封装了文件系统元数据，并使得查询这些元数据成为可能。

- *脚本化。* 该类别中的类帮助你的程序对 AppleScript 脚本和 Apple 事件命令做出响应。

- *分布式对象。* 你使用分布式对象类在同一台计算机上或网络上不同计算机的进程进行通信。这些类中的两个（`NSDistantObject` 和 `NSProtocolChecker`）的根类（`NSProxy`）与 Cocoa 中其他其他类的根类不同。

## AppKit (Mac OS X)

AppKit 是一个框架，包含了你在 Mac OS X 中实现图形化、事件驱动界面所需的所有对象；窗口、按钮、菜单、滚动条、文本字段——AppKit 为你处理所有细节，因为它高效地在屏幕上绘图、与硬件设备和缓冲区通信、清除绘制区域以及裁剪视图。AppKit 中的类数量起初看起来可能令人生畏。然而，大多数 AppKit 类都是你间接使用的支持类。它们允许你选择何时使用 AppKit：

- *使用 Interface Builder 创建从用户界面对象到应用程序控制对象的连接*，这些对象管理用户界面并协调用户之间的数据流。

- *通过编程实现用户界面*，你可能需要某些方法。这允许你选择何时使用 AppKit：

- *通过派生实现自己的类*，你可能需要了解其工作原理。

## AppKit 框架概述

AppKit 框架包含 125 个类，它们最终继承自 Foundation 类的 `NSObject`。图 1-8 显示了 AppKit 类的继承关系。

### 图 1-8 AppKit 类继承图

用户界面

Cocoa 绑定

*在框架中定义*

## 什么是 Cocoa？

从 Mac OS v10.5 开始，AppKit 的窗口和类支持了增强的动画功能。

`NSView` 是窗口中显示的所有对象的父类。所有子类都使用图形函数实现绘图；`drawRect:` 是你在创建新的 `NSView` 时需要覆盖的主要方法。
