
`1 2 3 4`
在 `count = 5` 时跳出循环

**图 5.13** | `break` 语句退出 `for` 语句。

# 5.10.2 continue 语句

`continue` 语句在 `for` 或 `do...while` 中执行时，会跳过循环体的剩余语句并进入循环的下次迭代。在 `while` 和 `do...while` 语句中，程序在 `continue` 语句执行后立即评估循环继续测试。对于 `for` 语句，执行增加表达式，然后评估循环继续测试。

```cpp
// // 图 5.14: ContinueTest.cpp
// // continue 语句终止 for 语句
// #include <iostream>
// using namespace std;
main() {
    unsigned int count; // 循环后的控制变量
    for (int count = 1; count <= 10; count++) { // 循环 10 次
        if (count == 5)
            continue; // 如果 count 为 5 则跳过循环
        cout << count << " ";
    }
}
```
`1 2 3 4 5 6 7 8 9 10`
`1 2 3 4 6 7 8 9 10`

**图 5.14** | `continue` 语句终止 `for` 语句。

# 第 5 章 控制语句：部分 2：逻辑运算符

| 1 2 3 4 5 6 7 8 9 10 |
| :--- |
| 使用 `continue` 打印 5 |

| 图 5.14 | `continue` 语句终止 `for` 语句。（部分 2）。 |

当 `for`（9–15 行）中的 10-12 行 `if` 语句检测到 `count` 为 5 时，第 11 行的 `break` 语句执行。这终止了语句，程序继续到第 17 行（语句之后），显示循环结束时控制变量的值。循环执行了 4 次而不是 10 次。

`switch` 的最后一个 `case`（或可选的 `default` 情况）不需要 `break` 语句，因为执行将继续进行 `switch` 之后的语句。

> 错误预防提示 5.8
> 在 `switch` 语句中提供一个 `default` 情况。这能让你关注处理异常情况的需要。

> 良好编程实践 5.3
> 虽然 `switch` 中的每个 `case` 和 `default` 情况可以按任何顺序出现，但请将 `default` 情况放在最后。当列出 `default` 情况时，该情况不需要 `break` 语句。

关于 `switch` 中每个 `case` 表达式的说明
当使用 `switch` 语句时，记住每个 `case` 必须包含一个常量表达式——任何求值为常量整数值的常量组合（例如，`-7` 或 `221`）。整数是一个简单的整数值。此外，你还可以使用字符常量——单引号中的特定字符，例如 `'A'`、`'7'` 或 `'S'`，它们代表字符的整数值和枚举常量（在第 6 节引入）（附录 B 显示了 ASCII 字符集中字符的整数值，它是 Unicode 字符子集）。
每个 `case` 中的表达式也可以是常量变量——一个在整个程序运行期间值不改变的变量。这种变量使用关键字声明（在第 6 章讨论）。
在第 12 章“面向对象编程：多态”中，我们将介绍一种更优雅的实现 `switch` 逻辑的方法——我们使用名为多态的技术来创建通常比 `switch` 逻辑更清晰、更容易维护且扩展到其他使用 `switch` 逻辑程序的程序。

# 5.10 break 和 continue 语句

在选择和迭代语句中，C++ 提供了 `break`（我们在 `switch` 语句的背景下讨论过）和 `continue` 来改变控制流。前节展示了如何使用 `break` 终止 `switch` 语句的执行。本节讨论了如何在迭代语句中使用 `break`。

## 5.10.1 break 语句

`break` 在 `while`、`for`、`do ...while` 或 `switch` 中执行，会导致立即离开该语句——执行将继续从控制语句后的第一条语句。`break` 的常见用途是跳出循环或跳过 `switch` 的剩余部分（如图 5.11 所示）。图 5.13 展示了 `break` 语句退出 `for` 循环。
当 `for`（9–15 行）中的 10-12 行 `if` 语句检测到 `count` 为 5 时，第 11 行的 `break` 语句执行。这终止了语句，程序继续到第 17 行（语句之后），显示循环结束时控制变量的值。循环执行了 4 次而不是 10 次。

## 5.10 break 和 continue 语句

```cpp
// // 图 5.13: BreakTest.cpp
// // break 语句退出 for 语句
// #include <iostream>
// using namespace std;
main() {
    unsigned int count; // 循环后的控制变量
    for (int count = 1; count < 10; count++) { // 循环 10 次
        if (count == 5) 
            break; // 如果 count 为 5 则终止循环
        cout << count << " ";
    }
}
```
`1 2 3 4`
在 `count = 5` 时跳出循环

**图 5.13** | `break` 语句退出 `for` 语句。

## 5.10.2 continue 语句

