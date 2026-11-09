
应用程序以及它在硬盘上的位置。这些信息会以键值对的形式存储在由 userInfo 返回的 NSDictionary 中。

将此行添加到 CurrentApp.m 中的 applicationDidLaunch: 方法中：

下载 Dictionaries/HelloApplication1/CurrentApp.m

```objc
-(void) applicationDidLaunch: (NSNotification *) notification {
    [self.delegate applicationDidLaunch:self];
    NSLog(@"%@", notification.userInfo);
}
```

点击“构建并运行”。启动应用程序时，你应该会在控制台窗口中看到 userInfo 字典。例如，当我启动 iCal 时，我在控制台中看到以下内容：

```
{
    NSApplicationBundleIdentifier = "com.apple.iCal";
    NSApplicationName = iCal;
    NSApplicationPath = "/Applications/iCal.app";
    NSApplicationProcessIdentifier = 7130;
    NSApplicationProcessSerialNumberHigh = 0;
    NSApplicationProcessSerialNumberLow = 987377;
    NSWorkspaceApplicationKey = "<NSRunningApplication:
        0x200019ae0 (com.apple.iCal - 7130)>";
}
```

你可以看到应用程序的名称及其在磁盘上的位置。你可以看到它的 bundle 标识符和其他标识符。我们先从提取名称开始。

### 13.2 从字典中读取

从字典中读取有很多方法。你可以使用键枚举器按顺序遍历字典条目并挑选出值。你可以获取包含所有键或所有值的数组。我们将使用 objectForKey: 方法：

```objc
[notification.userInfo objectForKey:@"NSApplicationName"]
```

现在，当我们点击“构建并运行”时，我们会将已启动应用程序的名称记录到控制台窗口。从字典中读取就是这么简单。

### 13.3 练习：显示名称

向 CurrentApp 添加一个名为 name、类型为 NSString 的属性。收到通知时，通过从 userInfo 字典中读取来设置 name 属性的值。你的应用程序窗口应该看起来像这样：

![](img/9355405953264484a02198b0e3d25b7e_214_0.png)

换句话说，当你更新文本字段时，启动或退出 iCal 时，消息应分别显示“Launched: iCal”或“Terminated: iCal”。

### 13.4 解决方案：显示名称

将 name 实例变量和属性添加到头文件。将内存模型指定为 copy，因为 NSString 遵循 NSCopying 协议。

```objective-c
#import <Cocoa/Cocoa.h>
#import "ActivityMonitorDelegate.h"

@interface CurrentApp : NSObject {
    NSObject <ActivityMonitorDelegate> *delegate;
    NSString *name;
}
@property IBOutlet NSObject <ActivityMonitorDelegate> *delegate;
@property(copy) NSString *name;

@end
```

在 CurrentApp.m 中的 applicationDidLaunch: 和 applicationDidTerminate: 方法中设置 name：

```objective-c
-(void) applicationDidLaunch: (NSNotification *) notification {
    self.name = [notification.userInfo objectForKey:@"NSApplicationName"];
    [self.delegate applicationDidLaunch:self];
}
-(void) applicationDidTerminate: (NSNotification *) notification {
    self.name = [notification.userInfo objectForKey:@"NSApplicationName"];
    [self.delegate applicationDidTerminate:self];
}
```

objectForKey: 让我们从字典中读取特定条目。我们传入键 NSApplicationName，并以 NSString 形式返回正在启动或终止的应用程序的名称。

利用应用程序作为参数传入 applicationDidLaunch: 和 applicationDidTerminate: 方法这一事实，在 ActivityController.m 中创建格式化字符串以增强输出。

下载 `Dictionaries/HelloApplication13/ActivityController.m`

```objective-c
#import "ActivityController.h"
#import "CurrentApp.h"

@implementation ActivityController

@synthesize activityDisplay;

-(void) applicationDidLaunch: (CurrentApp *) app {
    [self.activityDisplay setStringValue:
        [NSString stringWithFormat:@"Launched: %@", app.name]];
}
-(void) applicationDidTerminate: (CurrentApp *) app {
    [self.activityDisplay setStringValue:
        [NSString stringWithFormat:@"Terminated: %@", app.name]];
}
@end
```

