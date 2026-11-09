
你会如何为它编写代码？其实，我们先从完全不用代码开始。

创建一个名为 Counter 的新 Cocoa 项目。这个示例中我们将使用单个 nib，因此双击 MainMenu.xib。将一个 NSStepper 和一个文本字段拖入窗口，并调整它们的大小，使其看起来像我们的图片。NSStepper 包含你希望在文本字段中显示的值。你只需设置限制并建立连接。

对于 stepper 的限制，我们直接使用默认值即可。你可以点击 stepper，并使用 Attributes inspector 查看：stepper 的值从 0 开始，在 0 到 100 之间以步长 1 变化。选中 Behavior 复选框，这样值就会循环回绕。

![](img/9355405953264484a02198b0e3d25b7e_314_0.png)

现在我们来建立连接。选中 stepper。按住 Control 键点击 Connections inspector 中 Sent Actions 里 selector 右侧的圆圈。将连接拖到文本字段并释放，你应该会看到这些选项：

```
performClick:
print:
selectText:
takeDoubleValueFrom:
takeFloatValueFrom:
takeIntegerValueFrom:
takeIntValueFrom:
takeObjectValueFrom:
takeStringValueFrom:
```

选择 takeIntegerValueFrom:。最后一步，点击文本字段，并使用 Attributes inspector 将其标题设置为 0。这样，当用户运行你的应用程序时，初始值就会显示出来。保存工作，然后返回 Xcode。点击 Build & Run。你就得到了一个无需代码即可工作的计数器。

到目前为止，还没有任何观察行为发生。现在，当用户点击 stepper 时，stepper 会向文本字段发送一条消息。这是传统的 target-action 方法。下一节中，我们会用代码把这一点表达得更明确，以便你能看到消息发送的方向。然后，我们会颠覆这个模型，并引入观察者。

## 20.2 一个 Target-Action 计数器

在设置观察者之前，我要让你扩展这个示例：在 stepper 和文本字段之间插入两个对象，以说明我们目前使用的是 target action。stepper 会向 UpOrDown 对象发送消息，UpOrDown 对象会向 Display 对象发送消息，Display 对象会向文本字段发送消息。流程大致如下：

![](img/9355405953264484a02198b0e3d25b7e_315_0.png)

这可能感觉像是朝错误方向迈出的一步，但我认为，当我们在下一节讲到 KVO 时，这会有助于你更好地看清 KVO 能带来什么。

创建一个新的 Objective-C 类，命名为 Display。这个类需要一个 outlet，你会把它连接到文本字段；还需要一个方法，供 UpOrDown 对象调用，以传入文本字段的新值。

注意，displayField 没有对应的 property，所以我们在声明变量时将其标记为 IBOutlet。如果有对应的 property，从技术上讲，我们可以把 IBOutlet 标记留在实例变量声明处，但更好的做法是像我们之前那样把它移到 property 声明中。

下载 KVO/Counter2/Display.h

```objc
#import <Cocoa/Cocoa.h>

@interface Display : NSObject {
    IBOutlet NSTextField *displayField;
}
-(void)updateDisplay: (NSNumber *) newValue;
@end
```

Display 的实现只包含更新文本字段的那个方法：

下载 KVO/Counter2/Display.m

```objc
#import "Display.h"

@implementation Display

-(void)updateDisplay: (NSNumber *) value{
    [displayField setIntegerValue:[value integerValue]];
}

@end
```

另外，创建一个新的 Objective-C 类，命名为 UpOrDown，用来接收来自 stepper 的 action，并将其传递给 Display 对象。UpOrDown 需要一个 outlet 来连接 Display，还需要一个 action 方法：

下载 KVO/Counter2/UpOrDown.h

```objc
#import <Cocoa/Cocoa.h>
@class Display;

@interface UpOrDown : NSObject {
    IBOutlet Display *display;
}
-(IBAction) step:(id) sender;
@end
```

实现该 action，以调用 Display 的 updateDisplay: 方法：

下载 KVO/Counter2/UpOrDown.m

```objc
#import "UpOrDown.h"
#import "Display.h"

@implementation UpOrDown

-(IBAction) step: (id) sender {
    [display updateDisplay:
        [NSNumber numberWithInteger:[sender integerValue]]];
}
@end
```

保存工作，然后转到 Interface Builder，把所有连接都接好。

