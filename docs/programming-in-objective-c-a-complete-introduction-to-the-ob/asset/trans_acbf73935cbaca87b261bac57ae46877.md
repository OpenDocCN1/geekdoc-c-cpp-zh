

# 访问实例变量与数据封装

| 对象 | frac1 | frac2 |
| --- | --- | --- |
| 实例变量 | numerator 2 denominator 3 | numerator 3 denominator 7 |

图 3.5 唯一的实例变量

根据接收消息的对象不同，程序会引用正确的实例变量。因此，每当 `setNumerator:` 使用方法内部的名称 `numerator` 时，引用的都是 `frac1` 的 `numerator`：

```
[frac1 setNumerator: 2];
```

这是因为 `frac1` 是该消息的接收者。

# 访问实例变量与数据封装

你已经看到处理分数的方法是如何通过名称直接访问 `numerator` 和 `denominator` 这两个实例变量的。事实上，实例方法始终可以访问它的实例变量。然而，类方法不能这样做，因为它处理的是类本身，而不是该类的任何实例（可以想一下第二种情况）。但如果你想从其他地方访问你的实例变量呢——例如，从你的主程序（main routine）内部访问？你无法直接访问它们，因为它们是隐藏的。这种隐藏状态是一个核心概念，被称为**数据封装**（data encapsulation）。它允许编写封装，在程序员和类开发者之间提供了一个新的隔绝层。

你可以通过编写特殊的方法来设置和检索它们的值，以一种简洁的方式访问你的实例变量。我们在 `Fraction` 类中编写了 `setNumerator:` 和 `setDenominator:` 方法来设置两个实例变量的值。为了检索这些实例变量的值，你需要编写两个新方法。例如，你将创建两个新方法，恰好命名为 `numerator` 和 `denominator`，以访问作为消息接收者的 `Fraction` 对应的实例变量。结果是返回其对应的整数值。以下是你的两个新方法的声明：

- (int) numerator;
- (int) denominator;

以下是它们的定义：

```
(int) numerator
```

# 第 3 章 类、对象与方法

```objc
return numerator;
}
-(int) denominator
{
return denominator;
}
```

注意，方法名称与它们访问的实例变量名称是相同的。这样做没有问题（尽管起初看起来可能有点奇怪）；事实上，这是一种常见的做法。程序 3.4 测试了你的两个新方法。

# 程序 3.4

```objc
// 访问实例变量的程序 - 续
#import <Foundation/Foundation.h>
//---接口部分 ---
@interface Fraction : NSObject
{
int numerator;
int denominator;
}
-(void) print;
-(void) setNumerator:(int) n;
-(void) setDenominator:(int) d;
-(int) numerator;
-(int) denominator;
@end
//---实现部分 ---
@implementation Fraction
-(void) print
{
NSLog("@%i/%i", numerator, denominator);
}
-(void) setNumerator:(int) n
{
numerator = n;
}
-(void) setDenominator:(int) d
{
denominator = d;
}
-(int) numerator
{
return numerator;
}
```

# 访问实例变量与数据封装

```objc
-(int) denominator
{
return denominator;
}
@end

//-- 程序部分 ---

int main(int argc, char *argv[]) {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    Fraction *myFraction = [[Fraction alloc] init];

    // 设置分数为 1/3
    [myFraction setNumerator: 1];
    [myFraction setDenominator: 3];

    // 使用我们的两个新方法显示分数
    NSLog("@The value of myFraction is: %i/%i",
    [myFraction numerator], [myFraction denominator]);
    [myFraction release];
    pool drain;

    return 0;
}
```

# 程序 3.4 输出

The value of myFraction is 1/3

这条 `NSLog` 语句显示了向 `myFraction` 发送两个消息的结果：第一个用于获取其分子的值，第二个用于获取其分母的值。
`NSLog("@The value of myFraction is: %i/%i", [myFraction numerator], [myFraction denominator]);`



因此，在第一次调用中，`numerator` 将发送给 `Fraction` 对象 `myFraction`。在该方法内部，代码将返回该分数的 `numerator` 实例变量的值。记住，方法执行时的上下文是该方法的接收者对象。当 `numerator` 方法访问并返回 `numerator` 实例变量的值时，访问并返回的是 `myFraction` 的 `numerator`。该返回的整数值被传递给 `NSLog` 进行显示。

对于第二次调用，将调用 `denominator` 来访问并返回 `myFraction` 的分母的值，然后该值被传递给 `NSLog` 显示。

设置实例变量值的方法通常统称为 **setter**（set器），而用于检索实例变量值的方法称为 **getter**（get器）。对于 `Fraction` 类，`setNumerator` 和 `setDenominator` 是 setters，而 `numerator` 和 `denominator` 是 getters。setter 和 getter 统称为**访问器方法**（accessor methods）。

# 第 3 章 类、对象与方法

注意

不久后你将学习 Objective-C 2.0 的一个方便功能，该功能允许自动生成 getter 和 setter 方法。

确保你理解 setter 和 getter 之间的区别。setter 不返回结果，因为它们的目的是接收一个参数并将实例变量设置为该参数的值。在这种情况下，不需要返回任何值。这就是 setter 的目的：将实例变量设置为该参数的值。而另一方面，getter 的目的是获取实例变量的值。

这种封装在程序员和类开发者之间提供了一个新的隔绝层。允许封装在程序员和类开发者之间提供了一个新的隔绝层。通常情况下，使用两步的分配和初始化可以从概念上理解正在发生的事件：你正在创建一个新对象并初始化它。alloc 和 init。

# 总结

现在你已经知道如何定义类、创建类的实例并向这些对象发送消息。回到 `Fraction` 类并在后续章节中你将学习如何向方法传递多个参数、如何将类定义划分到单独的文件，以及如何使用继承和动态绑定等概念。但现在是时候学习更多数据类型和 Objective-C 表达式了。首先，尝试练习来测试你的理解。

# 练习

- 1. 以下哪些名称是无效的？为什么？

```
Int playNextSong 05
_calloc Xx alphaRoutine
clearScreen 1312
ReInitialize - A$
```

- 2. 根据本章的示例，想出一个你每天使用的对象。为它识别一个类并写出五个操作。

- 3. 使用以下语法重写练习 2 中的列表：



- 4. 假设你除了汽车还拥有一艘船和一辆自行车。列出对每个对象的操作。这些操作之间是否有重叠？

- 5. 根据第 4 题，假设你有一个 `Vehicle` 类以及一个名为 `myVehicle` 的对象，可以是汽车、自行车或船。想象你写了以下代码：

[myVehicle prep]
[myVehicle getGas]
[myVehicle service];

你认为能够将一个操作应用于多个类中的对象有什么优势？

- 6. 在 C 等过程化语言中，你考虑操作，然后编写代码对对象执行操作。参考汽车的示例，你可能会编写一个 C 程序来洗车，并在程序内部编写代码处理洗车、洗船、洗自行车等。如果你采用这种方法并想添加一种新的车辆类型（上一个练习），你认为使用这种过程化方法相对于面向对象的方法有什么优缺点？

- 7. 定义一个 `XYPoint` 类，用于存储笛卡尔坐标 (x, y)，其中 x 和 y 是整数。定义方法来分别设置点的 x 和 y 坐标并检索它们的值。编写一个 Objective-C 程序来实现你的新类并对其测试。

