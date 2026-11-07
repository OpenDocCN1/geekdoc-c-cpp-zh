
```cpp
135    // print bar of asterisks
136    for ( int stars = 0; stars < frequency[ count ]; ++stars )
137       cout << '*';
138
139       cout << endl; // start a new line of output
140    } // end outer for
141 } // end function outputBarChart
142
143 // output the contents of the grades array
144 void GradeBook::outputGrades()
145 {
146    cout << "\nThe grades are:\n\n";
147    cout << setw( 8 ) << " "; // align column heads
148
149    // create a column heading for each of the tests
150    for ( int test = 0; test < tests; ++test )
151       cout << "Test " << test + 1 << "   ";
152
153    cout << "Average" << endl; // student average column heading
154
155    // create rows/columns of text representing array grades
156    for ( int student = 0; student < students; ++student )
157    {
158       cout << "Student " << setw( 2 ) << student + 1;
159
160       // output student's grades
161       for ( int test = 0; test < tests; ++test )
162          cout << setw( 8 ) << grades[ student ][ test ];
163
164       // call member function getAverage to calculate student's average;
165       // pass row of grades and the value of tests as the arguments
166       double average = getAverage( grades[ student ], tests );
167       cout << setw( 9 ) << setprecision( 2 ) << fixed << average << endl;
168    } // end outer for
169 } // end function outputGrades
```

**图 7.23** 使用二维数组存储成绩的 GradeBook 类的成员函数定义。（第 4 部分，共 4 部分。）

五个成员函数（在图 7.22 的第 23–27 行中声明）执行数组操作以处理成绩。这些成员函数中的每一个都类似于早期一维数组版 GradeBook 类（图 7.15–7.16）中的对应函数。成员函数 getMinimum（定义于图 7.23 的第 57–74 行）确定该学期所有学生中的最低成绩。成员函数 getMaximum（定义于图 7.23 的第 77–94 行）确定该学期所有学生中的最高成绩。成员函数 getAverage（图 7.23 的第 97–107 行）确定某个学生的学期平均成绩。成员函数 outputBarChart（图 7.23 的第 110–141 行）输出该学期所有学生成绩分布的条形图。成员函数 outputGrades（图 7.23 的第 144–169 行）以表格格式输出二维数组，以及每个学生的学期平均成绩。

成员函数 getMinimum、getMaximum、outputBarChart 和 outputGrades 都使用嵌套 for 语句遍历数组 grades。例如，考虑下面的

```cpp
// Fig. 7.24: fig07_24.cpp
// Creates GradeBook object using a two-dimensional array of grades.

#include "GradeBook.h" // GradeBook class definition

// function main begins program execution
int main()
{
   // initialize two-dimensional array of student grades
   int gradesArray[ GradeBook::students ][ GradeBook::tests ] =
      { { 87, 96, 70 },
        { 68, 87, 90 },
        { 94, 100, 90 },
        { 100, 81, 82 },
        { 83, 65, 85 },
        { 78, 87, 65 },
        { 85, 75, 83 },
        { 91, 94, 100 },
        { 76, 72, 84 },
        { 87, 93, 73 } };

   GradeBook myGradeBook(
      "CS101 Introduction to C++ Programming", gradesArray );
   myGradeBook.displayMessage();
   myGradeBook.processGrades();
} // end main
```

![](img/bfd978e7e9b192bab46ec2a89e481263_339_0.png)

**图 7.24** | 使用二维成绩数组创建一个 GradeBook 对象，然后调用成员函数 `processGrades` 分析这些成绩。*(第 1 部分，共 2 部分。)*

```
40–49:
50–59:
60–69: ***
70–79: *******
80–89: ***********
90–99: ***************
100: ***
```

**图 7.24** | 使用二维成绩数组创建一个 GradeBook 对象，然后调用成员函数 processGrades 分析这些成绩。（第 2 部分，共 2 部分。）

## 7.11 C++ 标准库类模板 vector 简介

