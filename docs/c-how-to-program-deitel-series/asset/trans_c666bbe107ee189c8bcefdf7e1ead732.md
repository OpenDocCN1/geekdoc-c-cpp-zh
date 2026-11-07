

对象的数据成员 courseName 包含有效值（即不超过 25 个字符的字符串）的状态。因此，我们截断指定的课程名称，并将 name 的前 25 个字符赋给 courseName 数据成员（不幸的是，这可能会使课程名称截断得很不自然）。标准类 string 提供了成员函数 `substr`（“substring”的缩写），它通过复制现有 string 对象的一部分来返回一个新的 string 对象。第 24 行中的调用（即 `name.substr(0, 25)`）向 name 的成员函数 substr 传递两个整数（0 和 25）。这些参数指明了应该返回的字符串 name 的部分。第一个参数指定从原字符串中复制字符的起始位置——每个字符串的第一个字符都认为处于位置 0。第二个参数指定要复制的字符数。因此，第 24 行的调用返回从位置 0 开始的 name 的 25 个字符子串（即 name 的前 25 个字符）。例如，如果 name 的值为 "CS101 Introduction to Programming in C++"，则 substr 返回 "CS101 Introduction to Pro"。在调用 substr 之后，第 24 行将 substr 返回的子串赋给数据成员 courseName。这样，setCourseName 确保 courseName 始终被赋为包含 25 个或更少字符的字符串。如果成员函数必须截断课程名称以使其有效，第 26–27 行会使用 cerr 显示一条警告消息，如第 1 章所述。

第 21–28 行的 if 语句包含两条函数体语句——一条将 courseName 设置为参数 name 的前 25 个字符，另一条向用户打印附带消息。当 name 太长时，两条语句都应执行，因此我们将它们放在一对花括号 `{ }` 中。回想第 2 章所述，这将创建一个块。你将在第 4 章学习更多关于在控制语句的函数体中放置多条语句的内容。

第 26–27 行的语句也可以不在语句第二行开头使用流插入运算符，如下所示：

```
cerr << "Name \"" << name << "\" exceeds maximum length (25).\n"
     << "Limiting courseName to first 25 characters.\n" << endl;
```

*C++ 编译器会合并相邻的字符串字面量，即使它们出现在程序的不同行中。因此，在上述语句中，C++ 编译器会将字符串字面量 `"\" exceeds maximum length (25).\n"` 和 `"Limiting courseName to first 25 characters.\n"` 合并为单个字符串字面量，其输出与图 3.16 中第 26–27 行的输出相同。这种行为允许你在程序中跨行打印长字符串，而无需包含额外的流插入操作。*

## 测试 GradeBook 类

图 3.17 演示了带有验证的 GradeBook 类的修改版本（图 3.15–3.16）。第 12 行创建了一个名为 gradeBook1 的 GradeBook 对象。回想一下，GradeBook 构造函数调用 setCourseName 来初始化数据成员 courseName。在该类的先前版本中，在构造函数中调用 setCourseName 的好处并不明显。然而现在，构造函数利用了 setCourseName 提供的验证。构造函数只是调用 setCourseName，而不是重复其验证代码。当图 3.17 的第 12 行将初始课程名称 "CS101 Introduction to Programming in C++" 传递给 GradeBook 构造函数时，构造函数将该值传递给 setCourseName，实际初始化在此发生。由于课程名称包含超过 25 个字符，第二个 if 语句的函数体执行，导致 courseName 被初始化为截断后的 25 个字符的课程 "CS101 Introduction to Pro"（截断的部分在第 12 行中以蓝色突出显示）。图 3.17 中的输出包含了成员函数 setCourseName 中图 3.16 第 26–27 行输出的警告消息。第 13 行创建了另一个名为 gradeBook2 的 GradeBook 对象——传递给构造函数的有效课程名称恰好是 25 个字符。

