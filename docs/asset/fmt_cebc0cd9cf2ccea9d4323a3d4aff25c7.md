
`-(void)writeDescription:(NSString*)partialDescription {`

```
    [target writeObject:partialDescription];
}
```

`-(void)writeObject:(NSObject*)anObject {`

```
    [self writeDescription:[anObject description]];
}
```

`-(void)writeArray:(NSArray*)array {`

```
    [self writeDescription:@"("];
    BOOL first=YES;
    for (id obj in array) {
        if (first) {
            first=NO;
        } else {
            [self writeObject:@", "];
        }
        @autoreleasepool {
            [self writeObject:obj];
        }
    }
    [self writeDescription:@""]];
}
```

`@end`

`@implementation NSArray (StreamWriting)`

`-(void)writeOnStream:(MPWFilterStream*)aStream {`

```
    [aStream writeArray:self];
}
```

`@end`

`@implementation NSObject (StreamWriting)`

`-(void)writeOnStream:(MPWFilterStream*)aStream {`

```
    [aStream writeObject:self];
}
```

`@end`

每个对象都通过表示流接口的`writeObject:`消息写入流。然后流使用`writeOnStream:`消息请求对象写入自身，对象则通过发送一个编码其类别的消息给流来响应（见图 8.3）。虽然这看起来有很多消息，记住，与分配临时内存和解包/打包中间结果相比，消息是廉价的。

`NSMutableString`现在隐藏在`DescriptionStream`的目标之后，我们实际上可以将其替换为直接输出到`stdout`、`stderr`的对象，而不是在输出之前在内存中累积整个描述。这使得描述的内存消耗实际上变成了常数，即`O(1)`，而原始`description`方法为`O(n²)`，索引`describeOn:`为`O(n)`。

## 消除 description 中的无限递归

通过与对象图交互以产生描述的流，我们现在有一个地方可以保留足够的状态来捕获数据结构中的无限递归——例如示例 7.4 中相互递归的`JSONArray`对象。

当我们遇到一个正在描述过程中的对象时，我们不想再次描述它。为了实现这一点，我们需要跟踪`describeStream`正在描述的对象，并在遇到它们时跳出。

示例 8.7 中的`MPWDescriptionStream`拥有一个`NSMapTable`来跟踪正在被描述的对象，同时也接管了之前作为`describeOn:`直接参数的`NSMutableString`。示例 8.8 中的`writeObject`方法实现了上述描述的策略：首先将对象放入表中，如果它不在于表中，则对其进行描述，最后将其移除。如果对象在步骤 2 中已经于表中，我们只写入一个伪描述。

### 示例 8.7 Description Stream 定义

```
#import "MPWFilterStream.h"

@interface MPWDescriptionStream : MPWFilterStream
    NSMapTable *alreadySeen;
@property (atomic,retain) NSMapTable *alreadySeen;
-(void)writeObject:(id)anObject;
-(void)writeArray:(NSArray *)anArray;
-(void)describeObject:(id)anObject;
@end
```

### 示例 8.8 Description Stream 实现

```
@implementation MPWDescriptionStream
#define OPAQUEQPTR NSPointerFunctionsOpaquePersonality
```

# DescriptionStream 169

```
- (instancype) init
{
  id table=[NSMapTable mapTableWithKeyOptions:OPAQUEPTR
valueOptions:OPAQUEPTR];
  self[setAlreadySeen:table];
  return self;
}
```

```
- (void) writeObject:anObject
{
  if ([alreadySeen objectForKey:anObject] ) {
    [self appendDescriptionFormat:@
```

该过程确保了被描述的对象不再发生无限递归。通常情况下，如果你不想在输出中重复对象，只需将对象留在表中即可。到那个时候，你实际上构建了一个对象图序列化器，以及一个潜在循环引的检测器！

添加示例 8.9 的胶水代码，运行上一章的示例 7.4 不再会崩溃，而是输出类似的内容：( `<already seen: 0x7a0fb40a880>` )。该示例显然是不完整的；例如，它至少需要一个`writeDictionary`方法，而且如果所有对象使用`describeOn:`而不是`description`，也能获得这种保护。

### 示例 8.9 Description Stream 胶水代码

```
@implementation NSObject (describeOn)
-(void)describeOn:(MPWDescriptionStream *)aStream
{
  [aStream describeObject:self];
}
-(NSString*)fastDescription
{
  MPWDescriptionStream s=[MPWDescriptionStream stream];
  [s writeObject:self];
```

```
return [s target];
}
@end

@implementation NSArray (describeOn)
-(void)describeOn:(MPWDescriptionStream *)aStream
{
  [aStream describeArray:self];
}
@end
```

## 流的层次结构

这些转换的总和为我们提供了多态、可子类化且可组合的流，它们可以增量地处理数据。我们不再像上一章为了解决描述问题而直接写入`NSMutableString`，而是现在写入流中。

`MPWDescriptionStream`的子类可以轻松重写`writeArray`以输出 JSON 格式的字符串，而不是`description`创建的 NeXT 风格属性列表格式。