现在我们介绍 C++ 标准库类模板 vector，它表示一种更健壮的数组类型，具有许多附加功能。正如你将在后续章节中看到的，C 风格基于指针的数组（即到目前为止所表示的数组类型）很容易出错。例如，如前所述，程序很容易“走出”数组的任一端，因为 C++ 不检查下标是否超出数组范围。不能用相等运算符或关系运算符对两个数组进行有意义的比较。正如你将在第 8 章学到的，指针变量（更常称为指针）的值是内存地址。数组名只是指向数组在内存中起始位置的指针，当然，两个数组总是位于不同的内存位置。当把数组传递给旨在处理任意大小数组的通用函数时，必须将数组大小作为附加参数传递。此外，不能使用赋值运算符将一个数组赋给另一个数组——数组名是 const 指针，而且正如你将在第 8 章学到的，常量指针不能用在赋值运算符的左侧。这些以及其他功能对于处理数组来说显然像是“自然而然”的，但 C++ 并未提供此类功能。不过，C++ 标准库提供了类模板 vector，使你能够创建比数组更强大且更不易出错的替代方案。第 11 章将介绍实现 vector 所提供的这类数组功能的方法。你将学习如何自定义运算符以用于自己的类（这种技术称为运算符重载）。

vector 类模板可供任何使用 C++ 构建应用程序的人使用。vector 示例使用的表示法可能对你不熟悉，因为 vector 使用模板表示法。回想一下，6.18 节讨论了函数模板。第 14 章将讨论类模板。目前，你应能通过模仿本节所示示例中的语法，自如地使用类模板 vector。随着我们在第 14 章学习类模板，你的理解将会加深。第 22 章将详细介绍类模板 vector（以及若干其他标准 C++ 容器类）。

图 7.25 的程序演示了 C++ 标准库类模板 vector 提供的、C 风格基于指针的数组所不具备的功能。标准类模板 vector 提供了许多与我们在第 11 章构建的 Array 类相同的功能。标准类模板 vector 定义在头文件 <vector>（第 5 行）中，属于 std 命名空间。第 22 章讨论 vector 的完整功能。本节末尾，我们将演示 vector 类的边界检查功能，并介绍 C++ 的异常处理机制，该机制可用于检测和处理越界的 vector 索引。

```cpp
// Fig. 7.25: fig07_25.cpp
// Demonstrating C++ Standard Library class template vector.
#include <iostream>
#include <iomanip>
#include <vector>
using namespace std;

void outputVector( const vector< int > & ); // display the vector
void inputVector( vector< int > & ); // input values into the vector

int main()
{
   vector< int > integers1( 7 ); // 7-element vector< int >
   vector< int > integers2( 10 ); // 10-element vector< int >

   // print integers1 size and contents
   cout << "Size of vector integers1 is " << integers1.size()
        << "\nVector after initialization:" << endl;
   outputVector( integers1 );

   // print integers2 size and contents
   cout << "\nSize of vector integers2 is " << integers2.size()
        << "\nVector after initialization:" << endl;
   outputVector( integers2 );

   // input and print integers1 and integers2
   cout << "\nEnter 17 integers:" << endl;
   inputVector( integers1 );
   inputVector( integers2 );

   cout << "\nAfter input, the vectors contain:\n"
        << "integers1: " << endl;
   outputVector( integers1 );
   cout << "integers2: " << endl;
   outputVector( integers2 );

   // use inequality (!=) operator with vector objects
   cout << "\nEvaluating: integers1 != integers2" << endl;

   if ( integers1 != integers2 )
      cout << "integers1 and integers2 are not equal" << endl;

   // create vector integers3 using integers1 as an
   // initializer; print size and contents
   vector< int > integers3( integers1 ); // copy constructor

   cout << "\nSize of vector integers3 is " << integers3.size()
        << "\nVector after initialization:" << endl;
   outputVector( integers3 );
```

**图 7.25** | 演示 C++ 标准库类模板 vector。（第 1 部分，共 4 部分。）
