
在程序执行开始时被初始化，并在连续的方法调用中保留其值。

以下代码序列可能出现在 `showPage` 方法内部，该方法想要跟踪它被调用的次数（或者在这种情况下，可能是跟踪已打印的页面数）：

```
(int) showPage
{
    static int pageCount = 0;
    ...
    ++pageCount;
    ...
    return pageCount;
}
```

局部静态变量只会在程序启动时被设置为 0，并且会在 `showPage` 方法的连续调用中保留其值。

请注意将 `pageCount` 为局部静态变量与将其设为实例变量的区别。在一种情况下，`pageCount` 可以计算调用 `showPage` 方法的所有对象打印的页面数。在后一种，变量将计算每个独立对象打印的页面数；每个对象都拥有自己的 `pageCount` 副本。

记住，静态或局部变量只能从定义它们的方法内部访问。因此，即使是 `pageCount` 变量只能从 `showPage` 内部访问。你可以将变量声明移动到任何方法声明之外（通常位于实现文件的开头），以便任何方法都能访问，如下所示：

```
@import "Printer.h"
static int pageCount;
```

```
@implementation Printer
...
@end
```

现在，文件中任何实例方法或类方法都可以访问 `pageCount` 变量。第 10 章“变量和数据类型进”将详细介绍变量作用域这一主题。

回到分数，你可以将 `reduce` 方法的代码整合到你的 `Fraction.m` 实现文件中。别忘记在 `Fraction.h` 接口文件中也声明 `reduce` 方法。完成这些后，你可以在程序 7.4 中测试你的新方法。在这里我们展示了所有三个文件：接口文件、实现文件和测试程序文件。

# 程序 7.4. 接口文件：Fraction.h

```
#import <Foundation/Foundation.h>

// 定义 Fraction 类

@interface Fraction : NSObject

@property int numerator, denominator;

-(void) print;
-(void) setTo:(int) n over:(int) d;
-(double) convertToNum;
-(void) add:(Fraction*) f;
-(void) reduce;
@end
```

# 程序 7.4. 实现文件：Fraction.m

```
#import "Fraction.h"

@implementation Fraction

@synthesize numerator, denominator;

-(void) print {
    NSLog("%@/%@", numerator, denominator);
}

-(double) convertToNum {
    if (denominator != 0)
        return (double) numerator / denominator;
    else
        return NAN;
}

-(void) setTo: (int) n over: (int) d {
    numerator = n;
    denominator = d;
}

// 将一个 Fraction 加到接收者上

-(void) add: (Fraction *) f {
    // 加两个分数：
    // a/b + c/d = ((a*d) + (b*c)) / (b * d)
    numerator = numerator * f.denominator +
    denominator * f.numerator;
denominator = denominator * f.denominator;
}

-(void) reduce
{
int u = numerator;
int v = denominator;
int temp;

while (v != 0) {
    temp = u % v;
    u = v;
    v = temp;
}

numerator /= u;
denominator /= u;
}
}
```

# 程序 7.4. 测试文件 main.m

```
#import "Fraction.h"

int main (int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *aFraction = [[Fraction alloc] init];
        Fraction *bFraction = [[Fraction alloc] init];

        [aFraction setTo: 1 over: 4]; // 将第一个分数设为 1/4
        [bFraction setTo: 1 over: 2];      // 将第二个分数设为 1/2

        [aFraction print];
        NSLog("@+");
        [bFraction print];
        NSLog("=");

        [aFraction add: bFraction];

        // 约简加法结果并打印

        [aFraction reduce];
        [aFraction print];
    }

return 0;
}
```

# 程序 7.4. 输出

1/4
+
1/2
=
3/4

这样好多了！

# self 关键字

在程序 7.4 中，我们决定在 `add:` 方法外部约简分数。我们也可以在 `add:` 内部这样做；这个决定完全是任意的。然而，我们如何识别要约简的分数呢？我们到底想要约简哪个分数？我们想要约简发送给 `add:` 消息的同一个分数。

我们知道如何直接通过名称识别方法内部的实例变量，但不知道如何识别消息的接收者。幸运的是，有一种方法可以。

你可以使用 `self` 关键字来指代当前消息的接收对象。如果你在 `add:` 方法内部写了

```
[self reduce];
```

那么 `reduce` 方法将应用于作为 `add:` 消息接收者的 Fraction 对象，这正是你所想要的。你将在整本书中看到 `self` 是多么有用。
