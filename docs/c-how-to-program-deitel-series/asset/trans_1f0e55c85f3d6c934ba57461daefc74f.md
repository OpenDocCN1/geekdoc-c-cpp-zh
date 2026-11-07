

伪代码语句

```
Input, sum and count the quiz grades
```

需要一条重复语句（即循环）来依次输入每个成绩。我们事先不知道要处理多少个成绩，因此将使用哨兵控制的重复。用户一次输入一个合法成绩。输入最后一个合法成绩后，用户输入哨兵值。程序在每次输入成绩后检查哨兵值，当用户输入哨兵值时终止循环。上述伪代码语句的第二次细化如下：

```
Prompt the user to enter the first grade
Input the first grade (possibly the sentinel)
While the user has not yet entered the sentinel
    Add this grade into the running total
    Add one to the grade counter
    Prompt the user to enter the next grade
    Input the next grade (possibly the sentinel)
```

在伪代码中，我们不在构成While结构体的语句周围使用花括号。我们只需缩进While下方的语句，以表明它们属于该While。再次强调，伪代码仅仅是一种非正式的程序开发辅助工具。

伪代码语句

```
Calculate and print the total of all student grades and the class average
```

可以按如下方式细化：

```
If the counter is not equal to zero
    Set the average to the total divided by the counter
    Print the total of the grades for all students in the class
    Print the class average
else
    Print "No grades were entered"
```

我们测试除以零的可能性——这通常是一种致命的逻辑错误，如果未被发现，将导致程序失败（通常称为“崩溃”）。班级平均分问题的伪代码的完整第二次细化如图4.11所示。

![](img/b42ba5cd262b1358d16610173f975e4d_161_0.png)

> **常见编程错误 4.5**
>
> *除以零会导致未定义行为，通常会造成致命的运行时错误。*

```
1    Initialize total to zero
2    Initialize counter to zero
3
4    Prompt the user to enter the first grade
5    Input the first grade (possibly the sentinel)
6
7    While the user has not yet entered the sentinel
8        Add this grade into the running total
9        Add one to the grade counter
10       Prompt the user to enter the next grade
11       Input the next grade (possibly the sentinel)
12
13   If the counter is not equal to zero
14       Set the average equal to the total divided by the counter
15       Print the total of the grades for all students in the class
16       Print the class average
17   else
18       Print "No grades were entered"
```

**图4.11** | 使用哨兵控制的班级平均分问题的伪代码算法。

> **错误预防提示 4.5**
>
> 当除法的表达式值可能为零时，请显式测试这种可能性，并在程序中适当处理（例如打印错误消息），而不是让致命错误发生。在讨论异常处理（第7、9和17章）时，我们将进一步介绍如何处理这类错误。

![](img/b42ba5cd262b1358d16610173f975e4d_162_0.png)

图4.11中的伪代码解决了更一般的班级平均分问题。该算法只需要两级细化。有时需要更多级别。

> **软件工程观察 4.6**
>
> 当伪代码算法已详细到足以让你将其转换为C++时，就终止自顶向下、逐步细化的过程。通常，实现C++程序随后就会变得直接明了。

![](img/b42ba5cd262b1358d16610173f975e4d_162_1.png)

> **软件工程观察 4.7**
>
> 许多经验丰富的程序员编写程序时从不使用诸如伪代码之类的程序开发工具。这些程序员认为，他们的最终目标是在计算机上解决问题，而使用伪代码之类的程序开发工具只会推迟最终输出的产生。尽管这种方法可能适用于简单且熟悉的问题，但在大型复杂项目中可能会导致严重困难。

![](img/b42ba5cd262b1358d16610173f975e4d_162_2.png)

## 在GradeBook类中实现哨兵控制的重复

图4.12–4.13展示了包含成员函数determineClassAverage的GradeBook类，该函数实现了图4.11中的伪代码算法（该类在图4.14中演示）。尽管输入的每个成绩都是整数，但平均值计算很可能产生带小数点的数字——换句话说，是实数或浮点数（例如7.33、0.0975或1000.12345）。int类型无法表示这种数字，因此该类必须使用另一种类型来实现。C++提供了多种用于在内存中存储浮点数的数据类型，包括float和double。这些类型之间的主要区别在于，与float变量相比，double变量通常可以存储数值更大、精度更细的数字（即小数点右侧更多位数——也称为数字的精度）。该程序引入了一种称为**强制转换运算符**的特殊运算符，以强制平均值计算产生浮点数结果。

```cpp
// Fig. 4.12: GradeBook.h
// Definition of class GradeBook that declares a class average.
// Member functions are defined in GradeBook.cpp
#include <string> // program uses C++ standard string class

// GradeBook class definition
class GradeBook
{
public:
   explicit GradeBook( std::string ); // initializes course name
   void setCourseName( std::string ); // set the course name
   std::string getCourseName() const; // retrieve the course name
   void displayMessage() const; // display a welcome message
   void determineClassAverage() const; // averages user-entered grades
private:
   std::string courseName; // course name for this GradeBook
}; // end class GradeBook
```

**图4.12** | 使用哨兵控制的重复的班级平均分问题：GradeBook头文件。

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
// ensures that the course name has at most 25 characters
void GradeBook::setCourseName( string name )
{
   if ( name.size() <= 25 ) // if name has 25 or fewer characters
      courseName = name; // store the course name in the object
   else // if name is longer than 25 characters
   { // set courseName to first 25 characters of parameter name
      courseName = name.substr( 0, 25 ); // select first 25 characters
      cerr << "Name \"" << name << "\" exceeds maximum length (25).\n"
         << "Limiting courseName to first 25 characters.\n" << endl;
   } // end if...else
} // end function setCourseName

// function to retrieve the course name
string GradeBook::getCourseName() const
{
   return courseName;
} // end function getCourseName

// display a welcome message to the GradeBook user
void GradeBook::displayMessage() const
{
   cout << "Welcome to the grade book for\n" << getCourseName() << "\n\n"
        << endl;
} // end function displayMessage

// determine class average based on grades entered by user
void GradeBook::determineClassAverage() const
{
   // initialization phase
   int total = 0; // sum of grades entered by user
   unsigned int gradeCounter = 0; // number of grades entered

   // processing phase
   // prompt for input and read grade from user
   cout << "Enter grade or -1 to quit: ";
   int grade = 0; // grade value
   cin >> grade; // input grade or sentinel value

   // loop until sentinel value read from user
   while (grade != -1) // while grade is not -1
   {
      total = total + grade; // add grade to total
      gradeCounter = gradeCounter + 1; // increment counter

      // prompt for input and read next grade from user
      cout << "Enter grade or -1 to quit: ";
      cin >> grade; // input grade or sentinel value
   } // end while

   // termination phase
   if (gradeCounter != 0) // if user entered at least one grade...
   {
      // calculate average of all grades entered
      double average = static_cast< double > (total) / gradeCounter;

      // display total and average (with two digits of precision)
      cout << "\nTotal of all " << gradeCounter << " grades entered is "
           << total << endl;
      cout << setprecision(2) << fixed;
      cout << "Class average is " << average << endl;
   } // end if
```

**图4.13** | 使用哨兵控制的重复的班级平均分问题：GradeBook源代码文件。

