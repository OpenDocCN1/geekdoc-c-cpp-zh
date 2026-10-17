

**图 17.17** 添加到调试导航器中的内存视图

**图 17.18** 内存视图

**图 17.19** 内存视图控件

## 与控制台交互

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_264_0.png)

调试器控制台是你与调试器交互的命令行界面。无论你使用的是 GDB 还是 LLDB，你都能做的不仅仅是阅读应用程序输出的消息。这两个调试器都提供了命令行界面，功能与 Xcode 图形化呈现的功能相同。不过，通过控制台（图 17.20）向调试器快速输入几个命令有时会很有帮助，尤其是当你想要以文本形式输出结果的时候。

要向调试器控制台发出命令，你必须点击控制台窗口内部，将光标置于调试器提示符（`(gdb)` 或 `(lldb)`，取决于你所用的调试器）右侧。后面的示例将使用 GDB，因为 LLDB 仍处于“建设中”。

下面是一些有时用控制台处理反而更简单的常见任务。

> **注意：** 在撰写本文时，LLDB 尚不完整，某些在 GDB 中可用的命令在 LLDB 中不可用或尚不完整。

**图 17.20** 调试器控制台

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_265_0.png)

**图 17.21** TestApp 在调试器中暂停

### 打印对象和值

在控制台中有几种不同的方式可以打印对象和值。使用哪条命令取决于你想查看的信息类型。

#### 打印对象

“打印对象”（`po`）是 Cocoa 开发者最常用的调试器命令。该命令会要求 Objective-C 对象打印其常见的 `-description` 方法的返回结果。该方法继承自 NSObject，返回一个描述该对象的字符串。这个描述旨在用于调试。当应用程序在调试器中暂停时，当前堆栈中的所有符号对你都是可用的。这让你可以发出打印对象命令来检查对象（或这些对象所引用的其他对象）。

要打印一个对象，你需要在调试器中暂停应用程序。通常使用断点是最方便的。暂停后，找到一些有趣的东西来打印。图 17.21 显示 TestApp 再次在其 `-applicationDidFinishLaunching:` 方法中暂停。这一次，它暂停在创建 NSURL 对象并将其赋值给 `googleURL` 变量的那一行之下，这样你就有了一个方便打印的对象。要打印赋值给 `googleURL` 的对象，请在控制台中输入以下命令并按回车：

```
po googleURL
```

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_266_0.png)

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_266_1.png)

调试器会响应，记录 NSURL 对象被询问其 `-description` 时返回的字符串。**图 17.22** 显示了调试器控制台中的结果。你也可以在某个 Objective-C 类的实例方法中停止时打印 `self`。在当前示例的作用域中，`self` 指的是一个 `TestAppAppDelegate` 类的实例。**图 17.23** 显示了在该作用域中打印 `self` 的结果。在这种情况下，`TestAppAppDelegate` 类没有覆写 `-description`，因此显示的信息是继承自 NSObject 的默认描述格式。也就是说，显示的是所打印实例的类名和地址。

当然，你还可以通过其他对象的访问器来打印对象。例如，NSURL 有一个名为 `-scheme` 的字符串属性。要打印赋值给 `googleURL` 的 NSURL 实例的 scheme，你可以发出以下命令：

```
po [googleURL scheme]
```

调试器会调用 URL 对象的 `-scheme` 方法，然后调用返回对象的 `-description` 并打印：

```
http
```

你在示例中看到的信息并不是特别令人兴奋，但足以区分一个已打印的 NSArray 或 NSDictionary 对象中两个相似的对象。虽然 Cocoa API 中的许多对象带有比较有用的描述，但在开发者自己的对象中覆写 `-description` 并为自己的调试提供有意义的描述，这取决于开发者本身。

#### 打印值

`po` 命令只适用于对象。那么原始类型的值呢？如果你出于某种原因想知道 URL 对象的 scheme 所返回字符串的长度呢？你可能会认为下面的命令可行：

```
po [[googleURL scheme] length]
```

它不会起作用，因为 NSString 的 `-length` 方法返回的是 NSUInteger——一种原始类型，而不是对象。对于原始类型的值，你需要使用另一条打印命令。

```
p (NSUInteger)[[googleURL scheme] length]
```

调试器会回应：

