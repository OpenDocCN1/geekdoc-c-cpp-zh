

### 24.10 解决方案：在回调中使用块

你可以删除 response: 方法，并用以下方法替换 registerWithoutBlocks 方法：

```objc
// Download Blocks/Callback2/CallbackAppDelegate.m
-(void)registerWithBlocks {
    [[NSNotificationCenter defaultCenter]
                   addObserverForName:nil
                              object:nil
                               queue:nil
                          usingBlock:^(NSNotification *notification) {
                              NSLog(@"Received: %@", [notification name]);
                          }];
}
```

块的主体是旧的 response 方法的主体。为清晰起见，我将 NSNotification 的名称从 arg1 改为 notification。使用块的一个优点是，你在需要完成工作的地方表达需要做什么。你的逻辑不会分散得到处都是。

点击构建并运行，你的控制台应充满类似这样的通知：

```text
Received: NSMenuDidChangeItemNotification.
Received: NSWindowDidBecomeKeyNotification.
Received: NSWindowDidBecomeMainNotification.
```

这段代码有一个大问题。这个问题并非块特有的，但它很容易让人犯错，因此我们应该稍微讨论一下。几秒钟后，通知会停止。即使你调整应用程序窗口的大小，也不会看到 NSWindowDidResizeNotification 或其他相关事件通知。

你可能还记得我们在使用 KVO 时遇到的这个问题。在自动垃圾回收机制下，我们必须显式持有观察者，否则它会被垃圾回收，就没有对象在那里接收通知了。

向头文件中添加一个实例变量。

```objc
// Download Blocks/Callback3/CallbackAppDelegate.h
#import <Cocoa/Cocoa.h>
@interface CallbackAppDelegate : NSObject <NSApplicationDelegate> {
    NSWindow *window;
    NSObject *observer;
}
@property (assign) IBOutlet NSWindow *window;
@end
```

将 observer 设置为注册监听通知时返回的对象，并保留这个对象。

下载 Blocks/Callback3/CallbackAppDelegate.m

```objc
-(void)registerWithBlocks {
    observer = [[NSNotificationCenter defaultCenter]
                addObserverForName:nil object:nil queue:nil
                usingBlock:^(NSNotification *notification) {
                    NSLog(@"Received: %@.", [notification name]);
                }] retain];
}
```

现在一切正常。通知会一直发送和接收，直到我们退出应用程序。

块彻底颠覆了你思考代码的方式。你不再向一个知道如何处理参数的方法传递大量参数，而是向对象传入一个动作，以及一些需要被处理的数据快照。通过练习，你会逐渐判断自己所处的情况是否能从块中受益。

网上有很多关于块的好材料。BBum 在他的 weblog-o-mat 上有一系列必读文章。尤其要阅读 Basic Blocks⁴ 和 Blocks Tips & Tricks.⁶ Mike Ash 在他的周五问答系列中发布了两篇关于块的非常好的文章。⁷,⁸ Joachim Bengtsson 有一篇关于块的在线介绍，⁹ Drew McCormack 在他的 “Cocoa for Scientists” 系列中写了一篇出色的指南 “10 Uses for Blocks”。¹⁰

在本章中，你体验了在需要封装某些行为、使用回调或处理集合时使用块的各种方式。接下来，我们将研究并发，以及块是如何构建以使你的代码性能更好的。

- 5. http://www.friday.com/bbum/2009/08/29/basic-blocks/
- 6. http://www.friday.com/bbum/2009/08/29/blocks-tips-tricks/
- 7. http://mikeash.com/pyblog/friday-qa-2008-12-26.html
- 8. http://mikeash.com/pyblog/friday-qa-2009-08-14-practical-blocks.html
- 9. http://thundergod.eu/pwcblocks/
- 10. http://www.macresearch.org/cocoa-scientists-xxii-10-uses-blocks-cocoa-objective-c

```objective-c
- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    NSArray *arrayOfSpinners = [self arrayOfSpinners];
    for (NSProgressIndicator *spinner in arrayOfSpinners) {
        [self spin:spinner];
    }
}
```

