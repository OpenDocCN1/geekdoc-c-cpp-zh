

## 创建自定义工作队列

被推送了，但它们可能会以任意的顺序完成，并且可能有多个任务同时运行。

还有一个特殊的队列，旨在在主线程上运行。你可以通过 `dispatch_get_main_queue()` 获取它的引用。该队列在 OS X 10.6 上用于实现运行循环（run loop）。这是一个 FIFO（先进先出）队列，你可能想要创建类似的队列。FIFO 队列类似于轻量级线程。它按顺序执行，一次执行一个块。线程与队列之间的关系是变化的。取决于各种因素，你的所有队列最终可能会在不同的线程上并发运行，也可能都在在单个 OS 线程上执行。

你通过调用 `dispatch_queue_create()` 创建一个新的 FIFO 队列。当你有一许多需要按照定义顺序执行、但与程序的其余部分大部分独立的任务时，这非常有用。这有助于减少对显式同步的需求。

本章开头的示例向新队列推送了三个递增计数器的块，以及一个打印其最终值的块。这些块之间都是相互相关的；以错误的顺序执行它们是一个非常糟糕的主意。通过这种方法，它们彼此之间的执行顺序是有保证的，但对于程序的其余部分则不是。这意味着除非你计划从队列外部访问计数器变量，否则你不需要对计数器变量加任何锁。

## 通知

Objective-C 鼓励松散耦合，Foundation 框架中没有什么比*通知*机制*更能体现这一点的了。通知是为任意数量的监听者实现回调的一种简单方法。

你可以监听特定名称的、来自特定对象的或两者兼顾的通知。通知本身包含一个发送者、一个名称以及与之关联的字典，因此对象可以向监听通知的对象传递任意数量的信息。

如果你使用通知，就会让你的类复用变得非常容易。你不需要期望每个想要监听你的类事件的类都实现特定的接口，你只需要发布通知即可。任意数量的类可以监听来自同一个对象的通知，而你的类不需要实现存储这些类引用的任何逻辑。

## 请求通知

```objectivec
-(void)notify:(NSNotification*)note {
    NSLog("Received %@", note);
}
-(void)registerListener {
    NSNotificationCenter *nc =
        [NSNotificationCenter defaultCenter];
    [nc addObserver:self
          selector:@selector(notify:)
          name:"Example"
          object:nil];
}
-(void)dealloc {
    NSNotificationCenter *nc =
        [NSNotificationCenter defaultCenter];
    [nc removeObserver:self];
    [super dealloc];
}
```

来自: notify.m 要监听通知，你需要为你的线程向 `NSNotificationCenter` 对象注册这些感兴趣。这是通知的路由点。当通知被发布时，它会被发送到通知中心，通知中心将其转发给所有感兴趣的方。大多数情况下，你将使用默认通知中心。可以为不同的用途创建不同的通知中心，但最常见的是使用标准的那个。这是通过向 `NSNotificationCenter` 发送 `+default` 消息获取的。

要注册通知，你只需向中心发送 `-addObserver:selector:name:object:` 消息。注意此消息中的 `selector` 参数。单个对象可能在不同的方法上接收不同的通知。这非常有用，因为这意味着你不需要测试收到了什么种的通知，并且可以干净地将不同的事件处理器分离到不同的方法中。

在注册观察者时，对象或通知名称可以为 `nil`。这允许你注册接收特定对象发送的所有消息，或者接收特定类型的所有通知（无论其发送者是谁）。

这些对于调试比其他任何东西都有用。例如，你可以编写一个日志切面，监听所有特定类型的通知并记录发送者。

监听通知时需要记住的一点是，通知中心不会保留（retain）你的对象。如果你的对象在销毁时仍然注册了接收通知，那么当下次发送其中一个通知时，你的程序将会崩溃。

为了避免这种情况，请确保在 `-dealloc` 方法中发送 `-removeObserver:` 消息。如果你忘记这样做，崩溃将不会明显。你将在回溯轨迹中看到很多奇怪的东西，包括通知中心。

## 发送通知

```objectivec
NSNotificationCenter *nc = 
[NSNotificationCenter defaultCenter];
[nc postNotificationName:@"Example" 
object:@"sender" 
userInfo:nil];
```

来自: notify.m 发布通知比注册监听还要简单。发布通知对象的标准方法是构造一个 `NSNotification` 对象然后发送它。

在实践中，我认为我从未见过写执行这种操作的代码。通知中心有一些便利方法，可以在单次操作中构造并发布通知。

发送通知最常用的方法是 `-postNotificationName:object:userInfo:` 方法。还有该方法的简化版本，它省略了 `userInfo:` 参数，等同于将 `nil` 作为最后一个参数。

注意，对象——通知的发送者——被指定为一个参数。这意味着可能发送声称来自另一个对象的通知。这意味着，例如，外观模式（façades）或 C 代码可以代表其他对象发送通知。

## 队列通知

```objectivec
NSNotificationQueue *ng = [NSNotificationQueue defaultQueue];
NSNotification *note = [NSNotification notificationWithName:@"Example" object:@"sender"];
[ng enqueueNotification:note postingStyle:NSPostWhenIdle];
[NSRLoop currentLoop run];
```

来自: notify.m

有时，你的代码可能会产生大量的通知，或者产生一些不需要立即处理的通知。`NSNotificationQueue` 类解决了这两个问题。

通知队列既可以延迟交付通知，也可以合并它们。与 `NSNotificationCenter` 不同，队列没有构造通知的便利方法，你必须自己完成。然后以三种发布样式之一发布通知。

在示例中，通知的交付被延迟到运行循环没有其他事件时。定时器和文件描述符的数据就绪具有优先级。或者，你可以在下一次运行循环迭代或立即发布。

如果你发送大量相同类型的通知，那么缓存通知对象是一个好主意。反复将同一个对象传递给通知队列是非常廉价的，它可以自动发送一次通知。

如果你使用较长的队列通知方法，参数之一是 `coalesceMask:`，它决定了如何合并通知。你可以合并相同名称的通知、相同发送者的通知或两者。合并对于 `NSPostWhenIdle` 发布样式最有用。这对于触发某些低优先级计数代码非常理想。

## 在应用程序之间发送通知

```objectivec
[c
 addObserver:self
 selector:@selector(newCopyStarted:)
 name:ProcessDidStart
 object:nil
 suspensionBehavior:NotificationSuspensionBehaviorHold];
```

来自: distributedNotify.m 通知提供的松耦合非常有以以在 Foundation 框架内部得到了扩展，为应用程序之间的通信提供了一种（简单的）机制。`NSDistributedNotificationCenter` 类是 `NSNotificationCenter` 的子类，向其他应用程序广播通知。这种扩展需要一些更改。普通通知关联有一个发送者，它是指向某些对象的指针。指针在另一个地址空间的进程中并不特别有用，因此分布式通知使用字符串作为发送者。这可以是任何你喜欢的内容，但通常是应用程序名称。通知可以关联字典。在应用程序内部，这些字典可以包含任何对象，但对于广播，它们被限制为可以存储在属性列表中的对象（见第 9 章）。

