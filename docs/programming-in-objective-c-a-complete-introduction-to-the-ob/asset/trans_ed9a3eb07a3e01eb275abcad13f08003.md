

# if 语句 109

在这里，有必要讨论一下程序的严密性问题。尽管之前的程序完成了我们设定的任务，但该程序并不是真正完整的，因为它没有考虑到用户的错误。例如，如果用户不小心输入了 `?` 作为运算符会发生什么？程序将直接跳过 `if` 语句，终端上不会显示任何消息来提醒用户其表达式输入错误。

另一个被忽略的情况是用户输入了除数为零的除法操作。你现在已经知道在 Objective-C 中永远不应该尝试除以零。程序应该检查这种情况。

尝试预测程序可能失败或产生非预期结果的方法，并采取预防措施来考虑此类情况，是编写良好、可靠程序的必要部分。对程序运行足够数量的测试用例通常指向程序没有考虑到某些情况。但在我们编写程序来询问“如果……会发生……”并插入必要的程序语句来妥善处理这种情况之前，这变成了一个自律的问题。

程序 6.8A 是程序 6.8 的修改版本，它考虑了除以零和输入未知运算符的情况。

# 程序 6.8A

```objc
// 为了评估如下形式的简单表达式
//    operator value

#import <Foundation/Foundation.h>

// 在此处插入 Calculator 类的
// 接口和实现部分

int main(int argc, char *argv[]) {
    NSAutleasePool *pool = [[NSAutleasePool alloc] init];
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
``````

# 程序 6.8A 输出

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

# switch 语句

如果 `value` 非为 0，你执行除法；否则，你显示消息并将 `accumulator` 设置为值 `NAN`。通常情况下，让方法来处理特殊情况比仅依赖使用该方法的程序员的机智要好。

# switch 语句

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

# 程序 6.9

```objc
// 程序评估如下形式的简单表达式
// value value
#import <Foundation/Foundation.h>

// 在此处插入 Calculator 类的
// 接口和实现部分

int main(int argc, char *argv[]) {
    NSAutleasePool *pool = [[NSAutleasePool alloc] init];
    double value, value2;
    char operator;
    Calculator *deskCalc = [[Calculator alloc] init];

    NSLog(@"Type in your expression.");
    scanf("%lf %c %lf", &value, &operator, &value2);

    [deskCalc setAccumulator:value];

    switch ( operator ) {
    case '+':
        [deskCalc add:value2];
        break;
    case '-':
        [deskCalc subtract:value2];
        break;
    case '*':
        [deskCalc multiply:value2];
        break;
    case '/':
        [deskCalc divide:value2];
        break;
    default:
        NSLog(@"Unknown operator.");
        break;
    }

    NSLog(@"%.2f", [deskCalc accumulator]);
    [deskCalc release];
    [pool drain];
    return 0;
}
``````

# 程序 6.9 输出

Type in your expression.
178.99 - 326.8
-147.81

在读取表达式后，`operator` 的值将与每个 `case` 指定的值连续比较。当找到匹配项时，将执行 `case` 内部的语句。`break` 语句随后将执行移出 `switch` 语句，完成程序的执行。如果没有一个 `case` 匹配 `operator` 的值，则 `default` 情况将显示“Unknown operator.”。

在前面的程序中，`default` 情况中的 `break` 实际上是不必要的，因为 `switch` 内部之后没有其他语句。然而，在每个 `case` 结束包含 `break` 是一个良好的编程习惯。

编写 `switch` 语句时，请记住两个值可以是相同的。但是，你可以将一个 `case` 值与特定的程序语句关联。这通过在要执行的公共语句之前列出多个 `case` 值（每个值之前带有关键字 `case`，值后带有冒号）来实现。例如，在接下来的 `switch` 语句中，如果 `operator` 等于星号 `*` 或小写 `x`，则执行 `multiply:` 方法：

```objc
switch ( operator )
{
```

