
- 1 将总和初始化为零
- 2 将计数器初始化为零

- 4 提示用户输入第一个成绩
- 5 输入第一个成绩（可能是哨兵值）

- 7 当用户尚未输入哨兵值时
  - 8 将此成绩加入总和
  - 9 将成绩计数器加1
  - 10 提示用户输入下一个成绩
  - 11 输入下一个成绩（可能是哨兵值）

- 13 如果计数器不等于零
  - 14 将平均值设为总和除以计数器
  - 15 打印班级中所有学生的成绩总和
  - 16 打印班级平均分
- 17 否则
  - 18 打印“未输入任何成绩”

**图4.11** | 使用哨兵控制循环的班级平均分问题伪代码算法。

![](img/bfd978e7e9b192bab46ec2a89e481263_156_0.png)

> **错误预防提示 4.3**
> 
> 当使用值可能为零的表达式进行除法时，应显式测试这种可能性并在程序中妥善处理（例如打印错误消息），而不是允许致命错误发生。我们在讨论异常处理时会进一步介绍如何处理这类错误。

图4.11中的伪代码解决了更一般的班级平均分问题。该算法只需要两级细化。有时需要更多级。

![](img/bfd978e7e9b192bab46ec2a89e481263_156_1.png)

> **软件工程观察 4.6**
> 
> 当伪代码算法的细节足够充分，使你能将其转换成C++时，就应终止自顶向下、逐步细化的过程。通常，接下来的C++程序实现就很简单了。

![](img/bfd978e7e9b192bab46ec2a89e481263_156_2.png)

> **软件工程观察 4.7**
> 
> 许多经验丰富的程序员编写程序时从不使用伪代码这类程序开发工具。他们认为最终目标是在计算机上解决问题，编写伪代码只会推迟最终产出的生成。虽然这种方法对于简单且熟悉的问题可能有效，但在长期、复杂的项目中可能导致严重困难。

## 在GradeBook类中实现哨兵控制循环

图4.12–4.13展示了包含成员函数determineClassAverage的GradeBook类，该函数实现了图4.11中的伪代码算法（该类在图4.14中进行演示）。虽然输入的每个成绩都是整数，但平均值计算很可能产生带小数点的数字——即实数或浮点数（例如7.33、0.0975或1000.12345）。int类型无法表示这种数字，因此该类必须使用其他类型。C++提供了多种在内存中存储浮点数的数据类型，包括**float**和**double**。这些类型的主要区别在于，与float变量相比，double变量通常可以存储更大数值和更精细的细节（即小数点右侧更多位数——也称为数字的**精度**）。本程序引入了一种称为**强制转换运算符**的特殊运算符，以强制平均值计算产生浮点数结果。

```cpp
// Fig. 4.12: GradeBook.h
// Definition of class GradeBook that determines a class average.
// Member functions are defined in GradeBook.cpp
#include <string> // program uses C++ standard string class
using namespace std;

// GradeBook class definition
class GradeBook
{
public:
   GradeBook( string ); // constructor initializes course name
   void setCourseName( string ); // function to set the course name
   string getCourseName(); // function to retrieve the course name
   void displayMessage(); // function to welcome message
   void determineClassAverage(); // averages grades entered by the user
private:
   string courseName; // course name
}; // end class GradeBook
```

**图4.12** | 使用哨兵控制循环的班级平均分问题：GradeBook头文件。

```cpp
// Fig. 4.13: GradeBook.cpp
// Member-function definitions for class GradeBook that solves the
// class average program with sentinel-controlled repetition.
#include <iostream>
#include <iomanip> // parameterized stream manipulators
#include "GradeBook.h" // include definition of class GradeBook
using namespace std;

// constructor initializes courseName with string supplied as argument
GradeBook::GradeBook( string name )
{
   setCourseName( name ); // validate and store courseName
} // end GradeBook constructor

// function to set the course name;
// ensures that course name has at most 25 characters
void GradeBook::setCourseName( string name )
{
```

**图4.13** | 使用哨兵控制循环的班级平均分问题：GradeBook源代码文件。（第1部分，共3部分。）

