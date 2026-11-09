
我们的界面如下所示：

![](img/9355405953264484a02198b0e3d25b7e_325_0.png)

我们来删除 logger 文件。它们不会造成任何损害，但会让这个示例显得有点杂乱。你需要删除 Logger.h 和 Logger.m。别忘了从 Interface Builder 的 Document 窗口中删除 Logger 对象，并从 CounterAppDelegate 中移除 logger 属性。

现在 UpOrDown 需要两个输出口和两个属性：

下载 KVO/Counter/UpOrDown.h

```objc
#import <Cocoa/Cocoa.h>

@interface UpOrDown : NSObject {
    NSNumber *countOne, *countTwo;
}
@property(copy) NSNumber *countOne, *countTwo;
-(IBAction) stepOne:(id) sender;
-(IBAction) stepTwo:(id) sender;
@end
```

在 UpOrDown.m 中，你需要合成这两个变量，并实现这些动作，以使用当前计数器值设置属性：

下载 KVO/Counter/UpOrDown.m

```objc
#import "UpOrDown.h"

@implementation UpOrDown

@synthesize countOne, countTwo;

-(IBAction) stepOne: (id) sender {
    self.countOne = [NSNumber numberWithInteger:[sender integerValue]];
}
-(IBAction) stepTwo: (id) sender {
    self.countTwo = [NSNumber numberWithInteger:[sender integerValue]];
}
@end
```

在 Display.h 中为新增的文本字段添加第二个输出口：

下载 KVO/Counter7/Display.h

```objc
#import <Cocoa/Cocoa.h>
@class UpOrDown;

@interface Display : NSObject {
    IBOutlet NSTextField *displayFieldOne, *displayFieldTwo;
    IBOutlet UpOrDown *counter;
}
@end
```

在 Interface Builder 中连接好动作和输出口，并移除失效的链接。

回到 Xcode，用 Display.m 完成收尾。大部分工作我们都做了两遍。我们本可以用 KVC 取巧，但那样会掩盖本示例的重点：一个对象如何观察多个属性。

Display 对象同时在监听 countOne 和 countTwo 的变化。如果其中任意一个发生变化，就会调用 observeValueForKeyPath: 方法。这意味着我们必须弄清楚为什么会调用这个方法。这里强调的一种解决方案是检查键路径，必要时检查被观察的对象，以弄清是谁发出了通知以及为什么发出。

下载 KVO/Counter7/Display.m

```objc
#import "Display.h"

@implementation Display

- (void) updateDisplayOne: (NSNumber *) newValue{
    [displayFieldOne setIntegerValue:[newValue integerValue]];
}
- (void) updateDisplayTwo: (NSNumber *) newValue{
    [displayFieldTwo setIntegerValue:[newValue integerValue]];
}
- (void) awakeFromNib {
    [counter addObserver:self
              forKeyPath:@"countOne"
                 options:NSKeyValueObservingOptionNew
                 context:NULL];
    [counter addObserver:self
              forKeyPath:@"countTwo"
                 options:NSKeyValueObservingOptionNew
                 context:NULL];
}

- (void)observeValueForKeyPath:(NSString *)keyPath
                     ofObject:(id)object
                       change:(NSDictionary *)change
                      context:(void *)context {
    if ([keyPath isEqualToString:@"countOne"]) {
        [self updateDisplayOne:[object valueForKeyPath:keyPath]];
    } else if ([keyPath isEqualToString:@"countTwo"]) {
        [self updateDisplayTwo:[object valueForKeyPath:keyPath]];
    }
}
- (void) finalize {
    [counter removeObserver:self forKeyPath:@"countOne"];
    [counter removeObserver:self forKeyPath:@"countTwo"];
    [super finalize];
}
@end
```

我并不特别为这样的代码感到自豪。大多数情况下，你已经看到，在使用 Objective-C 进行 Cocoa 编程时，我们可以摆脱大量条件判断。这会让代码路径更清晰。

