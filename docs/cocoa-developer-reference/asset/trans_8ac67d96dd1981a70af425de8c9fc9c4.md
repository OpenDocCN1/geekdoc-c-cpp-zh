
### 实现暂停方法

你可以使用 performSelector: 来模拟暂停功能。假设你有一个名为 aLongMethod 的方法。要创建暂停，请将 aLongMethod 拆分为两部分，并使用 performSelector: 在延迟后触发第二部分。

```objective-c
- (id) aLongMethod {
    // Do things
    // Pause here...
    [self performSelector: @selector(restOfMethod:)
           withObject: anObject
           afterDelay: 1.0];
}

- (id) restOfMethod:(id)optionalObject {
    // Finish the rest after the pause
}
```

你还可以使用以下代码在当前线程中暂停执行

```objective-c
[NSThread sleepForTimeInterval: 2.0];
```

### 在单独的线程中运行选择器

performSelectorInBackground: 方法是在单独线程中运行方法的简单方式。由选择器指定的方法会从主线程分离并在后台运行。你无法控制线程优先级。如果需要传递参数，请使用 performSelectorInBackground:withObject:，并将参数打包到数组或字典中。

如果你不使用垃圾回收，后台方法必须实现自己的自动释放池，如下文“管理线程内存”部分所述。

### 跨线程传递消息

performSelector: 可以在特定线程中触发方法，并等待该方法完成：

```objective-c
[targetObject performSelector: @selector(aMethod:)
            onThread: aThread withObject: aParameterObject waitUntilDone: YES];
```

可选地，你可以在此签名末尾添加 modes 参数来指定线程模式。该参数接受一个字符串 NSArray，用于定义支持的 modes 列表。无法延迟消息，但可以使用 performSelector:withDelay: 方法延迟第二个 performSelector: 来触发消息。

aThread 是 NSThread 的实例。performSelectorOnMainThread: 选项会在主线程中选择目标对象，但也可以创建单独的自定义 NSThread 实例来从主应用程序中派生线程。

## 使用 NSThread

NSThread 在 OS X 中正逐渐成为遗留对象，但它在 iOS 中仍然有用，因为 iOS 的线程模型更简单。线程是独立于触发它的对象运行的方法。要创建线程，请使用

```objective-c
[NSThread detachNewThreadSelector: @selector(theThreadMethod:)
                         toTarget: self
                       withObject:anOptionalObject];
```

该方法通过以下方式实现

```objective-c
- (void) theThreadMethod: (id)theOptionalObject {
    // Do things
    [NSThread exit];
}
```

你可以向 theOptionalObject 中打包任意所需数据。它可以是单个 NSNumber，也可以是完整的键值对字典。

exit 调用会终止线程。或者，你可以创建一个独立的线程对象：

```objective-c
NSThread *theThread = [[NSThread alloc]
    initWithTarget: self
            selector: @selector(theThreadMethod)
              object: anOptionalObject];
```

### 暂停线程

使用独立对象时，你可以设置其属性，包括 name、stackSize 和 threadPriority——后者范围为 0.0 到 1.0。要运行线程，请使用 start 方法。要从外部结束线程，请向其发送 cancel 消息。根据线程代码的不同，这可能没有效果。

线程（包括主线程）可以通过以下方式暂停

```objective-c
[NSThread sleepForTimeInterval: aFloat];
```

从你想暂停的线程内部调用此方法。它是一个类方法，但 NSThread 会隐式识别调用它的线程并相应地暂停该线程。对应的 sleepUntilDate: 方法设置绝对唤醒时间/日期，而不是间隔。

> **注意**
>
> 如果暂停主线程超过几秒钟，就会出现沙滩球图标，并且应用程序会被标记为“未响应”。

## 管理线程内存

在 OS X 上，你可以使用垃圾回收来简化线程内存管理。在 iPhone 上，必须在线程启动时为其创建本地自动释放池，并在退出前释放它。

```objective-c
NSAutoreleasePool *aPool = [[NSAutoreleasePool alloc] init];
// Thread code goes here
[aPool release];
[NSThread exit];
```

这是标准样板代码，也是实现自动释放池所需的全部内容。

## 处理 UI 与线程交互

只有部分 AppKit 和 UIKit 是线程安全的，因此直接从线程访问 UI 对象可能有风险。通常，你使用线程执行后台操作，例如下载、搜索或归档操作，否则这些操作会拖慢执行速度。

如果你需要触发 UI 更新，请使用

