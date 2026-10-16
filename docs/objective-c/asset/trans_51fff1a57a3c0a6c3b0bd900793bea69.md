

添加至队列后，操作会一直保留在该队列中，直到执行完毕或被取消。

## 操作队列参数的操纵

随着每个操作被添加到队列中，队列开始取出操作进行处理。NSOperationQueue 结合 GCD 会根据当前系统状态自动配置适当数量的线程来处理你的操作。如果你想手动配置它将使用的线程数量，可以使用属性 maxConcurrentOperationCount。设置此属性会限制队列使用的线程数。如果你将其配置为 1，则实际上是在创建一个串行队列。

NSOperationQueue 还有其他方法可以让你确定队列的状态。你可以通过调用方法 -operationCount 来了解有多少个操作在队列中等待执行。你也可以从该方法中访问操作本身。如果你想阻塞当前线程直到队列完成所有工作，可以使用方法 -waitUntilAllOperationsAreFinished。

## 使用其他类型的操作

除了可以继承 NSOperation 并创建自己的操作之外，Foundation 还为你提供了另外两种内置的 NSOperation 子类。NSInvocationOperation 用于创建在已有对象上调用给定方法的操作，以及 NSBlockOperation，它接受一个块，该块将在操作 main 方法的一部分中执行。

NSInvocationOperation 在你已有完成当前任务的代码，但该代码属于已有类时很方便。将该代码重构并放入 NSOperation 中可能不方便。NSInvocationOperation 允许你就地调用给定方法。例如，假设你在 NSImage 上有一个类别，可以为你执行模糊操作。你可以通过类似于 16.11 节清单的方式创建操作来模糊你的图像。

### Listing 16.11

### 使用 NSInvocationOperation

```
-(void)processDirectoryOfFiles:(NSString *)inDirectoryPath
{
    NSArray *filesInDirectory = [...]; // get listing of files.

    queue = [[NSOperationQueue alloc] init];

    for(NSString *imagePath in filesInDirectory)
    {
```
```
```objective-c
NSImage *image = [NSImage imageAtPath:...];
NSOperation *op = [[NSInvocationOperation alloc]
                   initWithTarget:image
                   selector:@selector(blur)
                   [object:nil];
[queue addOperation:op];
}
}
```
```

目的只是为了展示如何使用 `NSInvocationOperation`。

正如你所见，你可以创建 `NSInvocationOperation` 并使其在图像对象上调用 blur 并将其添加到操作队列，就像 `NSOperation` 子类一样。

`NSBlockOperation` 如果你想要执行的操作可以用代码块轻松表达，则很方便。16.12 节清单展示了使用 `NSBlockOperation` 的相同模糊操作。

### Listing 16.12

### 使用 NSBlockOperation

```
```objective-c
- (void)processDirectoryOfFiles:(NSString *)inDirectoryPath
{
    NSArray *filesInDirectory = [...]; // get listing of files.

    queue = [[NSOperationQueue alloc] init];

    for(NSString *imagePath in filesInDirectory)
    {
        NSOperation *op = [NSBlockOperation blockOperationWithBlock:^
        {
            NSImage *image = [NSImage imageAtPath:imagePath];
            [image blur];
        }];

        [queue addOperation:op];
    }
}
```
```

如果需要，你可以通过使用方法 -addExecutionBlock: 向单个 NSBlockOperation 添加多个执行块。操作将按顺序执行每个块，并且只有在所有块都已执行后才会被视为完成。

## CAUTION

某些以块作为参数的调用会自动在后台线程中执行该块。这并不总是记录在案。因此，你应始终假设你传递给未编写的 API 的任何块都将在另一个线程中执行，并且应考虑到线程安全编写。这包括小心不要在块之外修改你可能有权访问的对象。

## Summary

本章中我向你展示的所有线程工具在构建利用多处理器和多核机器的应用程序时为你提供了巨大的能力。正如常言道，能力越大责任越大，你在使用这些工具时必须确保适当设计你的应用程序。

在可能的情况下，如果你有选择，我鼓励你在代码中使用单线程设计，而不是引入线程。只有在对你的问题域绝对合适时才使用线程。

当你确实使用线程时，使用能够实现你的目标的最高抽象级别，并且始终确保使用适当的线程锁定和同步，以防止多个线程在内存中相互踩踏。本章为你提供了编写 Objective-C 高性能多线程应用程序所需的所有工具。