自从 1998 年开始使用`FilterStreams`以来，我在`MPWFramework`中实现了二十多种类型的`FilterStream`，图 8.4 显示了其中一小部分。它们非常有帮助，特别是字节编码或转换规则（如压缩和编码）方面，编码之间的共同点被捕获，输出可以轻松重定向到缓冲区、网络或文件。

`Byte`子类泛化了你可以对 Unix 过滤器所的操作，实际上还包含一个调用 Unix 过滤器的类。数据流范式意味着`URL Fetch`可以轻松处理网络操作固有的异步性，而无需回调；我们在 Wunderlist 中对此发挥了极佳的作用。原因是“调用并返回”（call-and-return）需要立即返回结果，而数据流只需要将结果传递给下一个过滤器，而不必太具体关心何时发生。事实上，它不仅关心结果的时机，还关心数量。例如，过滤器可以向其目标写入多个结果或零个结果（例如发生错误时），这使得将错误处理排除在“快乐路径”之外并进行集中处理成为可能。

实际实现比这里显示的多一点。例如，`writeObject`发送的初始消息不是固定的，而是通过指定的

> 2. http://github.com/mpw/MPWFoundation

![](img/29111a88ed1326b01d04057a653fdbec_190_0.png)

图 8.4 FilterStream 层次结构

作为相关`FilterStream`的参数指定的，以便对象能够响应特定类型的流，但留了一个钩子以便通用行为可以被共享。

便利方法将流式架构风格适配到“调用并返回”。例如，定义在`rootFilterStream`类上的`+process:`消息初始化流，将对象写入流中并返回结果。

## 总结

在本章中，我们查看了将上一章使用流式方法的想法扩展为整个实现“管道与过滤器”（Pipes and Filters）架构风格的组件库。有了这个库，流处理被植入到底层，使得实现计算变得非常简单，这种方式不仅内存高效，而且易于异步化。

此页故意留空

# 9

# Swift

Swift 在 WWDC 2014 上备受欢烈地推出，是 Apple 的新编程语言，被誉为“去掉了 C 的 Objective-C”。这是一个有趣的营销口号，考虑到我们知道 Objective-C 是在 C 中添加 Smalltalk 创建的（公式 9.1）。

> Objective-C = C + Smalltalk (9.1)

根据我在高中学的一级代数规则，从等式的两边减去 C（公式 9.2）并不会产生 Swift，事实上 Swift 看起来与 C# 或 C++ 的关系比与 Smalltalk 或 Objective-C 的关系密切得多。

> Objective-C – C = Smalltalk (9.2)

撇细小的营销问题不谈，Swift 取得了巨大的成功，许多文章、书籍和会议都致力于这个主题。

## Swift 性能：主张

从一开始，Apple 就在大力推广 Swift 的性能，甚至体现在名字上：Swift。在平台大会上，新语言的性能是一个核心焦点，例如图 9.1 所示的性能对比。

这是一个令人印象深刻的展示，Swift 快了 3.9 倍……什么？Python。你可能会疑惑 Python 为什么出现在对比中，考虑到它是一种解释型脚本语言，并非为性能密集型工作设计。

事实证明当你比较 Objective-C 和 Swift 列时，2.6 与 3.9 之间只有 1.4 倍的差异，而当你将其绘图并将颜色与另一种相同时（如图 9.2 所示），那并不是一个特别令人惊讶的幻灯片。

# 第 9 章

![](img/29111a88ed1326b01d04057a653fdbec_193_0.png)

图 9.1 WWDC 2014 状态报告幻灯片，对比 Swift 与 Python

# 更好的性能意味着更好的应用。

Swift 程序的表现完全名不虚传。例如，一种常见的搜索算法使用 Swift 时完成速度要快得多。

![](img/29111a88ed1326b01d04057a653fdbec_194_0.png)

图 9.3 http://apple.com/swift 上的性能声明

一种编译语言如果是这种性能将令人失望的，而只比 Python 代码快约 2.5 倍的 Objective-C 代码简直令人不安。尽管在仔细观察后，这种说法并没有完全说服力，但 Apple 对 Swift 性能的营销非常有效。Swift 非常快，确实非常快，这一观点现在已经是 Apple 开发者社区的公认事实。

## 语言特性

尽管 Apple 没有提供关于 Swift 性能的任何坚实证据，但它给出了 Swift 惊人性能的原因。

- Swift 的设计比 Objective-C 具有更得多的静态性（请参见第 5 章的“栈分配”部分），这意味着在编译时有更多信息可供编译器用于优化。
- 特而言，动态分发被大幅减少，大多数“原生”Swift 方法都是进行静态分发的。

Objective-C 的动态分发是编译器感知的绝对障碍，这一直是编译器和运行时团队心头之刺。即时编译（JIT）编译器可以在运行时解决这个问题，但有很多理由不应该依赖 JIT 技术来获取性能。

