
## 3.10.6 实现程序

图3.3用计数器控制的迭代实现了该程序，并展示了两个示例执行。第8—10行和第16行声明了用于处理考试结果的变量。第13—29行循环10次。在每次迭代中，循环输入并处理一个考试结果。注意，用于处理每个结果的 if...else 语句（第20—25行）嵌套在 while 语句中。如果结果为1，则 if...else 语句递增 passes；否则，它假定结果为2并递增 failures。⁵ 第28行在再次测试第13行的循环条件之前递增 studentCounter。

```text
5  while student counter is less than or equal to 10
6      prompt the user to enter the next exam result
7      input the next exam result

9      if the student passed
10         add one to passes
11     else
12         add one to failures

14     add one to student counter

16 print the number of passes
17 print the number of failures

19 if more than eight students passed
20     print "Bonus to instructor!"
```

```cpp
1  // fig03_03.cpp
2  // Analysis of examination results using nested control statements.
3  #include <iostream>
4  using namespace std;

6  int main() {
7      // Initializing variables in declarations
8      int passes{0};
9      int failures{0};
10     int studentCounter{1};
```

**图3.3** | 使用嵌套控制语句分析考试结果。（第1部分，共2部分。）

5. 如果用户输入无效数据，假定结果为2可能是一个糟糕的假设。我们稍后将讨论数据验证技术。

```cpp
// process 10 students using counter-controlled loop
while (studentCounter <= 10) {
    // prompt user for input and obtain value from user
    cout << "Enter result (1 = pass, 2 = fail): ";
    int result;
    cin >> result;

    // if...else is nested in the while statement
    if (result == 1) {
        passes = passes + 1;
    }
    else {
        failures = failures + 1;
    }

    // increment studentCounter so loop eventually terminates
    studentCounter = studentCounter + 1;
}

// termination phase: prepare and display results
cout << "Passed: " << passes << "\nFailed: " << failures << "\n";

// determine whether more than 8 students passed
if (passes > 8) {
    cout << "Bonus to instructor!\n";
}
}
```

```text
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Passed: 9
Failed: 1
Bonus to instructor!
```

```text
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Passed: 6
Failed: 4
```

**图3.3** | 使用嵌套控制语句分析考试结果。（第2部分，共2部分。）

在输入10个值后，循环终止，第32行显示通过和未通过的数量。第35—37行中的 `if` 语句判断是否有超过八名学生通过了考试，如果是，则输出消息 "Bonus to instructor!" 图3.3展示了两个示例执行中的输入和输出。在第一个示例中，第35行的条件为真——超过八名学生通过了考试，因此程序输出一条消息，给教师一个奖励。

## 3.10.7 使用花括号初始化防止窄化转换

考虑图3.3第10行中的花括号初始化：

```cpp
int studentCounter{1};
```

它也可以写成

```cpp
int studentCounter = 1;
```

对于基本类型变量，花括号初始化器可防止可能导致数据丢失的**窄化转换**。例如，以下声明试图将 `double` 值 `12.6` 赋给 `int` 变量 `x`：

```cpp
int x = 12.6;
```

这里，C++通过截断浮点部分（`.6`）将 `double` 值转换为 `int`，因此该声明将 `12` 赋给 `x`。这种窄化转换会丢失数据。编译器通常会对此发出警告，但仍会编译代码。

然而，使用花括号初始化，如下所示：

```cpp
int x{12.6};
```

会产生**编译错误**，帮助你避免潜在的细微逻辑错误。即使你指定一个整数值的 `double` 值（如 `12.0`），仍然会得到**编译错误**。决定是否发生编译错误的是初始化器的类型（`double`），而不是它的值（`12.0`）。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_181_0.png)

C++标准文档没有规定错误消息的措辞。对于前面的声明，Visual Studio给出错误

```text
conversion from 'double' to 'int' requires a narrowing conversion
```

GNU C++给出错误

```text
error: narrowing conversion of '1.26e+1' from
    'double' to 'int' [-Wnarrowing]
```