`continue` 语句在 `for` 或 `do...while` 中执行时，会跳过循环体的剩余语句并进入循环的下次迭代。在 `while` 和 `do...while` 语句中，程序在 `continue` 语句执行后立即评估循环继续测试。对于 `for` 语句，执行增加表达式，然后评估循环继续测试。

```cpp
// // 图 5.14: ContinueTest.cpp
// // continue 语句终止 for 语句
// #include <iostream>
// using namespace std;
main() {
    unsigned int count; // 循环后的控制变量
    for (int count = 1; count <= 10; count++) { // 循环 10 次
        if (count == 5)
            continue; // 如果 count 为 5 则跳过循环
        }
        cout << count << " ";
    }
}
```
`1 2 3 4 5 6 7 8 9 10`
`1 2 3 4 6 7 8 9 10`

**图 5.14** | `continue` 语句终止 `for` 语句。

# 第 5 章 控制语句：部分 2：逻辑运算符

| 1 2 3 4 5 6 7 8 9 10 |
| :--- |
| 使用 `continue` 打印 5 |

| 图 5.14 | `continue` 语句终止 `for` 语句。（部分 2）。 |

当 `for`（9–15 行）中的 10-12 行 `if` 语句检测到 `count` 为 5 时，第 11 行的 `break` 语句执行。这终止了语句，程序继续到第 17 行（语句之后），显示循环结束时控制变量的值。循环执行了 4 次而不是 10 次。

`switch` 的最后一个 `case`（或可选的 `default` 情况）不需要 `break` 语句，因为执行将继续进行 `switch` 之后的语句。

> 错误预防提示 5.8
> 在 `switch` 语句中提供一个 `default` 情况。这能让你关注处理异常情况的需要。

> 良好编程实践 5.3
> 虽然 `switch` 中的每个 `case` 和 `default` 情况可以按任何顺序出现，但请将 `default` 情况放在最后。当列出 `default` 情况时，该情况不需要 `break` 语句。

关于 `switch` 中每个 `case` 表达式的说明
当使用 `switch` 语句时，记住每个 `case` 必须包含一个常 表达式——任何求值为常量整数值的常量组合（例如，`-7` 或 `221`）。整数是一个简单的整数值。此外，你还可以使用字符常量——单引号中的特定字符，例如 `'A'`、`'7'` 或 `'S'`，它们代表字符的整数值和枚举常量（在第 6 节引入）（附录 B 显示了 ASCII 字符集中字符的整数值，它是 Unicode 字符子集）。
每个 `case` 中的表达式也可以是常量变量——一个在整个程序运行期间值不改变的变量。这种变量使用关键字声明（在第 6 章讨论）。
在第 12 章“面向对象编程：多态”中，我们将介绍一种更优雅的实现 `switch` 逻辑的方法——我们使用名为多态的技术来创建通常比 `switch` 逻辑更清晰、更容易维护且扩展到其他使用 `switch` 逻辑程序的程序。

## 5.11.1 逻辑与 (&&) 运算符

假设我们想在程序的某处确保两个条件都真，然后选择特定的执行路径。在这种情况下，我们可以使用 `&&`（逻辑与）运算符，如下所示：

```cpp
if (gender == FEMALE && age >= 65) {
    ++seniorEmployees;
}
```

## 5.11 逻辑运算符

该语句包含两个简单条件。条件 `gender == FEMALE` 比较性别，而 `age >= 65` 可能会被评估以判断一个人是否为老年人。`if` 语句考虑了组合条件

```
gender == FEMALE && age >= 65
```

只有当两个简单条件都为真时，结果为真。在这种情况下，`if` 语句会将 `seniorFemales` 加 1。如果其中一个或两个简单条件为假，程序将跳过加操作。添加冗余的括号会让前面的条件更具可读性，例如：

```
gender == FEMALE && (age >= 65)
```

5.15 中的表格总结了 `&&` 运算符。该表显示了 `expression1` 和 `expression2` 对于布尔值 `false` 和 `true` 的所有可能组合。此类表格被称为真表。C++ 将所有包含关系运算符、等等运算符或逻辑运算符的表达式评估为零（假）或非零（真）。

| expression1 | expression2 | expression1 && expression2 |
|---|---|---|
| false | false | false |
| false | true | false |
| true | false | false |
| true | true | true |

> 图 5.15 `&&`（逻辑与）运算符真表。

### 5.11.2 逻辑或 (||) 运算符

现在我们希望在选择执行路径之前，确保两个条件中至少有一个或都为真。在这种情况下，我们使用（逻辑或）运算符，如下程序段：

