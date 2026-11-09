
# 乔问……
## 为什么我要费心使用点语法？

关于这个问题一直存在不少争议。有些人反对这一点：当你编写如下代码时：

```
self.name = newName;
```

你实际上是在进行方法调用，即使看起来不像。确实如此，但使用点语法的优势在于，获取或设置属性与向对象发送消息是两种不同的活动，即使底层机制相同。点语法能明确你的意图。

当你发送如下消息时：

```
[greeter greeting];
```

这显然与设置或获取属性值完全不同。你会发现 Apple 在其现代 API 中采用了点语法。当你查看某个类的任务时，你会看到其中许多实际上是属性。在你使用点号表示法进行获取和设置一段时间后，你会发现代码更易读，也能更快理解。

在 http://eschatologist.net/blog/?p=160 上，Chris Hanson 充满热情地更详细解释了为什么你要对属性使用点语法。

现在我们已经声明并合成了一个属性，因此你现在像这样设置变量的值：

```
self.name = newName;
```

我们并没有绕回原点。当你使用 self.name = newName 时，你使用的是设置方法，而不是直接设置底层变量。

你希望使用属性而不是变量，以利用我们很快会添加到属性上的各种设置。这是属性最常见的错误之一。你费尽周折声明并合成一个属性，然后却忘记使用 self，最终直接使用了实例变量而不是属性。

更重要的是，我们可以从 HelloWorldAppDelegate 访问这个属性。首先，我想重新看一下 HelloWorldAppDelegate：

下载 Properties/HelloWorld14/HelloWorldAppDelegate.h

```objective-c
#import <Cocoa/Cocoa.h>

@interface HelloWorldAppDelegate : NSObject <NSApplicationDelegate> {
    NSWindow *window;
}
@property (assign) IBOutlet NSWindow *window;
@end
```

既然你了解了属性，就能认出类型为 NSWindow 的变量 window 被声明为属性。如果你查看 HelloWorldAppDelegate.m 的顶部，你会看到它已被合成；你可能还记得，在 applicationDidFinishLaunching: 的底部，当我们把标签添加到其内容视图时，是以属性方式访问它的。

```objective-c
[[self.window contentView] addSubview:label];
```

一旦你重构 setUpperCaseName: 方法中的代码以利用点语法，它应该像这样：

下载 Properties/HelloWorld14/HelloWorldAppDelegate.m

```objective-c
-(void) setUpperCaseName:(Greeter *) greeter {
    NSLog(@"The name was originally %@", greeter.name);
    greeter.name = [greeter.name uppercaseString];
    NSLog(@"The name is now %@", greeter.name);
}
```

## 5.6 属性特性

属性声明的一般形式如下：

```objective-c
@property(attribute1, attribute2,...) PropertyType propertyName;
```

这些特性用于指明在合成属性时，你希望创建哪种访问器。

一组特性让你决定是生成获取器和设置器，还是只生成获取器。默认情况下，你会生成两者，因此不需要使用 readwrite 特性；但如果你只想生成获取器，就要使用 readonly。

另一组特性可用于设置访问器名称。这通常用于布尔值的情况。你可能有一个名为

另一个选项是将属性的底层变量设置为指向参数所指向的对象。这是 `assign` 的指针版本；如果没有内存管理，其实现会完全相同。假设我们有一个名为 `buddy`、类型为 `Greeter` 的属性。设置器大致如下：

```objective-c
-(void) setBuddy:newBuddy {
    if (buddy != newBuddy) {
        [buddy release];
        buddy = [newBuddy retain];
    }
} //retain
```

这些规则适用于 iPhone 和 Mac OS X 开发。如果你利用了垃圾回收器，那么不必担心保留和释放变量，因此凡是你原本会使用 `assign` 或 `retain` 的地方，都可以使用 `assign`。⁵

如果你想把属性声明为 `nonatomic`，还需要设置一个特性。默认情况下，访问器是 `atomic` 的。当属性是 `atomic` 时，对该属性的访问是线程安全的。在使用垃圾回收器的桌面应用中，这几乎没有成本。当你不使用垃圾回收器时，在获取器中必须设置对象级锁、取回所需值、释放锁，然后返回取回的值。在这种情况下实现原子设置器的细节也类似。

