
### 12.5 响应选择器

下面是你如何测试能否从委托方对象调用委托方法：

```objective-c
-(void) applicationDidLaunch: (NSNotification *) notification {
    if ([self.delegate
          respondsToSelector:@selector(applicationDidLaunch:)]) {
        NSLog(@"Delegate implements applicationDidLaunch.");
    } else {
        NSLog(@"We're on our own.");
    }
}
```

在调用方法之前，你要询问委托是否实现了该方法。你通过向委托发送 `respondsToSelector:` 消息，并传入正在检查的方法名来进行检查。

点击“构建并运行”。你应该会在控制台窗口中看到消息“Delegate implements applicationDidLaunch.”。

我们来制造一两个问题。在 `ActivityController.m` 中注释掉这一行：

```objective-c
self.currentApp.delegate = self;
```

点击“构建并运行”。这一次你应该会在控制台中看到“We’re on our own.”。

取消注释最后一行，并注释掉 `ActivityController.m` 中的 `applicationDidLaunch:` 方法。点击“构建并运行”。忽略警告。你又会看到控制台中出现“We’re on our own.”。

取消注释该方法，然后再次点击“构建并运行”，以确认委托方法能够被成功调用。

### 12.6 练习：调用委托方法

我们准备完成委托。在 `CurrentApp` 的 `applicationDidLaunch:` 方法中，检查委托是否响应名为 `applicationDidLaunch:` 的方法。如果是，则调用该方法，并传入 `self` 作为 `CurrentApp` 对象。

在 `CurrentApp` 的 `applicationDidTerminate:` 方法中做类似的事情。当你点击“构建并运行”时，在启动和退出应用程序时，你应该会在文本字段中看到“Launched.”和“Terminated.”。

### 12.7 解决方案：调用委托方法

这是那种描述起来可能比实际做起来更耗时的练习之一。以下是你在 `applicationDidLaunch:` 和 `applicationDidTerminate:` 中所做的更改：

```objc
- (void) applicationDidLaunch: (NSNotification *) notification {
    if ([self.delegate
            respondsToSelector:@selector(applicationDidLaunch:)]) {
        [self.delegate applicationDidLaunch:self];
    }
}
- (void) applicationDidTerminate: (NSNotification *) notification {
    if ([self.delegate
            respondsToSelector:@selector(applicationDidTerminate:)]) {
        [self.delegate applicationDidTerminate:self];
    }
}
```

你还需要在 `CurrentApp` 头文件中导入 `ActivityMonitorDelegate.h`。你可以在头文件中使用前向声明，并在实现文件中导入，但我知道我们马上就要移动它，所以我把导入放在头文件中。

### 12.8 练习：清理

给你一条经验法则：如果你在 Interface Builder 中*可以*做某事，那么你就*应该*在 Interface Builder 中做它。

当然，也有例外，我们也会尝试用代码做一些在 IB 中*可以*完成的事情，但如果你遵循这一原则，你会走得更远。

让我们把这个原则应用到当前示例中，做一点清理工作。在 nib 中创建 `CurrentApp` 对象，并在那里设置其委托。你需要持有这个对象，所以我们在应用程序委托中设置一个输出口，并将其连接到 `CurrentApp` 对象。

### 12.9 解决方案：清理

我们可以去掉 `ActivityController.m` 中的 `awakeFromNib` 方法，因为我们要在 nib 中创建对象并设置委托。

```objective-c
#import "ActivityController.h"
#import "CurrentApp.h"

@implementation ActivityController

@synthesize activityDisplay;

-(void) applicationDidLaunch: (CurrentApp *) app {
    [self.activityDisplay setStringValue:@"Launched"];
}
-(void) applicationDidTerminate: (CurrentApp *) app {
    [self.activityDisplay setStringValue:@"Terminated"];
}
@end
```

我们不再需要 `currentApp` 属性。确保从头文件中移除变量和属性声明以及前向声明：

```objective-c
#import <Cocoa/Cocoa.h>
#import "ActivityMonitorDelegate.h"

@interface ActivityController : NSObject <ActivityMonitorDelegate> {
    NSTextField *activityDisplay;
}
@property IBOutlet NSTextField *activityDisplay;
@end
```

我们将在应用程序委托中添加一个输出口，以便 `CurrentApp` 实例在我们需要时一直存在：