向 Document 窗口添加一个类型为 `Display` 的对象和一个类型为 `UpOrDown` 的对象。在 Connections Inspector 中，首先断开 stepper 与文本字段之间的直接连接。点击 `UpOrDown`，将 `display` outlet 连接到 `Display` 对象。将 `step:` 的 received action 连接到 stepper。点击 `Display`。将 `displayField` outlet 连接到文本字段。保存，然后点击 **构建并运行**。

从用户的角度看，这个版本与无代码版本没有区别。

注意，`Display` 对象不必了解 `UpOrDown` 对象的任何信息，但 `UpOrDown` 对象需要了解 `Display` 对象。接下来，当我们让 `Display` 对象成为观察者时，我们会把这个关系颠倒过来。

## 20.3 引入观察者

在传统的 target-action 方法中，`UpOrDown` 对象持有指向 `Display` 对象的句柄，并向该对象发送 `updateDisplay:` 消息。使用 KVO 时，观察者知道自己正在观察谁。被观察对象只会在状态发生变化时发出消息——所有已注册的观察者都会收到通知。

在我们的示例中，`Display` 对象需要向 `UpOrDown` 对象发送消息，以注册为观察者。这意味着我们的 `Display` 对象需要一个指向 `UpOrDown` 对象的句柄。此时，你得到的关系如下：

![](img/9355405953264484a02198b0e3d25b7e_317_0.png)

换句话说，你并没有改变 UpOrDown 与 stepper 之间，或 Display 与文本字段之间的关系。但现在 Display 需要了解 UpOrDown，而之前情况正好相反。

我们的图指出了一个以前没有、现在却存在的问题：没有任何东西持有 Display 对象。我们的应用程序在启用垃圾回收的情况下运行。除非我们持有它，否则 Display 对象会先将自己注册为观察者，然后被垃圾回收。

向 app delegate 添加一个 property：

下载 KVCO/Counter3/CounterAppDelegate.h

```
    #import <Cocoa/Cocoa.h>
    @class Display;

    @interface CounterAppDelegate : NSObject <NSApplicationDelegate> {
        NSWindow *window;
        Display *display;
    }
    @property (assign) IBOutlet NSWindow *window;
    @property IBOutlet Display *display;
    @end
```

在实现文件中合成该 property，并在 Interface Builder 中将这个 outlet 连接到 Display 对象。

接下来，我们将 Display 对象连接到 UpOrDown 对象，并为添加观察者做好准备。首先，在 Display 的头文件中添加一个 IBOutlet：

下载 KVCO/Counter3/Display.h

```
    #import <Cocoa/Cocoa.h>
    @class UpOrDown;

    @interface Display : NSObject {
        IBOutlet NSTextField *displayField;
        IBOutlet UpOrDown *counter;
    }
    @end
```

我已经移除了 updateDisplay: 方法的声明。我们仍然会实现这个方法，但它不再是 Display 公共接口的一部分。

接下来，我们转到它正在观察的对象。UpOrDown 头文件可以稍作修改。我们会移除所有对 Display 的引用，并添加一个名为 count、类型为 NSNumber 的 ivar。

下载 KVC/Counters/UpOrDown.h

```objc
#import <Cocoa/Cocoa.h>

@interface UpOrDown : NSObject {
    NSNumber *count;
}
-(IBAction) step:(id) sender;
@end
```

我们去修正 nib 文件，然后再回来实现这两个类。在 Interface Builder 中，断开 UpOrDown 的 display outlet 与 Display 之间的连接。选中 Display，并将其 counter outlet 连接到 UpOrDown。保存工作。

现在，我们准备好设置观察者了。基本步骤有三步：

- 1. 观察者需要向包含其想要观察的 property 的对象注册。
- 2. 被观察对象必须以其观察者会收到变更通知的方式来更新 property。
- 3. 观察者必须响应它收到的通知。

我们依次来看这几点。

## 20.4 注册观察者

注册为观察者很容易。你只需向想要观察的对象发送这条消息：

```
addObserver:forKeyPath:options:context:
```

第一个参数传入指向观察者的指针。在这个例子中，我们会传入 self，但你可以使用任何对象。keypath 是指向我们所关注的 property 的路径。这与你学习 KVC 时看到的形式相同。有四个选项可用，你可以使用 | 将它们组合起来。

四个 NSKeyValueObservingOptions 分别是 NSKeyValueObservingOptionNew、NSKeyValueObservingOptionOld、NSKeyValueObservingOptionInitial 和 NSKeyValueObservingOptionPrior。前两个控制你获取所观察属性的新值还是旧值。第三个会在你首次设置观察者时发送通知。最后一个表示你希望在每次变化前后都收到消息，而不只是在变化之后。
