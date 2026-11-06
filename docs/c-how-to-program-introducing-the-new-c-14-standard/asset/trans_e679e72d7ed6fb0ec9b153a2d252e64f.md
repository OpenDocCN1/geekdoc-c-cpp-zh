

变量 `row` 使用参数 `a` 中的一个元素进行初始化。

查看 `array` 的声明，可以看到该 `array` 包含以下类型的元素：

```cpp
array<int, columns>
```

因此，编译器推断出 `row` 引用的是一个包含三个 `int` 值的 `array`（同样，`columns` 的值为 3）。`row` 声明中的 `const&` 表明不能通过该引用修改行，同时也可以避免将每一行*复制*到范围变量中。内层循环的范围变量 `element` 使用 `row` 所表示的 `array` 中的一个元素进行初始化，因此编译器推断出 `element` 引用的是一个 `int`，因为每一行都包含三个 `int` 值。在 IDE 中，通常可以将鼠标悬停在使用 `auto` 声明的变量上，IDE 会显示该变量推断出的类型。第 28 行显示给定行和列中的值。

## 嵌套计数控制的 `for` 语句

我们也可以使用计数控制迭代来实现嵌套循环，如下所示：

```cpp
for (size_t row{0}; row < a.size(); ++row) {
    for (size_t column{0}; column < a[row].size(); ++column) {
        cout << a[row][column] << ' ';
    }

    cout << endl;
}
```

## 其他常见的二维 `array` 操作

下面的 `for` 语句将**图 7.16**中 `array a` 的第 2 行的所有元素设置为零：

```cpp
for (size_t column{0}; column < 4; ++column) {
    a[2][column] = 0;
}
```

该 `for` 语句只改变第二个下标（即列下标）。前面的 `for` 语句等价于以下赋值语句：

```cpp
a[2][0] = 0;
a[2][1] = 0;
a[2][2] = 0;
a[2][3] = 0;
```

下面的嵌套计数控制 `for` 语句计算**图 7.16**中 `array a` 的所有元素之和：

```cpp
total = 0;
for (size_t row{0}; row < a.size(); ++row) {
    for (size_t column{0}; column < a[row].size(); ++column) {
        total += a[row][column];
    }
}
```

该 `for` 语句逐行计算 `array` 中元素的总和。外层 `for` 语句首先将 `row`（即行下标）设置为 `0`，这样内层 `for` 语句就可以计算第 0 行元素的总和。随后，外层 `for` 语句将 `row` 自增为 `1`，于是可以计算第 1 行元素的总和。接着，外层 `for` 语句将 `row` 自增为 `2`，于是可以计算第 2 行元素的总和。当嵌套的 `for` 语句终止时，`total` 中包含所有 `array` 元素的总和。这个嵌套循环也可以使用基于范围的 for 语句实现：

```cpp
total = 0;
for (auto row : a) { // for each row
    for (auto column : row) { // for each column in row
        total += column;
    }
}
```

## 7.9 案例研究：使用二维 `array` 的 `GradeBook` 类

在**第 7.6 节**中，我们介绍了 `GradeBook` 类（**图 7.13**），该类使用一维 `array` 存储学生在一次考试中的成绩。在大多数学期中，学生需要参加多次考试。教师可能希望分析整个学期的成绩，既包括单个学生的成绩，也包括全班学生的整体成绩。

### 在 `GradeBook` 类中使用二维 `array` 存储学生成绩

**图 7.18**显示了汇总 10 名学生三次考试成绩的输出结果。我们将成绩作为二维 `array` 存储在下一版本的 `GradeBook` 类（**图 7.19**）的对象中。`array` 的每一行表示一名学生在整个课程中的成绩，每一列表示所有学生在某一次特定考试中取得的成绩。客户端程序（例如**图 7.20**）将该 `array` 作为参数传递给 `GradeBook` 构造函数。由于有 10 名学生和三次考试，因此我们使用一个十行三列的 `array` 来存储成绩。

欢迎使用以下课程的成绩册：
CS101 C++ 编程基础！

成绩如下：

