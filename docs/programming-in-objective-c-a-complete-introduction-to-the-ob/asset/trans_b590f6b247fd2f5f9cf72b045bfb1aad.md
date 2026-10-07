

## 第 6 章 决策

让我们在程序 6.2 中使用这种新方法。

## 程序 6.2

```objc
#import <Foundation/Foundation.h>

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
-(double) convertToNum;
@end

@implementation Fraction
-(void) print
{
    NSLog("%@ %*i", numerator, denominator);
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

-(int) denominator
{
    return denominator;
}

-(double) convertToNum
{
    if (denominator != 0)
        return (double) numerator / denominator;
    else
        return NAN;
}
@end

int main (int argc, char *argv[])
{
NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];

Fraction *fraction = [[Fraction alloc] init];
Fraction *bFraction = [[Fraction alloc] init];

[fraction setNumerator: 1]; // 第一个分数是1/4
[fraction setDenominator: 4];

[fraction print];
NSLog("%@ = %@");
NSLog("%@ = %f", [fraction convertToNum]);

[bFraction print]; // 从未赋值
NSLog("%@ = %@");
NSLog("%@ = %f", [bFraction convertToNum]);
[fraction release];
[bFraction release];

[pool drain];
return 0;
}
```

## 程序 6.2 输出

1/4
=0.25
0/0
nan

在将一个 Fraction 设置为 1/4 后，程序使用 `convertToNum` 方法将分数转换为小数值。该值显示为 0.25。

在第二种情况下，bFraction 的值没有被显式地设置，因此它的分子和分母被初始化为零，这是实例变量的默认值。这解释了 `print` 方法的输出。它还导致 `convertToNum` 方法内部的 `if` 语句返回值 NAN，你会注意到它实际上被 `NSLog` 显示为 nan。

## if-else 结构

如果有人问你某个数字是偶数还是奇数，你很可能会通过检查数字的最后一位数字来判断。如果这个数字是 0、2、4、6 或 8，你会很快地断定该数字是偶数。否则，你会声称该数字是奇数。

计算机判断某个数字是偶数还是奇数的更简单方法是：不检查数字的最后一位数字是否为 0、2、4、6 或 8，而是简单地判断该数字是否能被 2 整除。如果是，该数字就是偶数；否则，它是奇数。

你已经看到过如何使用模运算符 `%` 来计算一个整数除以另一个整数的余数。这使其成为判断一个整数是否能被 2 整除的完美运算符。如果除以 2 后的余数为0，它就是偶数；否则，它就是奇数。

现在让我们写一个程序，判断用户输入的整数值是偶数还是奇数，并在终端上显示适当的消息——参见程序 6.3。

## 程序 6.3

```objc
// 判断数字是偶数还是奇数的程序

#import <Foundation/Foundation.h>
int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc];

    int number_to_test, remainder;

    NSLog("@@输入要测试的数字: ");
    scanf("%d", &number_to_test);

    remainder = number_to_test % 2;

    if (remainder == 0) {
        NSLog("@@该数字是偶数.");
    }
    if (remainder != 0) {
        NSLog("@@该数字是奇数.");
    }

    [pool drain];
    return 0;
}
```

## 程序 6.3 输出

输入要测试的数字:
2455
该数字是奇数。

## 程序 6.3 输出（重新运行）

输入要测试的数字:
1210
该数字是偶数。

输入数字后，程序会计算除以 2 后的余数。第一个语句测试该余数的值，看它是否等于零。如果是，则显示消息“该数字是偶数。”

## if 语句

第二个 `if` 语句测试余数判断是否不等于零，如果是那样，则显示一条说明该数字是奇数的消息。

每当第一个语句成功时，第二个语句必须失败，反之亦然。当你回想起在本节开始处关于偶奇数的讨论时，我们说过，如果数字能被 2 整除，它就是偶数；否则，它就是奇数。

在编写程序时，这种“else”概念被频繁地需要，因此提供了一个特殊的结构来处理这种情况。在 Objective-C 中，这被知为 `if-else`，其通用格式如下：

```objc
if ( expression )
    program statement 1
else
    program statement 2
```

`if-else` 实际上是 `if` 语句通用格式的扩展。如果表达式评估的结果为真，则执行紧随其后的程序语句 1；否则，执行程序语句 2。在任何情况下，程序语句 1 或程序语句 2 其中之一个会被执行，但两者都不会同时执行。

你可以将 `if-else` 语句合并到之前的程序，用一个单一的 `if-else` 语句替换两个语句。你会看到这种新的程序结构实际上某种程度上降低了程序的复杂度并提高了其可读性。

## 程序 6.4

```objc
// 判断数字是偶数还是奇数（版本 2）

#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    int number_to_test, remainder;

    NSLog("@输入要测试的数字:");
    scanf("%d", &number_to_test);

    remainder = number_to_test % 2;
    if (remainder == 0) {
        NSLog("@该数字是偶数.");
    } else {
        NSLog("@该数字是奇数.");
    }

    [pool drain];
    return 0;
}
```

## 程序 6.4 输出

输入要测试的数字:
1234
该数字是偶数。

## 程序 6.4 输出（重新运行）

输入要测试的数字:
6551
该数字是奇数。

不要忘记双等号 `(==)` 是相等性测试，而单等号是赋值运算符。忘记这一点并在语句中无意使用赋值运算符会导致很多麻烦。

## 复合关系测试

到目前为止在本章中使用的 `if` 语句建立的是两个数字之间的简单关系测试。程序 6.1 比较了数字与零，而程序 6.2 比较了分母与零。有时，使用更复杂的测试变得理想甚至是必要的。假设你想统计考试成绩在 70 到 79 之间的数量（包含边界）。在这种情况下，你希望不仅将成绩与一个边界比较，而且确保 70 和 79 这两个边界都在指定的范围内。

Objective-C 语言提供了执行这类复合关系测试的机制。复合关系测试是一个或多个简单关系测试通过逻辑字符 `&&` 或 `||`（两条垂直线）分别连接起来。例如，下面的 Objective-C 语句只有当成绩值大于等于 70 且小于等于 79 时，才会增加 `grades_70_to_79` 的值：

```objc
if ( grade >= 70 && grade <= 79 )
    ++grades_70_to_79;
```

同样，下面的语句当 `index` 小于 0 或大于 99 时会导致 `NSLog` 语句执行：

```objc
if ( index < 0 || index > 99 )
    NSLog("Error index out of range");
```复合运算符可以在 Objective-C 中形成极其复杂的表达式。Objective-C 语言赋予了程序员形成表达式的终极灵活性，这种灵活性是一种程序员经常滥用的能力。简单的表达式几乎更容易阅读和调试。

在形成复合关系表达式时，务必使用括号以避免表达式的可读性问题，并避免由于对表达式运算符优先级的错误假设而导致麻烦。（`&&` 运算符的优先级较低
```
