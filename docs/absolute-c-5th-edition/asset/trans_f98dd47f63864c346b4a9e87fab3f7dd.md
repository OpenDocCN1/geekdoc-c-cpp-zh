

## 第5章 数组

请注意，对于二维数组参数，第一维的大小是不给出的，我们必须包含一个 `int` 类型参数来给出该第一维的大小。对于普通数组，编译器允许你通过在第一组括号中放置一个数字来指定第一维。然而，这个数字仅仅是一个注释；编译器会忽略该数字。）第二维的大小（如果超过两个维度，则所有其他维度的大小）在数组参数之后给出，与参数的情况相同。

```
const char p[100]
```

如果你意识到多维数组是“数组的数组”，那么这个规则就变得有意义了。由于二维数组参数

```
const char p[][100]
```

是一个数组的数组的参数，第一维实际上是数组的索引，其处理方式与普通一维数组的索引相同。第二维是基类型描述的一部分，该基类型是一个大小为 100 的字符数组。

## 多维数组参数

多维数组参数出现在函数头或声明中，其第一维的大小不给出，但其余维度的大小必须在方括号中给出。由于未给出第一维的大小，通常需要一个额外的 `int` 类型参数来提供该第一维的大小。以下是一个带有二维数组参数 `p` 的函数声明示例：

```
void getPage(char p[][100], int sizeDimension);
```

## 示例：二维评分程序

显示 5.9 包含一个程序，该程序使用一个名为 `grade` 的二维数组来存储并显示一个小班级的成绩记录。该班级有四名学生，记录包括三次测验。显示 5.10 展示了如何使用数组 `grade` 来存储数据。第一个数组索引用于指定学生，第二个数组索引用于指定指定的测验。由于学生和测验是从 1 开始编号的而不是 0，我们必须从学生编号中减 1，并从测验编号中减 1，以获得存储特定测验的索引变量。例如，第 4 号学生在第一次测验中得到的得分存储在 `grade[3][0]` 中。

我们的程序还使用了两个多维数组。数组 `stave` 将用于记录每个学生的平均测验分。例如，程序将 `stAve[0]` 设置为第 1 号学生得分的平均值，将 `stAve[1]` 设置为第 2 号学生测验得分的平均值，

## 多维数组

## 示例：（续）

依此类推。数组 `quizAve` 将用于记录每次测验的得分。例如，程序将 `quizAve[0]` 设置为所有学生在第 1 次测验的平均分，`quizAve[1]` 将记录第 2 次测验的平均分，依此类推。显示 5.10 展示了数组 `grade`、`stAve` 和 `quizAve` 之间的关系。这些数据反过来决定了程序存储在 `stAve` 和 `quizAve` 中的值。显示 5.11 也显示了这些程序为 `stAve` 和 `quizAve` 计算的数值。

填充数组 `grade` 并在计算和显示学生平均分及测验平均分的完整程序位于显示 5.9 中。在该程序中，我们将数组维度声明为全局常量。这些过程无法在其他地方复用，因为我们在过程体内使用了全局定义的常量，而不是使用数组维度尺寸的参数。由于是常规操作，显示部分没有显示填充数组的代码。

## 5.9 二维数组（3 部分第 1 部分）

```
// 将每个学生的测验得分读入二维数组 
//grade（但此显示中未显示输入代码）
// 计算每个学生的平均分以及每次测验的平均分。
// 显示测验得分和平均分。
#include <iostream>
#include <iomap>
using namespace std;
const int NUMBER_STUDENTS = 4, NUMBER_QUIZZES = 3;
void computeStAve(const int grade[], double stave[]);
// 前置条件：全局常量 NUMBER_STUDENTS 和 NUMBER_QUIZZES
// 是数组 grade 的维度。每个索引变量
// grade[stNum-1,quizNum-1] 包含学生 stNum 在
// quizNum 次测验中的得分。
// 后置条件：每个 stAve[stNum-1] 包含学生 stNum
// 的平均分。

void computeQuizAve(const int grade[], NUMBER_QUIZZES,
//double quizAve[]);
// 前置条件：全局常量 NUMBER_STUDENTS 和 NUMBER_QUIZZES
// 是数组 grade 的维度。每个索引变量
// grade[stNum-1,quizNum-1] 包含学生 stNum 在
// quizNum 次测验中的得分。
// 后置条件：每个 quizAve[quizNum-1] 包含
// 所述 quizNum 次测验的平均分。
```

（续）

## 第5章 数组

显示 5.9 二维数组（3 部分第 2 部分）

```
20 void display(const int grade[][NUMBER_QUIZZES],
21                             const double stave[],
22                             const double quizAve[]);
23 // 前置条件：全局常量 NUMBER_STUDENTS 和 NUMBER_QUIZZES
24 // 是数组 grade 的维度。每个索引变量
25 //grade[stNum-1,quizNum-1] 包含 stNum 在
26 //quizNum 上的得分。每个 stave[stNum-1] 包含学生
27 //stNum 的平均分。每个 quizAve[quizNum-1] 包含
28 //quizNum 次测验的平均分。
29 // 后置条件：grade、stave 和 quizAve 中的所有数据
30 // 已输出。
31 int main()
32 {
33     int grade[NUMBER_STUDENTS][NUMBER_QUIZZES];
34     double stave[NUMBER_STUDENTS];
35     double quizAve[NUMBER_QUIZZES];
36 
37     // 填充数组的代码在这里，但未显示。
38 
39     computeStAve(grade, stave);
40     computeQuizAve(grade, quizAve);
41     display(grade, stave, quizAve);
42     return 0;
43 }
44 void computeStAve(const int grade[][NUMBER_QUIZZES], double stave[])
45 {
46     for (int stNum = 1; stNum <= NUMBER_STUDENTS; stNum++)
47         // 处理 stNum:
48             double sum = 0;
49             for (int quizNum = 1; quizNum <= NUMBER_QUIZZES; quizNum++)
50                 sum += grade[stNum-1][quizNum-1];
51         // 包含学生 stNum 的总分。
52             stave[stNum-1] = sum/NUMBER_STUDENTS;
53     // 学生 stNum 的平均分是 stave[stNum-1] 的值
54 void computeQuizAve(const int grade[][NUMBER_QUIZZES], double quizAve[])
55 {
56     for (int quizNum = 1; quizNum <= NUMBER_QUIZZES; quizNum++)
57         // 处理一次测验（针对所有学生）：
58             double sum = 0;
59             for (int stNum = 1; stNum <= NUMBER_STUDENTS; stNum++)
60                 sum += grade[stNum-1][quizNum-1];
61 // 包含所有学生在第 quizNum
62 //quizNum 次测验的总分。
63  quizAve[quizNum-1] = sum/NUMBER_STUDENTS;
64     // quizNum 次测验的平均分是 quizAve[quizNum-1] 的值
65 }
66 }
```