```objective-c
#import <Cocoa/Cocoa.h>
@class ActivityController;
@class CurrentApp;

@interface HelloApplicationAppDelegate : NSObject <NSApplicationDelegate> {
    NSWindow *window;
    ActivityController *ac;
    CurrentApp *currentApp;
}
@property IBOutlet NSWindow *window;
@property IBOutlet ActivityController *ac;
@property IBOutlet CurrentApp *currentApp;
@end
```

记得在实现文件中合成 `currentApp` 属性。

下载 Protocols/HelloApplication10/HelloApplicationAppDelegate.m

```objc
#import "HelloApplicationAppDelegate.h"

@implementation HelloApplicationAppDelegate

@synthesize window, ac, currentApp;

- (void)applicationDidFinishLaunching: (NSNotification *)aNotification {
}
@end
```

最后，既然我们将在 IB 中设置委托，我们需要更仔细地指定类型。像这样修改 `CurrentApp.h`：

下载 Protocols/HelloApplication10/CurrentApp.h

```objc
#import <Cocoa/Cocoa.h>
#import "ActivityMonitorDelegate.h"

@interface CurrentApp : NSObject {
    NSObject <ActivityMonitorDelegate> *delegate;
}
@property IBOutlet NSObject <ActivityMonitorDelegate> *delegate;

@end
```

我们将 `id` 改为 `NSObject`。我还将协议名插入到尖括号中。注意 `*` 属于变量。如果你试图让它与 `NSObject` 放在一起，这将无法编译。我们还将委托属性标记为输出口。

委托属性的类型声明中的这一更改有一个不错的副作用。现在我们可以从 `CurrentApp.m` 的 `applicationDidLaunch:` 方法中移除这个保护子句：

```objc
if ([self.delegate
        respondsToSelector:@selector(applicationDidLaunch:) ] )
```

既然我们已经声明委托实现 `ActivityMonitorDelegate` 协议，而该协议要求实现 `applicationDidLaunch:` 方法，我们就不再需要这个检查。`applicationDidTerminate:` 方法也是如此。以下是 `CurrentApp.m` 中简化后的方法：

```objc
-(void) applicationDidLaunch: (NSNotification *) notification {
    [self.delegate applicationDidLaunch:self];
}
-(void) applicationDidTerminate: (NSNotification *) notification {
    [self.delegate applicationDidTerminate:self];
}
```

保存你的工作，然后我们转到 Interface Builder。在库的 Classes 标签页中找到 `CurrentApp`，并将其拖到文档窗口中。打开连接检查器。选择 `HelloApplicationAppDelegate` 对象，并将其 `currentApp` 输出口连接到 `CurrentApp` 对象。选择 `CurrentApp` 对象，并将其 `delegate` 输出口连接到 `ActivityController` 对象。保存你的工作，然后退出 IB。

点击“构建并运行”，你的应用程序应该和之前完全一样运行。

我们现在会在应用程序启动或终止时接收通知，并使用协议和委托在模型与控制器之间通信。然而，我们还没有对收到的通知做太多处理。其中包含大量我们目前只是忽略的信息。我们将在下一章解决这个问题。

## 第 13 章：使用字典

在过去的两章中，我们使用通知和委托来输出“Launched.”和“Terminated.”。在本章中，你将学习使用字典来回答“启动了什​​么？”和“终止了什么？”这两个问题。

通知中包含大量我们尚未使用的信息。请记住，`NSNotification` 包含通知名称、发送通知的对象，以及一个名为 `userInfo` 的字典，其中填充了关于特定通知的键值对信息。

在本章中，我们将深入探讨该字典的内容。[^1] 事实证明，这是一项需要了解的重要技术——Cocoa 框架到处都在使用字典。

### 13.1 查看用户信息

通知有三种基本的使用模式：

- 第一种情况下，重要的是你收到了通知——你只需要知道你一直在等待的事件已经发生。
- 第二种情况下，你可能会使用通知的名称或对象。
- 第三种情况下，你需要 `userInfo` 字典中包含的进一步信息。例如，当你收到应用程序已启动的通知时，你可能想知道……的名称

[^1]: 取决于你来自哪种编程语言，你可能会使用术语 *哈希* 而不是 *字典*。