```cpp
if ((semesterAverage >= 90) || (finalExam >= 90)) {
  cout << "Student grade is A\n";
}
```

该语句也包含两个简单条件。条件 `semesterAverage >= 90` 评估学生在整个学期的表现是否值得获得 A。条件 `finalExam >= 90` 评估判断学生在期末考试中表现优异是否值得获得 A。`if` 语句考虑了组合条件

```
(semesterAverage >= 90) || (finalExam >= 90)
```

如果两个简单条件中的任一个或都为真，则授予学生一个“A”。只有当两个简单条件都为假时，才不打印消息 "Student grade is A"。False 是逻辑运算符 OR (`||`) 的真表。运算符 `&&` 的优先级高于 `||`。两个运算符都从左到右结合。

## 第 5 章 控制语句：第 2 部分：逻辑运算符

| expression1 | expression2 | expression1 || expression2 |
|---|---|---|
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | true |

图 5.16 `||`（逻辑或）运算符真表。

### 5.11.3 短路求值

包含 `&&` 或 `||` 运算符的表达式部分仅评估到已知条件为或假为止。然后，表达式的评估

```
gender == FEMALE && (age >= 65)
```

如果 `gender` 不等于 `FEMALE`（即整个表达式为假），则立即停止；如果 `gender` 等于 `FEMALE`（即如果条件 `age >= 65` 为真，整个表达式可能为真），则继续。逻辑与与或表达式的这种特性是短路求值。

## 常见编程错误 5.8

在使用运算符 `&&` 时，一个条件——我们称之为依赖条件——可能需要另一个条件为真，以便该依赖条件的评估才有意义。在这种情况下，依赖条件应该放在 `&&` 之后以防止错误。条件 `(i == 0) && (10 / i == 2)` 必须出现在 `&&` 运算符之后，以防止除以零的可能性。

### 5.11.4 逻辑否定 (!) 运算符

`!`（逻辑否定），也称为逻辑非或逻辑补运算符，会“反转”条件的含义。与结合两个条件的二元运算符 `&&` 和 `||` 不同，逻辑否定运算符是一个只有一个操作数的一元运算符。要对一个条件取否定，请将逻辑否定运算符放在原始代码之前，如程序段所示：

```cpp
if (!(grade == sentinelValue)) {
    cout << "The next grade is " << grade << "\n";
}
```

只有当 `grade` 不等于 `sentinelValue` 时才执行体体。条件 `grade == sentinelValue` 周的括号是必要的，因为逻辑否定运算符的优先级高于相等运算符。

在大多数情况下，你可以通过使用适当的关系或相等运算符不同的方式表达条件来避免逻辑否定。例如，之前的语句可以写为：

```cpp
if (grade != sentinelValue) {
    cout << "The next grade is " << grade << "\n";
}
```

### 5.11 逻辑运算符

这种灵活性可以帮助你以更方便的方式表达条件。图 5.17 是逻辑否定运算符的真表。

| expression | !expression |
|---|---|
| false | true |
| true | false |

图 5.17 | `!`（逻辑否定）运算符表。

### 5.11.5 逻辑运算符示例

5.18 使用逻辑运算符来生成本节讨论的真表。输出显示了每个被评估的表达式及其布尔结果。默认情况下，布尔值 `true` 和 `false` 被 `cout` 和流插入分别显示为 1 和 0。我们在第 8 行使用流操纵符 `boolalpha`（一种粘性操作符）来指定每个布尔表达式的值应显示为单词 "true" 或 "false"。第 8–12 行产生 & 的真表。第 15–19 行产生 | 的真表。

```cpp
// Fig. 5.18: LogicalOperators.cpp
// 逻辑运算符.
#include <iostream>
using namespace std;
int main() {
    // create truth table for && (logical AND)
    cout << boolalpha << "LOGICAL AND (&&)";
    cout << "\nfalse && false: " << (false && false);
    cout << "\nfalse && true: " << (false && true);
    cout << "\ntrue && false: " << (true && false);
    cout << "\ntrue && true: " << (true && true) << "\n\n";
    // create truth table for | (logical OR)
    cout << "Logical OR (|)";
    cout << "\nfalse | false: " << (false | false);
    cout << "\nfalse | true: " << (false | true);
    cout << "\ntrue | false: " << (true | false);
    cout << "\ntrue | true: " << (true | true) << "\n";
    // create truth table for ! (logical negation)
    cout << "Logical negation (!)";
    cout << "\nfalse: " << (!false);
    cout << "\ntrue: " << (!true) << endl;
}
```

# 234 第 5 章 控制语句：第 2 部分；逻辑运算符

而是编写

```cpp
x == 1;
```
