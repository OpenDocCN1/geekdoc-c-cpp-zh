

```cpp
public:
   // constructor initializes courseName with string supplied as argument
   GradeBook( string name )
   {
      setCourseName( name ); // call set function to initialize courseName
   } // end GradeBook constructor

   // function to set the course name
   void setCourseName( string name )
   {
      courseName = name; // store the course name in the object
   } // end function setCourseName

   // function to get the course name
   string getCourseName()
   {
      return courseName; // return object's courseName
   } // end function getCourseName

   // display a welcome message to the GradeBook user
   void displayMessage()
   {
      // call getCourseName to get the courseName
      cout << "Welcome to the grade book for\n" << getCourseName()
           << "!" << endl;
   } // end function displayMessage
private:
   string courseName; // course name for this GradeBook
}; // end class GradeBook
```

*图 3.9 | 与 main 分离的文件中的 GradeBook 类定义。（第 2 部分，共 2 部分。）*

```cpp
// Fig. 3.10: fig03_10.cpp
// Including class GradeBook from file GradeBook.h for use in main.
#include <iostream>
#include "GradeBook.h" // include definition of class GradeBook
using namespace std;

// function main begins program execution
int main()
{
   // create two GradeBook objects
   GradeBook gradeBook1( "CS101 Introduction to C++ Programming" );
   GradeBook gradeBook2( "CS102 Data Structures in C++" );

   // display initial value of courseName for each GradeBook
   cout << "gradeBook1 created for course: " << gradeBook1.getCourseName()
        << "\ngradeBook2 created for course: " << gradeBook2.getCourseName()
        << endl;
} // end main
```

*图 3.10 | 为了在 main 中使用 GradeBook 类而包含文件 GradeBook.h。（第 2 部分，共 2 部分。）*

```
gradeBook1 created for course: CS101 Introduction to C++ Programming
gradeBook2 created for course: CS102 Data Structures in C++
```

*图 3.10 | 为了在 main 中使用 GradeBook 类而包含文件 GradeBook.h。（第 2 部分，共 2 部分。）*

## 包含含有用户自定义类的头文件

像 GradeBook.h（图 3.9）这样的头文件不能用于启动程序执行，因为它不包含 main 函数。如果尝试单独编译并链接 GradeBook.h 来创建可执行应用程序，Microsoft Visual C++ 2008 会产生以下链接器错误消息：

```
error LNK2001: unresolved external symbol _mainCRTStartup
```

要在 Linux 上为 GNU C++ 进行编译和链接，必须先将头文件包含在 `.cpp` 源代码文件中，然后 GNU C++ 会产生包含以下内容的链接器错误消息：

```
undefined reference to `main'
```

此错误表示链接器无法找到程序的 main 函数。要测试 GradeBook 类（定义于图 3.9 中），必须编写一个包含 main 函数的独立源代码文件（例如图 3.10），该函数实例化并使用这个类的对象。

编译器并不知道 GradeBook 是什么，因为它是一个用户自定义类型。事实上，编译器甚至也不知道 C++ 标准库中的类。为了帮助编译器了解如何使用一个类，我们必须显式地向编译器提供该类的定义——例如，要使用 string 类型，程序必须包含 `<string>` 头文件。这使编译器能够确定必须为该类的每个对象预留多少内存，并确保程序正确调用该类的成员函数。

要在图 3.10 的第 11–12 行中创建 GradeBook 对象 gradeBook1 和 gradeBook2，编译器必须知道 GradeBook 对象的大小。虽然从概念上讲，对象包含数据成员和成员函数，但 C++ 对象实际上只包含数据。编译器只创建一份类的成员函数副本，并在该类的所有对象之间共享这份副本。当然，每个对象都需要拥有自己的类数据成员副本，因为这些成员的内容可能因对象而异（例如，两个不同的 BankAccount 对象拥有两个不同的 balance 数据成员）。然而，成员函数的代码不可修改，因此可以由该类的所有对象共享。因此，对象的大小取决于存储类数据成员所需的内存量。通过在第 4 行包含 GradeBook.h，我们向编译器提供了它所需的信息（图 3.9，第 37 行），使其能够确定 GradeBook 对象的大小，并确定该类的对象是否被正确使用（图 3.10 的第 11–12 行和第 15–16 行）。

第 4 行指示 C++ 预处理器在编译程序之前，用 GradeBook.h 的内容副本（即 GradeBook 类定义）替换该指令。编译源代码文件 fig03_10.cpp 时，它现在包含 GradeBook 类定义（这是由 `#include` 导致的），因此编译器能够确定如何创建 GradeBook 对象，并检查是否正确调用了它们的成员函数。现在，类定义位于一个头文件中（其中不包含 main 函数），我们可以在任何需要复用 GradeBook 类的程序中包含这个头文件。

### 头文件的定位方式

请注意，图 3.10 第 4 行中的 GradeBook.h 头文件名称使用引号（`""`）括起来，而不是使用尖括号（`< >`）。通常，程序的源代码文件和用户自定义头文件位于同一目录中。当预处理器遇到使用引号括起来的头文件名称时，它会尝试在包含 `#include` 指令的文件所在的同一目录中查找该头文件。如果预处理器无法在该目录中找到头文件，就会在与 C++ 标准库头文件相同的位置中搜索。当预处理器遇到使用尖括号括起来的头文件名称（例如 `<iostream>`）时，它会假定该头文件属于 C++ 标准库，而不会在正在进行预处理的程序目录中查找。

> **错误预防提示 3.3**
>
> 为确保预处理器能够正确定位头文件，`#include` 预处理器指令应将用户自定义头文件的名称放在引号中（例如 `"GradeBook.h"`），并将 C++ 标准库头文件的名称放在尖括号中（例如 `<iostream>`）。

### 其他软件工程问题

现在，GradeBook 类定义在一个头文件中，因此该类可以复用。遗憾的是，如图 3.9 所示，将类定义放在头文件中仍会向类的客户端公开该类的全部实现——GradeBook.h 只是一个任何人都可以打开和阅读的文本文件。传统的软件工程观点认为，要使用一个类的对象，客户端代码只需要知道要调用哪些成员函数、为每个成员函数提供哪些参数，以及每个成员函数应返回什么类型。客户端代码不需要知道这些函数是如何实现的。

如果客户端代码确实知道类的实现方式，编写客户端代码的程序员可能会基于类的实现细节来编写代码。理想情况下，如果实现方式发生变化，该类的客户端不应需要进行更改。隐藏类的实现细节可以更容易地更改类的实现，同时最大限度地减少，甚至希望完全消除对客户端代码的修改。

在第 3.8 节中，我们将展示如何将 GradeBook 类拆分为两个文件，从而使：

- 1. 该类可以复用；
- 2. 类的客户端能够知道该类提供哪些成员函数、如何调用这些函数以及应期待哪些返回类型；并且
- 3. 类的客户端*不知道*该类的成员函数是如何实现的。

## 3.8 将接口与实现分离

在前一节中，我们展示了如何通过将类定义与使用该类的客户端代码（例如函数 main）分离来提高软件的可复用性。现在，我们介绍优秀软件工程的另一个基本原则——将接口与实现分离。

### 类的接口

接口定义并规范了事物（例如人员和系统）彼此交互的方式。例如，收音机的控制装置充当了以下两者之间的接口：

