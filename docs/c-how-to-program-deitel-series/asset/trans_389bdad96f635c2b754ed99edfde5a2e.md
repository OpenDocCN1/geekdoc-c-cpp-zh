
```
gradeBook1 created for course: CS101 Introduction to C++ Programming
gradeBook2 created for course: CS102 Data Structures in C++
```

**图 3.13** | 将接口与实现分离后的 GradeBook 类演示。（第 2 部分，共 2 部分。）

如图 3.10 所示，图 3.13 的第 5 行包含了 GradeBook.h 头文件，以便编译器能够确保在客户端代码中正确创建和操作 GradeBook 对象。在执行此程序之前，图 3.12 和图 3.13 中的源代码文件都必须先编译，然后链接在一起——也就是说，客户端代码中的成员函数调用需要与类的成员函数实现绑定——这一工作由链接器完成。

## 编译与链接过程

图 3.14 中的示意图展示了编译和链接过程，该过程最终生成可供教师使用的可执行 GradeBook 应用程序。通常，类的接口和实现由一位程序员创建并编译，而另一位实现客户端代码的程序员则使用它们。因此，该图展示了类实现程序员和客户端代码程序员各自所需的内容。图中的虚线分别展示了类实现程序员、客户端代码程序员和 GradeBook 应用程序用户所需的部分。[*注：图 3.14 不是 UML 图。*]

负责创建可重用 GradeBook 类的类实现程序员会创建头文件 GradeBook.h 和源代码文件 GradeBook.cpp（其中 #includes 该头文件），然后编译源代码文件以生成 GradeBook 的目标代码。为了隐藏类的成员函数实现细节，类实现程序员会向客户端代码程序员提供头文件 GradeBook.h（该头文件指定了类的接口和数据成员）以及 GradeBook 目标代码（即表示 GradeBook 成员函数的机器码指令）。客户端代码程序员*不会*获得 GradeBook.cpp，因此客户端始终无法了解 GradeBook 的成员函数是如何实现的。

客户端代码程序员要使用该类，只需要了解 GradeBook 的接口，并且必须能够链接其目标代码。由于类的接口是 GradeBook.h 头文件中类定义的一部分，因此客户端代码程序员必须能够访问该文件，并且必须在客户端的源代码文件中 #include 它。当客户端代码被编译时，编译器使用 GradeBook.h 中的类定义来确保 main 函数正确创建和操作 GradeBook 类的对象。

- 要创建可编译的 GradeBook 应用程序，最后一步是链接：

  1. main 函数的目标代码（即客户端代码），
  2. GradeBook 类成员函数实现的目标代码，
  3. 类实现程序员和客户端代码程序员所使用的 C++ 类（如 string）的 C++ 标准库目标代码。

链接器的输出是*可执行*的 GradeBook 应用程序，教师可以用它来管理学生的成绩。编译器和 IDE 通常会在编译完代码后为你调用链接器。

很有可能。假设一所大学可以打印课程名称不超过 25 个字符的学生成绩单。如果该大学使用包含 GradeBook 对象的系统来生成成绩单，我们可能希望 GradeBook 类确保其数据成员 courseName 永远不会超过 25 个字符。图 3.15–3.17 中的程序增强了 GradeBook 的成员函数 setCourseName 以执行此验证（也称为有效性检查）。

## GradeBook 类定义

GradeBook 的类定义（图 3.15）——因而也是其接口——与图 3.11 的完全相同。由于接口保持不变，当成员函数 setCourseName 的定义被修改时，该类的客户端无需更改。这使得客户端只需将客户端代码链接到更新后的 GradeBook 目标代码，即可利用改进后的 GradeBook 类。

```cpp
// Fig. 3.15: GradeBook.h
// GradeBook class definition presents the public interface of the class.
// the class-member-function definitions appear in GradeBook.cpp.
#include <string> // program uses C++ standard string class

// GradeBook class definition
class GradeBook
{
public:
   explicit GradeBook( std::string ); // constructor initialize courseName
   void setCourseName( std::string ); // sets the course name
   std::string getCourseName() const; // gets the course name
   void displayMessage() const; // displays a welcome message
private:
   std::string courseName; // course name for this GradeBook
}; // end class GradeBook
```

**图 3.15** | GradeBook 类定义展示了类的公共接口。

## 使用 GradeBook 成员函数 setCourseName 验证课程名称

对 GradeBook 类的更改体现在构造函数（图 3.16 的第 9–12 行）和 setCourseName（第 16–29 行）的定义中。构造函数现在不再使用成员初始化器，而是调用 setCourseName。通常，所有数据成员都应使用成员初始化器进行初始化。然而，有时构造函数还必须验证其参数——这通常在构造函数体内处理（第 11 行）。调用 setCourseName 会验证构造函数的参数并设置数据成员 courseName。最初，在构造函数体执行之前，courseName 的值会被设置为空字符串，然后 setCourseName 会修改 courseName 的值。

在 setCourseName 中，第 18–19 行的 if 语句判断参数 name 是否包含有效的课程名称（即长度不超过 25 个字符的字符串）。如果课程名称有效，第 19 行将其存储到数据成员 courseName 中。注意第 18 行中的表达式 name.size()。这是一个成员函数调用，就像 myGradeBook.displayMessage() 一样。C++ 标准库的 string 类定义了一个成员函数 size，它返回字符串对象中的字符数。参数 name 是一个 string 对象，因此调用 name.size() 会返回 name 中的字符数。如果该值小于或等于 25，则 name 有效，并执行第 19 行。

```cpp
// Fig. 3.16: GradeBook.cpp
// Implementations of the GradeBook member-function definitions.
// The setCourseName function performs validation.
#include <iostream>
#include "GradeBook.h" // include definition of class GradeBook
using namespace std;

// constructor initializes courseName with string supplied as argument
GradeBook::GradeBook( string name )
{
   setCourseName( name ); // validate and store courseName
} // end GradeBook constructor

// function that sets the course name;
// ensures that the course name has at most 25 characters
void GradeBook::setCourseName( string name )
{
   if ( name.size() <= 25 ) // if name has 25 or fewer characters
      courseName = name; // store the course name in the object

   if ( name.size() > 25 ) // if name has more than 25 characters
   {
      // set courseName to first 25 characters of parameter name
      courseName = name.substr( 0, 25 ); // start at 0, length of 25

      cerr << "Name \"" << name << "\" exceeds maximum length (25)\n"
           << "Limiting courseName to first 25 characters.\n" << endl;
   } // end if
} // end function setCourseName

// function to get the course name
string GradeBook::getCourseName() const
{
   return courseName; // return object's courseName
} // end function getCourseName

// display a welcome message to the GradeBook user
void GradeBook::displayMessage() const
{
   // call getCourseName to get the courseName
   cout << "Welcome to the grade book for\n" << getCourseName()
        << "!" << endl;
} // end function displayMessage
```

**图 3.16** | GradeBook 类的成员函数定义，其中的 set 函数验证数据成员 `courseName` 的长度。

第 21–28 行的 if 语句处理 setCourseName 收到*无效*课程名称（即长度超过 25 个字符的名称）的情况。即使参数 name 太长，我们仍然希望让 GradeBook 对象保持*一致的状态*——也就是说，

很有可能。假设一所大学可以打印课程名称不超过 25 个字符的学生成绩单。
