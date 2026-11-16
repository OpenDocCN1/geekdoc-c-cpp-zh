

## 图 5.1 if 流程图

![](img/e84ad11adb18201d71595b31ce6c9eff_101_0.png)

- 布尔表达式条件决定是否执行主体。布尔表达式必须像所示那样用括号括起来。

- 语句是在布尔表达式为真时要执行的语句。该语句构成了 if 语句的主体。第 5.4 节展示了主体如何由多个语句组成。

良好的编码风格要求我们应该缩进主体以强调可选执行并提高程序的可读性。编译器不要求缩进。有时程序员会将单语句主体放在 if 同一行；例如，以下 if 语句可选地给 y 赋值：

```cpp
if (x < 10)
    y = x;
```

并可以写成

```cpp
if (x < 10) y = x;
```

但不应写成

```cpp
if (x < 10)
    y = x;
```

因为缺少缩进隐藏了程序可选地执行赋值语句这一事实。编译器会接受它，但对于习惯于缩进惯例的人类读者来说，这具有误导性。当然，编译器会接受写成如下形式的代码

```cpp
if (x<10) y=x;
```

但缺少空格使得人类难以阅读。

![](img/e84ad11adb18201d71595b31ce6c9eff_102_0.png)

当 if 语句以首选方式（使用两行源代码）编写时，重要的是不要在第一行末尾放置分号：

```cpp
if (x < 10); // No! Don't do this!
    y = x;
```

在这里，分号终止了 if 语句，但缩进暗示第二行意图作为 if 语句的主体。然而，编译器将格式不良的 if 语句解释为如果写成如下形式：

```cpp
if (x < 10)
    ; // This is what is really going on.
    y = x;
```

在 C++ 中这是合法的；它意味着 if 语句有一个空主体。在这种情况下，赋值不是主体的一部分。赋值语句在主体之后，并且无论布尔表达式的真值如何，都将始终执行。

在检查相等性时，如
if (x == 10)
std::cout << "ten";
请务必使用关系相等运算符 (==)，而不是赋值运算符 (=)。由于赋值语句有一个值（被赋的值，见第 4.3 节），C++ 允许在条件表达式中使用 =。然而，初学者在这种上下文中使用 = 几乎总是一个错误。Visual C++ 在警告级别 4 下检查条件表达式中赋值的使用；默认级别 3 不会。

## 5.4 复合语句

有时你需要根据特定条件可选地执行多个语句。清单 5.4 (alternatedivision.cpp) 展示了你必须如何使用花括号将多个语句分组为一个复合语句。

### 清单 5.4: alternatedivision.cpp

```cpp
#include <iostream>
int main() {
  int dividend, divisor, quotient;
  // Get two integers from the user
  std::cout << "Please enter two integers to divide:";
  std::cin >> dividend >> divisor;
  // If possible, divide them and report the result
  if (divisor != 0) {
    quotient = dividend / divisor;
    std::cout << dividend << " divided by " << divisor << " is "
              << quotient << '\n';
  }
}
```

赋值语句和打印语句都是 if 语句主体的一部分。给定特定程序运行期间布尔表达式 divisor != 0 的真值，要么两个语句都将执行，要么两个语句都不会执行。

复合语句由零个或多个语句组成，并用花括号分组。我们说花括号定义了一组语句块。作为一种风格，许多程序员总是使用花括号来界定 if 语句的主体，即使主体只包含一个语句。

```cpp
if (x < 10) {
  y = x;
}
```

他们这样做是因为如果以后向主体添加更多语句且程序员忘记添加所需的花括号，很容易引入逻辑错误。

以下代码的格式

```cpp
if (x < 10)
    y = x;
    z = x + 5;
```

暗示两个赋值都是 if 语句主体的一部分。由于构成主体的多个语句必须位于花括号内的复合语句中，编译器将代码片段解释为如果写成如下形式

![](img/e84ad11adb18201d71595b31ce6c9eff_104_0.png)

```cpp
if (x < 10)
    y = x;
    z = y + 5;
```

这样的代码将可选地执行第一个赋值语句，并 *始终* 执行第二个赋值语句。

程序员可能本意是将其写成

```cpp
if (x < 10) {
    y = x;
    z = x + 5;
}
```

如果主体由单个语句组成，则花括号是可选的。如果主体只包含一个语句且未使用花括号，那么终止主体中语句的分号也终止 if 语句。如果使用花括号来界定主体，则不需要在主体的右花括号后加分号。

一对空花括号表示一个空块。空块是一个有效的复合语句。

## 5.5 if/else 语句

清单 5.3 (betterdivision.cpp) 的一个不良方面是，如果用户输入零除数，程序不打印任何内容。最好向用户提供一些反馈，以指示提供的除数无法使用。if 语句有一个可选的 else 子句，仅在布尔表达式为假时执行。清单 5.5 (betterfeedback.cpp) 使用 if/else 语句来提供所需的效果。

### 清单 5.5: betterfeedback.cpp

```cpp
#include <iostream>

int main() {
    int dividend, divisor;

    // Get two integers from the user
    std::cout << "Please enter two integers to divide:";
    std::cin >> dividend >> divisor;

    // If possible, divide them and report the result
```

## 图 5.2 if/else 流程图

![](img/e84ad11adb18201d71595b31ce6c9eff_105_0.png)

```cpp
if (divisor != 0)
    std::cout << dividend << "/" << divisor << " = "
              << dividend/divisor << '\n';
else
    std::cout << "Division by zero is not allowed\n";
}
```

给定的程序运行将恰好执行 `if` 主体或 `else` 主体中的一个。与清单 5.3 (betterdivision.cpp) 不同，始终会显示一条消息。

```
Please enter two integers to divide: 32 0
Division by zero is not allowed
```

`else` 子句包含一个替代主体，如果条件为假则执行该主体。程序的执行流程如图 5.2 所示。

清单 5.5 (betterfeedback.cpp) 避免了导致程序过早终止的除以零运行时错误，但它仍然提醒用户存在问题。另一个应用程序可能以不同的方式处理这种情况；例如，它可能用某个默认值替代 `divisor`，而不是零。

if/else 语句的一般形式是

![](img/e84ad11adb18201d71595b31ce6c9eff_106_0.png)

- 保留字 if 开始 if/else 语句。
- 条件是一个布尔表达式，用于确定运行中的程序将执行语句 1 还是语句 2。与简单的 if 语句一样，条件必须出现在括号内。
- 如果条件为真，程序执行语句 1。为了使 if/else 语句更具可读性，请将语句 1 的缩进比 if 行多一些空格。if 语句的这一部分有时称为 if 的主体。
- 保留字 else 开始 if/else 语句的第二部分。
- 如果条件为假，程序执行语句 2。为了使 if/else 语句更具可读性，请将语句 2 的缩进比 else 行多一些空格。if/else 语句的这一部分有时称为 else 的主体。

if/else 语句中 else 子句的主体可以是复合语句：

```cpp
if (x == y)
    std::cout << x;
else {
    x = 0;
    std::cout << y;
}
```

或者仅 if 主体可以是复合语句：

```cpp
if (x == y) {
    std::cout << x;
    x = 0;
}
else
    std::cout << y;
```

或者两部分都可以是复合语句：

```cpp
if (x == y) {
    std::cout << x;
    x = 0;
}
```