### 13.5 减少冗余

CurrentApp 中的两个 applicationDidXxx: 方法实现几乎完全相同。在每种情况下，我都插入了对委托是否响应我们选择器的检查，以防止传入未实现的方法名。

```objc
if ([self.delegate
        respondsToSelector:@selector(applicationDidXxx:)]) {
    self.name = [notification.userInfo objectForKey:@"NSApplicationName"];
    [self.delegate applicationDidXxx:self];
}
```

我们只需要一种方法，确保在一种情况下 Xxx 是 Launch，在另一种情况下是 Terminate。我们可以将通知传递给一个实用方法，并根据通知的名称选择要调用的方法，如下所示：

下载 `Dictionaries/HelloApplication14/CurrentApp.m`

```objective-c
-(void) respondToChange: (NSNotification *) notification {
    SEL methodName;

    if (notification.name == NSWorkspaceDidLaunchApplicationNotification) {
        methodName = @selector(applicationDidLaunch:);
    } else {
        methodName = @selector(applicationDidTerminate:);
    }
    if ([self.delegate respondsToSelector:methodName]) {
        self.name = [notification.userInfo objectForKey:@"NSApplicationName"];
        [self.delegate performSelector:methodName withObject:self];
    }
}

-(void) applicationDidLaunch: (NSNotification *) notification {
    [self respondToChange:notification];
}

-(void) applicationDidTerminate: (NSNotification *) notification {
    [self respondToChange:notification];
}
```

这样好多了。² 我们在 respondToChange: 方法中捕获了共同行为。我们首先根据 notification.name 的值将方法名设置为 applicationDidLaunch: 或 applicationDidTerminate:。

一个区别是我们调用方法并将 self 作为参数传入的方式。当我们拥有方法名时，我们可以像这样调用：

```objc
[self.delegate applicationDidLaunch:self]
```

现在我们需要使用 performSelector:withObject:

```objc
[self.delegate performSelector:methodName withObject:self];
```

我很高兴我们消除了重复代码，但我对 if 语句感到困扰。像 if、for、case 等控制语句不一定是坏事，但你应该考虑代码中是否有更直接的路径。

在我们的简单案例中，有很多方法可以消除 if。我将向你展示一种使用字典的技术。

2. 正如一位审稿人所指出的，此时我们可以完全删除 applicationDidLaunch: 和 applicationDidTerminate: 方法，进一步消除冗余。不幸的是，我们不得不在后面几节中重新添加它们，所以我保留它们。

### 13.6 使用字典进行流程控制

让我们再看一下那个 if 语句：

下载 Dictionaries/HelloApplication1/CurrentApp.m

```objc
if (notification.name == NSWorkspaceDidLaunchApplicationNotification) {
    methodName = @selector(applicationDidLaunch:);
} else {
    methodName = @selector(applicationDidTerminate:);
}
```

让我们创建一个字典，以通知名称为键，以方法名称为值。然后我们可以用以下内容替换 if 语句：

下载 Dictionaries/HelloApplication1/CurrentApp.m

```objc
SEL methodName = NSSelectorFromString(
    [delegateMethods objectForKey:[notification name]]);
```

无需做决定。我们只需从字典中取出方法名。

我们需要在 CurrentApp.h 中声明一个名为 delegateMethods、类型为 NSDictionary 的实例变量。我们不需要将它设为属性。我们将像这样初始化它：³

下载 Dictionaries/HelloApplication1/CurrentApp.m

```objc
- (void) initializeMethodDictionary {
    delegateMethods = [[NSDictionary alloc] initWithObjectsAndKeys:
        @"applicationDidLaunch:",
        NSWorkspaceDidLaunchApplicationNotification,
        @"applicationDidTerminate:",
        NSWorkspaceDidTerminateApplicationNotification,
        nil];
}
```

我们以逗号分隔、以 nil 结尾的列表传入键值对。在每一对中，我们先传入值，再传入键。我们将方法名存储为 NSString，因为我们放入字典的值必须是对象。

### 13.7 使用可变字典添加和删除条目

有时你想向字典添加一个条目，或从字典中删除一个或多个条目。你不能进行这些

3. 在 init 方法末尾添加对 initializeMethodDictionary 的调用。
