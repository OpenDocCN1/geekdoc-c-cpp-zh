

## 第 17 章：网络访问

NSURLDownload 封装了从远程 URL 的下载操作。更复杂的是 NSURLConnection，它提供了一种更底层的方法来处理请求和响应。

URL 加载系统与协议无关，但它期望一种请求-响应格式。请求被封装在 `NSURLRequest` 中，然后你将其传递给这两个类之一。它会建立连接并发送请求，然后为你提供一个或多个 `NSURLResponse` 对象作为响应。

默认情况下，Foundation 框架可以从 `file://`、`http://`、`https://` 和 `ftp://` URL 加载数据。你可以通过实现 `NSURLProtocol` 子类来添加对其他协议的支持。这种需求并不常见，但例如，你可能想在该类中实现对 SFTP 或类似协议的支持。然后你可以重用那些将文件访问委托给 URL 加载系统的现有代码。

本节开头的示例展示了如何从用户指定的远程 URL 获取文件。这使用了一个代理类来向用户报告进度，尽管这不是强制要求的。

代理类存储了响应的大小，以便提供进度报告。如果传输失败，它将报告一个本地化的错误消息。如果运行成功，每下载 1%，它就会在终端打印一个点。

URL 加载系统非常强大，但大多数情况下，你只需要限制在示例所示的子集中。这让你用极少的代码就能与简单的网络服务集成。

## 调试 Objective-C

程序员分为两种：一种是第一次就能写出完美代码的人，另一种是确实存在的人。如果你属于第一类，可以跳过本章。如果你属于第二类，那么总会有尝试运行代码并发现它运行得并不符合预期的时候。

这是一个令人恼的体验，但如果你能快速修复问题，痛苦就会少很多。在本章中，我们将查看一些定位 Objective-C 程序错误原因的技术。

## 第 18 章：调试 Objective-C

### 检查对象

```objc
@interface DebugObject : NSObject @end
@implementation DebugObject
-(NSString*)description {
  return @"Not a very helpful message";
}
@end
void debug(id any) {}
```

来自：description.m

在大多数情况下，当你调试 Objective-C 程序时，你会使用 GNU 调试器 (GDB)，它对 Objective-C 有一些内置支持。如果你正在使用 Xcode，那么你实际上是通过图形化界面在使用 GDB。你可以从“运行（Run）”菜单访问命令行界面。这通常非常有用，因为 Xcode 只为调试器最常用的功能提供了 GUI，而不是涵盖所有功能。

注意：较新版本的 Xcode 使用 LLVM 调试器 (LLDB) 代替 GDB。图形界面是相同的，且 LLDB 支持的功能与 GDB 大体相同。

GDB 有两个特性使其非常适合 Objective-C。第一个是它附带了简单的 Objective-C 解析器和解释器，因此你可以在调试器中编写 Objective-C 表达式并以这种方式检查变量。第二个是 `print-object` 命令。

```bash
$ gdb ./a.out debug
(gdb) break debug
Breakpoint 1 at 0x100000e4d: file description.m,
  line 10.
(gdb) r
Starting program: a.out
Breakpoint 1, debug (anObject=0x100111bc0) at
  description.m:10
void anObject(id anObject) {
(gdb) print anObject
$1 = (id) 0x100111bc0
(gdb) print-object anObject
Not a very helpful message
(gdb) print-object [NSObject new]
<NSObject: 0x100111c30>
(gdb) print-object [anObject class]
DebugObject
(gdb) print-object [anObject className]
DebugObject
(gdb) print-object anObject->isa
DebugObject
```

输出来自：description

这会打印一个对象。它是通过向对象发送 `-description` 消息来实现的，该消息返回一个描述对象的 `NSString`。这意味着它只对有效对象有效。如果你尝试对过早释放或内存损坏的对象使用此命令，调试器将崩溃，或者捕获到段错误信号。

该方法在 `NSObject` 中的默认实现只是打印类名和地址。其他各种标准对象以不同的方式实现了它。例如，集合类（Collection classes）以属性列表（property list）格式打印其内容。这个示例返回了一个毫无用的消息，但在你的代码中，你应该尝试提供一些更有帮助的内容。

### 识别内存问题

```objc
id pool = [AutoreleasePool new];
MutableString *str = [MutableString stringWith:@
```

来自：prematureDealloc.m

Objective-C 中常见的问题之一是过早释放。如果你在某处漏掉了 `-retain`，那么你就持有一个指针而没有增加它的引用计数。如果其他东西持有它的引用，或者它是自动释放的（autoreleased），那么该指针就会失效。如果你在环境中设置了 `NSZombieEnabled=YES`，你就能捕获到。当指针失效时，你将得到崩溃。

如果你使用 ARC，将不安全指针转换为弱引用（weak）可以确保它们在指针释放时置零，并帮助你安全地检查指针是否有效。通常，你只需要通过查看源文件就能找到被释放的对象。

```bash
$ gcc -g prematureDealloc.ma.out
$ gdb ./a.out
(gdb) r
Starting program: a.out
Program received signal SIGSEGV, Segmentation fault.
Reason: KERN_BAD_ACCESS at address: 0x0000000000007a00
```

输出：prematureDealloc.m


