

```
输入 10 个考试成绩，并统计及格和不及格的人数
```

需要使用一个循环依次输入每次考试的成绩。我们预先知道确切有 10 个考试成绩，因此适合使用计数器控制的循环。在循环内部（即嵌套在循环中的部分），双重选择结构将确定每个考试成绩是及格还是不及格，并将相应的计数器递增。因此，前面伪代码语句的细化结果如下：

```
当学生计数器小于或等于 10 时
    提示用户输入下一个考试成绩
    输入下一个考试成绩
    如果学生及格
        将及格人数加 1
    否则
        将不及格人数加 1
    将学生计数器加 1
```

我们使用空行将 If…Else 控制结构隔开，这样可以提高可读性。

伪代码语句

```text
打印考试成绩摘要，并决定是否应发放奖金
```

可以细化如下：

```text
打印及格人数

打印不及格人数

如果及格学生超过 8 人
    打印“给教师的奖金！”
```

## 4.11.5 伪代码的完整第二次细化

完整的第二次细化结果如**图 4.13**所示。注意，我们还使用空行将 *While* 结构隔开，以提高程序的可读性。现在，这段伪代码已经足够详细，可以转换为 C++。

```
1  将及格人数初始化为零
2  将不及格人数初始化为零
3  将学生计数器初始化为一

4
5  当学生计数器小于或等于 10 时
6      提示用户输入下一个考试成绩
7      输入下一个考试成绩

8
9      如果学生及格
10         将及格人数加 1
11     否则
12         将不及格人数加 1

13
14     将学生计数器加 1

15
16 打印及格人数
17 打印不及格人数

18
19 如果及格学生超过 8 人
20     打印“给教师的奖金！”
```

图 4.13 考试成绩问题的伪代码。

## 4.11.6 实现伪代码算法的程序

实现该伪代码算法的程序以及两次示例执行结果如**图 4.14**所示。`main` 中的第 8–10 行和第 16 行声明了用于处理考试成绩的变量。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_471_0.png)

### 错误预防提示 4.4

> 在声明局部变量时对其进行初始化，有助于避免因尝试使用未初始化变量而产生的编译警告，也有助于避免使用未初始化变量所导致的逻辑错误。

```cpp
// Fig. 4.14: Analysis.cpp
// Analysis of examination results using nested control statements.
#include <iostream>
using namespace std;

int main() {
    // initializing variables in declarations
    unsigned int passes{0};
    unsigned int failures{0};
    unsigned int studentCounter{1};

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

    // termination phase; prepare and display results
    cout << "Passed: " << passes << "\nFailed: " << failures << endl;

    // determine whether more than 8 students passed
    if (passes > 8) {
        cout << "Bonus to instructor!" << endl;
    }
}
```

```
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

```
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

**图 4.14** 使用嵌套控制语句分析考试成绩。

`while` 语句（第 13–29 行）循环执行 10 次。在每次迭代中，循环输入并处理一个考试成绩。注意，用于处理每个成绩的 `if...else` 语句（第 20–25 行）**嵌套**在 `while` 语句中。如果 `result` 为 `1`，`if...else` 语句就会使 `passes` 递增；否则，它假定 `result` 为 `2`，并使 `failures` 递增。第 28 行在第 13 行再次测试循环条件之前递增 `studentCounter`。输入 10 个值后，循环终止，第 32 行显示 `passes` 和 `failures` 的数量。第 35–37 行的 `if` 语句确定是否有超过 8 名学生通过考试；如果有，则输出消息 `"Bonus to instructor!"`

**图 4.14**展示了两次示例程序执行的输入和输出。在第一次执行中，第 35 行的条件为 *真*——超过 8 名学生通过了考试，因此程序输出一条为教师发放奖金的消息。

## 4.11.7 使用列表初始化防止窄化转换

正如你在**第 2 章**中所学，C++11 引入了列表初始化，使你能够使用一种语法初始化任意类型的变量。请看**图 4.14**中的第 10 行：

```cpp
unsigned int studentCounter{1};
```

也可以将其写成：

```cpp
unsigned int studentCounter = {1};
```

不过，更推荐使用不带 `=` 的形式。在 C++11 之前，你需要这样写：

```cpp
unsigned int studentCounter = 1;
```

对于基本类型变量，列表初始化语法可以*防止*可能导致*数据丢失*的**窄化转换**。例如，以前你可以这样写：

```cpp
int x = 12.7;
```

这会尝试将 `double` 值 `12.7` 赋给 `int` 变量 `x`。在这种情况下，C++ 会通过*截断*浮点部分（`.7`）将 `double` 值转换为 `int`，这是一种会造成数据丢失的*窄化转换*。实际赋给 `x` 的值是 `12`。许多编译器会对此发出警告，但仍允许该语句编译通过。然而，使用列表初始化时，例如：

```cpp
int x{12.7};
```

或：

```cpp
int x = {12.7};
```

则会产生*编译*错误，从而帮助你避免潜在且隐蔽的逻辑错误。例如，Apple 的 Xcode LLVM 编译器会给出以下错误：

```text
Type 'double' cannot be narrowed to 'int' in initializer list
```

我们将在后续章节中讨论列表初始化器的其他功能。

### *回顾* **图 4.10**

你可能认为**图 4.10**中的以下语句

```cpp
int average(total / 10); // int division yields int result
```

包含窄化转换，但 `total` 和 `10` 都是 `int` 值，因此初始化值也是 `int` 类型。如果在前一条语句中 `total` 是 `double` 变量，或者我们使用 `double` 字面值 `10.0`，那么初始化值的类型就会是 `double`。在这种情况下，编译器会由于尝试进行窄化转换而发出错误消息。

## 4.12 复合赋值运算符

**复合赋值运算符**是赋值表达式的缩写。类似于

```
variable = variable operator expression;
```

这样的语句，其中 *operator* 是二元运算符 **+**、**-**、**\***、**/** 或 **%**（以及我们将在本文后续部分讨论的其他运算符），都可以写成以下形式：

```
variable operator= expression;
```

例如，可以使用**加法复合赋值运算符** **+=**，将语句

```
c = c + 3;
```

缩写为

