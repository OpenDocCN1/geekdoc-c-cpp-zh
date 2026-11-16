

```
switch (integral expression) {
    case integral constant 1:
        statement sequence 1
        break;
    case integral constant 2:
        statement sequence 2
        break;
    case integral constant 3:
        statement sequence 3
        break;
    ...
    case integral constant n:
        statement sequence n
        break;
    default:
        default statement sequence
}
```

在 switch 语句中

- 保留字 switch 标识一个 switch 语句。
- 紧跟在 switch 关键字后的带括号表达式必须求值为整型值。任何整数类型、字符和布尔表达式均可接受。浮点表达式和其他非整型类型均被禁止。
- `switch` 的主体由必需的花括号括起来。
- 每个 `case` 关键字后面都跟着一个整型 `constant` 和一个冒号 (:)。我们将这个整型常量称为 `case label`。该标签可以是字面量值或 `const` 符号值（参见第 3.6 节）。特别是，非 `const` 变量和其他表达式明确被禁止。

case label 在代码中定义一个位置；它不是可执行语句。case label 表示程序执行流可以跳转到的目标。

如果 `case` 标签与 `switch` 的表达式匹配，则执行该标签后面的语句，直到遇到 `break` 语句为止。每个 `case` 标签后面的语句和 `break` 语句都是可选的。为多个 `case` 标签执行同一组语句的一种方法是为一个或多个标签提供空语句，如下所示：

```
std::cin >> key; // get key from user
switch (key) {
  case 'p':
  case 'P':
    std::cout << "You chose \"P\"\n";
    break;
  case 'q':
  case 'Q':
    done = true;
    break;
}
```

这里，大写或小写的 `P` 都会导致相同的操作——将打印 `You chose P`。如果用户输入大写或小写的 `Q`，则 `done` 布尔变量被设置为 true。如果用户既不输入 `P` 也不输入 `Q`，则 `switch` 中的任何语句都不会执行。

`break` 语句是可选的。当匹配 `case` 标签时，后面的语句会执行，直到遇到 `break` 语句。然后控制流转移出 `switch` 的主体。这样，`switch` 中的 `break` 就像循环中的 `break` 一样工作：跳过语句主体的其余部分，程序执行在主体之后的下一条语句处恢复。缺少 `break` 语句是一个常见错误，当其遗漏不是故意时，会导致执行后续 `case` 标签的语句。该过程持续到遇到 `break` 或到达 `switch` 主体末尾。

- 如果没有任何 `case` 标签匹配，则匹配 `default` 标签。它像多路 `if/else` 语句中的最终 `else` 一样，作为一个兜底选项。`default` 标签是可选的。如果缺少它且没有任何 `case` 标签与表达式匹配，则 `switch` 主体内的任何语句都不会执行。

`switch` 语句有两个限制，使其不如多路 `if/else` 通用：

- `switch` 的参数必须是整型表达式。
- case 标签必须是常量整型值。整型字面量和常量是可接受的。变量或表达式 **不** 允许。

为了说明这些限制，请考虑以下可以轻松翻译为等效 `switch` 语句的 `if/else` 语句：

```
if (x == 1) {
    // Do 1 stuff here . . .
}
else if (x == 2) {
    // Do 2 stuff here . . .
}
else if (x == 3) {
    // Do 3 stuff here . . .
}
```

对应的 switch 语句是：

```
switch (x) {
case 1:
    // Do 1 stuff here . . .
    break;
case 2:
    // Do 2 stuff here . . .
    break;
case 3:
    // Do 3 stuff here . . .
    break;
}
```

现在考虑以下 if/else：

```
if (x == y) {
    // Do "y" stuff here . . .
}
else if (x > 2) {
    // Do "> 2" stuff here . . .
}
else if (z == 3) {
    // Do 3 stuff here . . .
}
```

这段代码无法轻松翻译为 switch 语句。变量 y 不能用作 case 标签。第二个选择检查的是不等式而不是精确匹配，因此直接翻译为 case 标签是不可能的。在最后一个条件中，检查的是不同的变量 z 而不是 x。switch 语句的控制流由单个值（例如 x 的值）决定，但多路 if/else 语句不受此限制。

