
因此，编译器解释为 `row` 指向一个包含三个 `int` 值的三元素数组（再次强调，`columns` 为 3）。`row` 声明中的 `const& row` 表明该引用不能用于修改行，并防止每行都拷贝复制到范围中。内部范围变量 `element` 使用由 `row` 所代表的数组中的一个元素进行初始化，因此编译器解释为 `element` 指向一个 `int` 类型，因为每行都包含三个 `int` 值。在 IDE 中，你通常可以将鼠标悬停在用 `auto` 声明的变量上，IDE 将显示推断出的类型。第 28 行显示了给定行和列的值。

## 嵌套的计数器控制 for 语句

我们按照如下方式实现了计数器控制迭代的嵌套循环：

```cpp
for (size_t row=0; row < a.size(); ++row) {
    for (size_t column=0; column < a[row].size(); ++column) {
        cout << a[row][column] << ' ';
    }
    cout << endl;
}
```

## 其他常见的二维数组操作

以下语句将图 7.16 中数组 `a` 的第 2 行的所有元素置为零：

```cpp
for (size_t column=0; column < 4; ++column) {
    a[2][column] = 0;
}
```

该语句仅改变了第二个下标（即列下标）。之前的语句等于以下赋值语句：

```cpp
a[2][0] = 0;
a[2][1] = 0;
a[2][2] = 0;
a[2][3] = 0;
```

以下嵌套计数器控制语句确定了图 7.16 中数组 `a` 中所有元素的总和：

```cpp
total = 0;
for (size_t row=0; row < a.size(); ++row) {
    for (size_t column=0; column < a[row].size(); ++column) {
        total += a[row][column];
    }
}
```

该语句一次计算一个数组行的总和。外部语句首先将 `row`（即行下标）设置为 0，因此第 0 行的元素由内部语句计算总和。然后，外部语句将 `row` 增加到 1，因此可以计算第 1 行元素的总和。接着，外部语句将 `row` 增加到 2，因此可以计算第 2 行元素的总和。当嵌套语句结束时，`total` 包含所有数组元素的和。此嵌套循环可以使用基于范围的 for 语句实现：

```cpp
total = 0;
for (auto row : a) { // 对于每一行
    for (auto column : row) { // 对于每行中的每一列
        total += column;
    }
}
```

## 7.9 案例：使用二维数组的 GradeBook 类

在第 7.6 节中，我们展示了 `GradeBook` 类（图 7.13），它使用一维数组来存储学生单次考试的成绩。在大多数学期中，学生都会参加考试。教授可能会分析整个学期的成绩，包括针对单个学生以及针对整个班级。

### 在 GradeBook 类在二维数组中存储学生成绩

图 7.18 显示了汇总 10 名学生在三次考试中成绩的输出。我们在 `GradeBook` 类下一个版本的对象（图 7.19）中将成绩以二维数组的形式存储。数组的每行代表一个学生整个课程的成绩，每列列代表学生在特定某次考试中获得的成绩。客户端程序（如图 7.20 所示）将数组作为参数传递给 `GradeBook` 构造函数。由于有 10 个学生和三次考试，我们使用十行三列的数组来存储成绩。

![](img/09cee61886647f0b1e06dc44c0065a38_351_0.png)

**图 7.18** | 使用二维数组的 `GradeBook` 输出。（第一部分，共 2 部分）。

| 范围 | 计数 |
| :--- | :--- |
| 20-29: | |
| 30-39: | |
| 40-49: | |
| 50-59: | |
| 60-64: | ****** |
| 70-79: | ******* |
| 80-89: | ******** |
| 90-99: | *** |
| 100: | *** |

**图 7.18** 使用二维数组的 `GradeBook` 输出。

```cpp
#include <array>
#include <string>
#include <iostream>
#include <iomanip>
// 7.19: GradeBook.h
// 定义 GradeBook 类
// 使用二维数组存储测试成绩
class GradeBook {
public:
    // 静态常量
    static const size_t students = 10;
    static const size_t tests = 3;
    // 构造函数
    GradeBook(const std::string& name, const std::array<std::array<int, tests>, students>& a);
    // 成员函数
    std::string getName() const;
    int getGrade(size_t row, size_t column) const;
    double getAverage(const std::array<int, tests>& setGrades) const;
    void outputGrades() const;
    void outputChart() const;
private:
    std::string name;
    std::array<std::array<int, tests>, students> grades;
};
```