```cpp
// termination phase
if ( gradeCounter != 0 ) // if user entered at least one grade...
{
   // calculate average of all grades entered
   average = static_cast< double >( total ) / gradeCounter;

   // display total and average (with two digits of precision)
   cout << "\nTotal of " << gradeCounter << " grades entered is "
        << total << endl;
   cout << "Class average is " << setprecision( 2 ) << fixed << average
        << endl;
} // end if
else // no grades were entered, so output appropriate message
   cout << "No grades were entered" << endl;
} // end of function determineClassAverage
```

**图4.13** | 使用哨兵控制循环的班级平均分问题：GradeBook源代码文件。（第3部分，共3部分。）

```cpp
// Fig. 4.14: fig04_14.cpp
// Create GradeBook object and invoke its determineClassAverage function.
#include "GradeBook.h" // include definition of class GradeBook

int main()
{
   // create GradeBook object myGradeBook and
   // pass course name to constructor
   GradeBook myGradeBook( "CS101 C++ Programming" );

   myGradeBook.displayMessage(); // display welcome message
   myGradeBook.determineClassAverage(); // find average of 10 grades
} // end main
```

```text
Welcome to the grade book for
CS101 C++ Programming

Enter grade or -1 to quit: 97
Enter grade or -1 to quit: 88
Enter grade or -1 to quit: 72
Enter grade or -1 to quit: -1

Total of all 3 grades entered is 257
Class average is 85.67
```

**图4.14** | 使用哨兵控制循环的班级平均分问题：创建GradeBook对象并调用其determineClassAverage成员函数。

本例将控制语句逐个堆叠——while语句（图4.13中的第60–68行）之后紧跟一个if...else语句（第71–83行）。该程序中的大部分代码与图4.9中的代码相同，因此我们重点讨论新增特性和问题。

第48行声明了double变量average。回想一下，在前一个示例中我们使用int变量存储班级平均分。在当前示例中使用double类型可以将班级平均分计算的结果存储为浮点数。第52行将变量`gradeCounter`初始化为0，因为还没有输入任何成绩。请记住，本程序使用哨兵控制循环。为了准确记录输入的成绩数量，程序仅当用户输入有效成绩值且程序完成该成绩的处理后才递增变量`gradeCounter`。最后，注意两个输入语句（第57行和第67行）之前都有一个提示用户输入的输出语句。

![](img/bfd978e7e9b192bab46ec2a89e481263_160_0.png)

> **良好编程实践 4.4**
> 
> 为每次键盘输入提示用户。提示应指明输入的形式以及任何特殊的输入值。在哨兵控制循环中，请求数据输入的提示应明确提醒用户哨兵值是什么。

### 哨兵控制循环与计数器控制循环的程序逻辑

将本应用中哨兵控制循环的程序逻辑与图4.9中计数器控制循环的逻辑进行比较。在计数器控制循环中，while语句（图4.9中的第54–60行）的每次迭代都会从用户处读取一个值，共读取指定的迭代次数。在哨兵控制循环中，程序在到达while之前先读取第一个值（图4.13中的第56–57行）。该值决定程序的控制流是否应进入while循环体。如果while的条件为假，说明用户输入了哨兵值，因此while循环体不会执行（即未输入任何成绩）。另一方面，如果条件为真，则循环体开始执行，循环将成绩值加入总和（第62行），并将gradeCounter加1（第63行）。然后循环体中的第66–67行提示用户并输入下一个值。接下来，程序控制到达第68行循环体的右花括号（}），因此执行继续测试while的条件（第60行）。该条件使用用户最近输入的成绩来决定是否应再次执行循环体。变量grade的值总是在程序测试while条件之前立即从用户处输入。这使程序能够在处理该值（即将其加入总和并递增gradeCounter）之前确定刚输入的值是否为哨兵值。如果输入了哨兵值，循环终止，程序不会将值−1加入总和。

循环终止后，执行第71–83行的if...else语句。第71行的条件确定是否输入了任何成绩。如果没有，则执行if...else语句的else部分（第82–83行）并显示消息“未输入任何成绩”，然后成员函数将控制权返回给调用函数。

注意图4.13中while循环中的块。如果没有大括号，循环体中的后三条语句将落在循环之外，导致计算机错误地解释此代码，如下所示：

```cpp
// loop until the sentinel value read from user
while ( grade != -1 ) {
    total = total + grade; // add grade to total
    gradeCounter = gradeCounter + 1; // increment counter

    // prompt for input and read next grade from user
    cout << "Enter grade or -1 to quit: ";
    cin >> grade;
}
```