> 1. 参见 Jitterdammerung (http://blog.metaobject.com/2015/10/jitterdammerung.html)。

# 第 9 章 Swift

- 更多地使用结构体进行值语义（请参见第 5 章的“栈分配”部分），被认为让我们摆脱堆分配和引用计数的代价，特别是 ARC（请参见第 7 章的“引用计数”部分），而且在 Swift 中处理引用确实特别昂贵，比 Objective-C 昂贵得多。
- 原始类型和对象之间的联系更加紧密，因此，Foundation `NSArray`只能包含对象引用，而 Swift `Array`可以包含原始类型、结构体或对象引用。当原始类型在对象上下文中使用时，可以很容易进行装箱和拆箱（通常是自动的）。
- 泛型允许应用特化，例如，数组的泛型`sort`方法可以通过整数比较函数进行特化，从而产生一个优化的整数排序函数，而无需通过指针间接访问或消息发送来操作。

这些都是很好的特性，无疑为编译器优化提供了机会。拥有一个更统一的语法，而不是两个拼凑在一起并用胶带粘在一起的系统，无疑是受欢迎的。

然而，所有这些机制仅仅导致了更好的性能；并没有保证它们真的能这样做，而且对于 Objective-C 程序员来说，像这样的原始类型是不可用的。Objective-C 对整数、浮点数等原始类型，以及`NSPoint`、`CGPoint`、`NSRect`、`NSRange`等结构体大量使用了值语义。

让这些类型变得稍微方便一点点，这本身并不是什么难事，但它实际上对性能并没有实际帮助，特别是因为 Apple 建议并期望大多数情况下使用类进行建模：

> “在所有其他情况下，定义一个类，并创建该类的实例进行管理和通过引用传递。在实践中，这意味着大多数数据构造都是类或结构体。”

Apple Inc., 2014. 《Swift 编程语言 (Swift 3)》。电子书。

我们知道，使用类的建议被采纳，因为对于 97% 或更多的代码来说，这种微型优化是不值得的。然而，这与 Apple 对 Swift 的建议相冲突，除非有充分理由不这样做，否则它强烈倾向于使用结构体。

问题在于，这两项建议都是正确的，这种内在的冲突与过去 40 年左右收集的关于性能集体智慧背道而驰：首先进行适当的建模；之后再进行针对优化。在 Swift 中，你应该在应用程序的建模阶段做出这种性能选择。

Objective-C 也有且仍然存在这个问题，正如前面的章节所示，它某些机制允许开发者应用针对性的优化以获得更好的性能，例如`IMP`缓存、对象缓存，或使用`char*`等基础 C 数据类型代替`String`。这些机制经常允许让你在保留“建模蛋糕”的同时，享用一些美味的“性能大餐”，但这些机制在 Swift 中要么被削减，要么被完全消除了。

相反，程序员应该以这种方式组织程序，以便向编译器提供尽可能的信息。这样编译器就能理解整个程序，然后依靠优化器实际上找出如何最有效地将高层抽象映射到高效/最佳机器实现。

我将这种方法称为“编译器导向开发（COD）”，因为它似乎更侧重于让编译器生活便利，而不是让开发者。

这与 Objective-C 所代表的混合模型非常不同，我们在第 1 章的“混合的力量”部分中讨论过那种模型：编译器大部分不干涉，语言提供简单且易于理解的抽象。识别热点并使用提供的许多工具修复它们，是开发者的工作。

## 基准测试

这是一个简短的章节。虽然 Apple 提供了幻灯片和标题性的对比数字，但它没有提供这些数字所依据的基准测试，甚至没有详细结果。提供这些基准测试源代码的请求遭到了沉默。简而言之，Apple 关于 Swift 的性能没有可用的实证数据。

# 评估 Swift 性能

由于 Apple 没有公布 Swift 的实际性能特性，我们必须自己去获取，至少对它们是什么有一定的了解。在接下来，我将对 Swift 的现状给出概述和分析。

# 基础性能

我们在第 1 章已经看到了一些性能情况，编译与 Objective-C 并不相似，当涉及对象时，增长从约 50% 上升到 100%。为了找到原因，我检查了示例 9.1。

# 示例 9.1 Swift 的汇编代码

```
0000000000000f5f cmp 0x3baca00, -0x(%rbp) # imm = 0x3BACA
0000000000000f67 jg 0x1000db
0000000000000f69 movq -0x(%rip), %rax
0000000000000f64 addq _tw10swift($rip), %rax
0000000000000f74 set %cl
0000000000000f77 movq %rax, -0x18(%rbp)
0000000000000d7b movb %cl, -0x19(%rbp)
0000000000000d7e jmp 0x1000eda
0000000000000f84 movq -0x(%rbp), %rax
0000000000000f88 movq %rax, _tw10swift($rip)
0000000000000f8f movq -0x(%rbp), %rcx
0000000000000d93 incq %rcx
0000000000000d96 set %dl
0000000000000d99 movq %rcx, -0x28(%rbp)
0000000000000d94 movb %dl, -0x29(%rbp)
```
