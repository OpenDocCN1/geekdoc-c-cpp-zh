
```
gradeBook1 created for course: CS101 Introduction to C++ Programming
gradeBook2 created for course: CS102 Data Structures in C++
```

![](img/bf54db922e6fa8319cba11069e785521_640_0.png)

如图 16.10 所示，图 16.13 第 5 行包含了 GradeBook.h 头文件，以便编译器能够确保在客户端代码中正确创建和操作 GradeBook 对象。在执行此程序之前，图 16.12 和图 16.13 中的源代码文件都必须先编译，然后链接在一起——也就是说，客户端代码中的成员函数调用需要与类成员函数的实现绑定——这项工作由链接器完成。

## 编译和链接过程

图 16.14 中的图表展示了编译和链接过程，最终生成可供教师使用的可执行 GradeBook 应用程序。通常，一个类的接口和实现会由一名程序员创建和编译，然后由另一名程序员使用，该程序员实现使用该类的客户端代码。因此，该图表显示了类实现程序员和客户端代码程序员各自所需的内容。图表中的虚线分别显示了类实现程序员、客户端代码程序员和 GradeBook 应用程序用户所需的部分。[注意：图 16.14 *不是* UML 图。]

负责创建可重用的 GradeBook 类的类实现程序员创建头文件 GradeBook.h 以及包含该头文件的源代码文件 GradeBook.cpp，然后编译源代码文件以生成 GradeBook 的目标代码。为了隐藏类的成员函数实现细节，类实现程序员会向客户端代码程序员提供头文件 GradeBook.h（它指定了类的接口和数据成员）以及 GradeBook 目标代码（即表示 GradeBook 成员函数的机器代码指令）。客户端代码程序员*不会*获得 GradeBook.cpp，因此客户端不知道 GradeBook 的成员函数是如何实现的。

客户端代码程序员只需了解 GradeBook 的接口即可使用该类，并且必须能够链接其目标代码。由于类的接口是 GradeBook.h 头文件中类定义的一部分，因此客户端代码程序员必须能够访问此文件，并在客户端源代码文件中 #include 它。当客户端代码被编译时，编译器使用 GradeBook.h 中的类定义来确保 `main` 函数正确地创建和操作 GradeBook 类的对象。

要创建 *可执行* 的 GradeBook 应用程序，最后一步是链接

- 1. `main` 函数的目标代码（即客户端代码）
- 2. GradeBook 类成员函数实现的目标代码
- 3. 类实现程序员和客户端代码程序员使用的 C++ 类（例如 `string`）的 C++ 标准库目标代码。

链接器的输出是教师可用于管理学生成绩的 *可执行* GradeBook 应用程序。编译器和 IDE 通常在编译代码后为您调用链接器。

![](img/bf54db922e6fa8319cba11069e785521_641_0.png)

图 16.14 | 生成可执行应用程序的编译和链接过程。

有关编译多源文件程序的更多信息，请参阅编译器的文档。我们在 C++ 资源中心 www.deitel.com/cplusplus/ 上提供了各种 C++ 编译器的链接。

## 16.8 使用 set 函数验证数据

在第 16.4 节中，我们介绍了 set 函数，以便允许类的客户端修改私有数据成员的值。在图 16.5 中，类 GradeBook 定义了成员函数

第 21–28 行的 if 语句处理 setCourseName 接收到无效课程名称的情况（即长度超过 25 个字符的名称）。即使参数 name 过长，我们仍然希望保持 GradeBook 对象处于一致状态——即对象的 data member courseName 包含有效值（即长度为 25 个字符或更少的字符串）的状态。因此，我们截断指定的课程名称，并将 name 的前 25 个字符赋给 courseName 数据成员（不幸的是，这可能会导致课程名称被不自然地截断）。标准类 string 提供了成员函数 substr（“substring”的缩写），它返回一个通过复制现有字符串对象的一部分而创建的新字符串对象。第 24 行的调用（即 name.substr(0, 25)）向 name 的成员函数 substr 传递两个整数（0 和 25）。这些参数指示 substr 应返回的字符串部分。第一个参数指定从原始字符串中复制字符的起始位置——每个字符串中的第一个字符被视为位置 0。第二个参数指定要复制的字符数。因此，第 24 行的调用返回从位置 0 开始的 name 的 25 个字符子字符串（即 name 中的前 25 个字符）。例如，如果 name 持有值 "CS101 Introduction to Programming in C++"，substr 返回 "CS101 Introduction to Pro"。调用 substr 后，第 24 行将 substr 返回的子字符串赋给数据成员 courseName。这样，setCourseName 确保 courseName 总是被赋值为包含 25 个或更少字符的字符串。如果成员函数必须截断课程名称以使其有效，则第 26–27 行使用 cerr 显示警告消息。

