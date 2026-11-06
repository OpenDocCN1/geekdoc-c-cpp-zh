

## 4.10.3 实现哨兵控制迭代

在**图 4.12**中，`main` 函数实现了**图 4.11**的伪代码算法。虽然用户输入的每个成绩都是整数，但平均值的计算很可能产生带小数点的数字——即实数或**浮点数**（例如 7.33、0.0975 或 1000.12345）。`int` 类型无法表示这样的数字，因此此示例必须使用另一种类型来实现。C++ 提供了 `float` 和 `double` 数据类型来在内存中存储浮点数。这两种类型的主要区别在于，`double` 变量通常可以存储数值范围更大、精度更高（即小数点右侧的位数更多，也称为数字的**精度**）的数字。C++ 还支持 `long double` 类型，用于存储比 `double` 数值范围更大、精度更高的浮点值。我们将在**第 5 章**中进一步讨论浮点类型。

```cpp
// Fig. 4.12: ClassAverage.cpp
// Solving the class-average problem using sentinel-controlled iteration.
#include <iostream>
#include <iomanip> // parameterized stream manipulators
using namespace std;

int main() {
   // initialization phase
   int total{}; // initialize sum of grades
   unsigned int gradeCounter{}; // initialize # of grades entered so far

   // processing phase
   // prompt for input and read grade from user
   cout << "Enter grade or -1 to quit: ";
   int grade;
   cin >> grade;

   // loop until sentinel value read from user
   while (grade != -1) {
      total = total + grade; // add grade to total
      gradeCounter = gradeCounter + 1; // increment counter

      // prompt for input and read next grade from user
      cout << "Enter grade or -1 to quit: ";
      cin >> grade;
   }

   // termination phase
   // if user entered at least one grade...
   if (gradeCounter != 0) {
      // use number with decimal point to calculate average of grades
      double average{static_cast<double>(total) / gradeCounter};

      // display total and average (with two digits of precision)
      cout << "\nTotal of the " << gradeCounter
           << " grades entered is " << total;
      cout << setprecision(2) << fixed;
      cout << "\nClass average is " << average << endl;
   }
   else { // no grades were entered, so output appropriate message
      cout << "No grades were entered" << endl;
   }
}
```

```text
Enter grade or -1 to quit: 97
Enter grade or -1 to quit: 88
Enter grade or -1 to quit: 72
Enter grade or -1 to quit: -1

Total of the 3 grades entered is 257
Class average is 85.67
```

**图 4.12** 使用哨兵控制迭代解决班级平均分问题。

回想一下，整数除法产生整数结果。本程序引入了一种称为**强制转换运算符**的特殊运算符，以强制平均值计算产生浮点数值结果。本程序还将控制语句一个接一个地**堆叠**起来（按顺序）——`while` 语句（第 19–26 行）后面依次跟着一个 `if...else` 语句（第 30–42 行）。本程序中的大部分代码与图 4.10 中的相同，因此我们重点关注新概念。

### *哨兵控制迭代与计数器控制迭代的程序逻辑*

第 10 行将 `gradeCounter` 初始化为 `0`，因为尚未输入任何成绩。请记住，本程序使用*哨兵控制迭代*来输入成绩。程序仅在用户输入有效成绩时递增 `gradeCounter`。第 32 行声明了 `double` 变量 `average`，用于将班级平均分存储为浮点数。

将本程序中哨兵控制迭代的程序逻辑与图 4.10 中计数器控制迭代的逻辑进行比较。在计数器控制迭代中，`while` 语句（图 4.10 第 12–18 行）的每次迭代都会在指定的迭代次数内从用户读取一个值。在哨兵控制迭代中，程序在到达 `while` 语句*之前*提示并读取第一个值（**图 4.12**第 14 行和第 16 行）。该值决定了程序的控制流是否应进入 `while` 的主体。如果 `while` 的条件为*假*，则用户输入了哨兵值，因此 `while` 的主体不会执行（即未输入任何成绩）。另一方面，如果条件为*真*，则主体开始执行，循环将 `grade` 值添加到 `total` 并递增 `gradeCounter`（第 20–21 行）。然后，循环主体中的第 24–25 行从用户输入下一个值。接下来，程序控制到达第 26 行循环主体的右花括号，因此执行继续测试 `while` 的条件（第 19 行）。该条件使用用户最近输入的 `grade` 来确定循环主体是否应再次执行。

变量 `grade` 的值总是在程序测试 `while` 条件*之前*立即从用户输入。这允许程序在处理该值（即将其添加到 `total`）*之前*确定刚输入的值是否为哨兵值。如果输入了哨兵值，循环终止，并且程序不会将 −1 添加到 `total`。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_452_0.png)

### 良好编程实践 4.3

*在哨兵控制循环中，提示应提醒用户哨兵值。*

循环终止后，第 30–42 行的 `if...else` 语句执行。第 30 行的条件确定是否输入了任何成绩。如果未输入任何成绩，则 `if...else` 语句的 `else` 部分执行并显示消息 `"No grades were entered"`。

### *`while` 语句中的花括号*

请注意**图 4.12**（第 19–26 行）中 `while` 语句的*块*。如果没有花括号，循环会将其主体视为仅第一条语句，即将 `grade` 添加到 `total`。块中的最后三条语句将落在循环主体之外，导致计算机错误地将代码解释为如下：

```cpp
{
    while (grade != -1)
        total = total + grade; // add grade to total
    gradeCounter = gradeCounter + 1; // increment counter

    // prompt for input and read next grade from user
    cout << "Enter grade or -1 to quit: ";
    cin >> grade;
}
```

如果用户未在第 16 行（`while` 语句之前）输入哨兵值 `-1`，上述代码将导致程序出现*无限循环*。

## 4.10.4 在基本类型之间显式和隐式转换

如果至少输入了一个成绩，**图 4.12** 的第 32 行

```cpp
double average{static_cast<double>(total) / gradeCounter};
```

计算结果的平均值。回顾**图 4.10**，整数除法产生整数结果。即使变量 `average` 被声明为 `double`，如果我们把第 32 行写成

```cpp
double average{total / gradeCounter};
```

那么在除法结果用于初始化 `average` *之前*，就会丢失商的小数部分。

### `static_cast` 运算符

为了在此示例中使用整数执行浮点计算，首先使用 `static_cast` **运算符**创建*临时*浮点值。第 32 行将括号中操作数（`total`）的临时副本转换为尖括号中的类型（`double`）。存储在 `total` 中的值仍然是整数。以这种方式使用强制转换运算符称为**显式转换**。

### *提升*

强制转换操作之后，计算由 `total` 的临时 `double` 副本除以整数 `gradeCounter` 组成。对于算术运算，编译器只知道如何计算操作数类型*相同*的表达式。为了确保这一点，编译器对选定的操作数执行称为**提升**（也称为**隐式转换**）的操作。在包含 `int` 和 `double` 数据类型值的表达式中，C++ 将 `int` 操作数**提升**为 `double` 值。因此，在第 32 行中，C++ 将 `gradeCounter` 值的临时副本提升为 `double` 类型，然后执行除法。最后，用浮点结果初始化 `average`。**第 6.5 节**讨论了允许的基本类型提升。

### *适用于任何类型的强制转换运算符*

强制转换运算符可用于所有基本类型以及类类型。该运算符由关键字 `static_cast` 后跟尖括号（`<` 和 `>`）中的类型名构成。它是一个**一元运算符**——即只有一个操作数。C++ 还支持

