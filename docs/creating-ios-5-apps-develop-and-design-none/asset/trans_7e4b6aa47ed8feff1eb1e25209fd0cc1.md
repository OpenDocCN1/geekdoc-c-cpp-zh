

## 方法

剥离所有花哨的功能后，Objective-C 方法本质上就是一个 C 函数。因此，我们学到的关于函数的一切都同样适用于方法。然而，有一个重要的区别。当我们调用 C 函数时，函数及其参数在编译时（静态绑定）连接在一起。相比之下，在 Objective-C 中，我们实际上并不是在调用方法；而是在向对象发送消息，请求它调用该方法。对象随后使用方法名来选择实际函数。这种选择器、函数和参数的连接是在运行时（动态绑定）完成的。

这有许多实际意义。首先也是最重要的，你可以向任何对象发送任何方法。毕竟，我们可以在运行时动态添加方法的实现，也可以将方法完全转发给另一个对象。

更常见的是，我们将此功能与对象标识符类型 `id` 结合使用，`id` 可以引用任何对象（包括类对象）。注意，声明 `id` 变量时我们不需要使用星号。`id` 类型已经被定义为指向对象的指针。

```
id myString = @"This is a string";      // This is an NSString.
id myStringClass = [myString class];    // This is a class object.
```

`id` 类型和动态绑定的组合拳让我们避免了静态绑定语言通常需要的许多复杂、冗长的构造，但这不仅仅是无拘无束地自由运行；作为开发者，我们通常比编译器更了解我们的应用。

例如，如果我们只将 NSString 对象放入数组，我们就知道该数组中的所有对象都会响应 `length` 消息。在 C++ 或 Java 中，我们需要说服编译器允许我们进行该调用（通常是通过强制转换对象）。Objective-C（在很大程度上）相信我们知道自己在做什么。

不过，这也不是完全随心所欲的“西部荒野”式编程。Xcode 的编译器和静态分析器在分析我们的代码和发现常见错误（比如拼错的方法名）方面做得非常出色，即使在编写高度动态的代码时也是如此。

## 向 nil 发送消息

在 Objective-C 中，向 `nil` 发送消息是完全合法的。这常常让有 Java 背景的人感到震惊。在 Java 中，如果你对 `null` 调用方法（`null` 和 `nil` 是相同的，都是值为 0 的指针——基本上是指向“无”的指针），你的应用会崩溃。而在 Objective-C 中，该方法只是返回 0 或 `nil`（取决于返回类型）。

Objective-C 新手经常争辩说这掩盖了错误。通过立即崩溃，Java 可以防止程序在错误状态下继续运行，从而避免可能产生错误输出或稍后在应用中的某个时刻莫名其妙地崩溃。这有一定道理。然而，一旦你接受了可以向 `nil` 发送消息这一事实，你就能利用它编写出简单、优雅的算法。

让我们看一个比较常见的设计模式。想象一个 RSS 阅读器必须下载一百个不同的订阅源。首先你调用一个方法来下载 XML 文件，然后解析 XML。由于可能存在网络问题，第一个方法很可能非常不可靠。在 Java 中，我们需要检查并确保收到了有效结果。

```
XML xml = RSS.getXMLforURL(myURL);
// Make sure we have a valid xml object.
if (xml != null) {
    xml.parse();
    ...
}
```

在 Objective-C 中，这些检查是不必要的。如果 XML 是 `nil`，方法调用就什么也不做。

```objectivec
XML* xml = [RSS getXMLforURL:myURL];
[xml parse];
...
```

另外，让我们面对现实：空指针在 Java 应用程序中是常见的 bug 来源。Java 的空指针违反了该语言原本严格的静态类型。既然可以将它赋给对象变量，就应该能够像对待任何其他对象一样对待它。这包括调用实例方法和获得合理的结果。

## 调用方法

Objective-C 方法使用方括号调用。在括号内，我们有接收者和消息。接收者可以是任何计算结果为对象的变量（包括 `self`）、`super` 关键字或类名（对于类方法）。消息是方法的名称以及任何参数。

```
[receiver message]
```