我将调整窗口大小并放置进度指示器，以便如果它们全部同时可见，看起来会像这样：

![](img/9355405953264484a02198b0e3d25b7e_398_0.png)

为此，在 Interface Builder 中调整窗口大小，使其宽度为 415，高度为 56。使用 Xcode 在 arrayOfSpinners 方法中创建并放置进度指示器。

```objective-c
- (NSArray *) arrayOfSpinners {
    NSMutableArray *array = [[NSMutableArray alloc] initWithCapacity:25];
    for (int i = 0; i < 25; i++) {
        NSProgressIndicator *spinner = [[NSProgressIndicator alloc]
                         initWithFrame:NSMakeRect(16 + i * 8, 20, 16, 16)];
        [spinner setStyle:NSProgressIndicatorSpinningStyle];
        [spinner setControlSize:NSSmallControlSize];
        [spinner setDisplayedWhenStopped:NO];
        [window.contentView addSubview:spinner];
        [array addObject:spinner];
    }
    return array;
}
```

arrayOfSpinners 方法返回一个填满进度指示器的数组。我们遍历这个数组，告诉每个进度指示器开始动画，休眠一秒钟，然后停止动画。

```objective-c
- (void) spin:(NSProgressIndicator *) spinner {
    [spinner startAnimation:self];
    sleep(1);
    [spinner stopAnimation:self];
}
```

点击构建并运行。应用程序将启动，进度指示器将出现并一次旋转一个。如果你将鼠标指针悬停在窗口上，你会看到旋转的沙滩球。你可能注意到该窗口不是活动窗口。如果你尝试点击该窗口，它将无响应。

![](img/9355405953264484a02198b0e3d25b7e_399_0.png)

如果你创建应用程序的发布版本并将其作为独立应用程序运行，也可以看到这一点。在用于强制退出应用程序的窗口中，它会被报告为“未响应”。

![](img/9355405953264484a02198b0e3d25b7e_399_1.png)

应用无响应是因为其主事件处理线程被阻塞，正在等待 spin 方法完成。我们将使用操作和队列来修复这种无响应问题。操作有三种基本类型。我们将从一种允许我们将方法调用转换为操作的类型开始。

### 25.2 调用操作

现在，我们只是直接调用 spin: 方法：

```objc
for (NSProgressIndicator *spinner in arrayOfSpinners) {
    [self spin:spinner];
}
```

NSInvocationOperation 允许我们通过指定方法、方法的目标以及要传递给方法的参数，从此方法调用创建一个对象。

```objc
NSInvocationOperation *op =
    [[NSInvocationOperation alloc] initWithTarget:self
        selector:@selector(spin:)
        object:spinner];
```

一旦你有了某种操作，就把它添加到一个操作队列中，该队列管理其中的操作。

下载 Operations/Spinner2/SpinnerAppDelegate.m

```objc
- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    NSArray *arrayOfSpinners = [self arrayOfSpinners];
    NSOperationQueue *queue = [[NSOperationQueue alloc] init];
    for (NSProgressIndicator *spinner in arrayOfSpinners) {
        [queue addOperation:[[NSInvocationOperation alloc]
            initWithTarget:self
            selector:@selector(spin:)
            object:spinner]];
    }
}
```

点击构建并运行，情况就大不相同了。¹ 所有进度指示器会同时旋转，而且你可以选择应用程序窗口。没有旋转的沙滩球。窗口将成为活动窗口。

![](img/9355405953264484a02198b0e3d25b7e_400_0.png)

那么，我们如何让进度指示器一次旋转一个呢？我们可以限制可并发执行的操作数量。我们可以将此值设为三，并观察三个进度指示器同时旋转。作为一种特殊情况，我们可以将此值设为一，将队列变成串行队列。操作将一次执行一个。

下载 Operations/Spinner3/SpinnerAppDelegate.m

```objc
- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    NSArray *arrayOfSpinners = [self arrayOfSpinners];
    NSOperationQueue *queue = [[NSOperationQueue alloc] init];
    [queue setMaxConcurrentOperationCount:1];
```

- 1. 如果这进行得太快，你可能想将睡眠时间从一秒钟增加到十秒钟。