```cpp
// 7.19: GradeBook.cpp
#include "GradeBook.h"
// 构造函数
GradeBook::GradeBook(const std::string& name, const std::array<std::array<int, tests>, students>& a)
    : name(name), grades(a) {}
// 获取名称
std::string GradeBook::getName() const {
    return name;
}
// 获取特定成绩
int GradeBook::getGrade(size_t row, size_t column) const {
    return grades[row][column];
}
// 计算一组成绩的平均分
double GradeBook::getAverage(const std::array<int, tests>& setGrades) const {
    int total{0};
    for (int grade : setGrades) {
        total += grade;
    }
    return static_cast<double>(total) / setGrades.size();
}
// 输出成绩
void GradeBook::outputGrades() const {
    std::cout << "\nthe grades are:\n";
    for (size_t row = 0; row < students; ++row) {
        std::cout << name << " ";
        for (size_t column = 0; column < tests; ++column) {
            std::cout << grades[row][column] << "\t";
        }
        std::cout << std::endl;
    }
}
// 输出成绩分布图表
void GradeBook::outputChart() const {
    std::cout << "overall grade distribution:" << std::endl;
    // 存储 10 个范围的频率
    std::array<unsigned int, 10> frequency{}; // 初始化为 0
    // 对于每个学生的成绩，增加频率
    for (auto const& student : grades) {
        for (auto const& test : student) {
            frequency[test / 10]++;
        }
    }
    // 对于每个范围，打印频率、图表
    for (size_t count = 0; count < frequency.size(); ++count) {
        // 输出图表 "0-9", ..., "90-99", "100"
        if (count == 0) {
            std::cout << " 0-9: ";
        } else if (count < 10) {
            std::cout << count * 10 << "-" << (count * 10) + 9 << ": ";
        }
        // 打印星号
        for (unsigned int stars = 0; stars < frequency[count]; ++stars) {
            std::cout << "*";
        }
        std::cout << std::endl; // 换行
    }
}
```

```cpp
// main.cpp
#include "GradeBook.h"
int main() {
    std::array<std::array<int, 3>, 10> classGrades = {{
        {{90, 85, 88}},
        {{80, 92, 85}},
        {{70, 75, 80}},
        {{95, 98, 92}},
        {{60, 70, 65}},
        {{88, 87, 89}},
        {{92, 91, 93}},
        {{78, 75, 70}},
        {{85, 80, 82}},
        {{99, 97, 95}}
    }};
    GradeBook book("Class A", classGrades);
    book.outputGrades();
    book.outputChart();
    return 0;
}
```

## 7.9 案例研究：使用二维数组的 GradeBook 类

```cpp
// 为每个测试创建一个列标题
for (size_t test=0; test < tests; ++test) {
    std::cout << "Test " << test + 1 << " ";
}
```

```cpp
std::cout << "Average" << std::endl;
```

```cpp
// 创建代表数组分数的文本行/列
for (size_t student=0; student < grades.size(); ++student) {
    std::cout << "Student " << std::setw(2) << student + 1;
```

```cpp
// 输出学生的成绩
for (size_t test=0; test < grades[student].size(); ++test) {
    std::cout << std::setw(8) << grades[student][test];
}
```

```cpp
// 调用成员函数 getAverage 计算学生的
// 平均分：将一行成绩作为参数传递
double average = getAverage(grades[student]);
std::cout << std::setw(3) << std::setprecision(2) << std::fixed
    << average << std::endl;
```

```cpp
private:
    std::string courseName; // 该成绩单的课程名称
    std::array<std::array<int, tests>, students> grades; // 二维数组
```

图 7.19 | GradeBook 类的定义，使用二维数组存储测试成绩。（4 部分，共 4 部分）

## GradeBook 函数概述

