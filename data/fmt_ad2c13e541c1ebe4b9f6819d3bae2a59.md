
**图 16.11** | `GradeBook` 类定义，其中包含了指定该类接口的函数原型。

在第 11 行（16.11）中的原型表示构造函数需要一个字符串参数。记住，构造函数没有返回类型，因此函数原型中没有出现返回类型。成员函数 `setCourseName` 需要一个字符串参数且不返回值（即其返回类型为 `void`）。成员函数 `getCourseName` 的函数原型表示该函数不需要参数并返回一个字符串。成员函数 `displayMessage` 的函数原型（第 14 行）指定了 `displayMessage` 不需要参数且不返回值。这些函数原型与 16.9 中相应函数定义的开头行相同，区别在于没有包含参数名称（参数名称在原型中是可选的），且每个函数原型必须以分号结束。

> **良好的编程实践 16.2** 尽管函数原型中的参数名称是可选的（它们会被编译器忽略），但许多程序员为了文档目的会使用这些名称。

![](img/fa81e30d8bce030c9060826ba9997d7b_643_0.png)

### `GradeBook.cpp`: 在单独源文件中定义成员函数

源文件 `GradeBook.cpp`（图 16.12）定义了 `GradeBook` 的成员函数，这些函数在 16.11 的第 11–14 行中声明。第 39–33 行中的定义与图 16.9 第 13–35 行中的成员函数定义几乎相同。注意，`const` 关键字必须同时出现在函数原型（图 16.11，第 13–14 行）和 `courseName` 及 `displayMessage` 函数的定义（第 22 和 28 行）中。

```cpp
// 图 16.12: GradeBook.cpp
// GradeBook 成员函数定义。此文件包含
// 在 GradeBook.h 中声明的成员函数的实现。
# include <iostream>
#include "GradeBook.h" // 包含 GradeBook 类定义
using namespace std;
// 构造函数使用提供的字符串初始化 courseName
GradeBook::GradeBook(string name)
    : courseName( name ) // 初始化 courseName 的成员初始化列表
{
    // 空体
} // GradeBook 构造函数
// 设置课程名称的函数
void GradeBook::setName(string name)
{
    courseName = name; // 将课程名称存储在对象中
} // 函数 setName
// 获取课程名称的函数
string GradeBook::getName() const
{
    return courseName; // 返回对象的 courseName
} // 函数 getCourseName
// 向 GradeBook 用户显示欢迎消息
void GradeBook::displayMessage() const
{
    // 调用 getCourseName() 获取 courseName
    cout << "Welcome to the grade book\n" << getCourseName() << endl;
} // 显示 displayMessage
```

**图 16.12** | `GradeBook` 成员函数定义

每个成员函数（第 9、16、22 和 28 行）之前都有类名和 `::`；这被称为作用域解析运算符。（现在已分离的）`GradeBook` 类定义（图 16.11）声明了类的成员函数和数据。如果没有在每个函数名之前加上 `GradeBook::`，编译器将不会将它们识别为 `GradeBook` 类的成员函数——编译器会将它们视为“自由”函数或像 `main` 一样的松散函数。这些也是全局函数。在不指定对象的情况下，此类函数无法访问 `GradeBook` 的私有数据或调用类的成员函数。因此，编译器将无法编译这些函数。例如，图 16.12 中第 18 行和第 24 行访问变量 `courseName` 会导致编译错误，因为 `courseName` 在每个函数中都未声明为局部变量——编译器并不知道 `courseName` 已声明为 `GradeBook` 类的数据成员。

![](img/fa81e30d8bce030c9060826ba9997d7b_643_0.png)

**常见错误 16.3** 在单独的源文件中定义成员函数时，如果在每个函数名之前省略 `GradeBook::`（作用域解析运算符），编译器将无法将其识别为 `GradeBook` 类的成员函数——编译器会将它们视为像 `main` 一样的“自由”函数或松散函数。这些也是全局函数。在不指定对象的情况下，此类函数无法访问 `GradeBook` 的私有数据或调用类的成员函数。因此，编译器将无法编译这些函数。例如，图 16.12 中第 18 行和第 24 行访问变量 `courseName` 会导致编译错误，因为 `courseName` 在每个函数中都未声明为局部变量——编译器并不知道 `courseName` 已声明为 `GradeBook` 类的数据成员。

![](img/fa81e30d8bce030c9060826ba9997d7b_647_0.png)

图 16.14 | 生成可执行应用程序的编译和链接过程。

有关编译多源文件程序的更多详细信息，请参阅您的程序员文档。我们在 C++ 资源中心 (`www.deit1.com/cplplus/`) 提供了各种 C++ 编译器的链接。

## 16.8 使用 set 函数验证数据

在 16.4 节中，我们引入了 `set` 函数，允许类的客户端修改私有数据成员的值。在图 16.5 中，`GradeBook` 类定义了成员函数 `setCourseName`，仅用于将接收到的参数名值赋值给数据成员 `courseName`。该成员函数并没有确保课程符合任何特定格式，也不遵循关于“有效”课程名称的任何规则（例如长度限制）。假设某大学可以打印包含长度不超过 25 个字符的课程名称的学生成绩单。如果该大学使用包含 `GradeBook` 对象的系统来生成成绩单，我们可能希望 `GradeBook` 确保数据成员 `courseName` 不包含超过 25 个字符。图 16.15–16.17 中的程序增强了 `GradeBook` 类成员函数 `setCourseName` 以执行此类验证（也称为有效性检查）。

