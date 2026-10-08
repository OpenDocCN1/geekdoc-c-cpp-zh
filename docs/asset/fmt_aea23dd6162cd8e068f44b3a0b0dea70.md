
如果 `hours` 的值大于 `40.0`，则 `wages` 包含加班费。假设 `hours` 为 50。第 1 行 `if` 语句中的表达式求值为 `true`，因此执行第 2 行的语句。相反，如果 `hours` 为 30 或任何小于或等于 `40` 的数字，第 1 行 `if` 语句中的表达式求值为 `false`。在这种情况下，程序跳过第 2 行的语句并执行第 4 行的语句——即执行保留字 `else` 之后的语句。

Copyright 2018 Cengage Learning. 版权所有。未经许可，全部或部分不得扫描或复制。WCN 02-200-203

以下程序确定员工的周薪。如果工作时间超过 40 小时，工资将包含加班费。

```
//程序：周薪

#include <iostream>

#include <iomanip>

using namespace std;

int main() {

    double wages, rate, hours;

    cout << fixed << setprecision(2);

    cout << "Line 8: Enter working hours and rate: " << endl;

    cin >> hours >> rate;

    if (hours > 40.0)

        wages = 40.0 * rate + 1.5 * rate * (hours - 40.0);

    else

        wages = hours * rate;

    cout << "Line 15: The wages are $" << wages << endl;

    return 0;

}
```

**示例运行：** 在此示例中，用户输入用阴影表示。

Line 8: Enter working hours and rate: 50.00 12.50
Line 15: The wages are $687.50

第 6 行的语句声明了程序使用的变量。第 7 行的语句将浮点数设置为小数格式的值，带有小数点和尾随零。第 8 行的语句提示用户输入工作小时和速率。第 9 行的语句将这些值分别输入到变量 `hours` 和 `rate` 中。第 10 行的语句检查工资是否大于 40.0。如果 `hours` 大于 40.0，则通过第 11 行的语句计算工资，包含加班费。否则，工资通过第 13 行的语句计算。

在二路选择语句中，在 `expression` 之后、`statement1` 之前放置分号会导致语法错误。如果 `if` 语句以分号结束，`statement1` 将不再是 `if` 语句的一部分，且 `if`...`else` 语句的 `else` 部分将独立存在。C++ 中没有独立的 `else` 语句。也就是说，它不能与 `if` 语句分离。

# 示例 4-8

以下语句显示了一个语法错误示例：

```
if (hours > 40.0);                   //Line 1
    wages = 40.0 * rate +
        1.5 * rate * (hours - 40.0);       //Line 2
else
    wages = hours * rate;               //Line 3
```

第 1 行 `if` 语句末尾的分号结束了 `if` 语句，并将第 2 行的语句与 `if` 分离。也就是说，`else` 是独立存在的。由于 C++ 中没有独立的 `else` 语句，此代码产生语法错误。如示例 4-5 所示，在单路选择中，`if` 语句末尾的分号是一个逻辑错误，而在二路选择示例中，它是语法错误。

让我们考虑另一个 `if` 语句的示例并检查可能发生的语义错误。

# 示例 4-9

考虑以下语句：

```
if (score >= 60)                   //Line 1
    cout << "Passing" << endl;          //Line 2
    cout << "Failure" << endl;            //Line 3
```

表达式 `(score >= 60)` 求值为假，第 2 行的输出语句不执行。输出结果将是 Failure。也就是说，这组语句的操作与第 3 行的 `if`...`else` 语句相同，而不是第 2 行。例如，如果 `score` 的值为 50，这些语句将输出以下行：

Failing

然而，如果表达式 `(score >= 60)` 求值为真，程序将执行两个输出语句，导致一个非常不理想的结果。例如，如果 `score` 的值为 70，这些语句将输出以下行：

Passing

Failing

`if` 语句只控制第 2 行语句的执行。第 3 行的语句始终执行。

![](img/d998292a174f7bfd8a26bfbada3d454e_246_0.png)

198 | 第 4 章：控制结构 I 选择

现在逻辑（布尔）表达式 `(score >= 60)` 求值为真或假。我们使用了不同的 `score` 值，一个逻辑表达式求值为真，另一个求值为假。这是一个彻底测试代码的示例。

根据 `score` 的值打印 Passing 或 Failing 的正确代码是：

```
if (score >= 60)
    cout << "Passing" << endl;
else
    cout << "Failing" << endl;
```

# 数据类型和逻辑（布尔）表达式

早期版本的 C++ 没有提供具有逻辑（布尔）真或假值的内置数据类型。因为逻辑表达式求值为 1 或 0，逻辑表达式的值存储在类型为 `int` 的变量中。因此，你可以使用 `int` 数据类型来。

200 | 第 4 章：控制结构 I（选择）