```objective-c
[mainThreadObject performSelectorOnMainThread: @selector(aMethod:)
                                      withObject: anObject
                                      waitUntilDone: BOOL];
```

将更新代码放在一个特殊的选择器/方法中，该方法执行更新但在主线程中运行，并且可以被远程触发。你可以选择暂停线程，等待主线程完成该选择器，或者继续。

要从 UI 接收消息，请使用等效的 performSelectorOnThread: 方法，指定线程以及其中的目标对象和方法。

![](img/2b293e29fc15b0797f113b85dd429b6e_292_0.png)

> **提示**
>
> 有时在线程退出前运行 `performSelectorOnMainThread:` 很有用，可以让主线程知道另一个线程已完成运行。如果需要，使用 `waitUntilDone: YES` 确保主线程已复制或读取运行的任何结果。

## 使用 NSOperation

NSOperation 比 NSThread 更晚出现，并具有以下优点：

- 线程是对象，而不是方法。
- 可以通过自定义的 init 方法传递任意数量的参数。
- **可以在线程对象运行时或终止前从其属性中读取结果。**
- **可以管理排队和并发。** 操作可以在后台*并发*运行——同时运行——或顺序运行。并发处理可以定义正在运行的线程的最大数量。

NSOperation 比 NSThread 需要更多设置，并且灵活性较低。当你需要对线程进行更多控制，并且需要向后台任务传递更广泛的对象和值时，可将其用于更复杂的线程应用程序。

接下来你将创建一个简单示例，使用 NSOperation 列出素数。

### 创建 NSOperation 对象

NSOperation 对象必须具有以下内容：

- **一个自定义 init 或 initWith: 方法，用于初始化其本地值。**
- **一个包含主线程代码的 main 方法。** 可以根据需要定义其他本地方法。

init 方法在创建对象时调用，main 方法在运行队列运行该对象时触发。下面是一个简单对象的头文件，它定义了 BackgroundTask 类：

```objective-c
#import <Foundation/Foundation.h>
@interface BackgroundTask : NSOperation {
    int limitInt;
}
@property int limitInt;
- (id) initWithInt: (int) anInt;
@end
```

要在 Xcode 中创建 NSOperation 对象，请按常规方式向项目中添加一个 NSObject：右键单击 Classes 文件夹，选择 Add New File，选择 OS X Cocoa Class 和 Objective-C class，并在类弹出菜单中选择 Subclass of NSObject。命名并保存它。

保存后，将类从 NSObject 改为 NSOperation，如前所示。

![](img/2b293e29fc15b0797f113b85dd429b6e_293_0.png)

> **注意**
>
> 不要忘记使用 `GetInfo` 将新文件的 Path Type 改为 Relative To Enclosing Group。

示例后台任务的代码如下：

```objective-c
#import "BackgroundTask.h"
#import "NSOperationAppDelegate.h"
@implementation BackgroundTask
@synthesize limitInt;
- (id) initWithInt: (int) anInt
{
    if (![super init]) return nil;
    limitInt = anInt;
    return self;
}
- (void) main {
    for (int i=0; i< limitInt; i++) {
        if ([self isPrime: i])
        NSLog (@"%i is prime", i);
    }
    [[NSOperationQueue shared] performSelectorOnMainThread:
    @selector(taskDidFinish:)
    withObject: self
    waitUntilDone: YES];
    return;
}
- (BOOL) isPrime: (int) testNumber {
    if (testNumber < 1) return NO;
    if ((testNumber == 2) || (testNumber == 3)
                    || (testNumber%2 == 0) || (testNumber%3 == 0)) return NO;
    int divisor = 5;
    int limit = 1+sqrt(testNumber);
    while (divisor < limit) {
        if ( ((testNumber%divisor) == 0) ||
                    (testNumber%(divisor+2)) == 0) return NO;
        divisor +=6;
    }
    return YES;
}
@end
```

代码的主要特性包括：

- **initWithInt: 方法将初始化内容复制到本地属性中。** `main` 不支持参数传递，因此必须通过 `init` 传递参数。
- **主循环遍历整数列表，测试它们，如果它们是素数则记录日志。** 素数测试位于单独的本地方法中。由于它是 NSOperation 对象的一部分，该方法也成为后台任务的一部分。
- **使用 performSelectorOnMainThread: 在线程完成时通知主线程。** 这是一个可选但有用的特性。
- **线程会自动退出。**
- **[NSOperationAppDelegate shared] 返回指向创建并运行此对象的应用程序委托的指针。** 接下来将更详细地描述它。
