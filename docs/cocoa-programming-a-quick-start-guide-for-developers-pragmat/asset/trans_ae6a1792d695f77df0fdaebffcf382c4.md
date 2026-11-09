
如果这还没有让你完全理解，也不用担心。我主要是希望你在本书后面编译器因此报错时能有所准备。你主要需要思考内存管理的地方，是在为 iPhone、iPod touch 和 iPad 创建应用时。在本章剩余部分，我们将看一个 iPhone 应用示例。

## 6.5 创建手电筒

目前，如果你的目标是 iPhone 或 iPad，就必须使用引用计数并自行管理内存。让我们构建 HelloWorld 项目的 iPhone 版本，以便试验你学到的一些规则。

你需要在 http://developer.apple.com/iphone 注册成为 iPhone 开发者。这是免费的，但要求你同意 Apple 的条款。当你准备部署到手机或在 App Store 上分发时，需要加入某个付费计划。

如果你还没有注册为 iPhone 开发者，可以继续使用当前的示例；只需将垃圾回收重新设置为 Unsupported。

在 Xcode 中新建项目（File > New Project...）。这次选择 iPhone > Application > Window-based Application 模板。确保用于 Core Data 的复选框未选中，然后点击 Choose。将项目命名为 Flashlight，并选择 Save。

点击 Build & Run，iPhone 模拟器将启动并运行你的应用。你应该会看到一个纯白屏幕，顶部有状态栏。恭喜，你构建了一个手电筒。人们曾在 App Store 上卖过这类东西。

我们需要复制 Greeter 类的头文件和实现文件。在 Groups & Files 中选择 Classes 文件夹。选择菜单项 Project > Add to Project...。导航到你存放 HelloWorld 项目的位置，选择 Greeter.h 和 Greeter.m，然后点击 Add 按钮。如有需要，选中将项目复制到 Flashlight 应用文件夹的复选框，然后点击 Add 按钮。你已经将 Greeter 类添加到了这个项目中。

你的 FlashlightAppDelegate.m 文件应该与之前的 HelloWorldAppDelegate.m 文件非常相似。

你应该得到如下内容：

```objc
#import "FlashlightAppDelegate.h"
#import "Greeter.h"

@implementation FlashlightAppDelegate
@synthesize window;

- (void)applicationDidFinishLaunching:(UIApplication *)application {
    Greeter *host = [[Greeter alloc] initWithName:@"Maggie"];
    NSLog(@"Greeter %@", host);
}
@end
```

点击 Build & Run，你会看到有一些问题需要修复。

首先，我们在 Greeter.h 中遇到一个错误：没有名为 Cocoa/Cocoa.h 的文件或目录。对于 iPhone，包含 GUI 和底层框架的框架是 UIKit/UIKit.h。这里我们不需要任何图形相关部分，因此只导入 Foundation 框架。将

```objc
#import <Cocoa/Cocoa.h>
```

替换为

```objc
#import <Foundation/Foundation.h>
```

（在 Greeter.h 中）。另一个问题是我们运行在模拟器上造成的现象。我们需要显式声明实例变量。下面是修正后的 Greeter.h 文件：

```objc
#import <Foundation/Foundation.h>
@interface Greeter : NSObject {
    NSString *name;
    NSInteger age;
    NSDate *today;
    BOOL upperCase;
}
-(NSString *) greeting;
-(id) initWithName:(NSString *)name;

@property(copy) NSString *name;
@property(assign, readonly) NSInteger age;
@property(assign) NSDate *today;
@property(assign, getter=isUpperCase) BOOL upperCase;

@end
```

我还把类型为 Greeter 的 buddy 对象替换为名为 `today` 的 NSDate。³ 我会在创建 Greeter 对象时用它生成实际时间戳。

```objc
#import "Greeter.h"

@implementation Greeter

@synthesize name, age, today, upperCase;
-(NSString *) greeting {
    return [[NSString alloc] initWithFormat:@"Hello, %@!", self.name];
}
-(id) initWithName:(NSString *) newName {
    if (self = [super init]){
        self.name = newName;
        self.upperCase = YES;
        self.today = [NSDate date];
    }
    return self;
}
-(id) init {
    return [self initWithName:@"World"];
}
-(NSString *)description {
    return [[NSString alloc] initWithFormat:@"name: %@ \n created: %@",
            self.name,self.today];
}
@end
```