在 C 中，方法的参数都集中在函数名后面的括号内。Objective-C 的处理方式略有不同。如果方法不带任何参数，方法名就是简单的单个词（通常是首字母小写的驼峰词）。

```
[myObject myFunctionWithNoArguments];
```

如果方法带一个参数，名称以冒号（:）结尾，参数紧随其后。

```
[myObject myFunctionWithOneArgument:myArgument];
```

多个参数分布在方法名中。通常，方法名会提示每个位置期望的参数类型。

```
[myObject myFunctionWithFirstArgument:first
                secondArgument:second
                thirdArgument:third];
```

在引用该方法时，我们通常将名称的所有部分连接起来，不带空格或参数。例如，上述方法名为 `myFunctionWithFirstArgument:secondArgument:thirdArgument:`。

虽然这种风格起初可能看起来别扭，但在编码时却大有帮助。几乎不可能意外地将参数放错顺序（这是我在类似 C 的语言中经常犯的错误）。将方法名和参数交错排列也鼓励使用更长、更具表现力的方法名，而且——依我看来——这总是一件好事。

方法通常在类的 `@interface` 块中声明，并在 `@implementation` 块中定义。与 C 函数一样，声明就是方法签名后跟一个分号。定义是方法签名后跟花括号内的代码块。

## 类方法

类方法在类上调用（使用类名），而不是在单个对象上调用。我们已经见识过类方法的实际应用；`alloc` 就是类方法的一个例子——我们调用 `[NSString alloc]`，而不是 `[myStringObject alloc]`。

大多数类方法是为简化新对象创建而设计的便捷方法。另一些则封装了与该类相关的实用工具函数。例如，NSString 定义了一个名为 `availableStringEncodings` 的类方法。你可以调用此方法，获得一个以 `nil` 结尾的列表，其中包含 NSString 类支持的所有字符串编码。

方法签名以 `+` 或 `-` 字符开头。`-` 用于实例方法，而 `+` 用于类方法。接下来是括号中的返回类型，然后是方法名。参数在名称中定义。只需在冒号后面跟上括号中的参数类型和参数名。

    - (void)simple;                       // No arguments, no return
                                         // value.
    - (int)count;                        // No arguments, returns an
                                         // integer.
    - (NSString*) nameForID:(int)id;     // Takes an integer argument.
                                         // Returns a string object.
                                         // Class method with multiple
                                         // arguments.
    + (NSString*) fullNameGivenFirstName:(NSString*)first
                                  middleName:(NSString*)middle
                                     lastName:(NSString*)last;

Objective-C 方法总是有两个隐藏参数：`self` 和 `_cmd`。`_cmd` 参数是方法的选择器。选择器是类型为 `SEL` 的唯一标识符，用于在运行时查找方法。你可以使用 `@selector()` 从方法名创建 `SEL`。也可以使用 `NSStringFromSelector()` 获取 `SEL` 的字符串表示。

C 函数和 Objective-C 方法之间的联系在你开始动态地向对象添加方法时变得清晰起来，如下所示：

```objc
// Defined before the @implementation block.
void myFunction(id self, SEL _cmd) {
    NSLog(@"Executing my method %@ on %@",
          NSStringFromSelector(_cmd),
          self);
}
// Defined inside the @implementation block.
+ (void)addMethod {
    SEL selector = @selector(myMethod);
    class_addMethod(self, selector, (IMP)myFunction, "v@:");
}
```

运行类方法 `addMethod` 将在运行时把 `myMethod` 添加到当前类。然后你可以调用 `[myObject myMethod]`，它将调用函数 `myFunction(myObject, @selector(myMethod))`。

## 初始化方法

我们已经讨论过对象的两步实例化。现在让我们看看初始化方法本身。这些只是和我们可能编写的任何其他方法一样的方法；然而，要让一切正确，我们需要遵循一些约定。

首先是名称。所有初始化方法传统上以 `init` 开头。帮自己（以及将来可能维护你代码的任何人）一个大忙，始终遵循这个命名约定。

接下来，有两个方法需要特别注意：类的指定初始化方法和父类的指定初始化方法。