## Objective-C 设计模式

使用 Objective-C 和 Foundation 框架开发的乐趣之一在于其设计者在使用工程 API 和语言时完全拥抱了最现代的软件开发方法论。事实上，一些专家认为这些方法论甚至起源于 Objective-C。

在 Objective-C 和 Foundation 中得到充分体现的方法论之一是设计模式的概念。事实上，证据表明，我们今天在编程中使用的许多常见设计模式的首次实现实际上起源于 Objective-C 社区。它们可能不一定以现代名称命名，例如“责任链”、“观察者”等，但可以毫无疑问地看出，这些常见（今天）的设计模式的 Objective-C 版本在 Objective-C 语言中得到了充分体现。

在本章中，我向你展示如何在 Objective-C 中实现一些更常见的设计模式。Objective-C、Foundation 和 Cocoa 在其各自的 API 中大量使用设计模式；因此，你将在 Objective-C 中经常遇到设计模式。了解这些设计模式具体在 Objective-C 中的实现方式会很有用，因为在 Objective-C 这样的动态编译语言中的实现有时可能与在 C++ 或 Java 等更严格类型的语言中的实现略有不同。

## 识别解决方案中的模式

你是否注意到，随着时间的推移，相同类型的问题往往在不同项目中一次又一次地出现在你的应用程序开发中？你可能会忙于工作，发现自己面临一个编程情况，与你在别处刚刚处理过的场景非常相似，但又不完全相同。也许问题接近另一个问题，但又不够接近，无法完全重用你在上一个解决方案中使用的代码。设计模式是对特定编程问题的一种通用、可重用解决方案，可以在广泛不同的应用程序架构范围内重复使用和重新应用。通常，经验丰富的开发人员发现自己在不同应用程序的上下文中面临相同类型的一般问题。经常，这些一般问题的解决方案可以在这些不同上下文中应用，利用已存在知识和代码。通常，这并不是完全重用来自先前解决方案的代码的情况，而是使用你以前用来解决问题的相同思想。

作为设计模式的一个典型例子，想象一下你可能有两个对象，对象 Foo 和对象 Bar。Bar 希望在对象 Foo 内部发生特定事件时得到通知。你将如何处理这个问题？

你在这个情况下可能会做的是让 Foo 引用 Bar 对象，这样每当发生相关事件时，它就知道随后调用 Bar 上的方法来通知 Bar。这是一个非常常见的问题和非常常见的解决方案。这两者共同构成了一个设计模式。事实上，这个特定的设计模式被称为委托设计模式。Bar 成为对象 Foo 的委托。

通常，开发人员认识到使用特定设计模式是合适的，有两种不同的状态。第一种是在应用程序的设计阶段。研究设计模式是有用的，因为它使开发人员在讨论应用程序设计的抽象思想时能够拥有一种“通用语言”来讨论特定解决方案。换句话说，而不是费力描述给定解决方案的细节，开发人员可以简单地说：“在这里我们将使用委托来解决这个特定问题。” 另一位开发人员立即知道你在说什么，并且可能在没有任何额外信息的情况下实现解决方案。这使得设计模式成为专家开发人员工具箱中绝对至关重要的工具。

设计模式通常出现的第二个地方是开发人员忙于处理特定问题时。开发人员经常发现自己面临表面上需要复杂解决方案的复杂问题。

设计模式训练你的思维立即对任何手头的编程问题做出正确的解决方案。

由于这些原因，详细研究设计模式几乎总是你时间的良好利用。如果可能，你应该努力使用特定于你正在使用的语言的资源来研究设计模式。换句话说，在 Objective-C 和 Cocoa 中研究设计模式。然而，可能有更多资源可用于使用伪代码对设计模式进行通用研究，而不是特定于 Objective-C。不要让这阻止你。其中大部分资源在 Objective-C 中同样适用。

在接下来的几节中，我回顾了如何在 Objective-C 中具体实现几种特定的设计模式。此讨论并不是 Objective-C 中所有设计模式的全面列表，但应该足以让你入门并帮助你理解如何

## In This Chapter

- Understanding design pattern usage in Objective-C
- Learning how to make a singleton in Objective-C
- Delegating responsibility using delegates
- Observing changes using notifications

代码中重复使用该