当你为 iPhone 编写代码时，不会有可用的垃圾回收器。如果你频繁访问属性，就会感到性能下降。因此，当我们为 iPhone 声明属性时，往往会设置 `nonatomic` 特性；而为桌面开发时，我们会使用默认设置。更多信息请阅读 Apple 的 *《Objective-C 编程语言》* [App09] 中的“Declared Properties”章节。

## 5.7 练习：添加属性

向 `Greeter` 添加这三个属性：一个名为 `age` 的 `NSInteger`，一个名为 `buddy` 的 `Greeter`，以及一个名为 `upperCase` 的 `BOOL`。

⁵ 我假设你的 Mac OS X 应用程序将以 Leopard 及更高版本为目标，因此你会使用垃圾回收器。对于桌面应用程序，你的两个内存特性选择是 `assign` 和 `copy`。

为了本练习的目的，假设你没有使用垃圾回收，因此需要区分 assign 和 retain。

使用正确的特性，使 age 有获取器但没有设置器，并让 upperCase 的获取器名为 isUpperCase。

## 5.8 解决方案：添加属性

所有困难的工作都在头文件中。你需要声明这三个实例变量，然后像这样声明属性：

下载 Properties/HelloWorld15/Greeter.h

```objc
#import <Cocoa/Cocoa.h>

@interface Greeter : NSObject {
    NSString *name;
    NSInteger age;
    Greeter *buddy;
    BOOL upperCase;
}
-(NSString *) greeting;
-(id) initWithName:(NSString *)name;
@property(copy) NSString *name;
@property(assign, readonly) NSInteger age;
@property(retain) Greeter *buddy;
@property(assign, getter=isUpperCase) BOOL upperCase;
@end
```

name 变量是 NSString，它符合 NSCopying，因此我们使用 copy 特性。

age 和 upperCase 都是基本类型，因此我们使用 assign。因为我们只为 age 生成获取器，所以还使用 readonly。为了遵循布尔值的正确命名约定，我们通过添加 getter=isUpperCase 来指定 upperCase 的获取器应为 isUpperCase。

buddy 属性是 Greeter。它是指向一个不符合 NSCopying 的对象的指针，因此我们使用 retain 作为内存特性。

在实现文件中，将三个新属性的名称添加到 @synthesize 行，并用逗号分隔。注意，我们还在 initWithName: 中初始化了 upperCase 变量：

下载 Properties/HelloWorld15/Greeter.m

```objc
#import "Greeter.h"

@implementation Greeter
```

那么，让我们移除为属性提供支持的实例变量。首先，让我们检查你的项目设置。从菜单栏用 Project > Edit Project Settings 打开它们。选择 Build 标签，将 Architectures 设置设为 64-bit Intel，并勾选仅构建活跃架构的复选框。

![](img/9355405953264484a02198b0e3d25b7e_100_0.png)

现在你可以从头文件中移除实例变量：

[下载 Properties/HelloWorld/Greeter.h](download)

```objc
#import <Cocoa/Cocoa.h>

@interface Greeter : NSObject {
}
-(NSString *) greeting;
-(id) initWithName:(NSString *)name;
@property(copy) NSString *name;
@property(assign, readonly) NSInteger age;
@property(retain) Greeter *buddy;
@property(assign, getter=isUpperCase) BOOL upperCase;

@end
```

点击 Build & Run，应用程序应和之前完全一样运行。如果移除实例变量后出现警告，请检查你是否在 64 位下运行，以及项目设置是否正确。

如果你是为 iPhone 开发，⁶ 你可以移除支持属性的实例变量；但如果你是在 32 位 Mac OS X 运行时上开发或为其开发，则不能这样做。

6. 在撰写本书时，针对 iPhone 时你可以移除这些变量，代码将在设备上正常工作。模拟器尚不支持移除变量。