接下来的两节中，我将向你展示两种不同的方法。首先，我们将使用 KVC，根据收到的通知的键来调用正确的方法。其次，我们将引入专用观察器对象。这两种方法的区别归结为：是在注册为观察器时做出决定，还是在收到通知时做出决定。我更喜欢使用专用观察器，但我并不拘泥于此。

## 20.10 使用 KVC 选择方法

当我们收到通知时，是因为 countOne 或 countTwo 发生了变化。因此，我们可以采取的一种方法是重命名用于更新两个显示字段的方法：

下载 KVC/CountDisplay.m

```objc
- (void) updateDisplayForCountOne: (NSNumber *) newValue {
    [displayFieldOne setIntegerValue:[newValue integerValue]];
}
- (void) updateDisplayForCountTwo: (NSNumber *) newValue {
    [displayFieldTwo setIntegerValue:[newValue integerValue]];
}
```

下载 KVO/Counter9/Observer.m

```objc
#import "Observer.h"

@implementation Observer

@synthesize targetObject, targetAction;

- (void)observeValueForKeyPath:(NSString *)keyPath
        ofObject:(id)object
          change:(NSDictionary *)change
         context:(void *)context {
    [self.targetObject performSelector:self.targetAction
                            withObject:[object valueForKeyPath:keyPath]];
}

- (id)initWithTarget:(id)object action:(SEL)action {
    if (self = [super init]) {
        self.targetObject = object;
        self.targetAction = action;
    }
    return self;
}
@end
```

现在可以简化 Display 类。在 Display 头文件中声明 Observer 类型的实例变量 observerOne 和 observerTwo：

下载 KVO/Counter9/Display.h

```objc
#import <Cocoa/Cocoa.h>
@class UpOrDown;
@class Observer;

@interface Display : NSObject {
    IBOutlet NSTextField *displayFieldOne, *displayFieldTwo;
    IBOutlet UpOrDown *counter;
    Observer *observerOne, *observerTwo;
}
@end
```

在 awakeFromNib 中注册新的观察器。移除 observeValueForKeyPath:ofObject:change:context: 方法。它现在在观察器中实现。在 finalize 方法中释放这些观察器。

下载 KVO/Counter9/Display.m

```objc
#import "Display.h"
#import "Observer.h"

@implementation Display

- (void) updateDisplayOne: (NSNumber *) newValue {
    [displayFieldOne setIntegerValue:[newValue integerValue]];
}
- (void) updateDisplayTwo: (NSNumber *) newValue {
    [displayFieldTwo setIntegerValue:[newValue integerValue]];
}
- (void) awakeFromNib {
    observerOne = [[Observer alloc]
                    initWithTarget:self
                            action:@selector(updateDisplayOne:)];
    observerTwo = [[Observer alloc]
                    initWithTarget:self
                            action:@selector(updateDisplayTwo:)];
    [counter addObserver:observerOne
               forKeyPath:@"countOne"
                  options:NSKeyValueObservingOptionNew
                  context:NULL];
    [counter addObserver:observerTwo
               forKeyPath:@"countTwo"
                  options:NSKeyValueObservingOptionNew
                  context:NULL];
}
- (void) finalize {
    [counter removeObserver:observerOne forKeyPath:@"countOne"];
    [counter removeObserver:observerTwo forKeyPath:@"countTwo"];
    [super finalize];
}
@end
```

像 Observer 这样小型、单一用途的类可以让你的代码更整洁。每个 Observer 实例都知道在被调用时向哪个对象发送哪个方法。

## 20.12 更新依赖变量

有时在一个类中，你会有些变量依赖于其他变量的值。依赖变量始终可以根据独立变量重新计算。例如，假设我们想在 `UpOrDown` 中引入一个名为 `totalCount` 的新变量，它表示 `countOne` 和 `countTwo` 之和。用户每次点击任意一个步进器时，`totalCount` 的值都会改变。

我们需要能够做到以下几点：

- 注册 `totalCount` 依赖于 `countOne` 和 `countTwo`。
- 添加一个观察 `totalCount` 变化的观察器。实际上，它会监听上一步中我们注册的任意属性的变化。
- 指定当我们收到 `totalCount` 变化的通知时希望发生什么。

