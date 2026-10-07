

# <Foundation/Foundation.h>

```
1 #import <Foundation/Foundation.h>
2 @interface HelloWorld : NSObject
3 {
4 }
5 
6 - (void)printGreeting;
7 
8 @end
```

这是实现部分（HelloWorld.m）：

```
10 #import "HelloWorld.h"
11 @implementation HelloWorld
12 
13 - (void)printGreeting
14 {
15 NSLog("Hello World!");
16 }
17 
18 @end
```

在前面的示例中，定义了一个名为 HelloWorld 的对象。这个对象只定义了一个消息——printGreeting。这些奇怪的符号是什么意思？以行号为参考，我们可以逐行审查这段代码。

第 1 行包含一个编译器指令 `#import <Foundation/Foundation.h>`。为了让这个小程序知道其他对象（例如第 3 行的 `NSObject`），我们需要编译器读取其他接口文件。在这种情况下，`Foundation.h` 文件定义了 Foundation 框架的对象和接口。该框架包含了 iOS 和 Mac OS 系统中非用户界面基类的定义。这里重要的是，我们得到了一个 `NSObject` 对象的定义。我们对象的实际开始于第 3 行，如下：

@interface HelloWorld : NSObject

HelloWorld 是对象，但 `: NSObject` 是什么意思？嗯，对象名称后面的冒号（`:`）表示我们计划从另一个类派生额外的功能。在这种情况下，HelloWorld 现在是 `NSObject` 的子类。

> 注意：为什么名字是 NSObject 而不是直接 Object？嗯，你还记得 Mac OS X 实际上是从 NeXTSTEP 移植而来的吗？“NS” 是 NeXTSTEP 的缩写，用于 Mac OS X 和 iOS 的许多基对象中——`NSObject`、`NSString`、`NSDictionary` 等。

第 4 行和第 5 行仅包含 `{ }` 字符。这个块用于由对象定义实例变量，但 `HelloWorld` 类足够简单，不需要实例变量。在稍后的第 9 章中，会有定义和使用实例变量的示例。

第 7 行包含了该对象的消息定义，如下：

+   - (void)printGreeting;

当你定义一个消息时，行必须以 `+` 或 `-` 字符开头。在 `HelloWorld` 对象的情况下，我们使用 `-` 表示此消息可以在对象创建后调用。`+` 字符用于可以在对象创建之前调用的消息。消息的剩余部分 `(void) printGreeting` 代表消息的返回值。在这种情况下，值 `(void)` 后面紧跟着实际的消息名 `printGreeting`。

第 9 行，`@` 表示 `HelloWorld` 接口定义完成。

这是对 `HelloWorld` 对象接口的完整描述；这里内容不多。更复杂的对象只会有更多的消息和实例变量。

第 12 行是对象实现的开始，如下：

```
@implementation HelloWorld
```

第 14 行是对象消息 `printGreeting` 的定义。它看起来与接口文件中的消息定义完全相同。这里的唯一区别是正在定义实现 `printGreeting` 消息的代码。

第 15-17 行形成了实现 `printGreeting` 消息的代码。对于这个简单的消息，调用了 `NSLog` 函数。这个底层函数接收一个格式化的 `NSString` 对象并将结果输出到控制台。`NSString` 类是一个 Objective-C 类，实现了字符字符串的行为。为什么要这个类呢？其一，它为框架提供了一个表示字符串的统一对象。此外，`NSString` 中有很多功能可以用于操纵、比较和转换实际数据。

这里使用简写方法指定了 `NSString` 对象。`@"Hello World!"` 是声明 `NSString` 对象的一种方法。符号 `@` 是用于指示所指定的字符串是一个 `NSString` 对象的符号。

第 19 行指示编译器实现部分的定义结束。

但等一下，还有更多。现在我们定义了一个新的 Objective-C 类，它是如何使用的呢？下面是另一段使用新创建的类的代码，主程序（myprogram.m）。

```
#import "HelloWorld.h"
int main(void)
{
    HelloWorld* myObject = [[HelloWorld alloc] init];
    [myObject printGreeting];

    [myObject release];
    return 0;
}
```

在新文件中，程序通过包含 `HelloWorld.h` 文件开始，这允许应用程序的这部分访问 `HelloWorld` 对象。

第 22 行，我们有主函数。记住，每个 Objective-C 程序都必须有一个 `main` 函数。

第 24 行比较复杂。它定义并实例化了 `HelloWorld` 类。你首先看到文本 `HelloWorld* myObject`。这定义了一个类型为 `HelloWorld` 的名为 `myObject` 的变量，这是我们的新类。星号 (`*`) 用于表示对象的指针。这种表示基本上意味着我们不需要对象本身；我们只需要获取它或指向它所在位置的指针。把它想象成一个给你名片的人。你有卡片，而不是本人。但名片是与某人联系的方式。

> 注意：实例化（Instantiation）创建一个真实的对象。分配（Allocation）意味着我们使用计算机内存的一部分来存储东西。在出现实例之前，类本身并不是 true可用。

行的下一部分是 `[[HelloWorld alloc] init]`。这是一个嵌套调用。`init` 消息被发送到由 `[HelloWorld alloc]` 创建的新对象。`init` 仅仅对对象进行基础初始化。这一切的最终返回是一个指向新对象的指针。

> 注意：在 Objective-C 中，每当向对象发送消息时，代码必须位于方括号 `[ ]` 内。

现在我们创建了一个新对象，就可以使用了。第 25 行 `[myObject printGreeting]` 将我们的对象投入使用。在这段代码中，我们通过发送消息 `printGreeting` 来使用我们新实例化的对象。程序将输出文本 `HelloWorld!`。

第 27 行向我们的对象发送另一个消息，`release` 消息。此消息告诉系统已完成对对象的使用，并释放与其相关的任何资源。

第 28 行向 `main` 函数的调用者返回值 0。这表示执行成功。

第 29 行结束代码块和程序。

> 注意：消息也可以接受多个参数。例如考虑 `[myCarObject switchRadioBandTo:FMAndTuneTo:104.7]`。这里的消息将是 `switchRadioBandTo:TuneTo:`。在每个冒号之后，实际发送消息时会放置参数值。你可能还会注意到这些消息的命名便于理解它们实际的作用。在开发类时，使用有帮助的消息名称是一个遵循的理想约定，因为它使得类类变得更加直观。保持消息命名的一致性也至关重要。