第 21–28 行的 if 语句包含两个主体语句——一个用于将 courseName 设置为参数 name 的前 25 个字符，另一个用于向用户打印相应的消息。

第 26–27 行的语句也可以不使用第二行的流插入运算符开头，如下所示：

```
cerr << "Name \"" << name << "\" exceeds maximum length (25).\n"
     "Limiting courseName to first 25 characters.\n" << endl;
```

C++ 编译器会合并相邻的字符串字面量，即使它们出现在程序的不同行中。因此，在上面的语句中，C++ 编译器会将字符串字面量 "\" exceeds maximum length (25).\n" 和 "Limiting courseName to first 25 characters.\n" 合并为一个字符串字面量，其输出与图 16.16 中第 26–27 行的输出相同。这种行为允许您通过在程序中跨行拆分长字符串来打印它们，而无需包含额外的流插入操作。

### 测试类 GradeBook

图 16.17 演示了具有验证功能的类 GradeBook 的修改版本（图 16.15–16.16）。第 12 行创建了一个名为 gradeBook1 的 GradeBook 对象。回想一下，GradeBook 构造函数调用 setCourseName 来初始化数据成员 courseName。在类的早期版本中，在构造函数中调用 setCourseName 的好处并不明显。然而，现在构造函数利用了 setCourseName 提供的验证。构造函数只是调用 setCourseName，而不是重复其验证代码。当图 16.17 第 12 行将初始课程名称 "CS101 Introduction to Programming in C++" 传递给 GradeBook 构造函数时，构造函数将此值传递给 setCourseName，在那里进行实际初始化。由于该课程名称包含超过 25 个字符，因此第二个 if 语句的主体被执行，导致 courseName 被初始化为截断的 25 个字符的课程名称 "CS101 Introduction to Pro"（截断部分在第 12 行中突出显示）。图 16.17 中的输出包含成员函数 setCourseName 中图 16.16 第 26–27 行输出的警告消息。第 13 行创建另一个名为 gradeBook2 的 GradeBook 对象——传递给构造函数的有效课程名称正好是 25 个字符。

```cpp
1  // Fig. 16.17: fig16_17.cpp
2  // Create and manipulate a GradeBook object; illustrate validation.
3  #include <iostream>
4  #include "GradeBook.h" // include definition of class GradeBook
5  using namespace std;
6
7  // function main begins program execution
8  int main()
9  {
10    // create two GradeBook objects;
11    // initial course name of gradeBook1 is too long
12    GradeBook gradeBook1( "CS101 Introduction to Programming in C++" );
13    GradeBook gradeBook2( "CS102 C++ Data Structures" );
14
15    // display each GradeBook's courseName
16    cout << "gradeBook1's initial course name is: "
17       << gradeBook1.getCourseName()
18       << "\ngradeBook2's initial course name is: "
19       << gradeBook2.getCourseName() << endl;
20
21    // modify gradeBook1's courseName (with a valid-length string)
22    gradeBook1.setCourseName( "CS101 C++ Programming" );
23
24    // display each GradeBook's courseName
25    cout << "\ngradeBook1's course name is: "
26       << gradeBook1.getCourseName()
27       << "\ngradeBook2's course name is: "
28       << gradeBook2.getCourseName() << endl;
29  } // end main
```

```
Name "CS101 Introduction to Programming in C++" exceeds maximum length (25).
Limiting courseName to first 25 characters.

gradeBook1's initial course name is: CS101 Introduction to Pro
gradeBook2's initial course name is: CS102 C++ Data Structures

gradeBook1's course name is: CS101 C++ Programming
gradeBook2's course name is: CS102 C++ Data Structures
```

**图 16.17** | 创建和操作课程名称长度限制为 25 个字符的 GradeBook 对象。

图 16.17 第 16–19 行显示了 gradeBook1 的截断课程名称（我们在程序输出中用蓝色突出显示）和 gradeBook2 的课程名称。第 22 行直接调用 gradeBook1 的 setCourseName 成员函数，以更改课程