```
$1 = 4
```

字符串 http 中当然有四个字符。让我们快速看一下这条命令的结构及其响应。

命令 `p`（print 的缩写）期望你给它的语句（`[[googleURL scheme] length]`）的结果被强制转换为预期的类型（`NSUInteger`），这样它就知道如何表示这个结果。这个类型应该是最终返回值的方法或函数（嵌套调用中最外层调用）的返回类型。就拿 NSString 的 `-length` 方法来说，返回值类型就是 NSUInteger。

这个响应实际上比看起来更有趣。调试器不仅打印结果，还贴心地将其赋值给一个局部变量，供你在以后的求值中使用。在这个示例中，数字 4（scheme 字符串的长度）被赋值给变量 `$1`。使用它很简单。假设你无法在脑中计算出将这个长度乘以二所需的数学运算。没问题！GDB 可以为你完成！

```
p (NSUInteger)($1 * 2)
```

GDB 会执行这个复杂的计算并回应：

```
$2 = 8
```

注意，连这次求值也被赋值给了新变量 `$2`。print 命令还有更多技巧，你可以在 http://xcodebook.com/printf 找到，但我们继续往下看。

#### 查看回溯

应用程序在当前（暂停）点的回溯信息与调试导航器中暂停线程下显示的信息相同，也就是堆栈。虽然 Xcode 的用户界面提供了格式良好的信息，可用于导航和控制调试会话，但例如在论坛或邮件列表中与他人分享信息时，它就不那么方便了。能够获得回溯的文本表示形式通常很有帮助。假设 TestApp 仍然暂停在与之前示例相同的位置，发出回溯命令（简称 `bt`）会产生以下输出：

```
#0  -[TestAppAppDelegate applicationDidFinishLaunching:]
    → (self=0x10015e520, _cmd=0x7fff84ad29c5, aNotification=
    → 0x114029af0) at /Users/jnozzi/Path/To/TestApp Suite/TestApp/
    → TestApp/TestAppAppDelegate.m:42

#1  0x00007fff83b568ea in _nsnote_callback ()

#2  0x00007fff835f1000 in __CFXNotificationPost ()

#3  0x00007fff835dd578 in _CFXNotificationPostNotification ()

#4  0x00007fff83b4d84e in -[NSNotificationCenter
→ postNotificationName:object:userInfo:] ()
#5  0x00007fff83e3e3d6 in -[NSApplication
→ _postDidFinishNotification] ()
#6  0x00007fff83e3e30b in -[NSApplication
→ _sendFinishLaunchingNotification] ()
#7  0x00007fff83f09305 in -[NSApplication(NSAppleEventHandling)
→ _handleAEOpen:] ()
#8  0x00007fff83f08f81 in -[NSApplication(NSAppleEventHandling)
→ _handleCoreEvent:withReplyEvent:] ()
#9  0x00007fff83b84e42 in -[NSAppleEventManager
→ dispatchRawAppleEvent:withRawReply:handlerRefCon:] ()
#10 0x00007fff83b84c72 in _NSAppleEventManagerGenericHandler ()
#11 0x00007fff88b50323 in aeDispatchAppleEvent ()
#12 0x00007fff88b5021c in dispatchEventAndSendReply ()
#13 0x00007fff88b50123 in aeProcessAppleEvent ()
#14 0x00007fff84e2c619 in AEProcessAppleEvent ()
#15 0x00007fff83e0e04b in _DPSNextEvent ()
#16 0x00007fff83e0d7a9 in -[NSApplication nextEventMatchingMask:
→ untilDate:inMode:dequeue:] ()
#17 0x00007fff83dd348b in -[NSApplication run] ()
#18 0x00007fff83dcc1a8 in NSApplicationMain ()
#19 0x00000001000010c2 in main (argc=1, argv=0x7fff5fbbf670) at
→ /Users/jnozzi/Path/To/TestApp Suite/TestApp/TestApp/main.m:12
```

如果你展开调试导航器中线程 1 下的栈帧，然后将细节滑块一直拖到最右边（以显示所有堆栈帧），你会发现信息确实是相同的。它远不如你在 Xcode 用户界面中看到的那么美观，但在你向其他开发者倾诉烦恼、希望他们能帮助你时，它还是很有用的。