| 学生 | 测试 1 | 测试 2 | 测试 3 | 平均分 |
|---|---:|---:|---:|---:|
| 学生 1 | 87 | 96 | 70 | 84.33 |
| 学生 2 | 68 | 87 | 90 | 81.67 |
| 学生 3 | 94 | 100 | 90 | 94.67 |
| 学生 4 | 100 | 81 | 82 | 87.67 |
| 学生 5 | 83 | 65 | 85 | 77.67 |
| 学生 6 | 78 | 87 | 65 | 76.67 |
| 学生 7 | 85 | 75 | 83 | 81.00 |
| 学生 8 | 91 | 94 | 100 | 95.00 |
| 学生 9 | 76 | 72 | 84 | 77.33 |
| 学生 10 | 87 | 93 | 73 | 84.33 |

成绩册中的最低成绩为 65  
成绩册中的最高成绩为 100

```text
Overall grade distribution:
  0-9:
 10-19:
 20-29:
 30-39:
 40-49:
 50-59:
 60-69: ***
 70-79: *****
 80-89: **********
 90-99: *********
    100: ***
```

图 7.18 使用二维 `array` 的 `GradeBook` 的输出结果。

```cpp
// Fig. 7.19: GradeBook.h
// Definition of class GradeBook that uses a
// two-dimensional array to store test grades.
#include <array>
#include <string>
#include <iostream>
#include <iomanip> // parameterized stream manipulators

// GradeBook class definition
class GradeBook {
public:
   // constants
   static const size_t students{10}; // number of students
   static const size_t tests{3}; // number of tests

   // two-argument constructor initializes courseName and grades array
   GradeBook(const std::string& name,
      std::array<std::array<int, tests>, students>& gradesArray)
      : courseName(name), grades(gradesArray) {
   }

   // function to set the course name
   void setCourseName(const std::string& name) {
      courseName = name; // store the course name
   }

   // function to retrieve the course name
   const std::string& getCourseName() const {
      return courseName;
   }

   // display a welcome message to the GradeBook user
   void displayMessage() const {
      // call getCourseName to get this GradeBook’s course name
      std::cout << "Welcome to the grade book for\n" << getCourseName()
         << "." << std::endl;
   }

   // perform various operations on the data
   void processGrades() const {
      outputGrades(); // output grades array

// call functions getMinimum and getMaximum
std::cout << "\nLowest grade in the grade book is " << getMinimum()
          << "\nHighest grade in the grade book is " << getMaximum()
          << std::endl;

outputBarChart(); // display grade distribution chart
}

// find minimum grade in the entire gradebook
int getMinimum() const {
    int lowGrade{100}; // assume lowest grade is 100

    // loop through rows of grades array
    for (auto const& student : grades) {
        // loop through columns of current row
        for (auto const& grade : student) {
            if (grade < lowGrade) { // if grade is lower than lowGrade
                lowGrade = grade; // grade is new lowest grade
            }
        }
    }

    return lowGrade; // return lowest grade
}

// find maximum grade in the entire gradebook
int getMaximum() const {
    int highGrade{0}; // assume highest grade is 0

    // loop through rows of grades array
    for (auto const& student : grades) {
        // loop through columns of current row
        for (auto const& grade : student) {
            if (grade > highGrade) { // if grade is higher than highGrade
                highGrade = grade; // grade is new highest grade
            }
        }
    }

    return highGrade; // return highest grade
}

// determine average grade for particular set of grades
double getAverage(const std::array<int, tests>& setOfGrades) const {
   int total{0}; // initialize total

   // sum grades in array
   for (int grade : setOfGrades) {
      total += grade;
   }

   // return average of grades
   return static_cast<double>(total) / setOfGrades.size();
}

// output bar chart displaying grade distribution
void outputBarChart() const {
   std::cout << "\nOverall grade distribution:" << std::endl;

   // stores frequency of grades in each range of 10 grades
   const size_t frequencySize{11};
   std::array<unsigned int, frequencySize> frequency{}; // init to 0s

   // for each grade, increment the appropriate frequency
   for (auto const& student : grades) {
      for (auto const& test : student) {
         ++frequency[test / 10];
      }
   }

   // for each grade frequency, print bar in chart
   for (size_t count{0}; count < frequencySize; ++count) {
      // output bar label ("0-9", ..., "90-99", "100"):
      if (0 == count) {
         std::cout << "  0-9: ";
      }
      else if (10 == count) {
         std::cout << "   100: ";
      }
      else {
         std::cout << count * 10 << "-" << (count * 10) + 9 << ": ";
      }
   }
```

