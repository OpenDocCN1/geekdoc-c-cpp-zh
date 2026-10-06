

# 注意

你应该使用 `printf` 来打印你的字符，因为 `NSLog` 在每次调用时都会显示新行。

# 9. 多态、动态类型和动态绑定

在本章中，你将学习 Objective-C 语言的某些特性，这些特性使其成为一种强大的编程语言，并将其区别于 C++ 等其他面向对象的编程语言。本章描述了三个核心概念：多态、动态类型和动态绑定。多态允许在开发程序时，使得不同类的对象可以定义方法。动态类型将对象所属类的确定推迟到程序执行时。动态绑定则将在对象上调用的实际方法的确定推迟到程序运行时间。

# 多态：相同名，不同类

程序 9.1 显示了名为 Complex 的类的接口文件，它用于在程序中表示复数。

# 程序 9.1. 接口文件 Complex.h

```
// Complex 类的接口文件

#import <Foundation/Foundation.h>

@interface Complex: NSObject

@property double real, imaginary;
-(void) print;
-(void) setReal:(double)a andImaginary:
```
(double) b;
-(Complex *) add: (Complex *) f;
@end
```

你应该已经从第 7 章“关于类的更多内容”的练习 5 和 6 中完成了该类的实现部分。我们添加了一个额外的 `setReal:andImaginary:` 方法，以便你通过一条消息同时设置数的实部和虚部，并合成了访问器方法。如下所示。

# 程序 9.1. 实现文件 Complex.m

```
// Complex 类的实现文件

#import "Complex.h"

@implementation Complex

@synthesize real, imaginary;

-(void) print
{
    NSLog("%g + %gi", real, imaginary);
}

-(void) setReal: (double) a andImaginary:
(double) b
{
    real = a;
imaginary = b;
}

-(Complex *) add: (Complex *) f
{
Complex *result = [[Complex alloc] init];
result.real = real + f.real;
result.imaginary = imaginary + f.imaginary;
return result;
}
@end
```

# 程序 9.1. 测试程序 main.m

```
// 共享方法名：多态

#import "Fraction.h"
#import "Complex.h"

int main(int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *f1 = [[Fraction alloc] init];
        Fraction *f2 = [[Fraction alloc] init];
        Fraction *fracResult;
        Complex *c1 = [[Complex alloc] init];
        Complex *c2 = [[Complex alloc] init];
        Complex *compResult;

        [f1 setTo: 1 over: 10];
        [f2 setTo: 2 over: 15];

        [c1 setReal: 18.0 andImaginary: 2.5];
        [c2 setReal: -5.0 andImaginary: 3.2];

        // 相加并打印两个复数
        [c1 print]; NSLog("+"); [c2 print];
        NSLog("-------");
        compResult = [c1 add: c2];
        [compResult print];
        NSLog("\n");

        // 相加并打印两个分数
        [f1 print]; NSLog("+"); [f2 print];
        NSLog("-------");
        fracResult = [f1 add: f2];
        [fracResult print];
    }
    return 0;
}
```

# 程序 9.1. 输出

```
18 + 2.5i
+
-5 + 3.2i
------
13 + 5.7i

1/10
+
2/15
----
7/30
```

注意，Fraction 和 Complex 类都包含 add: 和 print 方法。因此，当执行消息表达式时

```
compResult = [c1 add: c2];
[compResult print];
```

系统如何知道执行哪些方法？很简单：Objective-C 运行时知道 c1（第一条消息的接收者）是一个 Complex 对象。因此，它选择了为 Complex 类定义的 add 方法。

Objective-C 运行时系统还确定 compResult 是一个 Complex 对象，因此它选择了 Complex 类中定义的 print 方法来显示加法结果。同样的讨论也适用于以下消息表达式：

```
fracResult = [f1 add: f2];
[fracResult print];
```

# 注意

正如第 13 章“底层 C 语言特性”中更完整描述的那样，系统始终携带关于对象所属类的信息。这使得它能够在运行时而不是编译时做出这些关键决策。

根据 f1 和 fracResult 的类，选择了 Fraction 类中对应的方法来求值消息表达式。

如提到的，在不同类之间共享相同方法名的能力被称为多态。多态允许你开发一组类，每个类都可以响应相同的方法名。每个类的定义都封装了响应该特定方法所需的代码，这使得它与其它类的定义保持保持独立。这还允许你稍后添加可以响应具有相同名称方法的类类。

# 动态绑定和 id 类型

第 4 章简要提到了 `id` 数据类型，并指出它是一个泛型对象类型。也就是说，`id` 可以用于存储属于任何类的对象。这种数据类型的真正威力是在程序执行期间用它在变量中存储不同类型的对象时。研究程序 9.2 及其相关输出。

# 程序 9.2. 测试程序 main.m

```
// 演示动态类型和绑定

#import "Fraction.h"
#import "Complex.h"

int main (int argc, char * argv[])
{
    autoreleasepool {
        id dataValue;
        Fraction *f1 = [[Fraction alloc] init];
        Complex *c1 = [[Complex alloc] init];

        [f1 setTo: 2 over: 5];
        [c1 setReal: 10.0 and Imaginary: 2.5];

        // dataValue 首先获得一个分数
        dataValue = f1;
        [dataValue print];

        // 现在 dataValue 获得一个复数
        dataValue = c1;
        [dataValue print];
    }
    return 0;
}
```

# 程序 9.2. 输出

2/5
10 + 2.5i

变量 `dataValue` 被声明为 `id` 对象类型。因此，`dataValue` 可以用于持有程序中的任何类型的对象。注意声明行中没有星号：

id dataValue;

Fraction f1 被设置为 2/5，复数 c1 被设置为 (10 + 2.5i)。赋值操作

dataValue = f1;

将 Fraction f1 存储在 dataValue 中。现在，你可以对 dataValue 做什么？嗯，你可以在 dataValue 上调用任何你可以在 Fraction 对象上使用的方法，尽管 `dataValue` 的类型是 `id` 而不是 `Fraction`。但如果 `dataValue` 可以存储任何类型的对象，系统是如何知道要调用哪个方法的呢？也就是说，当它遇到消息表达式时

```
[dataValue print];
```

它如何知道调用哪个 print 方法？你为 Fraction 和 Complex 类都定义了 print 方法。

如之前所述，答案在于 Objective-C 系统始终跟踪对象所属的类。它也在于动态类型和动态绑定的概念——也就是说，系统在运行时而不是编译时动态地做出关于对象的类以及因此调用哪个方法的决策。

所以，程序执行期间，在系统向 `dataValue` 发送 print 消息之前，它首先检查存储在 `dataValue` 内部对象的类。在程序 9.2 的第一个情况下，该变量包含一个 Fraction 对象，因此使用了 Fraction 类中定义的 print 方法。这通过程序的输出验证了这一点。

在第二种情况下，发生了相同的事情。首先，将复数 c1 赋值给 dataValue。接下来，执行以下消息表达式：

```
[dataValue print];
```

这一次，因为 dataValue 包含一个属于 Complex 对象，因此选择了该类中对应的 print 方法进行执行。

这是一个简单的例子，但你可以将这一概念推广到更复杂的应用程序中。与多态结合，动态绑定和动态类型允许你轻松地编写代码，向不同类的对象发送相同的消息。

例如，考虑一个可以用于在屏幕上绘制图形对象的 draw 方法。你可能为你的每个图形对象定义了不同的 draw 方法，例如文本、圆形、矩形、窗口等。如果要绘制的特定对象

