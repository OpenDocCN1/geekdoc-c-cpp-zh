

## 第 7 章
## 其他条件和迭代语句

if/else 和 while 语句足以实现涉及条件执行和循环的算法。break 和 continue 语句虽然方便，但并非必须的。C++ 还提供了一些额外的条件和迭代语句，它们在某些情况下使用起来更加方便。这些额外的语句包括：

- switch：多分支 if/else 语句的替代方案
- 条件运算符：一种表现出 if/else 行为的表达式
- do/while：一种在执行完循环体后检查其运行的循环
- for：一种便于计数的循环

这些替代方案包含了算法中的某些部分，以便更清晰、更简洁地表达它们。本章将探索这些其他表达条件执行和迭代的语句。

## 7.1 switch 语句

switch 为多分支的 if/else 语句提供了一个方便的替代方案，如列表 5.15 (restlydigittow.cpp) 中的所示。列表 7.1 (switchdigittow.cpp) 使用了 switch 语句代替了多分支 if/else 语句。

### 列表 7.1：switchdigittow.cpp
```cpp
#include <iostream>

using namespace std;

int main() {
    int value;
    cout << "Please enter an integer in the range 0...5: ";
```

```
cin >> value;
switch (value) {
    case 0:
        cout << "zero";
        break;
    case 1:
        cout << "one";
        break;
    case 2:
        cout << "two";
        break;
    case 3:
        cout << "three";
        break;
    case 4:
        cout << "four";
        break;
    case 5:
        cout << "five";
        break;
    default:
        if (value < 0)
            cout << "Too small";
        else
            cout << "Too large";
        break;
}
cout << endl;
```

switch 的通用形式为：

```
switch ( 整数表达式 ) {
    case 整数常量 1 :
        语句序列 1
        break;
    case 整数常量 2 :
        语句序列 2
        break;
    case 整数常量 3 :
        语句序列 3
        break;
    ...
    case 整数常量 n :
        语句序列 n
        break;
    default:
        默认语句序列
}
```

在 switch 语句中：

- 留字 switch 用于标识一个 switch 语句。
- 紧跟 switch 单词的括号表达式必须求出一个整数值。任何整数类型、字符和布尔表达式都是接受的。禁止使用浮点表达式和其他非整数类型。
- switch 的体用必须的大括号括起来。
- 每个 case 单词的出现都跟着一个整数常量和一个冒号 (:)。我们将该整数常量称为 case 标签（case label）。该标签可以是字面量，也可以是 const 符号值（第 3.5 节）。特别禁止使用非 const 变量和其他表达式。

case 标签定义了代码中的一个位置；它不是一个可执行的语句。case 标签表示 switch 的执行流可以跳转的目标。

如果 case 匹配 switch 的表达式，则该标记的语句将被执行，直到遇到 break 语句为止。每个 case 标签之后的语句和 break 语句是可选的。可以为多个 case 标签执行一组语句，或者为一个或多个标签提供空语句，如下：

```
cin >> key; // 从用户获取键
switch (key) {
    case 'p':
    case 'q':
        cout << "You choose" << endl;
        break;
    case 'q':
    case 'Q':
        done = true;
        break;
}
```

在这里，用户输入大写或小写的 P，导致相同的动作——打印“You chose P”。done 布尔变量被设置为 true。如果用户既没有输入 P也没有输入 Q，则 switch 中的任何语句都不会执行。

break 语句是可选的。如果一个 case 被了标签，则随后的语句将被执行，直到遇到 break 语句。随后控制流转移到 switch 的体。通过这样，switch 内部的 break 作用相当于循环内部的 break：跳过 switch 体的剩余部分，程序执行返回到体之后的下一条语句。漏掉 break 语句是一种常见错误，当这不是刻意的，它会导致后续 case 标签的语句被执行。该过程一直持续，直到遇到 break 或到达 switch 的结束。

- 如果没有 case 标签匹配，则标记默认（default）。它相当于多分支 if/else 语句中的 else 等所有选项。default 标签是可选的。如果缺失且没有 case 标签匹配表达式，则 switch 内的任何语句都不会执行。

switch 语句有两个限制，使得它不如多分支的 if/else：

- switch 参数必须是一个整数表达式。
- case 标签必须是常量整数值。接受整数字面量和常量。不允许使用变量或表达式。

为了说明这些限制，请考虑以下 if/else 语句，它可以很容易地转换为等效的 switch 语句：

```
if (x == 1) {
    // 执行 1
} else if (x == 2) {
    // 执行 2
} else {
    // 执行 3
}
```

对应的 switch 语句是：

```
switch (x) {
    case 1:
        // 执行 1
        break;
    case 2:
        // 执行 2
        break;
    default:
        // 执行 3
        break;
}
```

## 7.2 条件运算符

作为一种纯语法上的构造，C++ 提供了一种 if/else 构造的替代方案，称为条件运算符。它的应用有限，但仍然很方便。以下代码段将两个值之一赋值给 x：

- 如果 z 不为零，则 y/z 的结果，或者
- 如果 z 为零，则为零；我们希望避免除以零的运行时错误。

```cpp
// 给 x 赋值：
if (z != 0)
    x = y/z; // 可以除法
else
    x = 0; // 赋值默认值
```

这段代码有两个赋值，但在任何给定时刻只有一个会被执行。条件运算符使得语句更加紧凑：

```cpp
// 给 x 赋值：
x = (z != 0) ? y/z : 0;
```

条件表达式的通用形式为：

![](img/e326304bd50fbc4f7d5a64c1487eb635_162_0.png)

- 条件（condition）是一个可能出现在 if 语句中的普通布尔表达式。条件周围的括号不是强制必须的，但为了提高可读性应该使用。
- 表达式 1（expression1）是条件为真时的条件表达式整体值。
- 表达式 2（expression2）是条件为假时的条件表达式整体值。

条件运算符使用了符号 ? 和 : 以及三个操作数。由于有三个操作数，它被归类为三元运算符（C++ 只有一个）。条件表达式的整体类型是 exp1 和 exp2 中占主的类型。条件表达式可以用任何可以使用表达式的地方。它不是语句；它是语句的一部分。

作为另一个例子，数学通过以下公式定义绝对值：

```
|n| = { n, 当 n >= 0; -n, 当 n < 0 }
```

也就是说，正数或零数的绝对值等于该数本身的加逆（负数）。以下 C++ 表达式表示变量 n 的绝对值：

```cpp
abs_n = (n >= 0) ? n : -n;
```

