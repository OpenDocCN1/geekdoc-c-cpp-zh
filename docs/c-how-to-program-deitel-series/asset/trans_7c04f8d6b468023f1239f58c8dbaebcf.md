

## 成员函数 `getMinimum` 和 `getMaximum`

processGrades 中的第 48～49 行调用成员函数 getMinimum 和 getMaximum，分别确定考试中任何学生的最高成绩和最低成绩。让我们来看成员函数 getMinimum 如何找到最低成绩。因为允许的最高成绩是 100，所以我们首先假设 100 就是最低成绩（第 58 行）。然后，我们将数组中的每个元素与最低成绩进行比较，寻找更小的值。成员函数 getMinimum 中的第 61～66 行遍历数组，第 64 行将每个成绩与 lowGrade 进行比较。如果某个成绩小于 lowGrade，则将 lowGrade 设置为该成绩。当第 68 行执行时，lowGrade 包含数组中的最低成绩。成员函数 getMaximum（第 72～85 行）的工作方式与成员函数 getMinimum 类似。

## 成员函数 `outputBarChart`

最后，成员函数 processGrades 中的第 52 行调用成员函数 outputBarChart，使用与图 7.9 类似的技术打印成绩数据的分布图。在那个示例中，我们只需查看一组成绩，就手动计算了每个类别（即 0～9、10～19、...、90～99 和 100）中的成绩数量。在本例中，第 110～111 行使用与图 7.10 和图 7.11 类似的技术来计算每个类别中成绩出现的频率。第 107 行声明并创建了一个由 11 个 unsigned int 组成的数组 frequency，用来存储每个类别中成绩的频率。对于数组 grades 中的每个成绩，第 110～111 行会递增 frequency 数组中相应的元素。为了确定要递增哪个元素，第 111 行使用整数除法将当前成绩除以 10。例如，如果成绩为 85，第 111 行会递增 frequency[8]，以更新 80～89 范围内的成绩计数。接下来，第 114～129 行根据数组 frequency 中的值打印条形图（见图 7.17）。与图 7.9 中的第 28～29 行类似，图 7.16 中的第 125～126 行使用数组 frequency 中的值来确定每个条形中显示的星号数量。

## 测试类 `GradeBook`

图 7.17 中的程序使用 int 数组 grades（在第 11～12 行声明并初始化）创建类 GradeBook（图 7.15～7.16）的一个对象。表达式“GradeBook::students”（第 11 行）中使用了作用域解析运算符（`::`）来访问类 GradeBook 的静态常量 students。我们在此使用这个常量来创建一个数组，其大小与类 GradeBook 中作为数据成员存储的数组相同。第 13 行声明了一个表示课程名称的 string。第 15 行将课程名称和成绩数组传递给 GradeBook 构造函数。第 16 行显示欢迎消息，第 17 行调用 GradeBook 对象的 processGrades 成员函数。

```cpp
// Fig. 7.17: fig07_17.cpp
// Creates a GradeBook object using an array of grades.
#include <array>
#include "GradeBook.h" // GradeBook class definition
using namespace std;

// function main begins program execution
int main()
{
   // array of student grades
   const array<int, GradeBook::students> grades =
      { 87, 68, 94, 100, 83, 78, 85, 91, 76, 87 };
   string courseName = "CS101 Introduction to C++ Programming";

   GradeBook myGradeBook( courseName, grades );
   myGradeBook.displayMessage();
   myGradeBook.processGrades();
} // end main
```

**图 7.17** | 使用成绩数组创建 GradeBook 对象，然后调用成员函数 processGrades 对其进行分析。（第 1 部分，共 2 部分。）

![](img/b42ba5cd262b1358d16610173f975e4d_337_0.png)

## 7.7 数组的排序与查找

在本节中，我们使用内置的 C++ 标准库 **sort** 函数将数组中的元素按升序排列，并使用内置的 **binary_search** 函数确定数组中是否存在某个值。

### 排序

**排序**数据——将其按升序或降序排列——是最重要的计算应用之一。银行按账号对所有支票排序，以便在每个月末准备个人银行对账单。电话公司按姓氏对电话簿排序；在姓氏*相同*的所有条目中，再按名字排序，以便轻松找到电话号码。实际上，每个组织都必须对某些数据进行排序，而且在许多情况下，数据量非常庞大。排序数据是一个引人入胜的问题，吸引了计算机科学领域一些最深入的研究工作。在第 20 章中，我们将研究并实现几种排序方案，讨论它们的性能，并介绍用于描述每种方案完成任务所需工作量的 Big O（读作“Big Oh”）表示法。

### 查找

通常可能需要确定数组中是否包含与某个**键值**匹配的值。查找数组中特定元素的过程称为**查找**。在第 20 章中，我们将研究并实现两种查找算法——用于在*无序数组*中查找的简单但缓慢的*线性查找*，以及用于在*有序数组*中查找的更复杂但快得多的*二分查找*。

