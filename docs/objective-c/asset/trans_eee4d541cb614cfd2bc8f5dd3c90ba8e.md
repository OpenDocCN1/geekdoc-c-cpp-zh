
提供了在 iPhone 和 iPad 上构建 GUI 应用所需的类，以及许多其他框架，这些框架提供特定于网络服务、图形等方面的功能。就本书而言，我们将只关注 Foundation。这个框架很容易就成为 MacOS X 上所有框架中跨平台支持最广的。它可以在 MacOS X、iPhone 和 iPad 上的官方 Apple 版本中使用，也可以在 Linux、BSD UNIX 甚至 Windows 上以开源第三方实现的形式使用。其中一种实现使你能够在 MacOS X 上使用 Xcode 开发应用，并交叉编译生成 Windows 可执行文件。在许多方面，Foundation 框架比一些专门为此目的构建的标准库提供了更好的可移植性和更强的功能。

不过，由于目前 Apple 平台是 Objective-C 开发者最流行的平台，我主要关注这些平台上可用的特性。

## 在项目中使用框架

尽管这专门针对 MacOS X，我还是要简单讨论一下在自己项目中使用框架的主题，以便你在需要时知道如何处理它们。

Apple 提供的框架通常安装在 Xcode 的安装目录中，默认是 /Developer。在这个目录下，你会找到一个名为 Platforms 的目录。在 Platforms 目录内，你会为每个已安装 SDK 的不同开发平台找到一个目录。例如，如果你安装了 iPhone SDK，你会看到与 iPhone OS 对应的目录。如果没有安装，则只会看到与 MacOS X 对应的目录。

在 SDK 目录内，你会找到一条通向 System/Library/Frameworks 的路径。所有用于该特定 SDK 中特定平台的框架都位于此目录中。

### 添加框架

向项目添加框架非常简单。你只需右键单击或按住 Option 键单击要添加框架的目标，然后选择“Add ⇧ Existing Frameworks”。此时会弹出框架选择对话框，如图 11.1 所示。

此对话框允许你从已安装框架列表中选择要与当前选定目标链接的任何框架。

图 11.1

框架选择对话框。

- AGL.framework
- Accelerate.framework
- AddressBook.framework
- AppKit.framework
- AppKitScripting.framework
- AppleScriptKit.framework
- AppleScriptObjC.framework
- AppleShareClientCore.framework
- ApplicationServices.framework
- AudioToolbox.framework
- AudioUnit.framework
- Automator.framework
- CP437.dylib
- CP850.dylib
- CalendarStore.framework
- Carbon.framework
- Cocoa.framework
- Collaboration.framework
- CoreAudio.framework
- CoreAudioKit.framework
- CoreData.framework
- CoreFoundation.framework
- CoreLocation.framework

全部

名称

添加其他...

取消

### 包含头文件

请记住，仅仅与框架链接并不足以让你实际使用其中包含的类和代码。你还需要确保将适当的头文件包含到源文件中。回想你学习导入头文件时，通过将导入的头文件名放在 <> 中，告诉编译器搜索已链接的框架目录。这样做会使编译器搜索系统包含目录以及所有框架目录。

### 考虑垃圾回收

链接第三方框架时，一个重要的考虑因素是确保所涉及的框架支持你为项目选择的内存管理模型。并非所有框架都同时支持垃圾回收和引用计数内存管理。因此，在查看打算链接到项目的框架文档时，务必确保你链接的是与你选择的内存管理系统对应的正确版本。链接错误的版本将导致编译错误。

### 小结

在本章中，我向你介绍了框架的概念，并讨论了 Foundation 框架，它是 Objective-C 最接近标准库的东西。本书这一部分的其余内容将大量使用 Foundation 框架，因此，你对这个框架及其提供的内容有一个概念性了解非常重要。现在你有了这些背景信息，就能更好地为接下来的详细编码示例做好准备。

## 使用字符串

任何好的标准库都需要一个出色的字符串类，Objective-C 与 Foundation 也不例外。实际上，Foundation 框架提供了一个优秀的字符串类 NSString。与 Foundation 中的许多底层核心类一样，NSString 有一个不可变版本，以及一个名为 NSMutableString 的可变版本。这两个类在处理字符串值时为你提供了大量的功能。

### 理解字符串声明语法

尽管 NSString 和 NSMutableString 有许多可用的初始化器和工厂方法，但字符串在 Objective-C 中是非常常用的类，因此特意创建了一种语言结构，以便轻松声明字符串。该结构如清单 12.1 所示。

### 清单 12.1
### Objective-C NSString 快捷语法

```
NSString *someString = @"this is a string";
```

本质上，编译器知道只要遇到 @ 后跟双引号内的字符串，它就应该创建一个 static const NSString 对象来包含所提供的字符串。

任何两个声明完全相同字符串值（即使存储在不同的变量名中）都会指向同一个对象。因此，你可以将这些字符串用作键，例如，将一个字符串与另一个该字符串的实例进行比较时，无论是使用 -isEqual: 对象方法还是使用 == 运算符（它将比较指针的值），都会认为它们是相等的。

### 本章内容

- 使用 NSString 和 NSMutableString 类
- 理解格式化字符串
- 使用 Objective-C 特有的字符串声明语法

为了说明这一点，请查看清单 12.2。

### 清单 12.2
### 检查字符串常量相等性

```
NSString *string1 = @"this is a string";
NSString *string2 = @"this is a string"; // same object as string1
NSString *string3 = [NSString stringWithString:string1]; // makes new

assert(string1 == string2); // true
assert([string1 isEqual:string2]); // also true
assert([string1 isEqual:string3]); // true
assert(string1 == string3); // false
```

大多数情况下，你使用 Objective-C 字符串结构声明字符串，但在 NSString 和 NSMutableString 类上仍然有许多初始化器和工厂方法可用。表 12.1 显示了一些更常用的方法。

### 表 12.1 NSString 和 NSMutableString 工厂方法

| 方法 | 用途 |
|---|---|
| +string | 构造一个新的空字符串。 |
| +stringWithFormat: | 使用给定的 printf 风格格式说明符以及格式说明符所需的任何参数构造一个新字符串。 |
| +stringWithCharacters:length: | 构造一个新字符串，其中包含从所提供的 C 风格数组中获取的 length 个字符。 |
| +stringWithString: | 用给定字符串的值构造一个新字符串。 |
| +stringWithCString:encoding: | 使用 C 风格字符串，通过指定的编码方式转换后构造一个新字符串。 |
| +stringWithUTF8String: | 使用采用 UTF-8 字符串编码的 C 风格字符串构造一个新字符串。这相当于调用 +stringWithCString:encoding: 并将 NSUTF8Encoding 作为 encoding 参数。 |
| +stringWithContentsOfFile:encoding:error: | 构造一个新字符串，其中包含使用所提供的编码读取的指定文件的内容。 |