### GradeBook 类定义
`GradeBook` 的类定义（图 16.15）以及其接口与图 16.11 相同。由于接口保持不变，当成员函数 `setCourseName` 的定义被修改时，类的客户端不需要修改。这使得客户端可以通过将客户端代码链接到更新后的 `GradeBook` 对象来利用改进后的 `GradeBook` 类。

```cpp
// Fig 16.15: GradeBook.h
// GradeBook 类定义展示了类的公共接口。
// 成员函数的定义出现在 GradeBook.cpp 中。
#include <string> // 程序使用 C++ 标准字符串类
// GradeBook 类定义
class GradeBook {
public:
    explicit GradeBook(std::string); // 构造函数初始化 courseName
    void setCourseName(std::string); // 设置课程名称
    std::string getCourseName() const; // 获取课程名称
    void displayMessage() const; // 显示欢迎消息
private:
    std::string courseName; // 此 GradeBook 的课程名称
};
```

**图 16.15** `GradeBook` 类定义展示了类的公共接口。

使用 `GradeBook` 成员函数 `setCourseName` 验证课程名称
对 `GradeBook` 类的修改位于构造函数（图 16.16，第 9–12 行）和 `setCourseName`（第 16–29 行）的定义中。构造函数不再使用成员初始化器，而是调用 `setCourseName`。通常情况下，所有数据成员都应该用成员初始化器进行初始化。然而，构造函数必须验证其参数——通常这是在构造函数体内处理的（第 11 行）。对 `setCourseName` 的调用确保了在构造函数体执行之前，参数的值将先设为空字符串，然后 `setCourseName` 将修改 `courseName` 的值。
在 `setCourseName` 中，第 18–19 行的语句判断参数名是否包含有效的课程名称（即长度为 25 或更字符的字符串）。如果课程名称有效，第 19 行将其存储在数据成员 `courseName` 中。注意第 18 行中的表达式 `name.size()`。这是一个类似于 `myGradeBook.displayMessage()` 的成员函数调用。C++ 标准库的 `string` 类定义了一个 `size` 函数，返回字符串对象中的字符数。参数 `name` 是字符串对象，因此调用 `name.size()` 返回字符数。如果此值小于或等于 25，则 `name` 有效并执行第 19 行。

```cpp
// Fig. 16.6: GradeBook.cpp
// GradeBook 成员函数定义的实现。
// setCourseName 函数执行验证。
#include <iostream>
#include "GradeBook.h" // 包含 GradeBook 类定义
using namespace std;
// 构造函数用提供的参数初始化 courseName
GradeBook::GradeBook(string name)
{
    setCourseName(name); // 验证并存储 courseName
} // GradeBook 构造函数结束
// 设置课程名称的函数；
// 确保课程名称最多有 25 个字符
void GradeBook::setCourseName(string name)
{
    if (name.size() <= 25 ) // 如果 name 有 25 或更少字符
        courseName = name; // 将课程名称存储在对象中
    else
    if (name.size() > 25 ) // 如果 name 超过 25 个字符
    {
        // 将 courseName 设置为参数名的前 25 个字符
        courseName = name.substr(0, 25); // 从 0 开始，长度为 25
        cerr << "" << name << " exceeds maximum length (25).\n"
             << "Limiting courseName to first 25 characters.\n" << endl;
    } // if结束
}
// 获取课程名称的函数
string GradeBook::getCourseName() const
{
    return courseName; // 返回对象的 courseName
} // getCourseName 结束
// 向 GradeBook 用户显示消息
void GradeBook::displayMessage() const
{
    cout << "Welcome to the grade book for\n" << getCourseName()
         << "!" << endl;
} // displayMessage 结束
```

**图 16.16** - `GradeBook` 类的成员函数定义，带有验证数据成员 `courseName` 长度的 `set` 函数。

## 16.8 使用 set 函数验证数据 619

对 "Pro" 的介绍（截断部分在第 12 行突出）。图 16.17 中的输出包含了图 16.16 第 26–27 行成员函数 `courseSourceName` 输出的警告。第 13 行创建了另一个 `GradeBook` 对象 `gradeBook2`——传递给构造函数的有效名称正好是 25 个字符。

```cpp
// 图 16.17: fig16_17.cpp
// 创建并操作一个 GradeBook 对象；演示验证。
#include <iostream>
#include "GradeBook.h" // 包含 GradeBook 类定义
using namespace std;
int main() {
    // 创建两个 GradeBook 对象；
    // gradeBook1 的初始课程名称太长
    GradeBook gradeBook1("CS101 Introduction to Programming in C++");
    GradeBook gradeBook2("CS102 C++ Data Structures");
    // 显示每个 GradeBook 的 courseName
    cout << "gradeBook1's initial course name is: " << gradeBook1.getSourceName();
    cout << "gradeBook2's initial course name is: " << gradeBook2.getSourceName() << endl;
    // 修改 gradeBook1 的 courseName（使用有效长度的字符串）
    gradeBook1.setSourceName("CS101 C++ Programming");
    // 显示每个 GradeBook 的 courseName
    cout << "gradeBook1's initial course name is: " << gradeBook1.getSourceName();
    cout << "gradeBook2's initial course name is: " << gradeBook2.getSourceName() << endl;
}
```
