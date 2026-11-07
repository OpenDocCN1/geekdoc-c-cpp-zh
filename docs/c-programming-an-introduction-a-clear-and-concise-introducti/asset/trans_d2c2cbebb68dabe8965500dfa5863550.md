
```cpp
int temps[2][7] = {{87, 85, 89, 92, 94, 88, 90},
                   {79, 86, 85, 88, 93, 91}};
```

### 初始化二维数组

要初始化二维数组，必须编写一个嵌套 for 循环，遍历行和列。下面是一个示例：

```cpp
const int rows = 2;
const int cols = 3;
int numbers[rows][cols];
    for(int r = 0; r < rows; ++r)
        for(int c = 0; c < cols; ++c)
            numbers[r][c] = 0;
```

在上面的代码片段中，外层 for 循环控制行，内层 for 循环控制列。因此，代码从第 0 行开始，将第 0、1、2 列填充为值 0，然后移到第 1 行，同样将第 0、1、2 列填充为值 0。

### 显示二维数组元素

我们可以使用与初始化时相同的嵌套 for 循环技术来显示上述二维数组的内容。下面是我们的第一次尝试：

```cpp
for(int r = 0; r < rows; ++r)
    for (int c = 0; c < cols; ++c)
        cout << numbers[r][c] << " ";
```

该代码片段的输出为：

```text
0 0 0 0 0 0
```

这是数组的内容，但我们希望按行/列顺序查看它。为此，我们需要在第一行之后写入换行符。我们可以通过在外层 for 循环之后添加一条 cout 语句来修改代码片段，以适应这一需求。下面是新的代码片段：

```cpp
for(int r = 0; r < rows; ++r) {
    for (int c = 0; c < cols; ++c)
        cout << numbers[r][c] << " ";
    cout << endl;
}
```

注意，我们必须把内层 for 循环放在一个块中，因为外层 for 循环的主体现在由两条语句组成：for 循环和 cout 语句。

该代码片段的输出为：

```text
0 0 0
0 0 0
```

### 二维数组示例

下面的程序演示了如何使用二维数组，从存储五名学生成绩的二维数组中计算每名学生的平均分。在讨论其工作原理之前，我们先看一下代码：

```cpp
// Array2D.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    const int rows = 5;
    const int cols = 5;
    int total = 0;
    double average = 0.0;
    int grades[rows][cols] = {{75, 82, 84, 79, 91},
                              {85, 81, 94, 96, 89},
                              {92, 91, 94, 89, 90},
                              {74, 72, 81, 78, 80},
                              {84, 82, 82, 83, 81}};

    for(int r = 0; r < rows; ++r) {
        cout << "Student " << r+1 << ": ";
        for(int c = 0; c < cols; ++c) {
            cout << grades[r][c] << " ";
            total += grades[r][c];
        }
        average = total / cols;
        cout << "Average: " << average << endl;
        total = 0;
        average = 0.0;
    }
    Console::ReadKey();
    return 0;
}
```

该程序的输出为：

```text
Student 1: 75 82 84 79 91 Average: 82
Student 2: 85 81 94 96 89 Average: 89
Student 3: 92 91 94 89 90 Average: 91
Student 4: 74 72 81 78 80 Average: 77
Student 5: 84 82 82 83 81 Average: 82
```

两个变量 total 和 average 在嵌套 for 循环之外声明并初始化。然后我们进入外层循环，它把我们置于成绩的第一行（学生 1）。当内层循环逐列移动时，每个成绩都会被访问、显示并加到 total 中。当循环到达最后一列时，控制权转移到外层循环，在那里计算并显示平均分。最后，在开始外层循环的新一轮迭代并移动到下一名学生之前，变量 total 和 average 会被重置为 0。不这样做会导致下一个总分和平均分计算错误。

### 执行列序计算

并非所有涉及二维数组的任务都需要在外层循环中处理行（这称为*行序*）。有时你可能希望改为按列序处理二维数组。使用上面成绩示例进行列序计算的一个例子是，我们想计算每场考试的平均分。为此，我们想把第一列中所有考试成绩相加，然后计算平均分，接着处理第二列的考试成绩，依此类推。要做到这一点，只需让外层循环处理列，内层循环处理行。程序的其余部分看起来与计算学生考试成绩平均分时完全一样。

