

# 第 7 章 类的更多内容

方法这是因为方法的调用者需要一个对象。因此，该方法的用户必须知道返回的对象是一个新实例，并且必须在之后释放。这可以通过提供给类用户的适当文档来告知。

> 注意
> 这里可以充分利用自动释放池（autorelease pool）来将 Fraction 对象标记为稍后释放。你将在第 15 章“数字、字符串和集合”以及第 17 章“内存管理”中看到如何这样做。

程序 7.5 测试了你新写的方法：`add:`。

## 程序 7.5 测试文件 main.m

```objc
#import "Fraction.h"

int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];

    Fraction *aFraction = [[Fraction alloc] init];
    Fraction *bFraction = [[Fraction alloc] init];

    Fraction *resultFraction;

    [aFraction setTo:1 over: 4]; // 将第一个分数设置为 1/4
    [bFraction setTo:1 over: 2]; // 将第二个分数设置为 1/2

    [aFraction print];
    NSLog("%@*=");
    [bFraction print];
    NSLog("%@*=");

    Fraction *resultFraction = [aFraction add: bFraction];
    [resultFraction print];

    // 这将直接打印结果
    // 此处内存泄漏：

    [[aFraction add: bFraction] print];
    [aFraction release];
    [bFraction release];
    [resultFraction release];

    [pool drain];
    return 0;
}
```

## 从方法中分配并返回对象

## 程序 7.5 输出

```
1/4
+
1/2
=
3/4
3/4
```

这里需要一些解释。首先，你定义了两个 Fraction 对象——aFraction 和 bFraction，并将它们的值分别设置为 1/4 和 1/2。你还定义了一个名为 resultFraction 的 Fraction 对象。该变量将按照如下所示存储你的加法操作结果。

下面这行代码向 aFraction 发送消息，并将 Fraction bFraction 作为其参数传递过去：

```objc
resultFraction = [aFraction add: bFraction];
```

在方法内部，分配了一个 Fraction 对象并执行了加法运算。存储在 Fraction 对象 result 中的结果由方法返回，并存储在变量 resultFraction 中。你可能已经注意到，我们没有在 main 函数中为 resultFraction 分配（或初始化）Fraction 对象；这是因为 `add` 方法为我们分配了该对象，然后返回了该对象的引用。该引用存储在 resultFraction 中。因此，resultFraction 最后存储的是我们在 `add` 方法中分配的 Fraction 对象的引用。

注意，你必须在程序结束时小心释放 resultFraction，即使你没有在 `main` 中自己分配过它。`add` 方法分配了它，但清理它是你的责任。

下面的消息表达式可能看起来像这样，但它实际上会产生问题：

```objc
[[aFraction add: bFraction] print];
```

因为 Fraction 返回后你直接向它发送了打印消息，你没有办法在随后释放由 `add:` 创建的 Fraction 对象。这是一个内存泄漏的示例。如果你在程序中多次进行这种嵌套消息，你将积累许多内存不会被释放的分数存储。每次，你都会分配或泄漏一点你无法直接恢复的内存。

一种解决方案是 `print` 方法返回其接收者（receiver），你可以对其进行释放。但这似乎有点迂回。更好的解决方案是将嵌套消息拆分为两个独立的消息，正如程序早部分所的那样。

让我们来看一下本章中的分数。对于我们的示例，让我们考虑以下级数的计算：

```
\sum_{i=1}^{n} 1/2^i
```

西格符号是求和的缩写。它在这里使用的意思是相加 1/2^i 的值，其中 i 从 1 变化到 n。即相加 1/2 + 1/4 + 1/8 .... 如果将 n 的值设得足够大，这些级数的和应该接近 1。让我们尝试不同的 n 值，看看我们接近多远。程序 7.6 根据输入的 n 值进行运行并执行计算。

## 程序 7.6 FractionTest.m

