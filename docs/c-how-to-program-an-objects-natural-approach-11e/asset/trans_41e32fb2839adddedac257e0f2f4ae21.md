

```text
1. set total to zero
2. set grade counter to one
3.
4. while grade counter is less than or equal to ten
   5. prompt the user to enter the next grade
   6. input the next grade
   7. add the grade into the total
   8. add one to the grade counter
9.
10. set the class average to the total divided by ten
11. print the class average
```

注意前面算法中对 total 和 counter 的引用。total 是用于累加若干值之和的变量。counter 是用于计数的变量——grade counter 表示用户即将输入的是 10 个成绩中的哪一个。用于存储总计值的变量在程序中使用前必须初始化为零。在伪代码中，我们没有用花括号括起构成伪代码 while 循环体的语句，但你可以这样做。

经验表明，用计算机解决问题最具挑战性的部分是开发求解算法。一旦指定了正确的算法，据此生成一个可运行的 C++ 程序通常很直接。

## 3.8.2 实现计数器控制的迭代

在图 3.1 中，main 函数使用计数器控制的迭代计算班级平均成绩。它允许用户输入 10 个成绩，然后计算并显示班级平均成绩。

```cpp
// fig03_01.cpp
// Solving the class-average problem using counter-controlled iteration.
#include <iostream>
using namespace std;

int main() {
   // initialization phase
   int total{0}; // initialize sum of grades entered by the user
   int gradeCounter{1}; // initialize grade # to be entered next

   // processing phase uses counter-controlled iteration
   while (gradeCounter <= 10) { // loop 10 times
      cout << "Enter grade: "; // prompt
      int grade;
      cin >> grade; // input next grade
      total = total + grade; // add grade to total
      gradeCounter = gradeCounter + 1; // increment counter by 1
   }
```

**图 3.1** | 使用计数器控制的迭代求解班级平均成绩问题。（第 1 部分，共 2 部分。）

```cpp
   // termination phase
   int average{total / 10}; // int division yields int result

   // display total and average of grades
   cout << "\nTotal of all 10 grades is " << total;
   cout << "\nClass average is " << average << "\n";
}
```

```text
Enter grade: 67
Enter grade: 78
Enter grade: 89
Enter grade: 67
Enter grade: 87
Enter grade: 98
Enter grade: 93
Enter grade: 85
Enter grade: 82
Enter grade: 100

Total of all 10 grades is 846
Class average is 84
```

**图 3.1** | 使用计数器控制的迭代求解班级平均成绩问题。（第 2 部分，共 2 部分。）

### main 中的局部变量

第 8、9、14 和 21 行分别声明 int 变量 total、gradeCounter、grade 和 average。变量 grade 存储用户输入。在块（例如函数体）中声明的变量是局部变量，只能从它的声明行使用到该块的右花括号。局部变量的声明必须出现在使用该变量之前。变量 grade——在第 14 行的 while 循环体中声明——只能在该块中使用。

### 初始化变量 total 和 gradeCounter

第 8–9 行声明 total 并将其初始化为 0，声明 gradeCounter 并将其初始化为 1。这些初始化发生在变量用于计算之前。每个总计变量和计数器变量都要初始化，可以在其声明中初始化，也可以在赋值语句中初始化。总计变量通常初始化为 0，计数器变量通常初始化为 0 或 1，具体取决于其用途。我们将展示何时使用 0 或 1 的示例。

### 从用户读取 10 个成绩

while 语句（第 12–18 行）在 gradeCounter 的值小于或等于 10 时持续迭代。第 13 行显示提示“Enter grade: ”。第 15 行输入用户输入的成绩，并将其赋给变量 grade。然后第 16 行将用户输入的新成绩加到 total 上，并将结果赋给 total，替换其先前的值。第 17 行将 gradeCounter 加 1，表示程序已处理一个成绩，并准备从用户输入下一个成绩。递增 gradeCounter 最终会使其超过 10，从而终止循环。