```cpp
// Fig. 3.17: fig03_17.cpp
// Create and manipulate a GradeBook object; illustrate validation.
#include <iostream>
#include "GradeBook.h" // include definition of class GradeBook
using namespace std;

// function main begins program execution
int main()
{
    // create two GradeBook objects;
    // initial course name of gradeBook1 is too long
    GradeBook gradeBook1( "CS101 Introduction to Programming in C++" );
    GradeBook gradeBook2( "CS102 C++ Data Structures" );

    // display each GradeBook's courseName
    cout << "gradeBook1's initial course name is: "
         << gradeBook1.getCourseName()
         << "\ngradeBook2's initial course name is: "
         << gradeBook2.getCourseName() << endl;

    // modify gradeBook1's courseName (with a valid-length string)
    gradeBook1.setCourseName( "CS101 C++ Programming" );

    // display each GradeBook's courseName
    cout << "\ngradeBook1's course name is: "
         << gradeBook1.getCourseName()
         << "\ngradeBook2's course name is:"
         << gradeBook2.getCourseName() << endl;
} // end main
```

```text
Name "CS101 Introduction to Programming in C++" exceeds maximum length (25).
Limiting courseName to first 25 characters.

gradeBook1's initial course name is: CS101 Introduction to Pro
gradeBook2's initial course name is: CS102 C++ Data Structures

gradeBook1's course name is: CS101 C++ Programming
gradeBook2's course name is: CS102 C++ Data Structures
```

**图 3.17** | 创建并操作一个课程名称长度限制为 25 个字符的 GradeBook 对象。

图 3.17 的第 16–19 行显示了 gradeBook1 的截断课程名称（在程序输出中以蓝色突出显示）和 gradeBook2 的课程名称。第 22 行直接调用 gradeBook1 的 setCourseName 成员函数，将 GradeBook 对象中的课程名称改为一个不需要截断的较短名称。然后，第 25–28 行再次输出 GradeBook 对象的课程名称。

## 设置函数的补充说明

像 setCourseName 这样的公有设置函数应仔细审查任何修改数据成员（例如 courseName）值的尝试，以确保新值对该数据项是合适的。例如，将日期中的日设为 37 的尝试应被拒绝，将一个人的体重设为零或负值的尝试应被拒绝，将考试分数设为 185（当正确范围是 0 到 100 时）的尝试应被拒绝，等等。

![](img/b42ba5cd262b1358d16610173f975e4d_132_0.png)

> **软件工程观察 3.3**  
> _将数据成员设为私有，并通过公有成员函数控制对这些数据成员的访问（尤其是写访问），有助于确保数据完整性。_

![](img/b42ba5cd262b1358d16610173f975e4d_132_1.png)

> **错误预防提示 3.4**  
> _仅仅将数据成员设为私有并不会自动带来数据完整性的好处——你必须提供适当的有效性检查并报告错误。_

设置函数可以返回一个值，指示是否有人尝试向类对象赋予无效数据。然后，客户可以测试设置函数的返回值，以确定修改对象的尝试是否成功，如果未成功则采取适当的措施。我们将在后面的章节中介绍更多编程技术后这样做。在 C++ 中，对象的客户还可以通过_异常处理机制_得到问题通知，我们将在第 7 章开始讨论该机制，并在第 17 章深入介绍。

## 3.9 小结

在本章中，你创建了用户自定义类，并创建和使用了这些类的对象。我们声明了类的数据成员，以维护类的每个对象的数据。我们还定义了操作这些数据的成员函数。你了解到，不修改类数据的成员函数应声明为 const。我们展示了如何调用对象的成员函数来请求对象提供的服务，以及如何将数据作为参数传递给这些成员函数。我们讨论了成员函数的局部变量与类的数据成员之间的区别。我们还展示了如何使用构造函数和成员初始化列表来确保每个对象都被正确初始化。你了解到，单参数构造函数应声明为 explicit，并且构造函数不能声明为 const，因为它会修改正在初始化的对象。我们演示了如何将类的接口与其实现分离，以促进良好的软件工程实践。你了解到，using 指令和 using 声明绝不应放在头文件中。我们给出了一个图示，展示了类实现程序员和客户代码程序员编译其所编写代码所需的文件。我们演示了如何使用设置函数来验证对象的数据，并确保对象保持一致的状态。UML 类图被用于对类及其构造函数、成员函数和数据成员进行建模。在下一章中，我们将开始介绍控制语句，控制语句指定函数中操作执行的顺序。

