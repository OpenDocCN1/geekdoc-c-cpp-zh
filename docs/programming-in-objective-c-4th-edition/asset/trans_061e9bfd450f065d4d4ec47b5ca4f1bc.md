

# 程序 7.1 输出

```
The value of myFraction is:
1/3
```

# 合成访问器方法 (Synthesized Accessor Methods)

从 Objective-C 2.0 开始，你可以让系统为你生成 setter 和 getter 方法（统称为访问器方法）。到目前为止，我们还没有向你展示如何这样做，因为对你来说，学会如何编写这些方法很重要。然而，这是语言提供的一项便利功能，现在是时候让你学习如何利用这一特性了。

第一步是在接口部分（interface section）中使用 `@property` 指令来标识你的属性。这些属性的命名通常与你的实例变量相同，尽管不必如此。在我们的 Fraction 类中，两个实例变量 `numerator`（分子）和 `denominator`（分母）属于这一类。下面是添加了新的 `@property` 指令后的接口部分。

```
@interface Fraction : NSObject

@property int numerator, denominator;

-(void)   print;
-(double) convertToNum;
@end
```

注意，我们不再包含 getter 和 setter 方法的定义：`numerator`、`denominator`、`setNumerator:` 和 `setDenominator::`。我们将让 Objective-C 编译器自动为我们生成或合成这些方法。这是实现的？只需在实现部分（implementation section）中使用 `@synthesize` 指令即可，如下所示。

```
#import "Fraction.h"

@implementation Fraction

@synthesize numerator, denominator;

-(void) print
{
    NSLog("%i/%i", numerator, denominator);
}

-(double) convertToNum
{
    if (denominator != 0)
        return (double) numerator / denominator;
    else
        return NAN;
}
@end
```

注意，当你使用 `@property` 指令时，不再需要在实现部分中声明对应的实例变量。如果你愿意，可以声明，但不再是必须的，因为编译器会为你处理。

以下这一行告诉 Objective-C 编译器为两个属性（`numerator` 和 `denominator`）各生成一对 getter 和 setter 方法：

```
@synthesize numerator, denominator;
```

通常情况下，如果你有一个名为 `x` 的属性，在实现部分中包含以下行，会导致编译器自动合成一个名为 `x` 的 getter 方法和一个名为 `setX` 的 setter 方法。

```
@synthesize x;
```

尽管这看起来可能不是什么大事，但让编译器为你这样做是值得的，因为生成的访问器方法将是高效的，并且可以在多线程、多机器、多核心上安全运行。

现在回到程序 7.1，并按照指示对接口和实现部分进行更改，以便为你合成访问器方法。验证在不对 `main.m` 做任何更改的情况下，你仍然从程序获得相同的输出。

# 使用点操作符访问属性

Objective-C 语言允许你使用更方便的语法来访问属性。要获取存储在 `myFraction` 中的 `numerator` 的值，你可以这样写：

```
[myFraction numerator]
```

这将向 `myFraction` 对象发送 `numerator` 消息，返回所需的值。在 Objective-C 中，你也可以使用点操作符编写以下等效表达式：

```
myFraction.numerator
```

这里的通用格式是：

```
instance.property
```

你也可以使用类似的语法来赋值：

```
instance.property = value
```

这等同于编写以下表达式：`[instance setProperty: value]`

在程序 7.1 中，你使用以下两行代码将分数的分子和分母设置为 1/3：

```
myFraction setNumerator: 1;
myFraction setDenominator: 3;
```

这里是编写相同代码行的等效方法：

```
myFraction.numerator = 1;
myFraction.denominator = 3;
```

在本文的剩余部分，我们将使用这些新特性来合成方法和访问属性。

值得指出的是，你可以在手动编写的方法上使用点操作符，而不仅仅是用于合成的方法。此外，如果你有一个名为 `numerator` 的 getter 方法，你仍然可以在程序中编写诸如 `myFraction.numerator` 这样的表达式，即使 `numerator` 没有被定义为属性。

# 注意事项

根据前面的讨论，请意识到虽然编写像 `myFraction.print` 这样的语句在语法上是正确的，但它被认为不是良好的编程风格。点操作符的初衷是用于属性的；通常用于设置/获取实例变量的值。确实有效的方法（例如计算两个分数的之和）在 Apple 的文档中被标记为“任务 (Tasks)”。任务通常不使用点操作符执行；传统的括号消息表达式是首选语法。

# 注意事项

如果你合成了访问器方法，不要以 `new`、`alloc`、`copy` 或 `init` 单词开头。这与编译器对将合成的相应方法的假设有关，并在第 17 章“内存管理与自动引用计数”中有更详细的描述。

# 方法的多个参数

让我们继续处理 Fraction 类并添加一些内容。你定义了六个方法。如果有一个方法可以通过一条消息同时设置分子和分母就太好了。你只需通过列出每个连续参数后跟冒号来定义接收多个参数的方法：这成为了方法名的一部分。例如，`addEntryWithName:andEmail` 方法接收两个参数，推测是一个名字和一个电子邮件地址。`addEntryWithName:andEmail:andPhone` 方法接收三个参数：一个名字、一个电子邮件地址和一个电话号码。

设置分子和分母的方法可以命名为 `setNumerator:andDenominator:`，你可能这样使用它：

```
[myFraction setNumerator: 1 andDenominator: 3];
```

这并不坏。而且这实际上是方法的第一个选择。但我们可以想出一个更有可读性的方法名。例如，如何使用 `setTo:`？这乍看可能没那么吸引人，但将其与之前的一个相比：

```
[myFraction setTo: 1 over: 3];
```

我认为这读起来好一点，但选择取决于你（有些人可能更喜欢第一个名字，因为它显式引用了类中的实例变量）。再次，良好的方法名对于程序的可读性很重要。让我们让这个新方法运行。首先，在接口文件中添加 `setTo:over:` 的声明，如程序 7.2 所示。

# 程序 7.2 接口文件: Fraction.h

```
@import <Foundation/Foundation.h>

// 定义 Fraction 类

@interface Fraction : NSObject

@property int numerator, denominator;

-(void) print;
-(void) setTo:(int) n over:(int) d;
-(double) convertToNum;
@end
```

接下来，在实现文件中添加新方法的定义。

# 程序 7.2 实现文件: Fraction.m

```
#import "Fraction.h"

@implementation Fraction

@synthesize numerator, denominator;

-(void) print
{
    NSLog("%i/%i", numerator, denominator);
}

-(double) convertToNum
{
    if (denominator != 0)
        return (double) numerator / denominator;
    return NAN;
}

-(void) setTo:(int) n over:(int) d
{
    numerator = n;
    denominator = d;
}
@end
```

新的 `setTo:` 方法只需将其两个整数参数赋值给分数、分子和分母的对应的实例变量。

这里有一个尝试新方法的测试程序。

# 程序 7.2 测试文件: main.m

```
#import "Fraction.h"

int main (int argc, char * argv[])
{
    @autoreleasepool {
        Fraction *aFraction = [[Fraction alloc]
        init];

        [aFraction setTo: 100 over: 200];
        [aFraction print];

        [aFraction setTo: 1 over: 3];
        [aFraction print];
    }

    return 0;
}
```

# 程序 7.2 输出

100/200
1/3

# 无参数名称的方法

在创建方法名称时，参数名称实际上是可选的。例如，你可以像这样声明一个方法：

+   - (int) set: (int) n: (int) d;

注意，与之前的示例不同，这里方法的第二个参数没有名称。该方法被命名为 `set::`。