而 clang++ 编译器给出错误

```text
error: type 'double' cannot be narrowed to 'int' in initializer list
    [-Wc++11-narrowing]
```

后面还有更多解释

```text
warning: implicit conversion from 'double' to 'int' changes value
from 12.6 to 12 [-Wliteral-conversion]
```

我们将在后续章节中讨论花括号初始化器的更多特性。

### 回顾图3.1

你可能会认为图3.1中的以下语句

```cpp
int average{total / 10}; // int division yields int result
```

包含窄化转换，但 total 和 10 都是 int 值，因此初始化器值是 int。如果前面语句中的 total 是 double，或者我们对分母使用 double 字面量 10.0，那么初始化器值将是 double 类型，编译器会发出窄化转换的错误消息。

### 检查点

- **1.** *（代码）* 为 `int` 变量 `temperature` 编写一条初始化语句。尝试用 double 值 `98.6` 初始化该变量，但要以能防止窄化转换的方式编写该语句。

  **答案：** `int temperature{98.6};`

- **2.** *（代码）* 在以下语句中，`average` 的初始值是什么？

  `int average{128 / 3};`

  **答案：** 在该语句中，128 和 3 都是整数，因此 128 / 3 产生整数结果。变量 average 的值将是 42。

- **3.** *（代码）* 编写一个循环三次的程序段。在每次迭代中，从用户处输入一个整数，然后使用嵌套的 `if...else` 语句判断并显示该数字是偶数还是奇数。

  **答案：**

  ```cpp
  int counter{1};

  while (counter <= 3) {
      cout << "Enter an integer: ";
      int number;
      cin >> number;

      if (number % 2 == 0) {
          cout << number << " is even\n";
      }
      else {
          cout << number << " is odd\n";
      }

      counter = counter + 1;
  }
  ```

  ```text
  Enter an integer: 2
  2 is even
  Enter an integer: 3
  3 is odd
  Enter an integer: 5
  5 is odd
  ```

## 3.11 复合赋值运算符

你可以将语句

```cpp
c = c + 3;
```

用加法复合赋值运算符 `+=` 缩写为

```cpp
c += 3;
```

`+=` 运算符将其右操作数的值加到左侧变量的值上，然后将结果存入左侧变量。因此，赋值表达式 `c += 3` 将 3 加到 `c` 上。下表列出了所有算术复合赋值运算符、示例表达式以及这些运算符作用的说明：

*假设：int c = 3, d = 5, e = 4, f = 6, g = 12：*

| 运算符 | 示例表达式 | 说明 | 赋值结果 |
|---|---|---|---|
| `+=` | `c += 7` | `c = c + 7` | 将 10 赋给 c |
| `-=` | `d -= 4` | `d = d - 4` | 将 1 赋给 d |
| `*=` | `e *= 5` | `e = e * 5` | 将 20 赋给 e |
| `/=` | `f /= 3` | `f = f / 3` | 将 2 赋给 f |
| `%=` | `g %= 9` | `g = g % 9` | 将 3 赋给 g |

### 检查点

- **1.** *（代码）* 编写一条语句，使用复合赋值运算符将变量 `total` 除以 5。

  **答案：** `total /= 5;`

## 3.12 自增和自减运算符

下表总结了 C++ 中用于将数值变量的值加 1 或减 1 的两个一元运算符——即一元自增运算符 `++` 和一元自减运算符 `--`：

| 运算符 | 运算符名称 | 示例表达式 | 说明 |
|---|---|---|---|
| `++` | 前缀自增 | `++number` | 将 number 加 1，然后在包含 number 的表达式中使用 number 的新值。 |
| `++` | 后缀自增 | `number++` | 在包含 number 的表达式中使用 number 的当前值，然后将 number 加 1。 |
| `--` | 前缀自减 | `--number` | 将 number 减 1，然后在包含 number 的表达式中使用 number 的新值。 |
| `--` | 后缀自减 | `number--` | 在包含 number 的表达式中使用 number 的当前值，然后将 number 减 1。 |

