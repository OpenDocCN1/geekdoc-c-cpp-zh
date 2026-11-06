

类定义从第 8 行开始，其中使用关键字 class，后面跟着类名 GradeBook。按照惯例，用户定义类的名称以大写字母开头；为了提高可读性，类名中后续每个单词也都以大写字母开头。这种大小写风格通常称为驼峰式命名法，因为大写字母和小写字母的排列模式类似于骆驼的轮廓。

每个类的主体都包含在一对左、右花括号（{ 和 }）中，如第 9 行和第 16 行所示。类定义以分号结束（第 16 行）。

> **常见编程错误 3.1**
>
> *忘记在类定义末尾添加分号会导致语法错误。*

回想一下，执行程序时，函数 main 总是会被自动调用。大多数函数不会被自动调用。正如你很快将看到的那样，你必须显式调用成员函数 displayMessage，告诉它执行相应的任务。

第 10 行包含访问说明符标签 public:。关键字 public 是一种访问说明符。第 12～15 行定义了成员函数 displayMessage。该成员函数出现在访问说明符 public: 之后，表示该函数“对公众可用”——也就是说，它可以被程序中的其他函数（例如 main）调用，也可以被其他类的成员函数调用（如果存在其他类的话）。访问说明符后总是跟着冒号（:）。在本文后面的内容中，当我们提到访问说明符 public 时，将像本句一样省略冒号。第 3.5 节将介绍第二种访问说明符 private。本书后面还会学习访问说明符 protected。

程序中的每个函数都会执行某项任务，并且在任务完成时可能返回一个值。例如，一个函数可能执行某项计算，然后返回该计算的结果。定义函数时，必须指定返回类型，以表明函数完成任务时所返回值的类型。在第 12 行中，函数名 displayMessage 左侧的关键字 void 就是该函数的返回类型。返回类型 void 表示 displayMessage 完成任务后不会向调用它的函数返回（即给回）任何数据（在本例中，调用它的函数是 main，我们稍后会看到）。在图 3.5 中，你将看到一个返回值的函数示例。

成员函数的名称 displayMessage 位于返回类型之后。按照惯例，函数名的第一个字母使用小写，名称中后续每个单词的首字母使用大写。成员函数名后面的圆括号表明这是一个函数。空圆括号（如第 12 行所示）表示该成员函数不需要额外数据即可执行其任务。你将在第 3.4 节中看到一个确实需要额外数据的成员函数示例。第 12 行通常称为函数头。每个函数的主体都由左、右花括号（{ 和 }）界定，如第 13 行和第 15 行所示。

函数主体包含执行函数任务的语句。在本例中，成员函数 displayMessage 包含一条语句（第 14 行），用于显示消息 "Welcome to the Grade Book!"。该语句执行后，函数就完成了它的任务。

> **常见编程错误 3.2**
>
> *从返回类型声明为 void 的函数中返回值会导致编译错误。*

```cpp
// Fig. 3.3: fig03_03.cpp
// Define a GradeBook with a member function that takes a parameter;
// Create a GradeBook object and call its displayMessage function.
#include <iostream>
#include <string> // program uses C++ standard string class
using namespace std;

// GradeBook class definition
class GradeBook
{
public:
   // function that displays a welcome message to the GradeBook user
   void displayMessage( string courseName )
   {
      cout << "Welcome to the grade book for\n" << courseName << "!"
           << endl;
   } // end function displayMessage
}; // end class GradeBook

// function main begins program execution
int main()
{
   string nameOfCourse; // string of characters to store the course name
   GradeBook myGradeBook; // create a GradeBook object named myGradeBook

   // prompt for and input course name
   cout << "Please enter the course name:" << endl;
   getline( cin, nameOfCourse ); // read a course name with blanks
   cout << endl; // output a blank line

   // call myGradeBook's displayMessage function
   // and pass nameOfCourse as an argument
   myGradeBook.displayMessage( nameOfCourse );
} // end main
```

**图 3.3** | 定义类 GradeBook 及其带参数的成员函数，创建 GradeBook 对象并调用其 displayMessage 函数。

以获取课程名称。在我们的示例程序执行过程中，我们使用课程名称“CS101 Introduction to C++ Programming”，该名称包含多个单词。（回想一下，我们会将用户提供的输入以粗体显示。）当使用流提取运算符和 cin 时，它会一直读取字符，直到遇到第一个空白字符。因此，前面的语句只能读取“CS101”。课程名称的其余部分必须通过后续的输入操作读取。

在本例中，我们希望用户输入完整的课程名称，然后按 Enter 将其提交给程序；同时，我们希望将完整的课程名称存储在字符串变量 nameOfCourse 中。第 28 行中的函数调用 `getline(cin, nameOfCourse)` 会从标准输入流对象 `cin`（即键盘）中读取字符，包括输入内容中用于分隔单词的空格字符，直到遇到换行符；然后将这些字符放入字符串变量 `nameOfCourse` 中，并丢弃换行符。当你在输入程序数据时按下 *回车*，输入流中就会插入一个换行符。此外，程序必须包含 `<string>` 头文件，才能使用函数 `getline`，并且必须声明名称 `getline` 属于命名空间 `std`。

第 33 行调用 `myGradeBook` 的成员函数 `displayMessage`。圆括号中的变量 `nameOfCourse` 是传递给成员函数 `displayMessage` 的实参，使该函数能够执行其任务。main 中变量 `nameOfCourse` 的值会成为第 13 行成员函数 `displayMessage` 的参数 `courseName` 的值。执行该程序时，成员函数 `displayMessage` 会将你输入的课程名称作为欢迎消息的一部分输出（在我们的示例执行中，该名称为 CS101 Introduction to C++ Programming）。

### 关于实参和形参的更多内容

要指定函数需要数据来执行其任务，可以将其他信息放入函数的参数列表中。参数列表位于函数名后面的圆括号中。参数列表可以包含任意数量的参数，也可以不包含参数（如图 3.1 第 12 行中的空圆括号所示），以表示函数不需要任何参数。成员函数 `displayMessage` 的参数列表（图 3.3 第 13 行）声明该函数需要一个参数。每个参数都必须指定一个类型和一个标识符。在本例中，类型 `string` 和标识符 `courseName` 表明成员函数 `displayMessage` 需要一个字符串来执行其任务。成员函数主体使用参数 `courseName` 来访问函数调用中传递给该函数的值（即 `main` 中的第 33 行）。第 15～16 行将参数 `courseName` 的值作为欢迎消息的一部分显示出来。参数变量的名称（第 13 行）可以与实参变量的名称（第 33 行）相同，也可以不同——你将在第 6 章“函数和面向对象编程简介”中了解其中的原因。

通过使用逗号将各个参数分隔开，函数可以指定多个参数（我们将在图 6.4～6.5 中看到一个示例）。函数调用中的实参数量和顺序必须与被调用函数函数头中参数列表的参数数量和顺序相匹配。此外，函数调用中的实参类型必须与函数头中相应参数的类型一致。（正如你将在后续章节中学习的那样，实参的类型及其对应参数的类型并不总是必须完全相同，但它们必须“保持一致”。）在本例中，函数调用中的一个 `string` 实参（即 `nameOfCourse`）与成员函数定义中的一个 `string` 参数（即 `courseName`）完全匹配。

> **常见编程错误 3.4**
>
> *在函数定义中包围参数列表的右圆括号后添加分号会导致语法错误。*

> **常见编程错误 3.5**
>
> *在函数主体中再次将函数参数定义为变量会导致编译错误。*

