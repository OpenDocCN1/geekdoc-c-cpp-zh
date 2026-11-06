

```cpp
// Fig. 4.6: Student.h
// Student class that stores a student name and average.
#include <string>

class Student {
public:
   // constructor initializes data members
   Student(std::string studentName, int studentAverage)
      : name(studentName) {

      // sets average data member if studentAverage is valid
      setAverage(studentAverage);
   }

   // sets the Student's name
   void setName(std::string studentName) {
      name = studentName;
   }

   // retrieves the Student's name
   std::string getName() const {
      return name;
   }

   // sets the Student's average
   void setAverage(int studentAverage) {
      // validate that studentAverage is > 0 and <= 100; otherwise,
      // keep data member average's current value
      if (studentAverage > 0)
         if (studentAverage <= 100) {
            average = studentAverage; // assign to data member
         }
   }

   // retrieves the Student's average
   int getAverage() const {
      return average;
   }

   // determines and returns the Student's letter grade
   std::string getLetterGrade() const {
      // initialized to empty string by class string's constructor
      std::string letterGrade;

      if (average >= 90) {
         letterGrade = "A";
      }
      else if (average >= 80) {
         letterGrade = "B";
      }
      else if (average >= 70) {
         letterGrade = "C";
      }
      else if (average >= 60) {
         letterGrade = "D";
      }
      else {
         letterGrade = "F";
      }

      return letterGrade;
   }

private:
   std::string name;
   int average{0}; // initialize average to 0
}; // end class Student
```

**图 4.6** 存储学生姓名和平均成绩的 `Student` 类。

## `StudentTest` 类

为了演示类 `Student` 的 `getLetterGrade` 成员函数中嵌套的 `if...else` 语句，`main` 函数（**图 4.7**）创建了两个 `Student` 对象（第 8-9 行）。接下来，第 11-16 行分别调用对象的 `getName`、`getAverage` 和 `getLetterGrade` 成员函数，显示每个 `Student` 的姓名、平均成绩和字母等级。

```cpp
// Fig. 4.7: StudentTest.cpp
// Create and test Student objects.
#include <iostream>
#include "Student.h"
using namespace std;

int main() {
    Student account1{"Jane Green", 93};
    Student account2{"John Blue", 72};

    cout << account1.getName() << "'s letter grade equivalent of "
         << account1.getAverage() << " is: "
         << account1.getLetterGrade() << "\n";
    cout << account2.getName() << "'s letter grade equivalent of "
         << account2.getAverage() << " is: "
         << account2.getLetterGrade() << endl;
}
```

```text
Jane Green's letter grade equivalent of 93 is: A
John Blue's letter grade equivalent of 72 is: C
```

**图 4.7** 创建并测试 `Student` 对象。

## 4.8 `while` 迭代语句

迭代语句允许你指定程序在某个条件保持为*真*时重复执行某个动作。伪代码语句

```text
While there are more items on my shopping list
    Purchase next item and cross it off my list
```

这描述了购物过程中的迭代。条件“购物清单上还有更多物品”可能为*真*或*假*。若为*真*，则执行动作“购买下一件物品并将其从清单上划掉”。只要条件保持为*真*，该动作就会*重复*执行。*While* 迭代语句中包含的一条或多条语句构成其循环体，循环体可以是单条语句，也可以是一个语句块。最终，条件会变为*假*（当购物清单上的最后一件物品被购买并划掉时）。此时，迭代终止，并执行迭代语句之后的第一条语句。

作为 C++ 的 `while` **迭代语句**的一个示例，考虑一段查找第一个大于 100 的 3 的幂的程序。执行下面的 `while` 语句后，变量 `product` 将包含结果：

```cpp
{
    int product{3};

    while (product <= 100) {
        product = 3 * product;
    }
}
```

`while` 语句的每次迭代都将 `product` 乘以 3，因此 `product` 依次取值 9、27、81 和 243。当 `product` 变为 243 时，`product <= 100` 变为*假*。这会终止迭代，因此 `product` 的最终值为 243。此时，程序继续执行 `while` 语句之后的下一条语句。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_425_0.png)

## 常见编程错误

*如果 `while` 语句的循环体中没有提供最终使 `while` 中的条件变为假的动作，会导致一种称为**无限循环**的逻辑错误（循环永不终止）。*

## `while` 语句的 UML 活动图

**图 4.8** 中的 UML 活动图展示了前面 `while` 语句的控制流。与之前一样，图中的符号（除了初始状态、转移箭头、一个最终状态和三个注释）表示一个动作状态和一个决策。此图引入了 UML 的**合并符号**。UML 将**合并符号**和决策符号都表示为菱形。合并符号将两条活动流合并为一条。在此图中，合并符号连接来自初始状态和动作状态的转移，使两者都流入决策，该决策确定循环是否应开始（或继续）执行。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_426_0.png)

**图 4.8** `while` 迭代语句的 UML 活动图。

决策符号和合并符号可以通过“传入”和“传出”转移箭头的数量来区分。决策符号有*一个*指向菱形的转移箭头，以及*两个或更多*从菱形指出的转移箭头，以表示从该点可能的转移。此外，每个从决策符号指出的转移箭头旁边都有一个守卫条件。合并符号有两个或更多指向菱形的转移箭头，且只有一个从菱形指出的转移箭头，表示多条活动流合并后继续活动。与合并符号关联的转移箭头均没有守卫条件。

**图 4.8** 清楚地显示了本节前面讨论的 `while` 语句的迭代过程。从动作状态伸出的转移箭头指回合并符号，程序流从那里转移回决策，该决策在循环的每次迭代开始时进行测试。循环继续执行，直到守卫条件 `product > 100` 变为*真*。然后 `while` 语句退出（到达其最终状态），控制权传递给程序中按顺序排列的下一条语句。

## 4.9 制定算法：计数器控制的迭代

为了说明算法是如何开发的，我们解决一个求学生平均成绩问题的两个变体。考虑以下问题描述：

- *一个由十名学生组成的班级进行了一次测验。你可以获得这次测验的成绩（0-100 范围内的整数）。计算班级的测验平均分。*

班级平均分等于成绩总和除以学生人数。在计算机上解决此问题的算法必须输入每个成绩、跟踪所输入所有成绩的总和、执行平均计算并打印结果。

### 4.9.1 使用计数器控制迭代的伪代码算法

让我们使用伪代码列出要执行的动作，并指定它们的执行顺序。我们使用**计数器控制的迭代**一次输入一个成绩。此技术使用一个称为**计数器**（或**控制变量**）的变量来控制一组语句的执行次数。计数器控制的迭代通常被称为**定次迭代**，因为迭代次数在循环开始执行*之前*就是已知的。在此示例中，当计数器超过 10 时迭代终止。本节给出了一个完整的伪代码算法（[图 4.9]）以及一个实现该算法的相应 C++ 程序（[图 4.10]）。在[第 4.10 节]中，我们演示如何从头开发伪代码算法。

1. 将总和设为 0
2. 将成绩计数器设为 1
3. 
4. *当成绩计数器小于等于十时*
5. &nbsp;&nbsp;&nbsp;提示用户输入下一个成绩
6. &nbsp;&nbsp;&nbsp;输入下一个成绩
7. &nbsp;&nbsp;&nbsp;将该成绩加入总和
8. &nbsp;&nbsp;&nbsp;将成绩计数器加一
9. 
10. 将班级平均分设为总和除以十
11. 打印班级平均分

**图 4.9** 使用计数器控制的伪代码算法

