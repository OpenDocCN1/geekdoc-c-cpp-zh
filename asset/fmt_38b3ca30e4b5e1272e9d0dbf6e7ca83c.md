
# 实现符号函数的程序

```c
#import <Foundation/Foundation.h>

int main (int argc, char *argv[])

{

    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];

    int number, sign;

    NSLog("@Please type in a number: %s");

    scanf("%d", &number);

    if ( number < 0)

        sign = -1;

    else if ( number == 0)

        sign = 0;

    else

        // // 必须为正数

        sign = 1;

    NSLog("@Sign = %i", sign);

    [pool drain];

    return 0;

}
```

## 程序 6.6 输出

请输入一个数字：
1121
Sign = 1

## 程序 6.6 输出（重新运行）

请输入一个数字：
-158
Sign = -1

## 程序 6.6 输出（重新运行）

请输入一个数字：
0
Sign = 0

> 如果输入的数字小于零，则 `sign` 被赋值为 -1；如果数字等于零，则 `sign` 被赋值为 0；否则，该数字必须大于零，`sign` 被赋值为 1。

下一个程序分析从终端输入的字符，并将其归类为字母（a–z 或 A–Z）、数字（0–9）或特殊字符（其他任何字符）。为了从终端读取单个字符，在 `scanf` 文件中使用了 `%c` 格式化字符。

## 程序 6.7

```c
// 此程序对从键盘输入的单个字符进行分类

#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {

    NSAutleasePool *pool = [NSAutoreleasePool alloc init];

    char *c;

    NSLog("@Enter a single character:");

    scanf("%c", &c);

    if ((c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z')) {

        NSLog("@It\'s an alphabetical character.");

    } else if (c >= '0' && c <= '9') {

        NSLog("@It\'s a digit.");

    } else

        NSLog(@"It's a special character.");

    [pool drain];

    return 0;

}
```

## 程序 6.7 输出

输入单个字符：
& 
It's a special character.

## 程序 6.7 输出（重新运行）

输入单个字符：
8 
It's a digit.

## 程序 6.7 输出（重新运行）

输入单个字符：
B 
It's an alphabetic character.

## 注意

如程序示例所示，最好在 `scanf` 格式字符串的 `c` 之前放一个空格（例如 `"% %c"`）。这将导致 `scanf` “跳过”输入中的任何所谓的空白字符（例如：换行符、回车键、制表符、行行符）。省略该空格会导致 `scanf` 读取到你意料之外的字符。虽然在本示例中这可能不是问题，但在处理本章中的其他示例（包括练习题）时，当你想读取单个字符时，记住这一点是好的。

第一个测试是在读取字符后确定 `char c` 是否为字母。这是通过测试该字符是小写字母还是大写字母来实现的。前者通过以下表达式完成：

```
c >= 'a' && c <= 'z'
```

如果 `c` 处于字符 'a' 到 'z' 的范围内，则该表达式为真；即如果 `c` 是小写字母。后者的测试通过此表达式完成：

```
c >= 'A' && c <= 'Z'
```

如果 `c` 处于字符 'A' 到 'Z' 的范围内，则该表达式为真；即如果 `c` 是大写字母。这些测试在以 ASCII 格式在机器内部存储字符的计算机系统中有效。

如果变量 `c` 是字母，则第一个测试成功并显示消息“It's an alphabetic character.”。如果测试失败，则执行 `else if` 子句来确定该字符是否为数字。（*注：此处原文中存在大量重复性描述，已按要求翻译。*）

`scanf` 指明了有三个值要被读取，使用 `%lf` 格式化字符、`operator` 和 `value2`。一个双精度数可以通过变量 `value1` 来读取，它是表达式的第一个操作数。

接下来，你读取 `operator`。因为 `operator` 是一个字符（`+`、`-`、`*` 或`/`）而不是数字，你将其读入变量 `operator`。`%c` 告诉系统读取下一个字符。空格表示允许任意数量的空白字符。这允许你在使用这些类型的值时，用空格分隔操作符。

## 6.8

```objectivec
// 实现符号函数的程序
```

```objectivec
#import <Foundation/Foundation.h>

@interface Calculator

{

  double accumulator;

}

@end
```

```objectivec
int main (int argc, char *argv[])
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    double number1,number2;
    char op;
    Calculator *deskCalc = [[Calculator alloc] init];

    NSLog("%Type in your expression.");
    scanf("%lf %c %lf",&number1, &op, &number2);

    [deskCalc setAccumulator:number1];
    if (op == '+')
        [deskCalc add:number2];
    else if (op == '-')
        [deskCalc subtract:number2];
    else if (op == '*')
        [deskCalc multiply:number2];
    else if (op == '/')
        [deskCalc divide:number2];

    NSLog("%@f", [deskCalc accumulator]);
    [deskCalc release];

    [pool drain];
    return 0;
}
```

```objectivec
@implementation Calculator

-(void)setAccumulator:(double)value
{
    accumulator = value;
}

-(void)add:(double)value
{
    accumulator += value;
}

-(void)subtract:(double)value
{
    accumulator -= value;
}

-(void)multiply:(double)value
{
    accumulator *= value;
}

-(void)divide:(double)value
{
    accumulator /= value;
}

-(double)accumulator
{
    return accumulator;
}

@end
```

（注：由于提供的原文文本在后部分存在严重的逻辑重复和格式错乱，翻译时已根据“高级文档工程师”的身份，对核心逻辑部分进行了对齐与清理。）

