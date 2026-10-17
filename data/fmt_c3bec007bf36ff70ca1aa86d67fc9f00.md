
**图 16.3** | 定义一个带有带参数成员函数的 GradeBook，创建一个 GradeBook 对象并调用其 `displayMessage` 函数。（2 部分中的第 1 部分。）

## 16.3 定义带有参数的成员函数 595

请输入课程名称：
`CS101 Introduction to C++ Programming`

欢迎来到成绩本：
`CS101 Introduction to C++ Programming`!

图 16.3 定义一个带有带参数成员函数的 GradeBook，创建一个 GradeBook 对象并调用其 `displayMessage` 函数。（2 部分中的第 2 部分。）

在讨论 GradeBook 的新功能之前，让我们看看如何在 `main` 中（第 21–34 行）使用新类。第 23 行创建了一个名为 `nameCourse` 的 `string` 类型变量，用于存储用户输入的课程名称。`string` 类型变量代表一个字符序列，例如 "`CS101 Introduction to C++ Programming`" 。字符串实际上是 C++ 标准库类的一个对象。该类定义在 `<string>` 中，且名称（如 `count`）属于命名空间 `std`。第 5 行和 23 行的指令中，第 5 行包含了 `<string>`。第 6 行的指令允许我们在第 22 行直接写 `string` 而不是 `std::`。现在，你可以使用其他类型的字符串变量，如 `int`。你将在第 16.8 节中学习额外的字符串功能。

第 24 行创建了一个名为 `myGradeBook` 的 `GradeBook` 对象。第 27 行提示用户输入课程名称。第 28 行从用户处读取名称并赋值给 `nameOfCourse` 变量，使用库函数 `getline` 执行输入。在解释这行代码之前，让我们解释为什么我们不能简单地使用

```cpp
cin >> nameOfCourse;
```

来获取课程名称。
在程序执行过程中，我们使用 "`CS101 Introduction to C++ Programming`" 这个名称，它包含多个由空格分隔的单词。（回想当用户以加粗输入数据时。）当使用流提取器读取时，`cin` 会读取字符直到遇到第一个空白字符。因此，在打印语句之前将只有 "`CS101`" 。课程名称的其余部分必须通过随后的输入操作来读取。

在这个示例中，我们希望用户完成课程名称并将其输入以提交给程序，并且我们将整个课程名称存储在 `string` 变量 `nameOfCourse` 中。第 28 行的函数调用 `getline(cin, nameOfCourse)` 从标准流对象 `cin`（即键盘）读取字符（包括分隔单词的空格字符），直到遇到换行符，将字符放入 `string` 变量 `nameOfCourse` 并丢弃换行符。当你输入数据并按回车键时，输入流中会插入变量。程序必须包含 `<string>` 头文件才能使用函数 `getline`，它属于命名空间 `std`。

第 33 行创建了 `myGradeBook` 的 `displayMessage` 成员函数。参数中的 `nameOfCourse` 变量是传递成员函数 `displayMessage` 的参数，以便其执行任务。`main` 中变量 `nameCourse` 的值被复制到第 13 行的成员函数参数 `parameterName`。当你执行此程序时，成员函数 `displayMessage` 将你输入的课程名称作为欢迎消息的一部分输出（在示例执行中为 `CS101 Introduction to C++ Programming`）。

# 第 16 章 类、对象与字符串介绍

## 关于参数的更多信息

要在函数定义中指定函数需要数据来执行任务，你需要在参数列表中放置额外信息，参数位于函数名后的括号内。参数列表可以包含任何数量的参数，也可以一个都没有。[16.4](img/fa8e30d8bce030c90682997d7b628_0.png)

**图 16.4** | 更新后的 GradeBook 类图

## 16.4 数据成员、set 成员函数

如你所知，在函数体中定义的变量称为局部变量，只能在声明它们的函数中使用。局部变量必须在使用之前进行声明。

一个类通常由一个或多个函数组成，这些函数操作属于特定对象的属性。属性在类定义中用变量表示。这些变量被称为数据成员，定义在类内部但在类函数定义的体之外。类的每个对象都维护其自己的属性。这些属性在对象的整个生命周期内都存在。本节的示例展示了一个 `GradeBook` 类，它包含一个 `courseName` 成员来表示特定 `GradeBook` 对象的课程名称。如果你创建了多个 `GradeBook` 对象，每个对象将有自己的 `courseName` 成员，这些成员可以创建不同的值。

### 带有数据成员和 set 成员函数的 GradeBook 类
在下一个示例中，`GradeBook`（图 16.5）将课程名称作为数据成员维护，以便在整个执行过程中使用或修改。执行过程包含成员函数 `setName`，`setName` 函数将课程名称存储在 `GradeBook` 数据成员中。成员函数 `getCourseName` 从该数据成员获取课程名称。成员函数 `displayMessage`——未指定任何参数——仍然显示包含课程名称的欢迎消息。然而，正如你将看到的，该函数现在通过调用同类的另一个函数——`getCourseName` 来获取课程名称。

> 图 16.5: `fig16_os.cpp`

```cpp
// 定义类 GradeBook，包含 courseName 数据成员
// 以及用于设置和获取其值的成员函数；
// 使用这些函数创建并操作 GradeBook 对象。
#include <iostream>
#include <string> //程序使用标准字符串类
using namespace std;
// GradeBook 类定义
class GradeBook
{
public:
// 设置课程名称的函数
void setName(string name )
{
    courseName = name; // 在对象中存储课程名称
} // 函数结束 setName
};
```

# 第16章 类、对象与字符串简介

```cpp
18 // 获取课程名称的函数
19 string getCourseName() const
20 {
21     return courseName; // 返回对象的 courseName
22 } // getCourseName 函数结束
23
24 // 显示欢迎信息的函数
25 void displayMessage() const
26 {
27 // 此语句调用 getCourseName 来获取
28 // GradeBook 代表的课程名称
29 cout << "Welcome to the grade book for\n" << getCourseName() << "!";
30 cout << endl;
31 } // displayMessage 函数结束
32 private:
33 string courseName; // GradeBook 的课程名称
34 }; // GradeBook 类结束
35 // main 函数开始程序执行
36 int main() {
37 string nameOfCourse; // 课程名称的字符串
38 GradeBook myGradeBook; // 创建一个名为 myGradeBook 的 GradeBook 对象
39
40 // 显示 courseName 的初始值
41 cout << "Initial course name is: " << myGradeBook.getCourseName();
42 cout << endl;
43
44 // 提示、输入并设置课程名称
45 cout << "nPlease enter the course name: " << endl;
46 getline(cin, nameOfCourse); // 读取包含空格的课程名称
47 myGradeBook.setCourseName(nameOfCourse); // 设置课程名称
48 cout << endl; // 输出空行
49 myGradeBook.displayMessage(); // 显示带有新课程名称的信息
50 } // main 函数结束
```