在适用的情况下，switch 语句允许程序员紧凑地表达多路选择逻辑。大多数程序员发现 switch 语句比等效的多路 if/else 结构更易读。

switch 语句限制的一个积极后果是，它允许编译器为 switch 生成比等效 if/else 更高效的代码。如果必须从多个选项中做出选择，并且可以使用 switch 语句，那么 switch 语句可能比相应的多路 if/else 更快。

## 7.2 条件运算符

作为纯粹的语法便利，C++ 提供了一种称为条件运算符的 if/else 结构替代方案。它应用有限，但仍然方便。以下代码片段将两个值之一赋给 x：

- y/z 的结果，如果 z 非零，或
- 零，如果 z 为零；我们希望避免除以零的运行时错误。

```
// Assign a value to x:
if (z != 0)
    x = y/z; // Division is possible
else
    x = 0;   // Assign a default value instead
```

这段代码有两个赋值语句，但任何给定时间只执行一个。条件运算符可以形成更紧凑的语句：

```
// Assign a value to x:
x = (z != 0) ? y/z : 0;
```

条件表达式的一般形式是：

![](img/e84ad11adb18201d71595b31ce6c9eff_175_0.png)

- condition 是一个可能出现在 if 语句中的普通布尔表达式。条件周围的括号不是必需的，但应使用以提高可读性。
- expression 1 是条件表达式的总体值，如果 condition 为 true。
- expression 2 是条件表达式的总体值，如果 condition 为 false。

条件运算符使用两个符号 (? 和 :) 和三个操作数。由于它有三个操作数，它被归类为三元运算符（C++ 中唯一的一个）。条件表达式的总体类型是 exp1 和 exp2 中更占优势的那个。条件表达式可以在任何可以使用表达式的地方使用。它本身不是语句；它用于语句中。

作为另一个示例，数字的绝对值在数学中由以下公式定义：

|n| = \begin{cases} n, & \text{when } n \ge 0 \\ -n, & \text{when } n < 0 \end{cases}

换句话说，正数或零的绝对值与该数字相同；负数的绝对值是该数字的加法逆元（负值）。以下 C++ 表达式表示变量 n 的绝对值：

```
(n < 0) ? -n : n
```

有人认为条件运算符晦涩难懂，因此其使用会降低程序的可读性。对资深 C++ 程序员来说，它相当容易理解，但由于其非常特定的性质，使用得比较少。

## 7.3 do/while 语句

执行中的程序在执行主体中的任何语句之前检查 while 语句（第 6.1 节）的条件；因此，我们说 `while` 循环是一个 *top-checking* 循环。有时，先检查条件再执行主体的顺序不方便；例如，请考虑清单 7.2 (goodinputonly.cpp)。

清单 7.2: goodinputonly.cpp

```cpp
#include <iostream>

int main() {
  int in_value = -1;
  std::cout << "Please enter an integer in the range 0-10 ";
  // Insist on values in the range 0...10
  while (in_value < 0 || in_value > 10)
    std::cin >> in_value;
  // in_value at this point is guaranteed to be within range
  std::cout << "Legal value entered was " << in_value << '\n';
}
```

清单 7.2 (goodinputonly.cpp) 中的循环会将用户困在 `while` 中，直到用户提供所需范围内的数字。其工作原理如下：

- `while` 的条件指定了一个包含所有 *不* 在所需范围内的值的集合。将 `in_value` 初始化为 -1 可确保 `while` 的条件最初为 true，因此程序总是至少执行一次循环主体。
- 程序执行进入循环之前，用户没有机会输入值。
- 用户逃离循环的唯一方法是输入违反条件的值——即所需范围内的值。

在循环检查之前初始化 `in_value` 有些人为。它仅用于确保进入循环主体。在用户有机会输入值之前检查有效值似乎不自然。在主体执行至少一次后才检查条件的循环会更合适。`do/while` 语句是一个 *bottom-checking* 循环，其行为正是这样。清单 7.3 (betterinputonly.cpp) 使用 do/while 语句来检查有效输入。

清单 7.3: betterinputonly.cpp

```cpp
#include <iostream>

int main() {
  int in_value;
  std::cout << "Please enter an integer in the range 0-10 ";
```