### 计算并显示班级平均成绩

当循环终止时，第 21 行在变量 average 的初始化器中执行平均计算。第 24 行显示文本“Total of all 10 grades is ”，后跟变量 total 的值。然后，第 25 行显示文本“Class average is ”，后跟 average 的值。当执行到达第 26 行时，程序终止。

## 3.8.3 整数除法与截断

此示例的平均计算产生 int 结果。程序的示例执行表明成绩之和为 846——除以 10 时，本应得到 84.6。像 84.6 这样包含小数点的数是浮点数。然而，在班级平均成绩程序中，total / 10 产生整数 84，因为 total 和 10 都是整数。两个整数相除会得到整数除法——计算中的任何小数部分都会被截断。下一节将展示如何从平均计算中获得浮点结果。例如，7 / 4 在常规算术中得 1.75，但在整数算术中会截断为 1，而不是四舍五入为 2。假设整数除法会四舍五入（而不是截断）可能导致错误结果。

## 3.8.4 算术溢出

在图 3.1 中，第 16 行

```cpp
total = total + grade; // add grade to total
```

将用户输入的每个成绩加到 total 上。即使是这条简单语句也有潜在问题——将这些整数相加可能产生一个太大而无法存储在 int 变量中的值。这称为算术溢出，会导致未定义行为，从而可能造成意外结果和安全问题。例如，参见

```text
https://en.wikipedia.org/wiki/Integer_overflow#Security_ramifications
```

以下表达式返回你系统的最大和最小 int 值：

```cpp
std::numeric_limits<int>::max()
std::numeric_limits<int>::min()
```

每个表达式都使用 C++ 标准库头文件 `<limits>` 中的 numeric_limits 类。你可以通过替换这些表达式中的 int，对任何整数类型或浮点类型使用类似表达式。

## 3.8.5 输入验证

当程序接收用户输入时，可能发生各种问题。例如，图 3.1 的第 15 行

```cpp
cin >> grade; // input next grade
```

假设用户将输入 0 到 100 的整数成绩，但用户可能输入：

- 小于 0 的整数，
- 大于 100 的整数，
- 超出可存储在 int 变量中的值范围的整数，
- 包含小数点的数字，或
- 包含字母或特殊符号、甚至不表示数字的值。

工业级程序必须测试所有可能的错误情况，以确保输入有效。输入成绩的程序应使用范围检查来验证成绩，确保它们是 0 到 100 的值。然后，你可以要求用户重新输入任何超出范围的值。如果程序要求输入来自特定值集合（例如非连续产品代码），则应确保每个输入都与该集合中的某个值匹配。

### ✔️ 检查点

- 1. （判断正误）两个整数相除会得到整数除法——计算中的任何小数部分都会四舍五入到最接近的整数。
  
  答案：错误。实际上，计算中的任何小数部分都会被截断。

- 2. （填空）在 _______（例如函数体）中声明的变量是局部变量，只能从它的声明行使用到对应的右花括号。
  
  答案：块。

- 3. （代码）重写以下代码中的初始化，使循环迭代 5 次。

  ```cpp
  int count{0};

  while (count < 5) {
      count = count + 1;
      cout << "count is: " << count << "\n";
  }
  ```

  答案：

  ```cpp
  int count{0};

  while (count < 5) {
      count = count + 1;
      cout << "count is: " << count << "\n";
  }
  ```

  ```text
  count is: 1
  count is: 2
  count is: 3
  count is: 4
  count is: 5
  ```

## 3.9 算法设计：哨兵控制的迭代

让我们推广 3.8 节的班级平均成绩问题。考虑以下问题：

> 开发一个班级平均成绩程序，每次运行时处理任意数量学生的成绩。

在前面的班级平均成绩示例中，问题描述指定了学生人数，因此成绩数量（10）是预先已知的。对于这个问题，我们不知道用户在程序执行期间会输入多少个成绩。程序必须处理任意数量的成绩。

