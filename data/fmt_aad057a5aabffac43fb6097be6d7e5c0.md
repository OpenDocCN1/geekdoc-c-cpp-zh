
`NSLog`("@Open of testout for writing failed");

return 2;

}

// 截断输出

[outFile truncateFileOffset:0];

// 从 infile 读取数据并写入 outFile

buffer = [inFile readDataToEndFile];

[outFile writeData:buffer];

}

// 关闭两个文件

[inFile closeFile];

[outFile closeFile];

// 验证文件内容

`NSLog`("%@", [NSString stringWithContentsFile:@"testout" encoding:NSUTFStringEncoding error:NULL]);

return 0;

}
```

## 程序 16.7 输出

这是一个包含数据的测试文件。
这里是另一行数据。
还有第三行。

若要在文件中回退等于五个整数的位置，请写入：
`[databaseHandle seekToFile offsetInFile]` $ * sizeof(int);

程序 16.8 将一个文件的内容追加到另一个文件中。其实现方法是打开第二个文件进行写入，定位到文件末尾，然后将第一个文件的内容写入第二个文件。

## 程序 16.8

```objc
// 将 "fileA" 追加到 "fileB" 的末尾

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {

    @autorelease {

        NSFileHandle *inFile, *outFile;

        NSData *buffer;

        // 以读取模式打开 "fileA"

        inFile = [NSFileHandle fileHandleForReadingAtPath:@"fileA"];

        if (inFile == nil) {

            NSLog(@"Open of fileA for reading failed");

            return 1;

        }

        // 以更新模式打开 "fileB"

        outFile = [NSFileHandle fileHandleForWritingAtPath:@"fileB"];

        if (outFile == nil) {

            NSLog(@"Open of fileB for writing failed");

            return 2;

        }

        // 定位到 outFile 的末尾

        [outFile seekToEndToFile];

        // 读取 inFile 并将其内容写入 outFile

        buffer = [inFile readDataToEndFile];

        [outFile write:buffer];

    }

}
```

```objc
// 关闭两个文件

[inFile closeFile];

[outFile closeFile];

// 验证内容

NSLog("%@", [NSString stringWithContentsFile:@"fileB"
encoding:NSUTF8StringEncoding error:NULL]);

}

return 0;

}
```

# 运行程序 16.8 之前 fileA 的内容：

这是第一个文件的第 1 行。
这是第一个文件的第 2 行。

# 运行程序 16.8 之前 fileB 的内容：

这是第二个文件的第 1 行。
这是第二个文件的第 2 行。

## 程序 16.8 输出

fileB 的内容
这是第二个文件的第 1 行。
这是第二个文件的第 2 行。
这是第一个文件的第 1 行。
这是第一个文件的第 2 行。

从从输出可以看出，第一个文件的内容已成功追加到第二个文件的末尾。顺带一提，`seekToEndToFile` 在执行完成后会返回当前的文件偏移量。我们选择忽略了该值；如果你有需要，可以使用该信息在程序中获取文件的大小。

## NSURL 类

`NSURL` 类为在程序中处理 URL 地址提供了一种方便的方法。例如，给出一个指向互联网上文件的 HTTP 地址，你可以通过几个方法轻松地读取该文件的内容。你会在 Foundation 中发现许多以 `NSURL` 对象作为参数的方法。只需记住，`NSURL` 对象不是像 `@"http://www.apple.com"` 这样的字符串对象，但使用 `URLWithString:` 方法可以很容易地从字符串对象创建一个。

# 第 16 章 与文件操作

程序 16.9 展示了如何将 Web 地址的 HTML 内容读取到程序中。

```objc
Program 16.9

// 读取存储 URL 中的文件内容

