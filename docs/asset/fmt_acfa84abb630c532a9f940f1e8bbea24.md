
来源：`libdispatch`

`FIFO` 自带三个并发队列，这些是默认创建的。这些队列注册在三个优先级级别：低、默认和高。每个队列上并发运行的任务数量取决于系统的负载和可用的 CPU 核心数。你可以使用上一节中看到的 `dispatch_get_global_queue()` 函数获取其中一个队列的句柄。

创建新的并发队列是没有意义的。推入并发队列的块将按照它们被

## 创建自定义工作队列

被推送了，但它们可能会以任意的顺序完成，并且可能有多个任务同时运行。

还有一个特殊的队列，旨在在主线程上运行。你可以通过 `dispatch_get_main_queue()` 获取它的引用。该队列在 OS X 10.6 上用于实现运行循环（run loop）。这是一个 `FIFO`（先进先出）队列，你可能想要创建类似的队列。`FIFO` 队列类似于轻量级线程。它按顺序执行，一次执行一个块。线程与队列之间的关系是变化的。取决于各种因素，你的所有队列最终可能会在不同的线程上并发运行，也可能都在在单个 OS 线程上执行。

你通过调用 `dispatch_queue_create()` 创建一个新的 `FIFO` 队列。当你有一许多需要按照定义顺序执行、但与程序的其余部分大部分独立的任务时，这非常有用。这有助于减少对显式同步的需求。

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
    NSNotificationCenter *nc = [NSNotificationCenter defaultCenter];
    [nc addObserver:self selector:@selector(notify:) name:"Example" object:nil];
}
-(void)dealloc {
    NSNotificationCenter *nc = [NSNotificationCenter defaultCenter];
    [nc removeObserver:self];
    [super dealloc];
}
```

来自: `notify.m` 要监听通知，你需要为你的线程向 `NSNotificationCenter` 对象注册这些感兴趣。这是通知的路由点。当通知被发布时，它会被发送到通知中心，通知中心将其转发给所有感兴趣的方。大多数情况下，你将使用默认通知中心。可以为不同的用途创建不同的通知中心，但最常见的是使用标准的那个。这是通过向 `NSNotificationCenter` 发送 `+default` 消息获取的。

要注册通知，你只需向中心发送 `-addObserver:selector:name:object:` 消息。注意此消息中的 `selector` 参数。单个对象可能在不同的方法上接收不同的通知。这非常有用，因为这意味着你不需要测试收到了什么种的通知，并且可以干净地将不同的事件处理器分离到不同的方法中。

在注册观察者时，对象或通知名称可以为 `nil`。这允许你注册接收特定对象发送的所有消息，或者接收特定类型的所有通知（无论其发送者是谁）。

这些对于调试比其他任何东西都有用。例如，你可以编写一个日志切面，监听所有特定类型的通知并记录发送者。

监听通知时需要记住的一点是，通知中心不会保留（retain）你的对象。如果你的对象在销毁时仍然注册了接收通知，那么当下次发送其中一个通知时，你的程序将会崩溃。

为了避免这种情况，请确保在 `-dealloc` 方法中发送 `-removeObserver:` 消息。如果你忘记这样做，崩溃将不会明显。你将在回溯轨迹中看到很多奇怪的东西，包括通知中心。

## 发送通知

```objectivec
NSNotificationCenter *nc = [NSNotificationCenter defaultCenter];
[nc postNotificationName:@"Example" object:@"sender" userInfo:nil];
```

来自: `notify.m` 发布通知比注册监听还要简单。发布通知对象的标准方法是构造一个 `NSNotification` 对象然后发送它。

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

来自: `notify.m`

有时，你的代码可能会产生大量的通知，或者产生一些不需要立即处理的通知。`NSNotificationQueue` 类解决了这两个问题。

通知队列既可以延迟交付通知，也可以合并它们。与 `NSNotificationCenter` 不同，队列没有构造通知的便利方法，你必须自己完成。然后以三种发布样式之一发布通知。

在示例中，通知的交付被延迟到运行循环没有其他事件时。定时器和文件描述符的数据就绪具有优先级。或者，你可以在下一次运行循环迭代或立即发布。

如果你发送大量相同类型的通知，那么缓存通知对象是一个好主意。反复将同一个对象传递给通知队列是非常廉价的，它可以自动发送一次通知。

如果你使用较长的队列通知方法，参数之一是 `coalesceMask:`，它决定了如何合并通知。你可以合并相同名称的通知、相同发送者的通知或两者。合并对于 `NSPostWhenIdle` 发布样式最有用。这对于触发某些低优先级计数代码非常理想。

## 在应用程序之间发送通知

```objectivec
[c addObserver:self selector:@selector(newCopyStarted:) name:ProcessDidStart object:nil suspensionBehavior:NotificationSuspensionBehaviorHold];
```

来自: `distributedNotify.m` 通知提供的松耦合非常有以以在 Foundation 框架内部得到了扩展，为应用程序之间的通信提供了一种（简单的）机制。`NSDistributedNotificationCenter` 类是 `NSNotificationCenter` 的子类，向其他应用程序广播通知。这种扩展需要一些更改。普通通知关联有一个发送者，它是指向某些对象的指针。指针在另一个地址空间的进程中并不特别有用，因此分布式通知使用字符串作为发送者。这可以是任何你喜欢的内容，但通常是应用程序名称。通知可以关联字典。在应用程序内部，这些字典可以包含任何对象，但对于广播，它们被限制为可以存储在属性列表中的对象（见第 9 章）。

# 第 16 章：通知

**注意：** 在 OS X 上，只有一种类型的分布式通知中心，它向与发送者具有相同用户 ID 的运行应用程序发送通知。GNUStep 提供了另外两种：一个用于与计算机上的所有应用程序通信（无论用户是谁），另一个用于在局域网中广播通知。

分布式通知的递送语义也略有不同。当你发布一个（普通）通知时，它是同步递送的。发送对象已经拥有了 CPU 的控制权。其方法的栈帧位于栈的顶端，它可以自由地将程序流委托给通知中心，然后由通知中心将其委托给通知监听器。

但对于分布式通知，情况并非如此。你不能直接在函数的中间¹中断正在运行的任何进程，而你必须等待到一个合适的时机。分布式通知通过与运行循环（run loop）交互来处理这个问题。要接收分布式通知，你必须使用 `NSRunLoop`。`distributedNotify.m` 示例是一个简单的程序，每当它自己的新实例启动时就会写入一条日志消息。

> ¹ 嗯，你可以这样做；信号（signals）正是这样做的，但你从信号处理器中能执行的操作是非常有限的。

# 在应用程序之间发送通知 309

```objectivec
- (id)init
NSDistributedNotificationCenter *c = [NSDistributedNotificationCenter defaultCenter];
[c addObserver:self selector:@selector(newCopyStarted:) name:ProcessDidStart object:nil suspensionBehavior:NSNotificationSuspensionBehaviorHold];
ProcessInfo *pinfo = [ProcessInfo processInfo];
NSNumber *pid = [NSNumber numberWithInt:[pinfo processIdentifier]];
NSDictionary *userInfo = [NSDictionary initWithObject:pid forKey:@"pid"];
[c postNotificationName:ProcessDidStart object:[pinfo projectName] userInfo:userInfo options:0];
[[NSRLoop currentRunLoop] run];
```

来自：此类的 `-init` 方法执行了所有的实际工作。首先，它为分布式通知注册了观察者。对象为 `nil`，因此它将从任何发送者处接收此通知。然后它构建了通知。`userInfo` 字典包含一个键值对，用于存储进程 ID。

发布通知后，它启动了运行循环。程序程序将处于阻塞状态，直到发生某些运行循环事件。此程序中只有一个事件定义了处理程序，因此它所能做的就是每当发布了 `ProcessDidStart:` 通知时，它就会接收到 `-newCopyStarted:` 消息，而这只会在运行该程序的另一个副本时才会发生。

如果你编译并运行此示例，你会发现它接收了它自己的通知，因此它会告诉你它已经启动。如果你运行另一个副本，你将从每个运行的实例收到一条日志消息，告诉你关于新实例的信息。

这是一个非常简单的示例，但也很用于分布式通知来处理更复杂的事件。例如，我在 XMPPPKit 中使用它们，以便在用户更改在线状态时通知所有运行的应用程序。其他程序监听此变化，并将新的状态消息推送到微博客站点。

## 网络访问

编写网络感知型应用程序的标准跨平台方法是 Berkeley Sockets API。它是作为开发 TCP/IP 的同一项资助的一部分编写的，并设计为与协议无关。

大多数语言都有此 API 的实现。在 Objective-C 中，你像既往一样可以自由使用 C 版本，它提供了底层接口的所有功能。

然而，在大多数情况下，这费了很大精力却收效甚微。Foundation 框架提供了几个类，使得编写网络应用程序变得更加容易。使用这些抽象有时会让你失去一些底层 API 的功能，但并不多。

# 第 17 章：网络访问

## 封装 C Socket

```objectivec
return [[NSFileHandle alloc] initWithFileDescriptor:s closeOnDealloc:YES] autorelease];
```

来自：`NSFileHandle+Socket.m`

我们在第 13 章中简要查看了 `NSFileHandle` 类，我提到过它封装了一个文件描述符（file descriptor）。socket API 的设计基于 UNIX 的“万物皆文件（即使在不符合逻辑的情况下也是）”模型，因此 socket 也是文件描述符。你可以对读取和写入 socket 使用相同的函数调用，就像你对任何其他文件描述符使用的那样。

你也可以使用 `NSFileHandle` 来封装 socket。这允许你使用底层 API 创建一个符合你精确规格的 socket，然后使用更抽象的方式与创建的 socket 交互。如果你需要使用底层 socket API 中任何高层 API 未方便暴露的set，那么这就是你可以使用的唯一解决方案。在其他情况下，它通常是最方便的方法。

将你的 socket 封装在文件描述符对象中最大的优势是你可以轻松将其与运行循环集成。这让你能够非常容易地编写事件驱动的 socket 代码。其他

# 封装 C Socket 313

**注意：** 记住，Objective-C 的目标是让 C 程序员的生活变得更容易。不要为了使用 API 而使用 Objective-C API，只有当它们比 C API 更能作为你特定问题的合理解决方案时才使用它们。使用仅仅是 C API 浅层封装的 Objective-C API 会增加开销和复杂性，但不会让你的代码变得更容易维护。

另一个巨大的优势是，你可以为 socket 使用 Objective-C 的引用计数。如果你在创建 `NSFileHandle` 时将 `YES` 作为参数传递给 `closeOnDealloc:`，那么该文件描述符将在对象被释放时被关闭。

如果你向你的对象发送 `waitForDataInBackgroundNotify` 消息，它会被添加到列表中。在 OS X 10.6 上，这是通过 Grand Central Dispatch（中央调度）实现的，但核心功能是相同的。

该方法的文档具有某种误导性。它声称该方法将创建一个线程。事实上，在 OS X 上运行循环使用 `kqueue()` API 并调用此

> ¹GNUstep 可能使用 `poll()` 或 `select()`。

# 314 第 17 章：网络访问

方法向等待的列表添加另一个文件描述符。如果你对此通知有处理程序，你就可以读取新数据。

最后一个优势是，你不再需要考虑缓冲区。当你从 socket 读取数据时，通常需要分配一个缓冲区并将其指针传递给 `read()` 或 `recv()` 系统调用。对于文件描述符对象，你需要 `NSData` 实例。

如果你正在编写字符串列表，你可能希望为 `NSFileHandle` 添加一个分类，提供 `-writeUTF8String` 和 `-readUTF8String` 方法，或者你的协议使用的等效方法，允许直接获取和发送字符串。

## 连接服务器

```objectivec
NSInputStream *in;
NSOutputStream *out;
NSHost *host = [NSHost hostWithName:@"example.com"];
[NSStream getStreamsToHost:host port:80 inputStream:&in &out];
[in open];
```

来自：`nsstream.m`
Objective-C 提供了一系列类似于 Java 的类用于网络通信，以及底层的 UNIX 接口。遗憾的是，流版本并不特别好用。它们没有提供一种清晰的方式来添加压缩等过滤器，或在连接中间协商加密，而许多现代协议都是如此。

然而，最令人遗憾的局限性是，它们很难支持 SRV 记录。这些是发布服务到端口映射、以及主机名到 IP 地址映射的 DNS 记录。它们被用于 DNS-SD，但 IP 地址的短缺使得它们在公共网络的分级 DNS 中越来越常见。

如果你在 OS X 上使用 POSIX `getaddrinfo()` 函数查找服务器地址，你提供一个主机名和服务名。系统随后会将这些映射到任何支持协议的网络地址和端口号。

当你构造 `NSStream` 时，你必须以整数指定端口号。这意味着它对于任何使用 DNS SRV 记录的服务都会失败。然而，如果你使用 `getaddrinfo()` 然后将 socket 封装在 `NSFileHandle` 中，它可以正常工作。在 EtoileFoundation 中，我们为 `NSFileHandle` 提供了一个分类，允许你直接从主机名和协议名创建文件句柄，封装了此调用。

## 第 17 章：网络访问

```c
hints.ai_family = PF_UNSPEC;
hints.ai_socktype = SOCK_STREAM;
//请求一个流地址。
error = getaddrinfo(server, service, &hints, &res0);
if (error) { return nil; }
int s = -1;
```
