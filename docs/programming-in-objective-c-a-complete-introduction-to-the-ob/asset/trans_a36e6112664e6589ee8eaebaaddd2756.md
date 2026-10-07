

# 第 3 章 类、对象与方法

在 Objective-C 中，分配类的新实例并对其进行初始化的两行序列操作非常频繁，因此这两个消息通常被合并在一起，如下：

```
myFraction = [[Fraction alloc] init];
```

首先求值这个内部消息表达式：

```
[Fraction alloc]
```

如你所知，此消息表达式的结果是实际分配的 Fraction 实例。你不再像以前那样将分配结果存储在变量中，而是直接对它应用 `init` 方法。因此，同样地，你首先分配一个新的 Fraction，然后对其进行初始化。初始化的结果被赋值给你的 `myFraction` 变量。

作为一种简写技术，分配和初始化通常直接整合到声明行中，如下：

```
Fraction *myFraction = [[Fraction alloc] init];
```

我们在本书的剩余部分将使用这种风格，因此理解它非常重要。到目前为止，你已经在程序中看到过自动释放池的分配：

```
NSAutleasePool * pool = [[NSAutleasePool alloc] init];
```

这里向 `NSleasePool` 类发送了一个 `alloc` 消息，请求创建一个新实例。向新创建的对象发送 `init` 消息以对其进行初始化。

回到程序 3.2，你现在准备好设置分数值的值了。这些程序行正是执行这一操作的：

```
// 设置分数的分子为: 1;
[myFraction setDenominator:3];
```

第一条消息语句向 `myFraction` 发送了 `setNumerator:` 消息。提供的参数是值 1。控制权传递到你为 `Fraction` 类定义的 `setNumerator:` 方法。Objective-C 系统知道该使用该类的这个方法，因为它知道 `myFraction` 是一个来自 `Fraction` 的对象。

在 `setNumerator:` 方法内部，传递的值 1 被存储在变量 `n` 中。该方法中的单行程序代码将值存储在实例变量 `numerator` 中。因此，你实际上已经将 `myFraction` 的分子设置为 1。

接下来消息调用了 `myFraction` 上的 `setDenominator:` 方法。参数 3 被赋值给 `setDenominator:` 方法内部的变量 `d`。该值被存储在 `denominator` 实例变量中，从而完成了将值 1/3 分配给 `myFraction` 的赋值。现在你准备好显示你的分数值了，你通过程序 3.2 中的以下代码行来实现：

```
// 使用 print 方法显示分数

NSLog(@"The value of myFraction is:");
[myFraction print];
```

`NSLog` 调用只需显示以下文本：

The value of myFraction is:

以下消息表达式调用了 `print` 方法：

```
[myFraction print];
```

在 `print` 方法内部，实例变量 `numerator` 和 `denominator` 的值被用斜杠字符分隔并显示出来。

程序中的消息释放了用于 `Fraction` 对象的内存：

```
[myFraction release];
```

这是良好编程风格的关键部分。每当你创建一个新对象时，你都在请求为它分配内存。此外，当你完成对象的操作后，你有责任在程序终止时释放内存。虽然内存在程序终止时内存会被释放，但如果你开始开发更复杂的应用程序，你可能会有数百（或数千）个消耗内存的对象。等待程序终止来释放内存是浪费内存，会减慢程序的执行速度，而且不是良好的编程风格。从现在起养成释放内存的习惯。

运行时系统提供了一种名为垃圾回收的机制，有助于内存的自动清理。然而，最好是在不依赖这种自动化机制的情况下学习如何自己管理内存。事实上，在某些不支持收集的平台（如 iPhone 或 iPad）上进行编程时，你无法依赖垃圾回收。出于这个原因，我们将在书的后后部分讨论垃圾回收。

看起来你必须编写多得代码来重复程序 3.2 中你的操作。对于这个简单的例子来说确实如此；但处理对象的最终目标是编写、维护和扩展。你会意识到这一点的。

让我们回到 `Fraction *myFraction` 的声明以及随后对其值的设置。

# 第 3 章 类、对象与方法

## 注意

注意 Xcode 在生成 `main` 函数的第一行创建 `autoreleasepool` 对象时在 `*` 之后插入了一个空格，这是不需要的，所以我们对对象也不会这样做。

在声明 `myFraction` 前的星号 (\*) 表示 `myFraction` 实际上是 `Fraction` 对象的引用（或指针）。变量 `myFraction` 并没有存储分数数据（即分子和分母值）。相反，它存储的是引用——实际上是一个内存地址——指示对象数据所在内存的位置。

随后在程序 3.2 中，分数的分子和分母被设置。图 3.4 展示了完全初始化的 Fraction 对象，其分子设置为 1，分母设置为 3。

| | | |
| myFraction | 1 | numerator |
| | 3 | denominator |
| Object's data | | |

图 3.4 设置分数的分子和分母

下一个示例展示了如何在程序中处理多个分数。在程序 3.3 中，你将一个分数设置为 2/3，另一个设置为 3/7，并显示两者。

# 程序 3.3

```
// 处理分数的程序
#import <Foundation/Foundation.h>
//---- @interface 部分 -----

@interface Fraction: NSObject
{
    int numerator;
    int denominator;
}

-(void) print;
-(void) setNumerator:(int) n;
-(void) setDenominator:(int) d;
@end

//---- implementation 部分 -----

@implementation Fraction
-(void) print;
{
    NSLog("@i@%i", numerator, denominator);
}

-(void) setNumerator:(int) n
{
    numerator = n;
}

-(void) setDenominator:(int) d
{
    denominator = d;
}
@end
```

# 第 3 章 类、对象与方法

```
//--- 程序部分 ---

int main (int argc, char *argv[]) {
    NSAutleasePool *pool = [[NSAutleasePool alloc] init];
    Fraction *frac1 = [[Fraction alloc] init];
    Fraction *frac2 = [[Fraction alloc] init];

    // 将第1个分数设置为 2/3
    [frac1 setNumerator:2];
    [frac1 setDenominator:3];

    // 将第2个分数设置为 3/7
    [frac2 setNumerator:3];
    [frac2 setDenominator:7];

    // 显示分数
    NSLog("First fraction is:%@\n", [frac1 print]);

    NSLog("Second fraction is:%@\n", [frac2 print]);

    [frac1 release];
    [frac2 release];

    [pool drain];
    return 0;
}
```

# 程序 3.3 输出

First fraction is:
2/3
Second fraction is:
3/7

@interface 和 @implementation 部分与程序 3.2 保持不变。程序创建了两个名为 frac1 和 frac2 的 Fraction 对象，并将值 2/3 赋值给第一个分数，将 3/7 赋值给第二个分数。请意识到，当 `setNumerator:` 方法应用于 `frac1` 作用于其实例变量时，`frac1` 的实例变量 `numerator` 被设置为 2。同样，`frac2` 使用相同的方法将其分子设置为 3，它独有的实例变量 `numerator` 被设置为值 3。每当你创建一个新对象时，它都会获得一组独特的实例变量。
图 3.5 展示了这一点。