表 4-3 定义了运算符 `!`（非）。当你使用该运算符时，`!true` 为 `false`，而 `!false` 为 `true`。在逻辑表达式前面加上 `!false` 会反转该逻辑表达式的值。

## 表 4-3 (非) 运算符

| 表达式 | !(表达式) |
| --- | --- |
| true (非零) | false (0) |
| false (0) | true (1) |

## 示例 4-10

| 表达式 | 数值 | 解释 |
| --- | --- | --- |
| ! ('A' > 'B') | true | 因为 'A' > 'B' 为 false，所以 `! ('A' > 'B')` 为 true。 |
| ! (6 <= 7) | false | 因为 6 <= 7 为 true，所以 `! (6 <= 7)` 为 false。 |

表 4-4 定义了运算符 `&&`（与）。根据此表可以推导出，当仅当 Expression1 和 Expression2 均为 true 时，Expression1 && Expression2 为 true；否则，Expression1 && Expression2 的求值为 false。

## 表 4-4 && (与) 运算符

| Expression1 | Expression2 | Expression1 && Expression2 |
| --- | --- | --- |
| true (非零) | true (非零) | true (1) |
| false (非零) | false (0) | false (0) |
| false (0) | true (非零) | false (0) |
| false (0) | false (0) | false (0) |

## 示例 4-11

| 表达式 | 数值 | 解释 |
| --- | --- | --- |
| (14 >= 5) && ('A' < 'B') | true | 因为 (14 >= 5) 为 true，('A' < 'B') 为 true，且 true && true 为 true，该表达式的求值为 true。 |
| (24 >= 35) && ('A' < 'B') | false | 因为 (24 >= 35) 为 false，('A' < 'B') 为 true，且 false && true 为 false，该表达式的求值为 false。 |

Copyright 2018 Cengage Learning. 版权所有。未经全部或部分复制、扫描或复制。WCN 020-200-203

表 4-5 定义了运算符 `||`（或）。根据此表可以推导出，当仅当 Expression1 或 Expression2 至少有一个为 true 时，Expression1 || Expression2 为 true；否则，Expression1 || Expression2 的求值为 false。

## 表 4-5 || (或) 运算符

| Expression1 | Expression2 | Expression1 || Expression2 |
| :--- | :--- | :--- |
| true (非零) | true (非零) | true (1) |
| false (非零) | false (0) | true (1) |
| false (0) | true (非零) | true (1) |
| false (0) | false (0) | false (0) |

## 示例 4-12

| 表达式 | 数值 | 解释 |
| :--- | :--- | --- |
| (14 >= 5) || ('A' > 'B') | true | 因为 (14 >= 5) 为 true，('A' > 'B') 为 false，且 true || false 为 true，该表达式的求值为 true。 |
| (24 >= 35) || ('A' > 'B') | false | 因为 (24 >= 35) 为 false，('A' > 'B') 为 false，且 false || false 为 false，该表达式的求值为 false。 |
| ('A' <= 'a') || (7 != 7) | true | 因为 ('A' <= 'a') 为 true，(7 != 7) 为 false，且 true || false 为 true，该表达式的求值为 true。 |

## 优先级

复杂的逻辑表达式可能很难评估。考虑以下逻辑表达式：

11 > 5 || 6 < 15 && 7 >= 8

该逻辑表达式会产生不同的结果，取决于先评估 `||` 还是 `&&`。如果先评估 `||`，表达式求值为 false。如果先评估 `&&`，表达式求值为 true。

一个表达式可能包含算术、关系和逻辑运算符，如下表达式所示：
5 + 3 <= 9 && 2 > 3

为了处理复杂的逻辑表达式，必须有一套评估运算符的优先级方案。表 4-6 显示了一些 C++ 运算符的优先级，包括算术、关系和逻辑运算符。（所有 C++ 运算符的优先级请参见附录 B。）

## 表 4-6 运算符优先级

| 运算符 | 优先级 |
| --- | --- |
| !, +, - (一元运算符) | 第一 |
| *, /, % | 第二 |
| +, - | 第三 |
| <, <=, >=, > | 第四 |
| ==, != | 第五 |
| && | 第六 |
| || | 第七 |
| = (赋值运算符) | 最后 |

> 注意 在 C++ 中，`&` 和 `|` 也是运算符。这些运算符的含义与 `&&` 和 `||` 的含义不同。用 `&` 代替 `&&` 或 `||`——这会导致拼写错误——将产生非常奇怪的结果。

表达式、关系运算符和逻辑运算符根据优先级规则从左到右进行评估。因为关系和逻辑运算符是从左到右评估的，所以这些运算符的结合性被称为从左到右。示例 4-13 说明了由变量组成的逻辑表达式是如何评估的。

## 示例 4-13

假设你有以下声明：

```cpp
bool found = true;
int age = 20;
double hours = 45.30;
double overtime = 15.00;
int count = 20;
char ch = 'B';
```

