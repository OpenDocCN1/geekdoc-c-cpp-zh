
## 协议与委托 (Protocols and Delegation)

协议（Protocol）是类之间共享的方法列表。协议中列出的方法没有相应的实现；它们旨在由其他人（比如你！）来实现。协议提供了一种定义一组与特定名称相关联的方法的方法。这些方法通常会有文档说明，以便你了解如何执行它们，并在需要时，你可以在你自己的类定义中实现它们。

协议是一个方法列表，其中某些方法你可以可选地实现，另一些方法则是你必须实现的。如果你决定实现特定协议的所有要求方法，你就被允许遵循（conform）或采用（adopt）该协议。你被允许定义一个所有方法都是可选的协议，或者所有方法都是要求的协议。

定义协议非常简单：只需使用 `@protocol` 指令，后跟协议的名称（名称由你决定）。之后，你可以像在接口（interface）部分中那样声明方法。在 `@end` 指令之前，的所有方法声明将成为协议的一部分。

当你与 Foundation 框架工作时，你会发现定义了几个协议。其中一个声明了一个方法，如果你的类要支持通过 `copy`（或 `copyWithZone:`）方法进行对象拷贝，你就需要实现该方法。（“拷贝对象”章节详细介绍了对象拷贝的主题。）

以下是 `NSCopying` 协议在标准 Foundation 头文件 `NSObject.h` 中的定义方式：

```objc
@protocol NSCopy
- (id)copyWithZone:(NSZone);
@end
```

如果你在类中采用 `NSCopying` 协议，你必须实现一个名为 `copyWithZone:` 的方法。通过在 `@interface` 行的尖角括号 `<..>` 中列出协议名称，告诉编译器你正在采用该协议。协议名称位于类名及其父类之后，如下：

```objc
@interface AddressBook: NSObject <NSCopying>
```

这表示 `AddressBook` 是一个父类为 `NSObject` 的类，并声明它遵循 `NSCopying` 协议。系统已经知道为协议定义的方法（例如，它从头文件 `NSObject.h` 中已知），你不需要在接口部分声明这些方法。然而，你需要在实现部分（implementation section）中定义它们。

在这个示例中，编译器期望在 `AddressBook` 的实现部分看到 `copyWithZone:` 方法的定义。

如果你的类采用了多个协议，只需将它们列在尖括号内，并用逗号隔开：

```objc
@interface AddressBook: NSObject <NSCopying, NSCoding>
```

## 第11章 类别与协议

这告诉编译器 `AddressBook` 采用了 `NSCopying` 和 `NSCoding` 协议。同样，编译器期望在 `AddressBook` 的实现部分看到这些协议的所有要求方法都已实现。

如果你定义了自己的协议，你不需要自己实现它。但是，你是在提醒其他程序员，如果他们想采用该协议，他们就必须实现这些要求方法。这些方法可以从父类继承。因此，如果一个类遵循了 `NSCopying` 协议，它的子类也是如此（尽管并不意味着这些方法在子类中被正确实现）。

你可以使用协议来定义你希望其他继承你类的人的人实现的方法。也许你可以为你的 `GraphicObject` 类定义一个 `Drawing` 协议；在其中，你可以定义绘制、擦除和勾轮廓的方法：

```objc
@protocol Drawing
-(void)paint;
-(void)erase;
@optional
-(void)outline;
@end
```

作为 `GraphicObject` 类的创建者，你并不一定要实现这些绘制方法。然而，你希望指定某些继承 `GraphicObject` 类的子类需要实现的方法，以符合他们尝试创建的对象的绘制标准。

> `@optional` 指令的说明：列在该指令之后的任何方法都是可选的。也就是说，``Drawing` 协议的采用者不需要实现 `outline` 方法即可遵循该协议。（你随后可以使用协议内部的 `@required` 指令切换回列出要求方法。）

## 注意 (Note)

总之，这本意如此。编译器允许你说你遵循某个协议，并且仅在你没有实现这些方法时才发出警告。

如果你为 `GraphicObject` 创建一个名为 `Rectangle` 的子类，并宣布（即文档化）你的 `Rectangle` 遵循 `Drawing` 协议，该类的用户就知道他们可以向该类的实例发送 `paint`、`erase` 和（可能的）`outline` 消息。

注意，协议没有引用任何类；它是无质量的。任何类都可以遵循 `Drawing` 协议，而不只是 `GraphicObject` 的子类。

你可以通过 `conformsToProtocol` 方法来检查对象是否遵循某个协议。例如，如果你有一个名为 `currentObject` 的对象，并想查看它是否遵循 `Drawing` 协议以便为其发送绘制消息，你可以写：

```objc
id currentObject;
...
if ([currentObject conformsToProtocol:@protocol(Drawing)] YES)
{
  // 向 currentObject 发送 paint, erase 和/或 outline 消息
}
```

这里使用的特殊的 `@protocol` 指令接收协议名称并产生一个 `Protocol` 对象，这是 `conformsToProtocol` 方法期望的参数。要检查 `currentObject` 是否已经实现了可选的 `outline` 方法，你可以写：

```objc
if ([currentObject respondsToSelector:@selector(outline)] YES)
    [currentObject outline];
```

你可以在类型名后的尖角括号内包含协议名称，利用委托来检查变量的遵循情况，如下：

`<id <Drawing>`

这告诉编译器 `currentObject` 将引用遵循 `Drawing` 协议的对象。如果你赋值一个不符合要求的强引用对象，编译器将发出一个错误：

`error: 'Square' does not conform to protocol 'Drawing'`
`note: 'Square' must implement the following:`

（注：由于提供的 OCR 文本存在大量重复和乱码，此处已根据文档逻辑进行了清理，保留了核心技术说明。）