下面是修改后的上述程序，它还计算考试平均分：

```cpp
// Array2D.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    const int rows = 5;
    const int cols = 5;
    int total = 0;
    double average = 0.0;
    int grades[rows][cols] = {{75, 82, 84, 79, 91},
                              {85, 81, 94, 96, 89},
                              {92, 91, 94, 89, 90},
                              {74, 72, 81, 78, 80},
                              {84, 82, 82, 83, 81}};
    for(int r = 0; r < rows; ++r) {
        cout << "Student " << r+1 << ": ";
        for(int c = 0; c < cols; c++) {
            cout << grades[r][c] << " ";
            total += grades[r][c];
        }
        average = total / cols;
        cout << "Average: " << average << endl;
        total = 0;
        average = 0.0;
    }
    cout << endl << "Test Averages: " << endl;
    total = 0;
    average = 0.0;
    for(int c = 0; c < cols; ++c) {
        cout << "Test " << c+1 << ": ";
        for(int r = 0; r < rows; ++r) {
            cout << grades[r][c] << " ";
            total += grades[r][c];
        }
        average = total / rows;
        cout << "Average: " << average << endl;
        total = 0;
        average = 0.0;
    }
    Console::ReadKey();
    return 0;
}
```

该程序列序部分的输出为：

```text
Test Averages:
Test 1: 75 85 92 74 84 Average: 82
Test 2: 82 81 91 72 82 Average: 81
Test 3: 84 94 94 81 82 Average: 87
Test 4: 79 96 89 78 83 Average: 85
Test 5: 91 89 90 80 81 Average: 86
```

### 练习

- 1. 编写一个程序，从文件中读取 10 个单词，将它们存储到数组中，并显示单词长度的直方图。
- 2. 编写一个程序，将一系列字符存储到数组中。判断这些字符是否构成回文，回文是指正读和反读拼写相同的单词。例如，racecar 和 bob 都是回文。
- 3. 编写一个程序，将 10 个随机成绩存储到数组中。显示所有大于 80 的成绩。
- 4. 编写一个程序，将一年中的月份存储到数组中，提示用户输入月份编号，然后显示与该编号对应的月份。例如，1-一月、2-二月、3-三月，等等。
- 5. 下表列出了不同校区某些课程的注册学生人数。编写一个程序，将这些数据放入二维数组，并显示每个校区各课程注册的学生总数，以及选修每门课程的学生总数。

  |  | 课程 1 | 课程 2 | 课程 3 |
  |---|---|---:|---:|---:|
  | 校区 1 | 23 | 34 | 15 |
  | 校区 2 | 12 | 21 | 19 |
  | 校区 3 | 14 | 19 | 23 |

## 第 11 章

### 类与面向对象编程

我们在 C++ 中编写的程序，是对我们与世界中所存在对象进行交互的模拟。例如，薪资程序模拟公司如何运作，以及如何为员工所做的工作支付报酬。薪资程序的每个组成部分都代表一个对象。例如，员工有一张工时表，或称考勤卡，用来存储他或她在某个薪资周期内工作的小时数。员工还有薪水或时薪，这代表他们的薪酬标准。

在面向对象编程中，我们编写的程序所创建的对象，映射了我们试图模拟的对象。在 C++ 中，对象由类定义。类既包含对象属性或特性的定义，也包含对象行为的描述。例如，在描述一辆汽车时，我们会描述汽车的外观以及它如何运行或表现。在 C++ 中，我们可以通过创建和使用类与对象来做同样的事情。

除了定义对象的属性和行为之外，类还定义对象之间如何交互。通常，对象通过相互发送消息来交互。再次使用汽车的类比，如果一个 Person 对象想让一个 Automobile 对象行驶，Person 会向 Automobile 发送一条“踩油门踏板”消息。发送和接收消息的能力被定义为对象行为的一部分。

类的另一个显著特征是能够显示或隐藏构成类的属性和行为。任何属性或行为都可以暴露给其他对象，也可以隐藏起来，使其他对象无法访问该属性或行为。这一特性称为封装，也是面向对象编程被证明如此成功的原因之一。

在实践中，可以把类视为一种用户定义类型。能够扩展编程语言可处理的类型，是编程语言的一项关键特性。

