
初始化。

## 7.5 基于范围的 `for` 语句

如我们所示，处理`array`的*所有*元素是很常见的。C++11 的**基于范围的`for`语句**允许你*在不使用计数器*的情况下做到这一点，从而避免了“超出”`array`边界的可能性，并且无需自己实现边界检查。**图7.11**使用基于范围的`for`来显示`array`的内容（第12–14行和第23–25行），并将`array`的每个元素值乘以2（第17–19行）。

![](img/eaad0ad48f0d708c37231c1ca852bf6cf9_924_0.png)

### 错误预防提示 7.2

*当处理`array`的所有元素时，如果不需要访问`array`元素的下标，请使用基于范围的`for`语句。*

```cpp
// Fig. 7.11: fig07_11.cpp
// Using range-based for to multiply an array's elements by 2.
#include <iostream>
#include <array>
using namespace std;

int main() {
   array<int, 5> items{1, 2, 3, 4, 5};

   // display items before modification
   cout << "items before modification: ";
   for (int item : items) {
      cout << item << " ";
   }

   // multiply the elements of items by 2
   for (int& itemRef : items) {
      itemRef *= 2;
   }

   // display items after modification
   cout << "\nitems after modification: ";
   for (int item : items) {
      cout << item << " ";
   }

   cout << endl;
}
```

```text
items before modification: 1 2 3 4 5
items after modification: 2 4 6 8 10
```

图7.11 使用基于范围的`for`将`array`的元素乘以2。

### 使用基于范围的`for`显示`array`的内容

基于范围的`for`语句简化了遍历`array`的代码。第12行可读作“每次迭代，将`items`的下一个元素赋值给`int`变量`item`，然后执行循环体。”因此，在每次迭代中，`item`表示`items`中的一个元素*值*（而非下标）。在基于范围的`for`的头部，你在冒号（`:`）左侧声明一个所谓的范围变量，并在右侧指定一个数组的名称。你可以将基于范围的`for`语句用于C++标准库中大多数预构建的数据结构（通常称为*容器*）。第12–14行等同于以下计数器控制的迭代：

```cpp
for (int counter(0); counter < items.size(); ++counter) {
    cout << items[counter] << " ";
}
```

### 使用基于范围的`for`修改`array`的内容

第17–19行使用基于范围的`for`语句将`items`的每个元素乘以2。在第17行，范围变量的声明表明`itemRef`是一个`int&`——即一个*引用*。回想一下，引用是内存中另一个变量的别名——在此例中，是`array`的一个元素。我们使用`int`引用，因为`items`包含`int`值，并且我们希望*修改*每个元素的值——由于`itemRef`被声明为*引用*，你对`itemRef`所做的任何更改都会更改`array`中相应的元素值。

### 使用元素的下标

只要循环遍历`array`的代码*不*需要访问元素的下标，就可以使用基于范围的`for`语句代替计数器控制的`for`语句。例如，对`array`中的整数求和（如图7.6所示）只需要访问元素值——元素的下标无关紧要。然而，如果程序必须使用下标，而不是仅仅为了遍历`array`（例如，像本章前面的示例那样在每个`array`元素值旁边打印下标编号），则应使用计数器控制的`for`语句。

## 7.6 案例研究：使用`array`存储成绩的`GradeBook`类

我们现在介绍案例研究的第一部分，该案例研究开发一个`GradeBook`类，教师可以用它来维护学生在一次考试中的成绩，并显示一份成绩报告，其中包含成绩、班级平均分、最低分、最高分和成绩分布条形图。本节介绍的`GradeBook`类版本将一次考试的成绩存储在一维数组中。在**7.9节**中，我们将介绍一个使用二维数组存储学生在*多次*考试中的成绩的`GradeBook`类版本。

### 在类`GradeBook`中把学生成绩存储在`array`中

**图7.12**显示了汇总10个成绩的输出，这些成绩存储在`GradeBook`类的一个对象（**图7.13**）中，该对象使用一个整数`array`存储10名学生在一次考试中的成绩。`grades`数组在第142行被声明为一个数据成员——因此，每个`GradeBook`对象都维护自己的成绩集。

```text
Welcome to the grade book for
CS101 Introduction to C++ Programming!

The grades are:

Student  1:  87
Student  2:  68
Student  3:  94
Student  4: 100
Student  5:  83
Student  6:  78
Student  7:  85
Student  8:  91
Student  9:  76
Student 10:  87

Class average is 84.90
Lowest grade is 68
Highest grade is 100

Grade distribution:
  0-9:
10-19:
20-29:
30-39:
40-49:
50-59:
60-69: *
70-79: ***
80-89: ****
90-99: **
   100: *
```

图7.12 在`array`中存储成绩的`GradeBook`示例的输出。

```cpp
// Fig. 7.13: GradeBook.h
// Definition of class GradeBook that uses an array to store test grades.
#include <string>
#include <array>
#include <iostream>
#include <iomanip> // parameterized stream manipulators

// GradeBook class definition
class GradeBook {
public:
   // constant number of students who took the test
   static const size_t students = 10; // note public data

   // constructor initializes courseName and grades array
   GradeBook(const std::string& name,
      const std::array<int, students>& gradesArray)
      : courseName{name}, grades{gradesArray} {
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
      // call getCourseName to get the name of this GradeBook's course
      std::cout << "Welcome to the grade book for\n" << getCourseName()
         << "!" << std::endl;
   }

   // perform various operations on the data (none modify the data)
   void processGrades() const {
      outputGrades(); // output grades array

      // call function getAverage to calculate the average grade
      std::cout << std::setprecision(2) << std::fixed;
      std::cout << "\nClass average is " << getAverage() << std::endl;

      // call functions getMinimum and getMaximum
      std::cout << "Lowest grade is " << getMinimum()
         << "\nHighest grade is " << getMaximum() << std::endl;
      outputBarChart(); // display grade distribution chart
   }

   // find minimum grade
   int getMinimum() const {
      int lowGrade{100}; // assume lowest grade is 100

      // loop through grades array
      for (int grade : grades) {
         // if current grade lower than lowGrade, assign it to lowGrade
         if (grade < lowGrade) {
            lowGrade = grade; // new lowest grade
         }
      }

      return lowGrade; // return lowest grade
   }

   // find maximum grade
   int getMaximum() const {
      int highGrade{0}; // assume highest grade is 0

      // loop through grades array
      for (int grade : grades) {
         // if current grade higher than highGrade, assign it to highGrade
         if (grade > highGrade) {
            highGrade = grade; // new highest grade
         }
      }

      return highGrade; // return highest grade
   }

   // determine average grade for test
   double getAverage() const {
      int total{0}; // initialize total

      // sum grades in array
      for (int grade : grades) {
         total += grade;
      }

      // return average of grades
      return static_cast<double>(total) / grades.size();
   }
}
```
