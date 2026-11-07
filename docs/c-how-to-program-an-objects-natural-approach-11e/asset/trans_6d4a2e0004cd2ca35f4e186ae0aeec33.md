

`continue` 语句执行时，在 `for` 语句中，先执行递增表达式，然后程序会评估循环继续测试。图 4.9 使用 `continue`（第 9 行）在嵌套的 `if` 判断出 `count` 的值为 5 时跳过第 12 行的语句。当 `continue` 语句执行时，程序控制继续转到 `for` 语句中控制变量的递增（第 7 行）。

```cpp
// fig04_09.cpp
// continue statement terminating an iteration of a for statement.
#include <iostream>
using namespace std;

int main() {
    for (int count{1}; count <= 10; ++count) { // loop 10 times
        if (count == 5) {
            continue; // skip remaining code in loop body if count is 5
        }

        cout << count << " ";
    }

    cout << "\nUsed continue to skip printing 5\n";
}
```

```text
1 2 3 4 6 7 8 9 10
Used continue to skip printing 5
```

**图 4.9** | `continue` 语句终止 `for` 语句的一次迭代。

## 软件工程与性能的权衡

有些程序员认为 `break` 和 `continue` 违反了结构化编程。由于相同的效果可以通过结构化编程技术实现，这些程序员倾向于避免使用 `break` 和 `continue`（但这会略微降低性能）。在实现高质量软件工程和实现最佳性能软件之间存在着一种张力。有时，其中一个目标的实现是以牺牲另一个目标为代价的。除去大多数对性能要求极高的情况，你应该首先让代码简单且正确，然后再让它变得快速且精简——但仅在必要时这样做。

## 检查点

- **1.** *(判断正误)* 在 `while`、`for` 或 `do...while` 语句中执行 `continue` 语句会跳过循环体中的剩余语句，并继续进行循环继续测试。**答案：** 错误。在 `while` 或 `do...while` 语句中，`continue` 会跳过循环体中的剩余语句，并继续进行循环继续测试。在 `for` 语句中，程序在评估循环继续测试之前，会先执行 `for` 的递增表达式。
- **2.** *(判断正误)* 在 `while`、`for`、`do...while` 或 `switch` 语句中执行 `break` 语句会导致立即退出该语句——程序继续执行控制语句之后的第一条语句。**答案：** 正确。

## 4.11 逻辑运算符

`if`、`if...else`、`while`、`do...while` 和 `for` 语句中的条件决定了程序的控制流如何继续。到目前为止，我们只介绍了简单的条件，例如 `count <= 10`、`number != sentinelValue` 和 `total > 1000`。你可以使用关系运算符（`<`、`>`、`>=` 和 `<=`）和相等性运算符（`==` 和 `!=`）来表达简单条件。有时控制语句需要更复杂的条件来确定程序的控制流。C++ 的逻辑运算符使你可以组合简单条件。逻辑运算符是 `&&`（逻辑与）、`||`（逻辑或）和 `!`（逻辑非）。

### 4.11.1 逻辑与（&&）运算符

2023 年，在新冠疫情三年之后，美国经历了一场导致空中交通混乱的飞行员短缺。为了缓解飞行员短缺，政府考虑将强制性飞行员退休年龄从 65 岁提高到 67 岁，这样身体健康的高级飞行员可以继续飞行两年。

假设一家航空公司想询问每位 63 岁及以上的高级飞行员，是否愿意申请继续飞行至 67 岁，而不是在 65 岁退休。航空公司可以编写一个程序来搜索其计算机化的员工记录，并确定 63 岁及以上高级飞行员的数量。该程序可以包含以下语句：

```cpp
if (employeeType == PILOT && age >= 63) {
    ++seniorPilots;
}
```

假设 `PILOT` 是一个常量。`if` 语句包含两个简单条件：

- `employeeType == PILOT` 判断员工是否为飞行员。
- `age >= 63` 判断员工是否接近退休年龄。

`if` 语句考虑组合条件，只有当两个简单条件都为真时，组合条件才为真。如果为真，`if` 语句的体会将 `seniorPilots` 增加 1；否则，程序跳过递增操作。有些程序员发现上述组合条件使用冗余的括号更易读，例如：

```cpp
if ((employeeType == PILOT) && (age >= 63)) {
    ++seniorPilots;
}
```

下面的真值表总结了 `&&` 运算符，显示了 `expression1` 和 `expression2` 的布尔值 `false` 和 `true` 的组合。C++ 会将所有包含关系运算符、相等性运算符或逻辑运算符的表达式评估为 false 或 true：