### 演示函数 sort 和 binary_search

图 7.18 首先创建一个未排序的字符串数组（第 13～14 行），并显示数组的内容（第 17～19 行）。接下来，第 21 行使用 C++ 标准库函数 sort 对数组的元素进行排序——按升序排列。sort 函数的参数指定应排序的元素范围——在本例中，是整个数组。我们将在后面的章节中详细讨论类模板 array 的 begin 和 end 函数。正如你将看到的，sort 函数可用于对多种不同类型数据结构中的元素进行排序。第 24～26 行显示排序后数组的内容。

第 29 行和第 34 行演示了使用 binary_search 确定数组中是否存在某个值。值的序列必须先按升序排序——binary_search 会

```cpp
#include <array>
using namespace std;

const size_t rows = 2;
const size_t columns = 3;
void printArray( const array< array< int, columns >, rows > & );

int main()
{
   array< array< int, columns >, rows > array1 = { 1, 2, 3, 4, 5, 6 };
   array< array< int, columns >, rows > array2 = { 1, 2, 3, 4, 5 };

   cout << "Values in array1 by row are:" << endl;
   printArray( array1 );

   cout << "\nValues in array2 by row are:" << endl;
   printArray( array2 );
} // end main

// output array with two rows and three columns
void printArray( const array< array< int, columns >, rows > & a )
{
   // loop through array's rows
   for ( auto const & row : a )
   {
      // loop through columns of current row
      for ( auto const & element : row )
         cout << element << ' ';

      cout << endl; // start new line of output
   } // end for
} // end function printArray
```

```text
Values in array1 by row are:
1 2 3
4 5 6

Values in array2 by row are:
1 2 3
4 5 0
```

**图 7.20** | *初始化多维数组。（第 2 部分，共 2 部分。）*

array1 的声明（第 13 行）提供了六个初始化器。编译器先初始化第 0 行的元素，然后初始化第 1 行的元素。因此，前三个值将第 0 行的元素初始化为 1、2 和 3，后三个值将第 1 行的元素初始化为 4、5 和 6。

array2 的声明（第 14 行）只提供了五个初始化器。前五个值先赋给第 0 行，然后是第 1 行。任何没有显式初始化器的元素都会被初始化为零，因此 array2[1][2] 为 0。

程序调用函数 printArray 输出每个数组的元素。请注意，函数原型（第 9 行）和函数定义（第 24～35 行）指定该函数接收一个两行三列的数组。参数按引用接收数组，并声明为 const，因为该函数不会修改数组的元素。

### 嵌套的基于范围的 for 语句

为了处理二维数组的元素，我们使用嵌套循环，其中*外层*循环遍历*行*，内层循环遍历给定行的*列*。函数 printArray 的嵌套循环是使用基于范围的 for 语句实现的。第 27 行和第 30 行引入了 C++11 的 `auto` 关键字，它告诉编译器根据变量的初始化器值来推断（确定）变量的数据类型。外层循环的范围变量 `row` 使用参数 `a` 中的元素进行初始化。查看数组的声明，可以看到该数组包含的元素类型为

```cpp
array< int, columns >
```

因此编译器推断 `row` 引用的是一个包含三个 int 值的数组（同样，columns 为 3）。row 声明中的 const & 表示该引用不能用于修改行，并且可以防止每一行被复制到范围变量中。内层循环的范围变量 `element` 使用 `row` 所表示的数组中的一个元素进行初始化，因此编译器推断 `element` 引用的是 int，因为每行包含三个 int 值。在 IDE 中，通常可以将鼠标悬停在用 auto 声明的变量上，IDE 会显示该变量的推断类型。第 31 行显示给定行和列中的值。

### 嵌套的计数器控制 for 语句

我们也可以用计数器控制循环来实现该嵌套循环，如下所示：

```cpp
for ( size_t row = 0; row < a.size(); ++row )
{
   for ( size_t column = 0; column < a[ row ].size(); ++column )
      cout << a[ row ][ column ] << ' ';
   cout << endl;
} // end outer for
```

### 其他常见数组操作

许多常见的数组操作都使用 `for` 语句。例如，下面的 for 语句将图 7.19 中数组 a 中第 2 行的所有元素设置为零：

```cpp
for ( size_t column = 0; column < 4; ++column )
   a[ 2 ][ column ] = 0;
```

该 `for` 语句仅改变第二个下标（即列下标）。前面的 `for` 语句等价于以下赋值语句：

```cpp
a[ 2 ][ 0 ] = 0;
a[ 2 ][ 1 ] = 0;
a[ 2 ][ 2 ] = 0;
a[ 2 ][ 3 ] = 0;
```

下面的嵌套计数器控制 `for` 语句计算图 7.19 中数组 a 的*所有*元素的总和：

```cpp
total = 0;
for ( size_t row = 0; row < a.size(); ++row )
   for ( size_t column = 0; column < a[ row ].size(); ++column )
      total += a[ row ][ column ];
```