#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {

    @autoreleasepool {

        NSURL *myURL = [NSURL URLWithString:@"http://classroomM.com"];

        NSString *myHomePage = [NSString stringWithContentsOfURL:myURL
            encoding:NSASCIIStringEncoding error:NULL];

        NSLog("%@", myHomePage);

        return 0;

    }

}
```

# 程序 16.9 部分输出

```html
<!DOCTYPE html PUBLIC "//W3C//DTD HTML 1.0 Transitional//EN"
"http://www.w3.org/TR/DTD/xhtml-transitional.dtd">
<html xmlns="http://www.w3.org/text/html"><head>
<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
<meta http-equiv="Content-Style" content="text/css" />
<meta name="google-site-verification" content="J75bly6mDQItHzDWpDbHbn6CrVucOOzlJ8ggzij9y*" />
<title>iPhone Online Course and iPhone Training - Home</title>
```

你可以看到从互联网获取数据是多么简单。如果你在 Web 地址上有一个列表形式存储的字典，你可以使用 `dictionaryWithContentsOfURL:` 方法将其读取进来。如果它是作为属性列表的数组，则改用 `arrayWithContentsOfURL:` 方法。你可能还想研究如何从 Web 地址读取任何类型的数据。

# NSBundle 类

当你创建一个应用程序时，系统会将与该程序相关的所有数据——包括图像、本地化字符串、图标等资源——存储在一个名为 bundle（包）的包结构中。为了从你的应用程序访问这些资源，你需要熟悉 `NSBundle` 类。

# 练习题 405

向应用程序中添加图像或文本文件等资源非常简单：你只需将文件拖入 Xcode 左侧窗格中。在提示出现时，你需要将文件添加到 bundle 中。要从你的应用程序访问这些资源，你可以使用 `NSBundle` 类找到资源的路径，然后加载它。

1. 编写一个程序，从 bundle 读取资源文件并将其内容输出到控制台。
2. 编写一个程序，从 bundle 加载图像并在窗口中显示。
3. 编写一个程序，从 bundle 加载本地化字符串并显示。
4. 编写一个程序，在加载之前检查 bundle 中是否存在特定资源。
5. 编写一个程序，从 bundle 加载属性列表并显示其内容。
6. 编写一个程序，使用 bundle 找到资源的路径。
7. 编写一个程序，从 bundle加载所有资源并显示它们的名称。
8. 编写一个程序，使用 bundle 加载特定资源并显示其数据。

# 第17 章 内存管理与自动引用计数

本章涵盖了内存管理的概念，尽管是在相当高的水平上。内存管理的核心在于清理（回收）未使用的内存，以便再次被使用。当一个对象不再被使用时，让我们重用它的内存。这听起来足够简单。但实际上并没有那么简单。必须有人发现这个事实。也就是说，某个人——这个人可能是你、计算机，或者两者都是——必须能够判断对象何时不再被使用，并且它占用的内存因此可以被回收。

已经开发了多种内存管理策略来协助这些工作。其中两种是自动方法：计算机跟踪对象并在必要时释放它们的内存。第三种方法是混合方法：系统为你完成部分工作，但也要求你（程序员）足够勤奋，并告知系统对象何时不再被使用。

在 Xcode 4.2 发布之前，内存管理一直是备关注的话题，这需要程序员具备大量的理解和远见。程序员必须小心地处理引用计数、保留（retains）、释放（releases）和自动释放（autoreleases）的世界，以产生明智使用内存且不会在最不恰宜的时间崩溃的应用——这种崩溃通常是因为尝试引用一个在准备就绪之前就意外销毁的对象导致的。

随着 Xcode 4.2 中自动引用计数（简称 ARC）的发布，程序员不再需要考虑内存管理问题了；一切都为你处理好了！你只需要学习几个特殊情况（这些我们建议参阅 Apple 的文档）。但总的来说，ARC 对 iOS 开发者来说确实是天赐。证明这一点的是直到这一章之前，我从未提到过内存管理。在本书的早期版本中，我费了大量精力确保读者能够完全且明智地应用适当的内存管理技术。

在本章中，你将概述适用于 Cocoa 和 iOS 开发者的不同内存管理方案。我们还描述了手动内存管理是如何工作的。这是以防你可能需要支持旧代码，或者出于某种原因不想避免使用目前的自动内存管理功能。

尽管你不再需要担心对象的生命周期（以及在完成后释放其内存等事情），但取决于你编写的应用类型，明智地使用内存仍然很重要。例如，如果你正在编写一个在程序执行期间创建许多对象的交互式绘画应用程序，你必须确保程序在运行时不会继续消耗更多资源。在某些情况下，智能地管理这些资源并确保不进行不必要的对象分配将成为你的责任。

为 Objective-C 开发者支持三种基本的内存管理模型：

- 1. 自动垃圾回收
- 2. 手动引用计数和自动释放池
- 3. 自动引用计数 (ARC)

## 自动垃圾回收

从 Objective 2.0 开始，被称为垃圾回收的内存管理形式变得可用。通过垃圾回收，系统会自动确定哪些对象拥有哪些其他对象，并在程序执行期间需要空间时，自动释放（或垃圾回收）不再被引用的对象。

iOS 运行时不支持垃圾回收，因此在为该平台开发程序时，你无法使用它。而且，从 OS X 10.8 (Mountain Lion) 开始，垃圾回收已被弃用（这意味着在未来的某个时刻将不再被支持）。Apple 不鼓励使用它，并建议你使用 ARC。

## 手动引用计数

如果你要在不用垃圾回收或 ARC 的情况下创建应用程序，或者你必须支持无法迁移到 ARC 的代码，你需要知道如何管理内存。也就是说，你需要学习如何处理引用计数工作。

通用概念如下：当一个对象被创建时，它的初始引用计数设置为 1。每当你需要确保该对象保持存在时，你实际上通过将其引用计数加 1 来创建对它的引用。这是通过向对象发送一个 retain 消息完成，如下：

```
[Fraction retain];
```

当你不再需要一个对象时，通过向它发送一个 release 消息将其引用计数减 1，如下：

```
[Fraction release];
```

当一个对象的引用计数达到 0 时，系统就知道该对象不再被使用（因为从理论上讲，它不再被应用程序的任何地方引用），它会释放（deallocate）它的内存。这个过程是通过向对象发送 dealloc 启动的。在很多情况下，你使用继承自 NSObject 的 dealloc 方法。然而，你可能需要重写 dealloc，以释放你的对象可能分配或保留的任何实例或其他对象。例如，如果你的类有一个 NSArray 对象作为其实例变量之一并且你分配了它，那么当你的对象被销毁时，你有责任释放它。你在 dealloc 中这样做。

手动引用计数策略的成功运行需要你（程序员）的勤奋，以确保引用计数在程序执行期间得到恰当的增加和减少。系统处理了其中一部分，但不是全部。

使用手动引用计数时，你应该注意 Foundation 框架中的某些方法会增加对象的引用计数，例如当使用 NSMutableArray addObject 方法将对象添加到数组中，或者使用 addSubview 方法将视图作为子视图添加时。同样，方法可能会减少对象的引用计数。removeObjectAtIndex: 和 removeFromSuperview 是两种方法。

在对象被销毁后（即它的引用计数已减到零并执行了 dealloc），对该对象的进一步引用将失效。如果你有一个经常被称为悬空指针（dangling pointer）的引用，发送此类指针会导致意外行为，包括你的应用程序崩溃。有时程序员没有准确地跟踪对象的 retain 和 release。这被称为过度释放对象（over-releasing），它通常会导致崩溃。

## 对象引用与自动释放池

你可能需要编写一个方法，该方法首先创建一个对象（使用 alloc）并返回该对象。这里有一个困境：尽管该方法使用了 alloc，但它不能释放它，因为它需要返回它的值。`NSAutleasePool` 类的创建是为了通过跟踪以后释放的对象来帮助解决问题，以后是指自动释放池清空的时候，这是通过向自动释放池发送 drain 消息完成的。

要添加到自动释放池维护的对象列表中，你可以向它发送 autorelease 消息，如下：

```
[result autorelease];
```

在处理使用 Foundation、UIKit 或 AppKit 框架的程序时，你必须为这些可以创建并返回自动释放对象的框架创建一个自动释放池。你在程序中使用 `@autoreleasepool` 指令这样做：

```
@autoreleasepool {
  statements
}
```

Xcode 在 main 开始处生成此指令，即使你没有启用 ARC。

当自动释放块结束时，系统清空池。这样做的效果是对每个发送过 autorelease 消息并因此添加到池中的对象发送 release 消息。如果其中任何对象的引用计数被减到零，这些对象将收到 dealloc 消息并释放内存。

注意，自动释放池并不包含对象本身，只包含在池清空时释放的对象引用。并不是所有新创建的对象都会添加到自动释放池中。事实上，任何通过名为 alloc、copy、mutableCopy 或 new 方法创建的对象都不会被自动释放。在这种情况下，你拥有该对象。当你使用一个对象时，你

在使用该对象时，负责释放该对象占用的内存。这是通过发送对象的释放（release）消息来实现的。你也可以将其添加到自动释放（autorelease）消息中。

如果使用手动引用计数，程序 3.3 中的主程序将如下所示：

```c
int main (int arg, char * argv[]) {
    @autoreleasepool {
        Fraction *frac1 = [[Fraction alloc] init];
        Fraction *frac2 = [[Fraction alloc] init];
        // 将第一个分数设置为 2/3
        [frac1 setNumerator: 2];
        [frac1 setDenominator: 3];
        // 将第二个分数设置为 3/7
        [frac2 setNumerator: 3];
        [frac2 setDenominator: 7];
        // 显示分数
        NSLog("@First fraction is:%@");
        [frac1 print];
        NSLog("@Second fraction is:%@");
        [frac2 print];
        [frac1 release];
        [frac2 release];
    }
    return 0;
}
```

注意，我们在 `main` 函数结束时释放了两个 `alloc` 过的对象。尽管在应用程序终止时所有内存都会被释放，但这个示例说明了在使用对象时释放对象的思想。

让我们再次看一眼程序 7.5 中使用的 `Fraction` 类的 `add` 方法：

```objc
- (Fraction *) add: (Fraction *) f
{
    // 为了相加:
    // a/b + c/d = (a*d) / (b*c)
    // result 将存储加法的结果
    Fraction *result = [[Fraction alloc] init];
    result.numerator = numerator * f.denominator + denominator *
    f.numerator;
    result.denominator = denominator * f.denominator;
    [result reduce];