考虑以下表达式：

| 表达式 | 数值 / 解释 |
| --- | --- |
| !found | false | 因为 `found` 为 true，所以 `!found` 为 false。 |
| hours > 40.00 | true | 因为 `hours` 为 45.30，45.30 > 40.00 为 true。 |
| !age | false | 因为 `age` 为 20（非零），所以 `!age` 为 false。 |
| !found && (age >= 18) | false | 因为 `!found` 为 false；`age >= 18` 为 true，因此 false && true 为 false。 |
| (!found && (age >= 18)) | false | 现在 `age >= 18` 为 true，因此 (!found && (age >= 18)) 为 false。 |
| hours + overtime <= 75.00 | true | 因为 `hours + overtime` 为 45.30 + 15.00 = 60.30，60.30 <= 75.00 为 true。 |
| (count >= 0) && (count <= 100) | true | 现在 `count` 为 20，20 >= 0 为 true，20 <= 100 为 true，因此 true && true 为 true。 |
| ('A' <= ch && ch <= 'Z') | true | 这里 `ch` 为 'B'。因为 'A' <= 'B' 为 true，'B' <= 'Z' 为 true，因此 ('A' <= ch && ch <= 'Z') 为 true。 |

注意，如果逻辑表达式的值为 true，其求值为 1；如果逻辑表达式的值为 false，其求值为 0。本书随附的 `LogicalOperators.cpp` 包含了这些表达式。

## 关系运算符与字符串类型

关系运算符适用于 `string` 类型的变量。字符串通过从第一个字符开始使用 ASCII 排序逐字符比较。逐字符比较持续到找到不匹配或比较完最后一个字符。以下示例显示了字符串类型变量的比较。

## 示例 4-15

假设你有以下语句：

```cpp
string str1 = "Hello";
string str2 = "Hi";
string str3 = "Air";
string str4 = "Bill";
string str5 = "Big";
```

以下表达式显示了字符串表达式的评估：

| 表达式 | 数值 / 解释 |
|---|---|
| str1 < str2 | true | `str1` 为 "Hello"，`str2` 为 "Hi"。`str1` 和 `str2` 的第一个字符相同，但 `str2` 的第二个字符 'i' 小于 `str1` 的第二个字符。因此 `str1 < str2` 为 true。 |
| str1 > "Hen" | false | `str1` 和 "Hen" 的前两个字符相同，但 `str1` 的第三个字符 'l' 小于 "Hen" 的第三个字符 'n'。因此 `str1 > "Hen"` 为 false。 |

## 第 4 章：控制结构 I（选择）

| 表达式 | 数值 / 解释 |
| :--- | :--- |
| str3 < "An" | **true** | `str3` 为 "Air"。`str3` 和 "An" 的第一个字符相同，但 "Air" 的第二个字符 'i' 小于 "An" 的第二个字符 'n'。因此 `str3 < "An"` 为 **true**。 |
| str1 == "hello" | **false** | `str1` 为 "Hello"。`str1` 的第一个字符 'H' 小于 "hello" 的第一个字符 'h'，'H' 的 ASCII 值为 72，而 'h' 的 ASCII 值为 104。因此 `str1 == "hello"` 为 **false**。 |
| str3 <= str4 | **true** | `str3` 为 "Air"，`str4` 为 "Bill"。`str3` 的第一个字符 'A' 小于 `str4` 的第一个字符 'B'。因此 `str3 <= str4` 为 **true**。 |
| str2 > str4 | **true** | `str2` 为 "Hi"，`str4` 为 "Bill"。`str2` 的第一个字符 'H' 大于 `str4` 的第一个字符 'B'。因此 `str2 > str4` 为 **true**。 |

如果比较两个长度不同的字符串且逐字符比较相等，则会到达短字符串的最后一个字符，短字符串被评估为小于较长字符串，如下所示：

| 表达式 | 数值 / 解释 |
| :--- | :--- |
| str4 >= "Billy" | **false** | `str4` 为 "Bill"。它有四个字符，而 "Billy" 有五个字符。因此 `str4` 是短字符串。`str4` 的四个字符与 "Billy" 的前四个字符相同，且 "Billy" 是较大的字符串。因此 `str4 >= "Billy"` 为 **false**。 |
| str5 <= "B" | **true** | `str5` 为 "Big"。它有三个字符，而 "B" 有六个字符。因此 `str5` 是短字符串。`str5` 的三个字符与 "B" 的前三个字符相同，且 "B" 是较大的字符串。因此 `str5 <= "B"` 为 **true**。 |

# 复合语句（块语句）

`if` 和 `if..else` 结构一次只能控制一条语句。然而，假设你希望在 `if` 或 `if..else` 语句中的表达式为真时，执行多条语句。为了允许更复杂的结构，C++ 提供了一种名为复合语句或块语句的结构。复合语句采用如下形式如下：

```
{
```
