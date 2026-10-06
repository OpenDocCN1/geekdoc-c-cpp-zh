

```c
break;
}
```

括号内的表达式值将依次与值 `value1`、`value2` 直 `valueen` 进行比较，这些值必须是简单的常量或常量表达式。如果找到与表达式值相等的 `case`，则执行该 `case` 之后的程序语句。注意，当包含多个程序语句时，它们不需要包含在大括号内。

`break` 语句表示特定 `case` 的结束，并终止 `switch` 语句的执行。请记住在每个 `case` 结尾包含 `break` 语句。如果对某个 `case` 忘记这样做，每当该 `case` 执行时，程序执行将继续进入下一个 `case`。有时这样做是有意意的；如果你选择这样做，请务必插入注释以提醒他人你的意图。

如果表达式的值不匹配任何 `case` 值，则执行名为 `default` 的特殊情况。这在概念上等同于上一个示例中使用的全捕 `else`。事实上，`switch` 语句的通用形式可以等价地表示为 `if switch` 语句，如下：

```c
if ( expression == value1 )
{
    program statement
    program statement
    ...
}
else if ( expression == value2 )
{
    program statement
    program statement
    ...
}
else if ( expression == valuen )
{
    program statement
    program statement
    ...
}
else
{
    program statement
    program statement
    ...
}
```

考虑到前面的代码，你可以将程序 6.8A 中的大型 `if` 语句转换为等效的 `switch` 语句。这在程序 6.9 中所示。

## 程序 6.9

```objc
// 用于求值形式为
//    value operator value 的简单表达式程序

#import <Foundation/Foundation.h>

// 在此处插入 Calculator 类的
// 接口和实现部分

int main (int argc, char * argv[])
{
    @autoreleasepool {
        double value1, value2;
        char operator;
        Calculator *deskCalc = [[Calculator
alloc]; init];

        NSLog("Type in your expression.");
        scanf("%lf %c %lf", &value1, &operator,
&value2);

        [deskCalc setAccumulator: value1];

        switch ( operator ) {
        case '+':
            [deskCalc add: value2];
            break;
        case '-':
            [deskCalc subtract: value2];
            break;
        case '*':
            [deskCalc multiply: value2];
            break;
        case '/':
            [deskCalc divide: value2];
            break;
        default:
            NSLog("Unknown operator.");
            break;
        }

        NSLog("%.2f", [deskCalc accumulator]);

        return 0;
    }
}
```

## 程序 6.9. 输出

Type in your expression.
178.99 - 326.8
-147.81

在读取表达式后，`operator` 的值将依次与每个 `case` 指定的值进行比较。当找到匹配时，执行包含在 `case` 内部的语句。`break` 语句将执行传出 `switch` 语句，完成程序的执行。如果没有一个 `case` 匹配 `operator` 的值，则执行显示 "Unknown operator." 的 `default` 情况。

在前面的程序中，`default` 情况中的 `break` 语句实际上是不必要的，因为在 `switch` 内部该情况之后没有语句。尽管如此，记住在每个 `case` 结尾包含 `break` 是一个良好的编程习惯。

编写 `switch` 语句时，请记住没有两个 `case` 值是可以相同的。然而，你可以将多个 `case` 值与一组特定的程序语句相关。这只需要在要执行的公共语句之前列出多个 `case` 值（在值之前使用 `case` 关键字，并在每个 `case` 之后加冒号）。例如，在下面的 `switch` 语句中，如果 `operator` 等于星号或小字母 `x`，则执行 `multiply:` 方法：

```objc
switch ( operator )
{
    ...
    case '*':
    case 'x':
        [deskCalc multiply: value2];
        break;
    ```

## 布尔变量

几乎每个学习编程的人很快都会面临编写一个生成素数表的任务。复习一下，如果一个正整数 `p` 不能被 1 以外的任何整数整除，则它是一个素数，第一个素数定义为 2。下一个素数是 3，因为它不能被 1 和 3 以外的任何整数整除；4 不是素数，因为它被 2 整除。

你可以采取多种方法来生成 50 以内的素数表，例如，生成此类表的最直接且最简单的算法只需测试每个整数 `p` 是否能被 2 到 `p-1` 的所有整数整除。如果任何这样的整数能整除 `p`，那么 `p` 就不是素数；否则它就是素数。

程序 6.10 生成从 2 到 50 的素数列表。

## 程序 6.10

```objc
// 生成素数表的程序

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int p, d, isPrime;
        for ( p = 2; p <= 50; p++) {
            isPrime = 1;
            for ( d = 2; d < p; d++) {
                if ( p % d == 0 ) {
                    isPrime = 0;
                    break;
                }
            }
            if ( isPrime ) {
                NSLog("%d", p);
            }
        }
        return 0;
    }
}
```

## 程序 6.10. 输出

2
3
5
7
11
13
17
19
23
29
31
37
41
43
47