GradeBook 的每个成员函数都与其早先一维数组版本的 GradeBook 中的对应函数相似（图 7.13）。成员函数 `getMinimum`（图 7.13 的第 52–66 行）确定了本学期所有学生中的最低分。成员函数 `getMaximum`（第 69–83 行）确定了本学期所有学生中的最高分。成员函数 `getAverage`（第 86–96 行）确定了特定学生的学期平均分。成员函数 `outputBarChart`（第 99–132 行）输出本学期所有学生成绩分布的柱状图。成员函数 `outputGrades`（第 135–161 行）以表格格式输出二维数组以及每个学生的学期平均分。

## getMinimum 和 getMaximum 函数

成员函数 `getMinimum`、`getMaximum`、`outputBarChart` 和 `outputGrades` 通过嵌套的范围 for 循环或计数器控制的语句遍历 `grades` 数组。例如，考虑成员函数 `getMinimum` 中的嵌套语句（第 56–63 行）。外部语句遍历代表每个学生的行，内部循环遍历给定学生的成绩。在内部语句的体中，每个成绩都与变量 `lowGrade` 进行比较。如果某个成绩小于 `lowGrade`，则将 `lowGrade` 设置为该成绩。这个过程一直持续，直到遍历完所有成绩行和列。当嵌套语句执行完成后，`lowGrade` 包含二维数组中的最小分数。成员函数 `getMaximum` 的工作方式与 `getMinimum` 类似。

# 第 7 章 类模板：array 和 vector：捕获异常

## outputBarChart 函数

图 7.19 中的成员函数 `outputBarChart` 与图 7.13 中的函数几乎相同。然而，为了输出整个学期的整体分布情况，该函数使用了嵌套 for 语句（图 7.19 的第 107–111 行），根据二维数组中的所有成绩来增加一维数组 `frequency` 的元素。两个 `outputBarChart` 成员函数中的其余代码是相同的。

## outputGrades 函数

成员函数 `outputGrades`（第 135–161 行）使用嵌套的计数器控制 for 语句输出 `grades` 数组的值，以及每个学生的学期平均分。图 7.18 中的输出显示了结果，它类似于教授物理成绩单的表格格式。第 140–142 行打印每个测试的列标题。我们使用计数器控制的 for 循环以便数字识别每个学生。同样，第 147–160 行的 for 语句首先使用计数变量输出行标签以识别学生（第 148 行）。数组索引从 0 开始，第 141 行和 148 行输出 +1 和 `student +1`，以产生从 1 开始的测试编号和学生编号（见图 7.18）。图 7.19 中第 151–153 行的内部语句使用外部 for 语句的计数器变量来遍历 `grades` 数组的特定行，并输出每个学生的测试成绩。最后，第 157 行通过将当前行的成绩（即 `grades[student]`）传递给成员函数 `getAverage` 来输出每个学生的学期平均分。

## getAverage 函数

成员函数 `getAverage`（第 88–96 行）接受一个特定学生的一维测试数组作为参数。当第 155 行调用 `getAverage` 时，第一个参数 `grades[student]` 指定了将二维数组的某一行传递给 `getAverage`。根据图 7.20 中创建的数组，参数 `grades[1]` 代表存储在二维数组 `grades` 第 1 行的三个值（一个一维成绩数组）。二维数组的行是一维的。成员函数 `getAverage` 计算数组元素的和，将其除以测试次数，并将浮点结果作为 `double` 类型返回（图 7.19，第 95 行）。

## 测试 GradeBook 类

图 7.20 中的程序使用第 9–19 行声明并初始化的 `int` 二维数组创建 `GradeBook` 类对象（图 7.19）。第 20 行访问 GradeBook 的静态常量和测试次数，以指示每个成绩数组的大小。第 21 行将课程名称和成绩传递给 GradeBook 构造函数。第 22–23 行调用 `myGradeBook` 的 `displayMessage` 和 `processGrades` 成员函数，分别显示欢迎消息和获取学生成绩报告。

## 7.10 C++ 标准库类模板 vector

```cpp
// 7.20: fig07_20.cpp
// 使用二维数组创建 GradeBook 对象
#include <array>
#include "GradeBook.h" // GradeBook 类定义
using namespace std;
int main() {
```
