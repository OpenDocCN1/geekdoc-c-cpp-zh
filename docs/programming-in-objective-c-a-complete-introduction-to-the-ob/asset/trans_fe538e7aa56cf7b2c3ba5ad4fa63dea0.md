
```objective-c
    [myFoo release];
return 0;
}
```

# 程序 17.6 输出

```
myFoo retain count = 1
after pool drain = 1
after autorelease = 1
after retain = 2
after second pool drain = 1
```

程序分配了一个新的 `Foo` 对象并将其赋值给变量 `myFoo`。正如你所看到的，它的初始引用计数为 1。注意这个 `autorelease` 消息，因此清空池不会使该对象失效。系统分配了一个新池，`myFoo` 通过 `autorelease` 消息被添加到池中。同样，它的引用计数没有变化，因为将对象添加到自动释放池不会影响它的引用计数——它只是将其标记为稍后释放。

接下来，你向 `myFoo` 发送了 `retain` 消息。这将其引用计数改为 2。当你第二次清空池时，`myFoo` 的引用计数由于之前发送的 `autorelease` 消息而减了 1，因此在池释放时它对应一个 `release` 消息。

由于 `myFoo` 在池释放之前被 `retain` 过，它在递减后的引用计数仍然大于 0。因此，`myFoo` 在池清空后依然存活并是一个有效对象。最后，你现在必须释放自己，我们在程序 17.6 中执行了这一点，以清理内存并避免内存泄漏。

如果你觉得对自动释放池的解释仍然有些模糊，请重读一遍。当你理解了程序 17.6，你就能彻底理解自动释放池及其工作原理。

# 内存管理规则总结

让我们总结一下在本章中学到的内存管理知识：

- 发送 `release` 消息并不一定会销毁对象。当对象的引用计数减到 0 时，对象会被销毁。系统通过向对象发送 `dealloc` 消息来释放其内存。

- 如果你需要持有一个对象以确保它不被他人销毁，你应该对其进行 `retain`。在使用完后，请务必对其进行 `release`。

- 对于你通过 `retain` 或使用 `copy`、`mutable-Copy`、`alloc` 或 `new` 方法创建的对象，都要进行 `release`。这包括带有 `retain` 或 `copy` 属性的属性。你可以重写 `dealloc` 方法在对象销毁时释放你的实例变量。

# 关于事件循环和内存分配

- `autorelease pool` 在池清空时自动释放对象。系统通过在池中的每个对象每次被 `autorelease` 时向其发送 `release` 消息来实现。自动释放池中任何引用计数变为 0 的对象都会收到 `dealloc` 消息并被销毁。
- 如果你在方法内部不再需要某个对象但需要返回它，请向它发送 `autorelease` 消息将其标记为稍后释放。`autorelease` 消息不会影响对象的引用计数。
- 当应用程序终止时，所有对象占用的内存都会被释放，无论它们是否在自动释放池中。
- 在开发 Cocoa 或 iOS 应用时，自动释放池会在程序执行期间不断创建和清空（每当事件发生时都会）。在这种情况下，如果你想确保你的对象在自动释放池清空时不被自动销毁，你需要对其进行 `retain`。所有引用计数大于其发送的 `autorelease` 消息数量的对象在池释放后都会存活。

正如上一节所述，Cocoa 和 iOS 应用运行在所谓的运行循环或事件循环内部。将事件想象为由你执行某些操作（例如按下 iPhone）或隐式操作（例如通过网络接收数据）触发的动作。为了处理事件，系统会创建一个新的自动释放池，并可能调用你应用程序中的某些方法来处理。当你处理完事件后，你会从方法返回，系统将等待下一个事件发生。在此之前，系统会清空自动释放池。这意味着你在处理该事件时创建的任何 `autorelease` 对象都会被销毁，除非你对这些对象进行了 `retain`，这样它们就能生存池清空。

查看以下来自一个 iOS 应用的接口部分。在这里我们定义了一个 `MyView` 类，包含一个名为 `data` 的实例：

```objective-c
#import <UIKit/UIKit.h>

@interface MyView : UIView
{
    NSMutableArray *data;
}
```

```objective-c
@property (nonatomic, retain) NSMutableData *data;
@end
```

假设我们在实现部分为 `data` 变量合成了访问器方法。进一步假设我们有一个名为 `viewDidLoad` 方法，每当你的视图加载到内存时，系统就会调用它（当你学习 iOS 编程时会学到更多，目前这些细节并不重要）。

假设你想在 `viewDidLoad` 方法中分配 `data` 数组，因此在该方法内部插入了以下行代码：

```objective-c
data = [NSMutableArray array];
```

如你所知，`array` 方法会创建一个 `autorelease` 数组，你将其直接赋值给实例变量 `data`。问题在于，一旦当前事件处理完成，数组就会被销毁。因为它被添加到了事件循环结束时清空的自动释放池中。为了确保数组在整个事件循环中存活，你有几种替代方案。以下是三行可以使用的代码：

```objective-c
data = [[NSMutableArray array] retain]; // 在池清空后存活
```

```objective-c
data = [[NSMutableArray alloc] init]; // 在池清空后存活
```

```objective-c
data = [[NSMutableArray array] copy]; // 在池清空后存活
```

```objective-c
data = [[NSMutableArray array] mutableCopy]; // 在池清空后存活
```

```objective-c
(void)dealloc {
    [data release];
    [super dealloc];
}
```