```objc
#import "Fraction.h"

int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];

    Fraction *aFraction = [[Fraction alloc] init];
    Fraction *sum = [[Fraction alloc] init];
    int i, n, pow2;

    [sum setTo:0 over 1]; // 将第一个分数设置为 0

    NSLog(@"Enter your value for n:");
    scanf("%d",&n);
    pow2 = 2;
    for (i = 1; i<=pow2; i++) {
        [aFraction setTo:1 over pow2];
        sum2 = [sum add:aFraction];
        [sum release]; // 释放之前的和
        sum = sum2;
        pow2 *= 2;
    }

    NSLog(@"After %i iterations, the sum is %g", i, [sum convertNum]);
    [aFraction release];
    [sum release];

    [pool drain];
    return 0;
}
```

## 程序 7.6 输出

## Enter your value for n:
After 5 iterations, the sum is 0.96875

## 程序 7.6 输出 (重新运行)

## Enter your value for n:
After 10 iterations, the sum is 0.999023

## 程序 7.6 输出 (重新运行)

## Enter your value for n:
After 15 iterations, the sum is 0.999969

通过将分子设置为 0，分母设置为 1，Fraction 的值设置为 0（如果将分子和分母都设置为 0 会发生什么？）。程序提示用户使用 `scanf` 输入 n 值。然后你进入一个 `for` 循环来计算级数的和。首先，你初始化变量 `pow2` 为 2。该变量用于存储 2² 的值。每次循环，它的值都会乘以 2。`for` 循环从 1 开始到 n。每次循环，Fraction 设为 1/pow2，或者说 1/2^i。让我们同时查看循环中的三个关键点：

- 1. `sum2 = [sum add: aFraction];` 这调用了方法并传递了参数 aFraction。在方法内部，Fraction 与接收者（sum）相加，并通过赋值语句将结果存储在变量 `sum2` 中。在进入下一步之前，确保你理解了这一点。

- 2. `[sum release];` 这释放了 sum 占据的内存。最初，这是程序启动时分配的分数。然而，这个变量在每次循环中（通过随后的语句）都会被修改以指向不同的分数。

- 3. `sum = sum2;` 这将 `add` 方法返回的引用赋值给 sum，准备下一次循环。在该语句之后，sum 和 sum2 指向同一个 Fraction 对象，即 `add` 方法分配并返回的对象。

`for` 循环完成后，使用 `convert` 方法将最终结果显示为小数。有两个对象需要释放：aFraction 和存储在 sum 中的最终对象。程序执行完成。输出显示了我们在 MacBook Air 上运行程序三次的情况。第一次，计算了级数并显示了 0.96875。第三次，我们将 n 设置为 15 运行程序，得到了非常接近 i 的结果。

## 扩展类定义和接口文件

你现在开发了一个处理分数的小方法库。事实上，这里是接口文件的完整内容，你可以看到通过这个类所完成的工作：

```objc
#import <Foundation/Foundation.h>

// 定义 Fraction 类

@interface Fraction : NSObject
{
    int numerator;
    int denominator;
}

@property int numerator, denominator;
-(void) print;
-(void)setTo:(int) n over:(int) d;
-(double) convertToNum;
-(Fraction *) add:(Fraction *) f;
-(void) reduce;
@end
```

你可能不需要处理分数，但这些示例展示了如何通过添加新方法来不断完善和扩展类。如果你将接口文件交给另一个处理分数的人，对于他们编写处理分数的程序来说足够了。如果那个人需要添加新方法，他可以直接这样做（扩展类定义），也可以间接地这样做（定义自己的子类并添加新方法）。你将在下一章中学习如何这样做。

## 练习

- 1. 在 Fraction 类中添加以下方法以完善分数的算术运算。在每个方法内部对结果约约：

// 接收者减去参数
-(Fraction *) subtract:(Fraction *) f;
// 接收者乘以参数
-(Fraction *) multiply:(Fraction *) f;
// 接收者除以参数
-(Fraction *) divide:(Fraction *) f;

- 2. 修改你 Fraction 类中的 `print` 方法，使其接受一个额外的 BOOL 参数，用于指示在显示时是否对分数约分。如果需要约分（即参数为 YES），请确保不要对分数本身进行任何永久更改。

