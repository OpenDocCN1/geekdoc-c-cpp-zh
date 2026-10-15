
依次执行。当 product 变为 243 时，条件——product <= 100——变为 false。这终止了重复，因此 product 的最终值为 243。此时，程序继续执行 while 语句之后的下一条语句。

### 常见编程错误 4.5

> 如果在 while 语句的循环体中，没有提供最终使 while 中的条件变为 false 的操作，通常会导致无限循环，即循环语句永远无法终止。

图4.5 的 UML 活动图说明了与前面 while 语句对应的控制流。同样，图中的符号（除初始状态、转换箭头、最终状态和三个注释外）表示一个动作状态和一个决策。该图还引入了 UML 的合并符号，它将两个活动流合并为一个活动流。UML 将合并符号和决策符号都表示为菱形。在此图中，合并符号连接来自初始状态和动作状态的转换，因此两者都流入决策，该决策确定循环是否应开始（或继续）执行。决策符号和合并符号可以通过“传入”和“传出”转换箭头的数量来区分。决策符号有一条指向菱形的转换箭头，并有两条或更多条从菱形指出的转换箭头，以表示从该点可能的转换。此外，每条从决策符号指出的转换箭头旁边都有一个守卫条件。合并符号有两条或更多条指向菱形的转换箭头，且只有一条从菱形指出的转换箭头，表示多个活动流合并后继续活动。请注意，与决策符号不同，合并符号在 C++ 代码中没有对应物。与合并符号关联的任何转换箭头都没有守卫条件。

图4.5 的图清楚地显示了本节前面讨论的 while 语句的重复。从动作状态出现的转换箭头指向合并，合并再转换回决策，每次循环时都会测试该决策，直到守卫条件 product > 100 变为 true。然后 while 语句退出（到达其最终状态），控制传递给程序中按顺序排列的下一条语句。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_145_0.png)

图4.5 | while 循环语句的 UML 活动图。

## 4.6 计数器控制循环

本节和第4.7节解决班级平均分问题的两个变体。考虑以下问题描述：

> 一个班有十名学生参加了一次测验。本次测验的成绩（0 到 100 范围内的整数）可供你使用。计算并显示所有学生成绩的总和以及本次测验的班级平均分。

班级平均分等于成绩总和除以学生人数。解决这个问题的程序必须输入每个成绩，计算平均分并打印结果。我们使用计数器控制循环来逐个输入成绩。

本节展示了一个 GradeBook 类版本（图4.6–图4.7），它在 C++ 成员函数中实现了班级平均分算法，以及一个应用程序（图4.8），该程序演示了算法的实际运行。

```cpp
// Fig. 4.6: GradeBook.h
// Definition of class GradeBook that determines a class average.
// Member functions are defined in GradeBook.cpp
#include <string> // program uses C++ standard string class
using std::string;

// GradeBook class definition
class GradeBook
{
public:
    GradeBook( string ); // constructor initializes course name
    void setCourseName( string ); // function to set the course name
    string getCourseName(); // function to retrieve the course name
    void displayMessage(); // display a welcome message
    void determineClassAverage(); // averages grades entered by the user
private:
    string courseName; // course name for this GradeBook
}; // end class GradeBook
```

图4.6 | 使用计数器控制循环的班级平均分问题：GradeBook 头文件。

```cpp
// Fig. 4.7: GradeBook.cpp
// Member-function definitions for class GradeBook that solves the
// class average program with counter-controlled repetition.
#include <iostream>
using std::cout;
using std::cin;
using std::endl;

#include "GradeBook.h" // include definition of class GradeBook

// constructor initializes courseName with string supplied as argument
GradeBook::GradeBook( string name )
{
    setCourseName( name ); // validate and store courseName
} // end GradeBook constructor

// function to set the course name;
// ensures that the course name has at most 25 characters
void GradeBook::setCourseName( string name )
{
    if ( name.length() <= 25 ) // if name has 25 or fewer characters
        courseName = name; // store the course name in the object
    else // if name is longer than 25 characters
    { // set courseName to first 25 characters of parameter name
        courseName = name.substr( 0, 25 ); // select first 25 characters
        cout << "Name \"" << name << "\" exceeds maximum length (25).\n"
            << "Limiting courseName to first 25 characters.\n" << endl;
    } // end if...else
} // end function setCourseName

// function to retrieve the course name
string GradeBook::getCourseName()
{
    return courseName;
} // end function getCourseName

// display a welcome message to the GradeBook user
void GradeBook::displayMessage()
{
    cout << "Welcome to the grade book for\n" << getCourseName() << "!\n"
        << endl;
} // end function displayMessage

// determine class average based on 10 grades entered by user
void GradeBook::determineClassAverage()
{
    int total; // sum of grades entered by user
    int gradeCounter; // number of the grade to be entered next
    int grade; // grade value entered by user
    int average; // average of grades

    // initialization phase
    total = 0; // initialize total
    gradeCounter = 1; // initialize loop counter

    // processing phase
    while ( gradeCounter <= 10 ) // loop 10 times
    {
        cout << "Enter grade: "; // prompt for input
        cin >> grade; // input next grade
        total = total + grade; // add grade to total
        gradeCounter = gradeCounter + 1; // increment counter by 1
    } // end while
```

图4.7 | 使用计数器控制循环的班级平均分问题：GradeBook 源代码文件。

第59行显示提示信息“Enter grade: ”。第60行读取用户输入的成绩并将其赋给变量 grade。第61行将用户输入的新成绩加到 total 上，并将结果赋给 total，从而替换其先前的值。

第62行将 gradeCounter 加 1，以表示程序已处理一个成绩并准备输入用户的下一个成绩。递增 gradeCounter 最终会使 gradeCounter 超过 10。此时，while 循环终止，因为其条件（第57行）变为 false。

当循环终止时，第66行执行平均分计算并将结果赋给变量 average。第69行显示文本“Total of all 10 grades is ”，后面跟变量 total 的值。第70行接着显示文本“Class average is ”，后面跟变量 average 的值。然后，成员函数 determineClassAverage 将控制权返回给调用函数（即图4.8中的 main）。

### 演示 GradeBook 类

图4.8 包含此应用程序的 main 函数，该函数创建一个 GradeBook 类对象并演示其功能。图4.8 的第9行创建一个名为 myGradeBook 的新 GradeBook 对象。第9行中的字符串被传递给 GradeBook 构造函数（图4.7 的第12–15行）。图4.8 的第11行调用 myGradeBook 的 displayMessage 成员函数，向用户显示欢迎消息。第12行接着调用 myGradeBook 的 determineClassAverage 成员函数，允许用户输入10个成绩，然后该成员函数计算并打印平均分。

```cpp
// Fig. 4.8: fig04_08.cpp
// Create GradeBook object and invoke its determineClassAverage function.
#include "GradeBook.h" // include definition of class GradeBook

int main()
{
    // create GradeBook object myGradeBook and
    // pass course name to constructor
    GradeBook myGradeBook( "CS101 C++ Programming" );

    myGradeBook.displayMessage(); // display welcome message
    myGradeBook.determineClassAverage(); // find average of 10 grades
    return 0; // indicate successful termination
} // end main
```

```
Welcome to the grade book for
CS101 C++ Programming

Enter grade: 67
Enter grade: 78
Enter grade: 89
Enter grade: 67
Enter grade: 87
```

图4.8 | 使用计数器控制循环的班级平均分问题：创建一个 GradeBook 类对象（图4.6–图4.7）并调用其 determineClassAverage 函数。（第1部分，共2部分。）