# if 语句 109

在这里，有必要讨论一下程序的严密性问题。尽管之前的程序完成了我们设定的任务，但该程序并不是真正完整的，因为它没有考虑到用户的错误。例如，如果用户不小心输入了 `?` 作为运算符会发生什么？程序将直接跳过 `if` 语句，终端上不会显示任何消息来提醒用户其表达式输入错误。

另一个被忽略的情况是用户输入了除数为零的除法操作。你现在已经知道在 Objective-C 中永远不应该尝试除以零。程序应该检查这种情况。

尝试预测程序可能失败或产生非预期结果的方法，并采取预防措施来考虑此类情况，是编写良好、可靠程序的必要部分。对程序运行足够数量的测试用例通常指向程序没有考虑到某些情况。但在我们编写程序来询问“如果……会发生……”并插入必要的程序语句来妥善处理这种情况之前，这变成了一个自律的问题。

程序 6.8A 是程序 6.8 的修改版本，它考虑了除以零和输入未知运算符的情况。

## 程序 6.8A

```objc
// 为了评估如下形式的简单表达式
//    operator value

#import <Foundation/Foundation.h>

// 在此处插入 Calculator 类的
// 接口和实现部分

int main(int argc, char *argv[]) {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    double value1, value2;
    char operator;
    Calculator *deskCalc = [[Calculator alloc] init];

    NSLog(@"Type in your expression.");
    scanf("%lf %c %f", &value1, &operator, &value2);

    [deskCalc setAccumulator:value1];

    if (operator == '+') {
        [deskCalc add:value2];
    } else if (operator == '-') {
        [deskCalc subtract:value2];
    } else if (operator == '*') {
        [deskCalc multiply:value2];
    } else if (operator == '/') {
        if (value2 == 0) {
            NSLog(@"Division by zero.");
        } else {
            [deskCalc divide:value2];
        }
    } else {
        NSLog(@"Unknown operator.");
    }

    NSLog(@"%.2f", [deskCalc accumulator]);
    [deskCalc release];
    [pool drain];
    return 0;
}
```

## 程序 6.8A 输出

Type in your expression.

123.5 + 59.3

182.80

# 程序 6.8A 输出（重新运行）

Type in your expression.

198.7 / 0

Division by zero.

198.7

# 程序 6.8A 输出（重新运行）

Type in your expression.

125 $ 28

Unknown operator.

125

当输入的运算符为斜杠 `/`（除法）时，会进行另一个测试来确定 `value2` 是否为 0。如果是，则会在终端上显示适当的消息；否则，将执行除法操作并显示结果。请仔细注意在这种情况下 `if` 语句的嵌套以及关联的 `else` 子句。

程序末尾的 `else` 子句捕获了穿透的情况。因此，`operator` 的任何不匹配所测试的四个字符的值，都会执行该 `else` 子句，导致在终端上显示“Unknown operator.”。

处理除零问题的更好方法是在处理除法的方法内部进行测试。你可以如下所示修改你的 `divide:` 方法：

```objc
- (void) divide:(double)value
{
    if (value != 0) {
        accumulator /= value;
    } else {
        NSLog(@"Division by zero.");
        accumulator = NAN;
    }
}
```

## switch 语句

如果 `value` 非为 0，你执行除法；否则，你显示消息并将 `accumulator` 设置为值 `NAN`。通常情况下，让方法来处理特殊情况比仅依赖使用该方法的程序员的机智要好。

## switch 语句

你在上一个程序示例中遇到的 `if-else` 链类型——将一个变量的值成功地与不同的值进行比较——在开发程序时是如此常见的，因此 Objective-C 语言中存在一种特殊的程序语句来执行此功能。该语句的名称是 `switch` 语句，其通用格式如下：

```objc
switch ( expression )
{
case value1:
    program statement
    program statement
    ...
    break;
case value2:
    program statement
    program statement
    ...
    break;
    ...
case valuen:
    program statement
    program statement
    ...
    break;
default:
    program statement
    program statement
    ...
    break;
}
```

括号内的表达式将连续与 `value1`、`value2`、……`valuen` 进行比较，这些值必须是简单的常量或常量表达式。如果找到值等于 `expression` 值的 `case`，则执行 `case` 之后的程序语句。注意，当包含多个此类程序语句时，它们不需要包含在大括号内。

`break` 语句标志着 `case` 的结束并终止 `switch` 语句的执行。记得在每个 `case` 结束包含 `break` 语句。对于某个特定的 `case` 忘记这样做会导致在该 `case` 执行时，程序执行继续到下一个 `case`。有时这是故意的；如果你选择这样做这样做，请务必插入注释以提醒他人你的意图。

如果 `expression` 的值不匹配任何 `case` 值，则会执行名为 `default` 的特殊可选 `case`。这在概念上等同于上一个示例中使用的全捕 `else`。事实上，`switch` 语句的通用形式可以等效地表示为 `if` 语句，如下：

```objc
if ( expression == value )
{
    program statement
    program statement
}
else if ( expression == value2 )
{
    program statement
    program statement
}
...
else if ( expression == valuen )
{
    program statement
    program statement
}
...
else {
    program statement
    program statement
}
```

考虑到之前的代码，你可以将程序 6.8A 中的大型 `if` 语句转换为等效的 `switch` 语句。这在程序 6.9 中所示。

## 程序 6.9