**逻辑与（&&）运算符真值表**

| expression1 | expression2 | expression1 && expression2 |
|---|---|---|
| false | false | false |
| false | true | false |
| true | false | false |
| true | true | true |

### 4.11.2 逻辑或（||）运算符

现在假设我们希望确保两个条件中的一个或两个为真，然后再选择某条执行路径。在这种情况下，我们使用 `||`（逻辑或）运算符，例如：

```cpp
if ((semesterAverage >= 90) || (finalExam >= 90)) {
    cout << "Student grade is A\n";
}
```

这条语句同样包含两个简单条件：

- `semesterAverage >= 90` 判断学生整个学期表现是否扎实，从而是否值得在该课程中获得 A。
- `finalExam >= 90` 判断学生期末考试是否表现出色，从而是否值得在该课程中获得 A。

然后 `if` 语句考虑组合条件：

```cpp
(semesterAverage >= 90) || (finalExam >= 90)
```

如果两个简单条件中的一个或两个为真，就授予学生 A。唯一不会打印 `"Student grade is A"` 的情况是两个简单条件都为假。以下是逻辑或（||）运算符的真值表：

**逻辑或（||）运算符真值表**

| expression1 | expression2 | expression1 \|\| expression2 |
|---|---|---|
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | true |

运算符 `&&` 的优先级高于运算符 `||`。两者都是从左向右结合。一般来说，如果对求值顺序存在歧义，请使用括号。

### 4.11.3 短路求值

包含 `&&` 或 `||` 运算符的表达式的各个部分仅在知道条件为真或假之前才进行求值。因此，对以下条件的求值：

```cpp
(employeeType == PILOT) && (age >= 63)
```

如果 `employeeType` 不等于 `PILOT`（即整个表达式为假），则立即停止；如果 `employeeType` 等于 `PILOT`（即如果 `age >= 63` 为真，整个表达式仍可能为真），则继续。这种短路求值是逻辑与和逻辑或表达式的性能特性。

在使用 `&&` 运算符的表达式中，一个条件（我们称之为依赖条件）可能需要另一个条件为真，这样对依赖条件的求值才有意义。在这种情况下，依赖条件应放在 `&&` 运算符之后以防止错误。考虑以下条件：

```cpp
(i != 0) && (10 / i == 2)
```

依赖条件 `(10 / i == 2)` 必须出现在 `&&` 运算符之后，以防止除以零的可能性。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_228_0.png)

### 4.11.4 逻辑非（!）运算符

`!` 逻辑非运算符（也称为逻辑 NOT 或逻辑补运算符）“反转”条件的意思。逻辑非运算符是一元运算符，只有一个条件作为操作数。要仅在条件为假时执行代码，请在原始条件前放置 `!`，例如：

```cpp
if (!(grade == sentinelValue)) {
    cout << "The next grade is " << grade << "\n";
}
```

只有在 `grade` 不等于 `sentinelValue` 时，才会执行循环体语句。条件 `grade == sentinelValue` 周围的括号是必需的，因为逻辑非运算符的优先级高于相等性运算符。

在大多数情况下，你可以通过使用适当的关系运算符或相等性运算符来表达条件，从而避免使用逻辑非。例如，使用 `!=` 运算符会使前面的语句更易读：

```cpp
if (grade != sentinelValue) {
    cout << "The next grade is " << grade << "\n";
}
```

以下是 `!` 逻辑非运算符的真值表：

**逻辑非（!）运算符真值表**

| expression | !expression |
|---|---|
| false | true |
| true | false |

### 4.11.5 示例：生成逻辑运算符真值表

图 4.10 生成了 `&&`、`||` 和 `!` 的逻辑运算符真值表（第 9–13、16–20 和 23–25 行）。输出显示了每个被求值的表达式及其布尔结果。默认情况下，`cout` 和流插入运算符将布尔值 `true` 和 `false` 显示为 1 和 0，但 `format` 函数会显示单词 `true` 或 `false`。

```cpp
// fig04_10.cpp
// Logical operators.
#include <format>
#include <iostream>
using namespace std;

int main() {
    // create truth table for && (logical AND) operator
    cout << "logical AND (&&)\n"
         << format("false && false: {}\n", false && false)
         << format("false && true: {}\n", false && true)
         << format("true && false: {}\n", true && false)
         << format("true && true: {}\n", true && true);
```

**图 4.10** | 逻辑运算符。（第 1 部分，共 2 部分。）