点击 Build & Run，你应该会再次看到你的手电筒，并且控制台输出与你在桌面版本中看到的相同。在模拟器中点击 Build & Analyze，你应该会看到与之前报告的相同内存泄漏。⁴ 我们将重点关注 FlashlightAppDelegate.m 中出现的那个泄漏。

## 6.6 在 Instruments 中查找泄漏

关于 Apple 的性能和调试工具，完全可以也应该写成整本书。我只想花一点时间向你展示，Instruments 应用本来也可以如何识别出 FlashlightAppDelegate.m 中的内存泄漏。

3. 我使用了便捷构造器 date，而不是 alloc 和 init。到本章结束时，你会明白为什么。

4. 我假设你正在针对模拟器运行所有性能工具。这样做是免费的。将应用部署到你的设备上则需要付费。

你已经执行过 Build & Run，因此有一个构建产物可供我们在 Instruments 中运行。在 Xcode 中选择菜单项 Run > Run with Performance Tool > Leaks。Instruments 应用将启动，你的 Flashlight 应用也会从 Instruments 中启动。几乎立刻，你应该会在 Instruments 窗口的顶行看到一条垂直蓝线，表示对象正在被分配。大约十秒后，你应该会在 Instruments 窗口的第二行看到一条红线以及一系列蓝线。红线表示发现的泄漏数量，蓝线表示已泄漏的字节数。

![](img/9355405953264484a02198b0e3d25b7e_111_0.png)

泄漏其实发生得早得多，但默认设置是每十秒采样一次泄漏。默认情况下，Object alloc 数据报告在 Instruments 窗口的右下部分。在左上角选择 Leaks 工具，你应该会看到泄漏信息。你可以在这个示例输出中看到，报告称泄漏源自 FlashlightAppDelegate 的 applicationDidFinishLaunching: 方法。这已经足够我们找到泄漏；不过，如果你双击报告泄漏的 Greeter 对象的那一行，就会跳转到源代码中有问题的代码行。既然知道泄漏在哪里，我们来修复它。

## 6.7 修复 iPhone 上的内存泄漏

内存管理是多种约束之间的平衡。最基本的一点是，你不希望在还有其他东西可能仍然指向某个对象时释放该对象的内存。另一方面，你也不希望在没人需要对象之后仍然长期持有它们，从而造成内存泄漏。在 Objective-C 中实现这一点的方式是引用计数。

你已经简要看到，当你用类似下面的代码创建 Greeter 类型的对象时，调用 alloc 后引用计数会被设为一：

```objective-c
Greeter *host = [[Greeter alloc] initWithName:@"Maggie"];
```

这正是 Build & Analyze 报告的错误。它知道你已将引用计数增加到一，并且再也没有使用过该变量。它希望你确认自己不再需要这个变量。你可以通过调用下面的代码来做到这一点：

```objective-c
[host release];
```

这会将引用计数递减一。在我们的例子中，这就足够了。host 的引用计数将变为零，它的 dealloc 方法会被调用，以清理对象资源并释放内存。当你知道不再需要 host 对象时，就向它发送 release 消息。在我们的例子中，你会在这里这样做：

```objective-c
Download Memory/Flashlight2/Classes/FlashlightAppDelegate.m

- (void)applicationDidFinishLaunching:(UIApplication *)application {
    Greeter *host = [[Greeter alloc] initWithName:@"Maggie"];
    NSLog(@"Greeter %@", host);
    [host release];
}
```

点击 Build & Analyze，这个特定的内存泄漏现在消失了。接下来，让我们花一点时间看看当你犯另一个关键内存错误时会发生什么。当你尝试向一个已被释放的对象发送消息时，会发生什么？

## 6.8 使用僵尸对象

到目前为止，我们创建了一个 Greeter 类型的对象，将其内容打印到控制台，并释放了该对象。现在让我们故意向这个已释放的对象再发送一条消息。我们就像这样再次将其内容打印到控制台：

```objective-c
Download Memory/Flashlight3/Classes/FlashlightAppDelegate.m

- (void)applicationDidFinishLaunching:(UIApplication *)application {
    Greeter *host = [[Greeter alloc] initWithName:@"Maggie"];
    NSLog(@"Greeter %@", host);
    [host release];
    NSLog(@"Greeter %@", host);
}
```
