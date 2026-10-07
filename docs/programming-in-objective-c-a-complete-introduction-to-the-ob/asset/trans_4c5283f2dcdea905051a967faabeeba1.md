

# 关于类的提问

在这个示例中，由变量 `action` 所指示的方法被发送到存储在 `graphicObject` 中的任何图形对象。推测该动作在程序执行期间可能会发生变化——也许基于用户的输入——尽管我们已经将动作显示为 `draw`。为了首先确保该对象能够响应该动作，你可能希望使用如下代码：

```objc
if ([graphicObject respondsToSelector:action] == YES)
    [graphicObject performSelector:action];
else
    //在此处处理错误
```

**注意**

`respondsToSelector:` 方法在 iOS 中广泛用于实现代理（delegation）概念。正如你将在第 10 章“变量和数据类型详解”中学到的，系统将让你选择，在你的类中实现一个或多个方法来处理某些事件（例如表格的行数）。为了让系统判断你是否实际上实现了某个特定方法，请使用 `respondsToSelector:` 来检查它是否可以将事件的处理委托给你的方法。如果你没有实现该方法，它将使用任何定义的默认行为来自行处理。

你也可以采用其他策略：你可以通过处理 `forwardInInvocation:` 方法将消息转发给另一个对象，但如何这样做超出了本文的范围。

程序 9.3 针对第 8 章“继承”中定义的 `Square` 和 `Rectangle` 类提问了一些问题。在查看实际输出之前，试着预测该程序的运行结果（不要偷看！）！

# 程序 9.3

```objc
#import "Square.h"

int main(int argc, char *argv[])
{
    NSAutleasePool *pool = [[NSAutleasePool alloc] init];

    Square *mySquare = [[Square alloc] init];

    // isMemberOf:

    if ([mySquare isKindOfClass:[[Square class]] == YES)
        NSLog("@mySquare is a member of Square class");

    if ([mySquare isKindOfClass:[[Rectangle class]] == YES)
        NSLog("@mySquare is a member of Rectangle class");

    if ([mySquare isKindOfClass:[[NSObject class]] == YES)
        NSLog("@mySquare is a member of NSObject class");

    // isKindOf:
    if ( [mySquare isKindOf:[Square class]] == YES )
     NSLog("@mySquare is a kind of Square");

    if ( [mySquare isKindOf:[Rectangle class]] == YES )
     NSLog("@mySquare is a kind of Rectangle");

    if ( [mySquare isKindOf:[NSObject class]] == YES )
     NSLog("@mySquare is a kind of NSObject");

    // respondsTo:
    if ( [mySquare respondsToSelector:@selector(set:)] == YES )
     NSLog("@mySquare responds to setTo:method");

    if ( [mySquare respondsToSelector:@selector(setWidth:andHeight)] == YES )
     NSLog("@mySquare responds to setWidth:andHeight:method");

    if ( [Square respondsToSelector:@selector(alloc)] == YES )
     NSLog("@Square class responds to alloc method");

    // instancesRespondTo:
    if ( [Rectangle instances respondsToSelector:@selector(set:)] == YES )
     NSLog("@Instances of Rectangle responds to setTo:method");

    if ( [Square instancesRespondToSelector:@selector(set:)] == YES )
     NSLog("@Instances of Square responds to setTo:method");
}
```

请确保使用 `Square`、`Rectangle` 和 `XYPoint` 类的实现文件构建此程序，这些类在第 8 章中都介绍过。

# 程序 9.3 输出

mySquare is a member of Square class
mySquare is a kind of Square
mySquare is a kind of Rectangle
mySquare is a kind of NSObject
mySquare responds to setTo: method
mySquare responds to setWidth:andHeight: method
Square class responds to alloc method
Instances of Square responds to setSide: method
Square is a subclass of a rectangle

程序 9.3 的输出应该是清晰的。记住，`isMemberOfClass:` 测试的是对类的直接成员身份，而 `isKind:` 检查的是继承体系中的成员身份。因此，`mySquare` 是 `Square` 类的成员——但它也是 `Square`、`Rectangle` 和 `NSObject` 的“一种”，因为它显然存在于这样的体系中；除非你定义了新的根对象，否则所有对象对 `NSObject` 类的 `isKindOf:` 测试都会返回 `YES`。

测试

```objc
if ( [ Square respondsToSelector:@selector(alloc)] == YES )
```

测试类 `Square` 是否响应类方法 `alloc`，它确实响应了——因为它继承自根对象 `NSObject`。请意识到你始终可以在消息表达式中直接使用类作为接收者，而不需要在之前的表达式中这样写（尽管你可能想这么做）：

- [Square class]

这是你唯一可以这样写的地方。在其他地方，你需要应用类方法来获取类对象。

# 使用 @try 进行异常处理

良好的实践要求你尝试预测程序中发生的问题。你可以通过测试可能导致程序异常终止的条件并处理这些情况来做到，例如通过记录日志消息并优雅地终止程序，或采取其他纠正措施。例如，你在本章的早期已经看到过如何测试对象是否响应特定的消息。在避免错误的情况下，在程序执行期间进行此项测试——可以让你避免向对象发送未识别的消息。当尝试发送此类未识别的消息时，你的程序将会。

# 第 9 章 多态、动态类型和动态绑定

# 使用 @try 进行异常处理 191

（注：文本中的 "191" 似乎是嵌入在 OCR 中的页码伪迹）

# 使用 @try 进行异常处理

（注：输入文本包含冗余章节和重叠标题。根据遵循所提供内容逻辑流的指令：）

（等等，查看提供的原始文本，它似乎是碎片化的并包含了不同页面的重复部分。我将根据提供的片段重建逻辑叙述。）

*实际上，我将按照要求提供清理后的文本流版本，合并去重和纠正后的片段。*

（此处省略了大量重复的 "de-duplicated" 字样，原文中存在严重的重复错误）

