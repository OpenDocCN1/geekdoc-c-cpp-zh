

```
=====================================================
====
This is the string
12345
98.6
```

输出验证了地址簿和你的 Foo 对象已成功从归档文件（Archiver file）中恢复。

# 使用归档器拷贝对象

在程序 18.2 中，你尝试过对一个包含可变字符串元素的数组进行拷贝，并看到了了是如何对数组进行浅拷贝的。也就是说，字符串本身并没有被复制——只复制了它们的引用。

你可以使用 Foundation 的归档功能来创建对象的深拷贝。例如，程序 19.11 通过将 `dataArray` 归档到缓冲区中然后进行反归档，并将结果赋值给 `dataArray2`，从而完成 `dataArray` 的拷贝。在这个过程中，你不需要使用文件；归档和反归档过程完全可以在内存中进行。

# 程序 19.11

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {

    @autoreleasepool {
        *data;
        NSData
        NSMutableArray *dataArray = 
        [NSMutableArray arrayWithObjects:
[NSMutableString stringWithString:
@"one"],
[NSMutableString stringWithString:
@"two"],
[NSMutableString stringWithString:
@"three"],
nil];
Mutable *dataArray2;
NSMutableString *mStr;

// 使用归档器进行深拷贝
data = [KeyedArchiver
archivedDataWithRootObject: dataArray]; 
dataArray2 = [KeyedUnarchiver
unarchiveObjectWithData: data];

mStr = [dataArray2 objectAtIndex: 0];
[mStr appendString: @"ONE"];

NSLog("@dataArray: ");
for ( NSString *elem in dataArray )
NSLog("%@@@", elem);

NSLog("\ndataArray2: ");
for ( NSString *elem in dataArray2 )
NSLog("%@@@", elem);

return 0;
}
}

```

# 程序 19.11 输出

```
dataArray:
one
two
three

dataArray2:
oneONE
two
three
```

输出验证了修改 `dataArray2` 的第一个元素对 `dataArray` 的第一个元素没有影响。这是因为通过归档/反归档过程创建了新的字符串副本。

程序 19.11 中的拷贝操作是通过以下两行实现的：

```objc
data = [NSKeyedArchiver
archivedDataWithRootObject: dataArray];
dataArray2 = [NSKeyedUnarchiver
unarchiveObjectWithData: data];
```

你甚至可以避免中间赋值，用一条语句完成拷贝，如下：

```objc
dataArray2 = [NSKeyedUnarchiver
unarchiveObjectWithData:
[NSKeyedArchiver
archivedDataWithRootObject: dataArray];
```

当你下次需要对一个对象或一个对象的对象进行深拷贝时，这种技术你可能会记住。

```bash
$ lookup gregory
```

# 第三部分：Cocoa, Cocoa Touch 和 iOS SDK

# 20. Cocoa 和 Cocoa Touch 简介

在整本书中，你开发了具有简单用户界面的程序。你依赖 `NSLog` 例程以简单文本行的形式显示输出。然而，尽管这个例程很有用，但它的功能非常有限。无疑，你在 Mac 或 iPhone 上使用的其他程序并不那么“不友好”。事实上，Mac 的声誉基于其用户友好的对话框和易用性。幸运的是，这里 Xcode 及其内置的用户界面设计工具派上了用场。这种组合不仅提供了一个强大的程序开发环境（包含编辑和调试工具，以及方便的在线文档访问），还提供了一个易于开发复杂的图形用户界面（GUI）的环境。

为你的 Mac OS X 应用提供丰富用户体验支持的框架被称为 Cocoa，它实际上由三个框架组成：你已经熟悉的 Foundation 框架、用于轻松存储和管理数据库驱动数据的 Core Data 框架，以及 Application Kit（或 AppKit）框架。最后这一个框架提供了与窗口、按钮、列表相关的类。

# 框架分级

通常使用图表来说明将最顶层应用程序与底层硬件隔离开的不同层级。其中一种表示方法如图 20.1 所示。

# 图 20.1 应用程序层次结构

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_690_0.png)

# 计算机资源（内存、磁盘、显示器等）

内核以设备驱动程序的形式提供硬件的底层通信。它管理系统资源，包括调度程序执行、管理内存和电源，以及执行基本的 I/O 操作。

正如其名，Core Services 提供的支持比上方层级更低或更处于“核心”层面。例如，在这里你可以找到对集合、网络、调试、文件管理、文件夹、内存管理、线程、时间和电源的支持。

Application Services 层包含对打印和图形渲染的支持，包括 Quartz、OpenGL 和 Quicktime。

紧邻你的应用程序下方的是 Cocoa 层。如所述，Cocoa 包含了 Foundation、Core Data 和 AppKit 框架。Foundation 提供了用于集合、字符串、内存管理、文件系统、归档等的类。AppKit 提供了管理视图、窗口、文档以及 Mac OS X 闻名的丰富用户界面的类。

从这个描述来看，某些层级之间似乎存在功能重复。集合存在于 Cocoa 层和 Core Services 层中。然而，前者建立在后者的支持之上。此外，在某些情况下，层级可以被跳过或“桥接”。例如，某些 Foundation 类（如处理文件系统的类）直接依赖 Core Services 层的功能，因此跳过了 Application Services 层。在许多情况下，Foundation 框架对低层 Core Services 层（主要用过程化 C 语言编写）中定义的数据结构进行了面向对象的映射。

# Cocoa Touch

iPhone、iPod Touch 和 iPad 等 iOS 设备包含一个运行精简版 Mac OS X 的计算机。iPhone 硬件中的某些功能（如加速度计）是手机特有的，在其他 Mac OS X 计算机（如 MacBook Pro 或 iMac）中无法找到。

> 注意
> 实际上，Mac 笔记本电脑包含加速度计，以便在电脑掉落时硬盘可以停靠；但是你无法从程序中直接访问此加速度计。

虽然 Cocoa 框架是为 Mac OS X 桌面和笔记本电脑的应用开发设计的，而 Cocoa Touch 框架用于针对 iOS的应用。

Cocoa 和 Cocoa Touch 共有 Foundation 和 Core Data 框架。然而，在 Cocoa Touch 下，UIKit 取替了 Cocoa 中的 AppKit 框架，为许多相同类型的对象支持，例如窗口、视图、按钮等。此外，Cocoa Touch 提供了用于处理加速度计、陀螺仪、通过 GPS 和 Wi-Fi 定位以及触摸界面的类，并消除了不需要的类。

这些 和 Cocoa Touch 的简要概述到此结束。在下一章，你将学习如何使用 iOS SDK 部分的模拟器为 iPhone 编写应用程序。

# 21. 编写 iOS 应用

在本章中，你将开发两个 iPhone 应用。第一个将介绍一些基本概念，让你熟悉使用 Interface Builder、建立连接以及理解代理（delegates）、输出（outlets）和动作（actions）。对于第二个 iPhone 应用，你将构建一个分数计算器。它将你在开发第一个应用时学到的与书中其余部分学到的知识结合。你在这里学的原理也可以用于开发其他 iOS 设备的应用。

# iOS SDK

要编写 iPhone 应用，你需要安装 Xcode 和 iOS SDK。此 SDK 可以从 Apple 网站免费获取。要下载 SDK，你需要注册成为 Apple 开发者。该过程也是免费的。要获取相应的链接，可以从 developer.apple.com 开始并进入相应的位置。熟悉该网站是一个很好的主意。

# 你的第一个 iPhone 应用

第一个应用程序展示了你如何在 iPhone 屏幕上放置一个黑色窗口，允许用户按下按钮，然后响应按钮点击显示某些文本。

